---
title: 동의 설정
description: 방문자에 대해 원하는 동의를 설정합니다.
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 동의 설정

**[!UICONTROL Set consent]** 작업은 태그 확장에서 데이터를 보내야 하는지(옵트인), 데이터를 버려야 하는지(옵트아웃) 또는 [기본 동의](../configure/consent.md)(알 수 없는 동의)를 사용해야 하는지 여부를 결정합니다. 사용자가 사이트에서 동의를 허용하거나 거부하는 경우 이 작업을 사용하여 환경 설정을 태그 확장과 동기화할 수 있습니다. 이 작업에 해당하는 JavaScript 라이브러리는 [`setConsent`](/help/collection/js/commands/setconsent.md) 명령입니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Rules]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL Actions]에서 기존 작업을 선택하거나 작업을 만듭니다.
1. [!UICONTROL Extension] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정한 다음 [!UICONTROL Action type]을(를) **[!UICONTROL Set consent]**(으)로 설정합니다.

태그 확장은 다음 표준을 지원합니다.

* **[Adobe 표준](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: 1.0 및 2.0 표준이 모두 지원됩니다.
* **[IAB 투명도 및 동의 프레임워크](/help/landing/governance-privacy-security/consent/iab/overview.md)**: 이 표준을 사용하는 경우, 구현이 올바르게 구성된 경우 방문자의 실시간 고객 프로필이 동의 정보로 업데이트됩니다.
   1. XDM 개인 프로필 스키마에 [IAB TCF 2.0 동의 필드 그룹](/help/xdm/field-groups/profile/iab.md)이(가) 포함되어 있습니다.
   1. 경험 이벤트 스키마에 [IAB TCF 2.0 동의 필드 그룹](/help/xdm/field-groups/event/iab.md)이(가) 있습니다.

Adobe에서는 동의 대화 상자 환경 설정을 데이터 요소와 같이 별도로 저장하는 것을 권장합니다. 태그 확장은 동의를 검색하는 방법을 제공하지 않습니다. 사용자 환경 설정이 태그 확장과 계속 동기화되도록 하려면 모든 페이지 로드 시 이 작업을 수행할 수 있습니다.

## 사용 가능한 필드

이 작업 유형은 다음 구성 옵션을 지원합니다.

* **[!UICONTROL Instance]**: 작업이 적용되는 SDK 인스턴스입니다. 구현에서 단일 SDK 인스턴스를 사용하는 경우 이 드롭다운 메뉴가 비활성화됩니다.
* **[!UICONTROL Identity map]**: ECID 생성 방법과 연결된 ID 동의 정보를 제어하는 데이터 요소입니다.
* **[!UICONTROL Consent information]**: 양식을 작성할지 또는 동의 정보가 포함된 데이터 요소를 제공할지 여부를 결정합니다.
* **[!UICONTROL Standard]**: 사용할 동의 표준입니다. 사용 가능한 옵션에는 &#39;[!UICONTROL Adobe]&#39; 및 &#39;[!UICONTROL IAB TCF]&#39;이(가) 있습니다.
* **[!UICONTROL Version]**: 사용할 동의 표준의 버전입니다.
* **[!UICONTROL Datastream configuration overrides]**: 이 명령은 데이터 스트림 구성 재정의를 지원하므로 이 데이터를 받을 앱 및 서비스를 제어할 수 있습니다. 개별 명령과 태그 확장 구성 설정 모두에서 데이터스트림 구성 재정의를 설정하면 개별 명령이 우선합니다. 자세한 내용은 [데이터 스트림 구성 재정의](../configure/configuration-overrides.md)를 참조하십시오.

## 동의 정보를 업데이트하는 규칙 만들기

이 작업을 사용하는 가장 이상적인 시기는 고객의 동의 환경 설정이 변경된 때입니다. 태그 규칙을 만들어 이 변경 내용을 수신할 수 있습니다.

1. 태그 속성 내에서 **[!UICONTROL Rules]**(으)로 이동하여 **[!UICONTROL Add rule]**&#x200B;을(를) 선택합니다.
1. 규칙에 원하는 이름을 지정한 다음 `+` 옆에 있는 &#39;**[!UICONTROL Events]**&#39; 아이콘을 선택합니다.
1. 왼쪽에서 다음 속성을 설정합니다.
   * **[!UICONTROL Extension]**:[!UICONTROL Core]
   * **[!UICONTROL EVent type]**: [!UICONTROL Custom code]
1. 오른쪽의 편집기를 열고 다음 코드를 템플릿으로 사용합니다.

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

1. **[!UICONTROL Keep changes]**&#x200B;를 선택합니다.

위의 사용자 지정 코드 블록은 다음 두 가지 작업을 수행합니다.

* 동의 환경 설정이 변경되면 규칙을 트리거합니다.
* 두 개의 데이터 요소 **IAB TCF 동의 문자열** 및 **IAB TCF 동의 GDPR**&#x200B;을 설정합니다.

이러한 데이터 요소는 &#39;[!UICONTROL Set Consent]&#39; 작업을 설정할 때 유용합니다.

1. `+` 옆에 있는 &#39;**[!UICONTROL Actions]**&#39; 아이콘을 선택하십시오.
1. 왼쪽에서 다음 속성을 설정합니다.
   * **[!UICONTROL Extension]**:[!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Set consent]
1. 오른쪽에서 다음 속성을 설정합니다.
   * **[!UICONTROL Standard]**:[!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**:[!UICONTROL 2.0]
   * **[!UICONTROL Value]**: `%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**: [!UICONTROL Provide a data element]&#x200B;(값: `%IAB TCF Consent GDPR%`)

![IAB 동의 설정 작업](../assets/iab-action.png)

>[!NOTE]
>
>이러한 데이터 요소는 사용자 지정 코드를 통해 만들어졌기 때문에 데이터 요소 선택기를 사용하여 선택할 수 없습니다. 퍼센트 기호가 있는 데이터 요소 이름을 입력해야 합니다.
