---
title: Experience Platform Launch에서 IAB TCF 2.0 사용
seo-title: Adobe Experience Platform Launch 및 Adobe Experience Platform 웹 SDK와 함께 IAB TCF 2.0 동의 설정
description: Adobe Experience Platform Launch 및 Adobe Experience Platform 웹 SDK를 사용하여 IAB TCF 2.0 동의 설정 방법 살펴보기
seo-description: Adobe Experience Platform Launch 및 Adobe Experience Platform 웹 SDK를 사용하여 IAB TCF 2.0 동의 설정 방법 살펴보기
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# Experience Platform Launch 및 AEP 웹 SDK 익스텐션과 함께 IAB TCF 2.0 사용

Adobe Experience Platform 웹 소프트웨어 개발 키트(Adobe Experience Platform 웹 SDK)는 Interactive Advertising Bureau Transparency &amp; Consent Framework, 버전 2.0(IAB TCF 2.0)을 지원합니다. 이 안내서에서는 Experience Platform Launch용 AEP 웹 SDK 익스텐션을 사용하여 Adobe에 IAB TCF 2.0 동의 정보를 보내기 위한 Adobe Experience Platform Launch 속성을 설정하는 방법을 보여 줍니다.

Experience Platform Launch을 사용하지 않으려면 Experience Platform Launch 없이 IAB TCF 2.0 [을 사용하는 방법에 대한 가이드를 참조하십시오](./without-launch.md).

## 시작하기

Experience Platform Launch 및 AEP 웹 SDK 확장 기능이 있는 IAB TCF 2.0을 사용하려면 XDM 스키마 및 데이터 세트를 사용할 수 있어야 합니다. 이러한 설정 중 하나를 설정하지 않은 경우 계속하기 전에 이 Adobe Experience Platform 웹 SDK 실행 빠른 시작 안내서를 참조하여 시작하십시오.

또한 이 가이드에서는 Adobe Experience Platform 웹 SDK에 대한 작업 이해를 필요로 합니다. 빠른 재교육을 위해 [Adobe Experience Platform 웹 SDK 개요](../../home.md) 및 [FAQ](../../web-sdk-faq.md) 설명서를 참조하십시오.

## 기본 동의 설정

확장 구성 내에 기본 동의에 대한 설정이 있습니다. 동의 쿠키가 없는 고객의 행동을 제어합니다. 동의 쿠키가 없는 고객에 대한 경험 이벤트를 대기시키려면 이 설정을 다음으로 설정하십시오 `pending`.

>[!NOTE]
>
>현재 Experience Platform Launch 확장을 통해 동적으로 설정할 수 있는 방법이 없습니다.

