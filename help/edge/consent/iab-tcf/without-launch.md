---
title: Experience Platform Launch 없이 IAB TCF 2.0 사용
seo-title: Adobe Experience Platform 웹 SDK로 IAB TCF 2.0 동의 설정
description: Adobe Experience Platform 웹 SDK를 사용하여 IAB TCF 2.0 동의 설정 방법 살펴보기
seo-description: Adobe Experience Platform 웹 SDK를 사용하여 IAB TCF 2.0 동의 설정 방법 살펴보기
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---


# AEP 웹 SDK 익스텐션에서 IAB TCF 2.0 사용

본 가이드는 Experience Platform Launch을 사용하지 않고 Interactive Advertising Bureau Transparency &amp; Consent Framework, 버전 2.0(IAB TCF 2.0)을 Adobe Experience Platform 웹 SDK와 통합하는 방법을 보여줍니다. IAB TCF 2.0과의 통합에 대한 개요는 [개요를 참조하십시오](./overview.md). Experience Platform Launch과 통합하는 방법에 대한 자세한 내용은 Experience Platform Launch에 대한 [IAB TCF 2.0 안내서를 참조하십시오](./with-launch.md).

## 시작하기

이 안내서에서는 `__tcfapi` 인터페이스를 사용하여 동의 정보에 액세스합니다. CMP(Cloud Management Provider)와 직접 통합하는 것이 더 쉬워질 수 있습니다. 그러나 CMP는 일반적으로 TCF API와 유사한 기능을 제공하므로 이 안내서의 정보는 여전히 유용할 수 있습니다.

>[!NOTE]
>
>이러한 예에서는 코드가 실행되는 시간까지 페이지에 정의되어 있다고 가정합니다. `window.__tcfapi` CMP는 개체가 준비되었을 때 이러한 기능을 실행할 수 있는 후크를 `__tcfapi` 제공할 수 있습니다.

Experience Platform Launch 및 AEP 웹 SDK 확장 기능이 있는 IAB TCF 2.0을 사용하려면 XDM 스키마를 사용할 수 있어야 합니다. 이러한 설정 중 하나를 설정하지 않은 경우 계속하기 전에 이 페이지를 확인하여 시작하십시오.

또한 이 가이드에서는 Adobe Experience Platform 웹 SDK에 대한 작업 이해를 필요로 합니다. 빠른 재교육을 위해 [Adobe Experience Platform 웹 SDK 개요](../../home.md) 및 [FAQ](../../web-sdk-faq.md) 설명서를 참조하십시오.

## 기본 동의 활성화

알 수 없는 모든 사용자를 동일하게 취급하려면 기본 동의를 로 설정할 수 있습니다 `pending`. 동의 기본 설정이 수신될 때까지 경험 이벤트를 대기시킵니다.

기본 동의에 대한 자세한 내용은 플랫폼 웹 SDK 구성 설명서의 [기본 동의 섹션을](../../fundamentals/configuring-the-sdk.md#default-consent) 참조하십시오.

### 기본 동의 설정 기준 `gdprApplies`

일부 CMP는 GDPR(General Data Protection Regulation)이 고객에게 적용되는지 여부를 판단할 수 있는 기능을 제공합니다. GDPR이 적용되지 않는 고객에 대한 동의를 가정하고 싶은 경우 TCF API 호출에서 `gdprApplies` 플래그를 사용할 수 있습니다.

다음 예에서는 이 작업을 수행하는 방법을 보여 줍니다.

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

이 예에서 이 `configure` 명령은 TCF API에서 가져온 `tcData` 후 호출됩니다. true `gdprApplies` 이면 기본 동의가 설정됩니다 `pending`. false `gdprApplies` 이면 기본 동의가 설정됩니다 `in`. 구성으로 `alloyConfiguration` 변수를 채워야 합니다.

>[!NOTE]
>
>기본 동의를 로 설정해도 이 명령 `in`을 사용하여 고객의 동의 환경 설정을 기록할 `setConsent` 수 있습니다.

## setConsent 이벤트 사용

IAB TCF 2.0 API는 고객이 동의를 업데이트할 때 이벤트를 제공합니다. 이 문제는 고객이 처음 기본 설정을 지정하고 고객이 기본 설정을 업데이트할 때 발생합니다.

다음 예에서는 이 작업을 수행하는 방법을 보여 줍니다.

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

이 코드 블록은 `useractioncomplete` 이벤트를 수신한 다음 동의 문자열과 `gdprApplies` 플래그를 전달하여 동의를 설정합니다. 고객에 대한 사용자 지정 ID가 있는 경우 반드시 `identityMap` 변수를 채워야 합니다. 전화에 대한 자세한 내용은 [동의](../../consent/supporting-consent.md) 지원 가이드를 참조하십시오 `setConsent`.

## sendEvent에 동의 정보 포함

XDM 스키마 내에서 경험 이벤트의 동의 환경 설정 정보를 저장할 수 있습니다. 이 정보를 모든 이벤트에 추가하는 방법에는 두 가지가 있습니다.

먼저 모든 호출에서 관련 XDM 스키마를 제공할 수 `sendEvent` 있습니다. 다음 예에서는 이 작업을 수행하는 방법을 보여 줍니다.

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

이 예제는 TCF API에 대한 동의 정보를 가져온 다음 XDM 스키마에 동의 정보가 추가된 이벤트를 전송합니다. 명령 옵션에 포함되어야 하는 내용을 [이해하려면 추적 이벤트](../../fundamentals/tracking-events.md) 안내서를 `sendEvent` 참조하십시오.

모든 요청에 동의 정보를 추가하는 다른 방법은 콜백입니다 `onBeforeEventSend` . 이를 수행하는 방법에 대한 자세한 내용은 추적 이벤트 설명서 내에서 전역 [으로 이벤트를](../../fundamentals/tracking-events.md#modifying-events-globally) 수정하는 섹션을 참조하십시오.

## 다음 단계

이제 AEP 웹 SDK 익스텐션과 IAB TCF 2.0을 사용하는 방법을 습득했으므로 Adobe Analytics 또는 실시간 고객 데이터 플랫폼과 같은 다른 Adobe 솔루션과 통합하도록 선택할 수도 있습니다. 자세한 내용은 [IAB Transparency &amp; Consent Framework 2.0 개요를](./overview.md) 참조하십시오.
