---
title: 태그와 Experience Platform Web SDK 확장을 사용하여 IAB TCF 2.0 지원 통합
description: 태그 및 Adobe Experience Platform Web SDK 확장을 사용하여 IAB TCF 2.0 동의를 설정하는 방법에 대해 알아봅니다.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# 태그와 Experience Platform Web SDK 확장을 사용하여 IAB TCF 2.0 지원 통합

Adobe Experience Platform Web SDK은 Interactive Advertising Bureau Transparency &amp; Consent Framework 버전 2.0(IAB TCF 2.0)을 지원합니다. 이 안내서에서는 Adobe Experience Platform Web SDK 태그 확장을 사용하여 IAB TCF 2.0 동의 정보를 Adobe으로 전송하기 위해 태그 속성을 설정하는 방법을 보여 줍니다.

태그를 사용하지 않으려면 [태그 없이 IAB TCF 2.0 사용](./without-tags.md)에 대한 안내서를 참조하십시오.

## 시작하기

태그 및 Experience Platform Web SDK 확장과 함께 IAB TCF 2.0을 사용하려면 XDM 스키마 및 데이터 세트를 사용할 수 있어야 합니다.

또한 이 안내서를 사용하려면 Adobe Experience Platform Web SDK에 대한 작업 이해도가 있어야 합니다. 빠른 새로 고침은 [Adobe Experience Platform Web SDK 개요](../../home.md) 및 [자주 묻는 질문](../../faq.md) 설명서를 참조하십시오.

## 기본 동의 설정

확장 구성 내에는 기본 동의에 대한 설정이 있습니다. 이는 동의 쿠키가 없는 고객의 행동을 제어합니다. 동의 쿠키가 없는 고객을 위해 경험 이벤트를 큐에 넣으려면 이를 `pending`(으)로 설정하십시오. 동의 쿠키가 없는 고객을 위해 경험 이벤트를 삭제하려면 이를 `out`(으)로 설정하십시오. 데이터 요소를 사용하여 기본 동의 값을 동적으로 설정할 수도 있습니다. 자세한 내용은 [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md)을(를) 참조하십시오.

## 동의 정보로 프로필 업데이트 {#consent-code-1}

고객 동의 환경 설정이 변경되었을 때 [`setConsent`](/help/web-sdk/commands/setconsent.md) 작업을 호출하려면 태그 규칙을 만듭니다. 새 이벤트를 추가하여 시작하고 코어 확장의 &quot;사용자 지정 코드&quot; 이벤트 유형을 선택합니다.

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

이 사용자 지정 코드는 다음 두 가지 작업을 수행합니다.

* 두 개의 데이터 요소를 설정합니다. 하나는 동의 문자열로 설정하고 하나는 `gdprApplies` 플래그로 설정합니다. 이 기능은 나중에 &quot;동의 설정&quot; 작업을 작성할 때 유용합니다.

* 동의 환경 설정이 변경되면 규칙을 트리거합니다. 동의 환경 설정이 변경될 때마다 &quot;동의 설정&quot; 작업을 사용해야 합니다. 확장에 &quot;동의 설정&quot; 작업을 추가하고 양식을 다음과 같이 입력합니다.

* 표준: &quot;IAB TCF&quot;
* 버전: &quot;2.0&quot;
* 값: &quot;%IAB TCF 동의 문자열%&quot;
* GDPR 적용: &quot;%IAB TCF 동의 GDPR%&quot;

![IAB 동의 설정 작업](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>이러한 데이터 요소는 사용자 지정 코드를 통해 만들어졌기 때문에 데이터 요소 선택기를 사용하여 선택할 수 없습니다. 퍼센트 기호가 있는 데이터 요소 이름을 입력해야 합니다. 이 코드는 고객이 변경될 때마다 새로운 동의 환경 설정으로 고객의 프로필을 업데이트합니다. 또한 서버는 쿠키 값을 반환하므로 Adobe Experience Platform Web SDK에서 경험 이벤트를 기록하지 못할 수 있습니다.

## 경험 이벤트에 대한 XDM 데이터 요소 생성

동의 문자열은 XDM 경험 이벤트에 포함되어야 합니다. 이렇게 하려면 XDM 개체 데이터 요소를 사용합니다. 새 XDM 개체 데이터 요소를 만들거나 이미 만든 데이터 요소를 이벤트 전송에 사용합니다. 스키마에 경험 이벤트 개인 정보 보호 스키마 필드 그룹을 추가한 경우 XDM 개체에 `consentStrings` 키가 있어야 합니다.

1. **[!UICONTROL consentStrings]**&#x200B;를 선택하십시오.

1. **[!UICONTROL 개별 항목 제공]**&#x200B;을 선택하고 **[!UICONTROL 항목 추가]**&#x200B;를 선택합니다.

1. **[!UICONTROL consentString]** 제목을 확장하고 첫 번째 항목을 확장한 다음 다음 값을 입력하십시오.

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %IAB TCF 동의 문자열%
* `gdprApplies`: %IAB TCF 동의 GDPR%

>[!IMPORTANT]
>
>이러한 데이터 요소는 사용자 지정 코드를 통해 만들어졌기 때문에 데이터 요소 선택기를 사용하여 선택할 수 없습니다. 퍼센트 기호가 있는 데이터 요소 이름을 입력해야 합니다.

## IAB TCF 2.0 동의 정보로 초기 경험 이벤트 보내기

페이지의 초기 경험 이벤트가 페이지 로드 이벤트로 트리거되는 경우 동의 문자열이 아직 로드되지 않았을 수 있습니다. 이 규칙은 현재 페이지 로드 이벤트를 대체하기 위한 것입니다. 동의 정보가 먼저 로드되었는지 확인하려면 새 규칙을 만들고 다음 코드를 사용자 지정 코드 이벤트로 추가합니다.

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

이 코드는 `useractioncomplete` 및 `tcloaded` 이벤트가 모두 처리된다는 점을 제외하면 이전 사용자 지정 코드와 동일합니다. [이전 사용자 지정 코드](#consent-code-1)은(는) 고객이 처음으로 기본 설정을 선택할 때만 트리거됩니다. 이 코드는 고객이 이미 환경 설정을 선택한 경우에도 트리거됩니다. 예를 들어 두 번째 페이지 로드 시.

Experience Platform Web SDK 확장 기능에서 &quot;이벤트 보내기&quot; 작업을 추가합니다. XDM 필드 내에서 이전 섹션에서 만든 XDM 데이터 요소를 선택합니다.

## IAB TCF 2.0 동의 정보로 다른 이벤트 보내기

초기 경험 이벤트 후에 이벤트가 트리거되면 두 데이터 요소가 계속 정의되므로 IAB 동의 정보를 전송하는 데 사용할 수 있습니다. 향후 이벤트를 전송하려면 동일한 XDM 데이터 요소를 사용합니다. IAB TCF 2.0 정보가 포함되어 있습니다.

## 다음 단계

Experience Platform Web SDK 확장 기능과 함께 IAB TCF 2.0을 사용하는 방법에 대해 배웠으므로 Adobe Analytics 또는 Adobe Real-Time Customer Data Platform과 같은 다른 Adobe 솔루션과 통합하도록 선택할 수도 있습니다. 자세한 내용은 [IAB Transparency &amp; Consent Framework 2.0 개요](./overview.md)를 참조하십시오.
