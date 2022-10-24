---
title: 태그 및 Platform Web SDK 확장을 사용하여 IAB TCF 2.0 지원 통합
description: 태그 및 Adobe Experience Platform Web SDK 확장을 사용하여 IAB TCF 2.0 동의를 설정하는 방법을 알아봅니다.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 태그 및 Platform Web SDK 확장을 사용하여 IAB TCF 2.0 지원 통합

Adobe Experience Platform Web SDK는 Interactive Advertising Bureau Transparency &amp; Consent Framework, 버전 2.0(IAB TCF 2.0)을 지원합니다. 이 안내서에서는 Adobe Experience Platform Web SDK 태그 확장을 사용하여 Adobe에 IAB TCF 2.0 동의 정보를 전송하는 태그 속성을 설정하는 방법을 보여줍니다.

태그를 사용하지 않으려면 다음 안내서를 참조하십시오 [태그 없이 IAB TCF 2.0 사용](./without-launch.md).

## 시작하기

태그 및 Platform Web SDK 확장과 함께 IAB TCF 2.0을 사용하려면 XDM 스키마 및 데이터 세트를 사용할 수 있어야 합니다.

또한 이 안내서에서는 Adobe Experience Platform Web SDK에 대한 작업 이해를 필요로 합니다. 빠른 재교육을 받으려면 [Adobe Experience Platform Web SDK 개요](../../home.md) 그리고 [FAQ](../../web-sdk-faq.md) 설명서.

## 기본 동의 설정

확장 구성 내에 기본 동의에 대한 설정이 있습니다. 이는 동의 쿠키가 없는 고객의 동작을 제어합니다. 동의 쿠키가 없는 고객에 대한 경험 이벤트를 대기열로 설정하려면 다음과 같이 설정하십시오 `pending`. 동의 쿠키가 없는 고객에 대해 경험 이벤트를 취소하려면 로 설정합니다. `out`. 데이터 요소를 사용하여 기본 동의 값을 동적으로 설정할 수도 있습니다.

기본 동의를 구성하는 방법에 대한 자세한 내용은 [기본 동의 섹션](../../fundamentals/configuring-the-sdk.md#default-consent) 를 참조하십시오.

## 동의 정보로 프로필 업데이트 {#consent-code-1}

를 호출하려면 `setConsent` 작업 고객의 동의 환경 설정이 변경되면 새 태그 규칙을 만들어야 합니다. 먼저 새 이벤트를 추가하고 코어 확장의 &quot;사용자 지정 코드&quot; 이벤트 유형을 선택합니다.

새 이벤트에 다음 코드 샘플을 사용하십시오.

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

이 사용자 지정 코드는 다음과 같은 두 가지 작업을 수행합니다.

* 동의 문자열이 있는 데이터 요소와 `gdprApplies` 플래그. 이 기능은 나중에 &quot;동의 설정&quot; 작업을 작성할 때 유용합니다.

* 동의 환경 설정이 변경되면 규칙을 트리거합니다. 동의 기본 설정이 변경될 때마다 &quot;동의 설정&quot; 작업을 사용해야 합니다. 확장 프로그램에 &quot;동의 설정&quot; 작업을 추가하고 양식을 다음과 같이 채웁니다.

* 표준: &quot;IAB TCF&quot;
* 버전: &quot;2.0&quot;
* 값: &quot;%IAB TCF 동의 문자열%&quot;
* GDPR이 적용되는 내용: &quot;%IAB TCF 동의 GDPR%&quot;

![IAB 설정 동의 작업](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>이러한 데이터 요소는 사용자 지정 코드를 통해 만들어졌기 때문에 데이터 요소 선택기를 사용하여 선택할 수 없습니다. 퍼센트 기호가 있는 데이터 요소 이름을 입력해야 합니다. 이 코드는 변경될 때마다 고객의 새 동의 환경 설정으로 고객 프로필을 업데이트합니다. 또한 서버가 쿠키 값을 반환하므로 Adobe Experience Platform Web SDK에서 Experience Events를 기록하지 못할 수 있습니다.

## 경험 이벤트에 대한 XDM 데이터 요소 만들기

동의 문자열은 XDM 경험 이벤트에 포함해야 합니다. 이렇게 하려면 XDM 개체 데이터 요소를 사용합니다. 먼저 새 XDM 개체 데이터 요소를 만들거나 이벤트 전송을 위해 이미 만든 데이터 요소를 사용합니다. 스키마에 경험 이벤트 개인 정보 스키마 필드 그룹을 추가한 경우 `consentStrings` 키를 누릅니다.

1. 선택 **[!UICONTROL consentStrings]**.

1. 선택 **[!UICONTROL 개별 항목 제공]** 을(를) 선택합니다. **[!UICONTROL 항목 추가]**.

1. 를 확장합니다. **[!UICONTROL consentString]** 머리글을 누르고 첫 번째 항목을 확장한 다음 다음 값을 입력합니다.

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %IAB TCF 동의 문자열%
* `gdprApplies`: %IAB TCF 동의 GDPR%

>[!IMPORTANT]
>
>이러한 데이터 요소는 사용자 지정 코드를 통해 만들어졌기 때문에 데이터 요소 선택기를 사용하여 선택할 수 없습니다. 퍼센트 기호가 있는 데이터 요소 이름을 입력해야 합니다.

## IAB TCF 2.0 동의 정보로 초기 경험 이벤트 보내기

페이지의 초기 경험 이벤트가 페이지 로드 이벤트로 트리거되는 경우 동의 문자열이 아직 로드되지 않았을 수 있습니다. 이 규칙은 현재 페이지 로드 이벤트를 대체하기 위한 것입니다. 동의 정보가 먼저 로드되도록 하려면 새 규칙을 만들고 다음 코드를 사용자 지정 코드 이벤트로 추가합니다.

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

이 코드는 두 가지 모두를 제외하고, 이전 사용자 지정 코드와 동일합니다 `useractioncomplete` 및 `tcloaded` 이벤트가 처리됩니다. 다음 [이전 사용자 지정 코드](#consent-code-1) 은 고객이 처음으로 환경 설정을 선택하는 경우에만 트리거됩니다. 이 코드는 고객이 이미 환경 설정을 선택했을 때도 트리거됩니다. 예를 들어, 두 번째 페이지 로드 시.

Platform Web SDK 확장에서 &quot;이벤트 보내기&quot; 작업을 추가합니다. XDM 필드 내에서 이전 섹션에서 만든 XDM 데이터 요소를 선택합니다.

## IAB TCF 2.0 동의 정보로 다른 이벤트 보내기

초기 경험 이벤트 후에 이벤트가 트리거되면 두 데이터 요소가 여전히 정의되며 IAB 동의 정보를 전송하는 데 사용할 수 있습니다. 동일한 XDM 데이터 요소를 사용하여 향후 이벤트를 전송합니다. IAB TCF 2.0 정보가 포함되어 있습니다.

## 다음 단계

이제 Platform Web SDK 확장과 함께 IAB TCF 2.0을 사용하는 방법을 알았으므로 Adobe Analytics 또는 Adobe Real-time Customer Data Platform과 같은 다른 Adobe 솔루션과 통합하도록 선택할 수도 있습니다. 자세한 내용은 [IAB Transparency &amp; Consent Framework 2.0 개요](./overview.md) 추가 정보.
