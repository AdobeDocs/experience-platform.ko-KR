---
title: Adobe Experience Platform Web SDK를 사용하여 IAB TCF 2.0 지원 통합
description: 태그를 사용하지 않고 웹 사이트에 대한 IAB TCF 2.0 지원을 설정하는 방법에 대해 알아봅니다.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Platform Web SDK와 IAB TCF 2.0 지원 통합

이 안내서에서는 태그를 사용하지 않고 대화형 Advertising Bureau Transparency &amp; Consent Framework, 버전 2.0(IAB TCF 2.0)을 Adobe Experience Platform Web SDK와 통합하는 방법을 보여줍니다. IAB TCF 2.0과 통합에 대한 개요를 보려면 [개요](./overview.md)를 읽어 보십시오. 태그와 통합하는 방법에 대한 안내서는 [태그에 대한 IAB TCF 2.0 안내서](./with-tags.md)를 참조하십시오.

## 시작하기

이 안내서에서는 동의 정보에 액세스하기 위해 `__tcfapi` 인터페이스를 사용합니다. CMP(클라우드 관리 공급자)와 직접 통합하는 것이 더 쉬울 수 있습니다. 그러나 CMP는 일반적으로 TCF API와 유사한 기능을 제공하므로 이 안내서의 정보가 유용할 수 있습니다.

>[!NOTE]
>
>이 예제에서는 코드가 실행될 때까지 페이지에 `window.__tcfapi`이(가) 정의되어 있다고 가정합니다. CMP는 `__tcfapi` 개체가 준비되었을 때 이러한 함수를 실행할 수 있는 후크를 제공할 수 있습니다.

태그 및 Adobe Experience Platform 웹 SDK 확장과 함께 IAB TCF 2.0을 사용하려면 사용 가능한 XDM 스키마가 있어야 합니다. 이러한 설정을 하지 않은 경우 계속 진행하기 전에 이 페이지를 보는 것부터 시작하십시오.

또한 이 안내서를 사용하려면 Adobe Experience Platform Web SDK에 대한 작업 이해 권한이 필요합니다. 빠른 새로 고침은 [Adobe Experience Platform Web SDK 개요](../../home.md) 및 [자주 묻는 질문](../../faq.md) 설명서를 참조하십시오.

## 기본 동의 활성화

알 수 없는 모든 사용자를 동일하게 취급하려면 [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md)을(를) `pending` 또는 `out`(으)로 설정할 수 있습니다. 이 설정은 동의 환경 설정을 받을 때까지 경험 이벤트를 큐에 추가하거나 삭제합니다.

### `gdprApplies`을(를) 기반으로 기본 동의 설정

일부 CMP에서는 GDPR(일반 데이터 보호 규정)이 고객에게 적용되는지 여부를 확인하는 기능을 제공합니다. GDPR이 적용되지 않는 고객에 대한 동의를 얻으려면 TCF API 호출에서 `gdprApplies` 플래그를 사용할 수 있습니다.

다음 예제에서는 이 작업을 수행하는 한 가지 방법을 보여 줍니다.

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

이 예에서 `configure` 명령은 TCF API에서 `tcData`을(를) 가져온 후에 호출됩니다. `gdprApplies`이(가) true이면 기본 동의가 `pending`(으)로 설정됩니다. `gdprApplies`이(가) false이면 기본 동의가 `in`(으)로 설정됩니다. 구성을 사용하여 `alloyConfiguration` 변수를 채우십시오.

>[!NOTE]
>
>기본 동의가 `in`(으)로 설정된 경우에도 `setConsent` 명령을 사용하여 고객 동의 환경 설정을 기록할 수 있습니다.

## setConsent 이벤트 사용

IAB TCF 2.0 API는 고객이 동의를 업데이트할 때에 대한 이벤트를 제공합니다. 이 문제는 고객이 처음에 환경 설정을 지정하고 고객이 환경 설정을 업데이트할 때 발생합니다.

다음 예제에서는 이 작업을 수행하는 한 가지 방법을 보여 줍니다.

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

이 코드 블록은 `useractioncomplete` 이벤트를 수신한 다음 동의를 설정하여 동의 문자열과 `gdprApplies` 플래그를 전달합니다. 고객에 대한 사용자 지정 ID가 있는 경우 `identityMap` 변수를 채우십시오. 자세한 내용은 [setConsent](../../../web-sdk/commands/setconsent.md)의 안내서를 참조하십시오.

## sendEvent에 동의 정보 포함

XDM 스키마 내에서 경험 이벤트의 동의 환경 설정 정보를 저장할 수 있습니다. 두 가지 방법으로 모든 이벤트에 이 정보를 추가할 수 있습니다.

먼저 모든 `sendEvent` 호출에 관련 XDM 스키마를 제공할 수 있습니다. 다음 예제에서는 이 작업을 수행하는 한 가지 방법을 보여 줍니다.

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

이 예제는 TCF API에 대한 동의 정보를 가져온 다음 XDM 스키마에 추가된 동의 정보로 이벤트를 전송합니다.

모든 요청에 동의 정보를 추가하는 또 다른 방법은 [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) 콜백을 사용하는 것입니다.

## 다음 단계

Platform Web SDK 확장과 함께 IAB TCF 2.0을 사용하는 방법에 대해 배웠으므로 Adobe Analytics 또는 Adobe Real-time Customer Data Platform과 같은 다른 Adobe 솔루션과 통합하도록 선택할 수도 있습니다. 자세한 내용은 [IAB Transparency &amp; Consent Framework 2.0 개요](./overview.md)를 참조하십시오.