기본 동의에 대한 자세한 내용은 SDK 구성 설명서의 [기본 동의 섹션](../../fundamentals/configuring-the-sdk.md#default-consent) 을 참조하십시오.

## 동의 정보가 있는 프로필 업데이트 {#consent-code-1}

고객의 동의 기본 설정이 변경되었을 때 조치를 `setConsent` 호출하려면 새 Experience Platform Launch 규칙을 만들어야 합니다. 먼저 새 이벤트를 추가하고 코어 익스텐션의 &quot;사용자 지정 코드&quot; 이벤트 유형을 선택합니다.

새 이벤트에 다음 코드 샘플을 사용합니다.

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

이 사용자 지정 코드에서는 다음 두 가지 작업을 수행합니다.

* 두 데이터 요소를 설정합니다. 하나는 동의 문자열, 하나는 `gdprApplies` 플래그. 이 기능은 나중에 &quot;동의 설정&quot; 작업을 채울 때 유용합니다.

* 동의 기본 설정이 변경되면 규칙을 트리거합니다. 동의 기본 설정이 변경될 때마다 &quot;동의 설정&quot; 동작을 사용해야 합니다. 확장자에 &quot;동의 설정&quot; 작업을 추가하고 다음과 같이 양식을 작성하십시오.

* 표준:&quot;IAB TCF&quot;
* 버전:&quot;2.0&quot;
* 값:&quot;%IAB TCF 동의 문자열%&quot;
* GDPR 적용:&quot;%IAB TCF 동의 GDPR%&quot;

![IAB 설정 동의 조치](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>데이터 요소 선택기는 사용자 지정 코드를 통해 만들어졌기 때문에 이러한 데이터 요소를 선택할 수 없습니다. 백분율 기호와 함께 데이터 요소 이름을 입력해야 합니다. 이 코드는 변경될 때마다 고객의 새로운 동의 환경 설정으로 고객의 프로필을 업데이트합니다. 또한, 서버는 쿠키 값을 반환하므로 Adobe Experience Platform 웹 SDK가 경험 이벤트를 기록하지 못하도록 할 수 있습니다.

## 경험 이벤트에 대한 XDM 데이터 요소 만들기

XDM 경험 이벤트에 동의 문자열을 포함해야 합니다. 이렇게 하려면 XDM 개체 데이터 요소를 사용하십시오. 먼저 새 XDM 개체 데이터 요소를 만들거나 이벤트를 전송하기 위해 이미 만든 데이터 요소를 사용하십시오. 사용자 스키마에 경험 이벤트 개인 정보 혼합을 추가한 경우 XDM 개체에 `consentStrings` 키가 있어야 합니다.

1. 동의문자열을 **[!UICONTROL 선택합니다]**.

1. 개별 **[!UICONTROL 항목]** 제공을 선택하고 [항목 **[!UICONTROL 추가]를 선택합니다]**.

1. consentString **[!UICONTROL 머리글을]** 확장하고 첫 번째 항목을 확장한 다음 다음 값을 입력합니다.

* `consentStandard`:IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`:%IAB TCF 동의 문자열%
* `gdprApplies`:%IAB TCF 동의 GDPR%

>[!IMPORTANT]
>
>데이터 요소 선택기는 사용자 지정 코드를 통해 만들어졌기 때문에 이러한 데이터 요소를 선택할 수 없습니다. 백분율 기호와 함께 데이터 요소 이름을 입력해야 합니다.

## IAB TCF 2.0 동의 정보가 있는 초기 경험 이벤트 전송

페이지의 초기 경험 이벤트가 페이지 로드 이벤트로 트리거되는 경우 동의 문자열이 아직 로드되지 않았을 수 있습니다. 이 규칙은 현재 페이지 로드 이벤트를 대체하기 위한 것입니다. 동의 정보가 먼저 로드되도록 하려면 새 규칙을 만들고 다음 코드를 사용자 지정 코드 이벤트로 추가하십시오.

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

이 코드는 `useractioncomplete` 및 `tcloaded` 이벤트가 모두 처리되는 경우를 제외하고, 이전 사용자 지정 코드와 동일합니다. [이전 사용자 지정 코드는](#consent-code-1) 고객이 처음 기본 설정을 선택할 때만 트리거됩니다. 이 코드는 고객이 이미 자신의 환경 설정을 선택했을 때도 트리거됩니다. 예를 들어 두 번째 페이지를 로드할 때

Adobe Experience Platform 웹 SDK 익스텐션에서 &quot;이벤트 보내기&quot; 동작을 추가합니다. XDM 필드 내에서 이전 섹션에서 작성한 XDM 데이터 요소를 선택합니다.

## IAB TCF 2.0 동의 정보가 있는 다른 이벤트 전송

초기 경험 이벤트 후에 이벤트가 트리거되면 두 데이터 요소가 여전히 정의되며 IAB 동의 정보를 전송하는 데 사용할 수 있습니다. 동일한 XDM 데이터 요소를 사용하여 향후 이벤트를 전송합니다. IAB TCF 2.0 정보가 포함되어 있습니다.

## 다음 단계

이제 IAB TCF 2.0을 Adobe Experience Platform 웹 SDK 익스텐션과 함께 사용하는 방법을 익혔으므로 Adobe Analytics 또는 실시간 고객 데이터 플랫폼과 같은 다른 Adobe 솔루션과 통합할 수도 있습니다. 자세한 내용은 [IAB Transparency &amp; Consent Framework 2.0 개요를](./overview.md) 참조하십시오.
