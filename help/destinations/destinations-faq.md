---
keywords: 대상;질문;FAQfaq;대상 faq
title: 대상 FAQ
seo-title: 대상 FAQ
description: Adobe Experience Platform 대상에 대해 자주 묻는 질문에 대한 답변
seo-description: Adobe Experience Platform 대상에 대해 자주 묻는 질문에 대한 답변
source-git-commit: 61678c5a62980cdb81714420016b7c4b2093f5c6
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 5%

---


# 대상 FAQ {#faq}

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**대상을 활성화하려면 어떻게 해야  [!DNL Facebook Custom Audiences]합니까?**

대상 세그먼트를 [!DNL Facebook]에 보내려면 먼저 다음 요구 사항을 충족해야 합니다.

* [!DNL Facebook] 사용자 계정은 사용하려는 광고 계정에 대해 **[!DNL Manage campaigns]** 권한이 활성화되어 있어야 합니다.
* **Adobe Experience Cloud** 비즈니스 계정을 [!DNL Facebook Ad Account]에서 광고 파트너로 추가해야 합니다.  `business ID=206617933627973`. 자세한 내용은 Facebook 설명서의 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897)를 참조하십시오.
   >[!IMPORTANT]
   >
   > Adobe Experience Cloud에 대한 권한을 구성할 때 **캠페인 관리** 권한을 활성화해야 합니다. 이 단계는 [!DNL Adobe Experience Platform] 통합에 필요합니다.
* [!DNL Facebook Custom Audiences] 서비스 약관을 읽고 서명합니다. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`로 이동하십시오. 여기서 `accountID`는 [!DNL Facebook Ad Account ID]입니다.

**광고주 계정에 앱 또는 픽셀을 추가해야  [!DNL Facebook] 합니까?**

아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.

**facebook은 Adobe Experience Platform의 정보를 처리하는 데 얼마나 걸립니까?**

2021년 3월 현재 [!DNL Facebook Custom Audiences]은(는) [!DNL Platform]로부터 받은 정보를 처리하기 위해 최대 1시간이 필요합니다.

**예를 들어 다른 앱 [!DNL Facebook Custom Audiences] 에서 대상 타깃팅 [!DNL Facebook] 을 사용할 수 있습니까 [!DNL Instagram]?**

[!DNL Facebook Custom Audiences] 대상을 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] 및 [!DNL Messenger]를 포함하여 [!DNL Facebook Custom Audiences]에서 지원되는 Facebook의 앱 모음 전체에서 대상 타깃팅에 사용할 수 있습니다. 광고주가 캠페인을 실행하려는 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.

**연결과  [!DNL Facebook Custom Audiences] 확장자 간의 차이점은  [!DNL Facebook Pixel] 무엇입니까?**

[!DNL Facebook Custom Audiences] 연결은 대상을 [!DNL Facebook]으로 보낼 때 [!DNL Platform] ID를 사용하고 [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md)은 웹 사이트에 통합된 [!DNL Facebook] 픽셀을 사용합니다.

이 두 가지 통합은 상호 보완적입니다. 두 가지 모두를 사용하여 대상 범위를 개선할 수 있습니다. 예를 들어 계정을 만들지 않은 예상 웹 사이트 방문자에 대해 [!DNL Facebook Pixel] 확장을 사용할 수 있지만 [!DNL Facebook Custom Audiences]은 [!DNL Platform] ID를 기반으로 기존 고객을 타깃팅하는 데 도움이 될 수 있습니다.

**Adobe Experience Platform과 통합되어 있는  [!DNL Facebook Custom Audiences] 지원 기능을 통해 더 이상 대상이 아닌 사용자가 자격이 박탈될 수 있습니까?**

예. 통합이 더 이상 자격이 없는 사용자를 [!DNL Facebook Custom Audiences]에서 제거하는 것을 지원합니다.

**대상 데이터를 보내기 전에 해시하려면 어떻게 해야  [!DNL Facebook]합니까?**

[!DNL Facebook] 는 PII(개인 식별 정보)가 명확하게 전송되지 않도록 요구합니다. 따라서 [!DNL Facebook]에 대해 활성화된 대상은 이메일 주소 또는 전화 번호와 같은 *해시된* 식별자에서 키잉할 수 있습니다.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/facebook.md#id-matching-requirements)을 참조하십시오.

**어떤 유형의 ID를 활성화할 수  [!DNL Facebook Custom Audiences]있습니까?**

[!DNL Facebook Custom Audiences] 에서는 다음 ID 활성화를 지원합니다.해시 처리된 이메일, 해시된 전화 번호,  [!DNL GAID] [!DNL IDFA]사용자 지정 외부 ID 및

## linkedIn 일치 대상 {#linkedin}

**광고주 계정에 앱 또는 픽셀을 추가해야  [!DNL LinkedIn] 합니까?**

아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.

**대상을 활성화하려면 어떻게 해야  [!DNL LinkedIn Matched Audiences]합니까?**

[!UICONTROL LinkedIn Matched Audience] 대상을 사용하려면 먼저 [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상이 있는지 확인하십시오.

[!DNL LinkedIn Campaign Manager] 사용자 권한을 편집하는 방법에 대한 자세한 내용은 LinkedIn 설명서의 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거를 참조하십시오.](https://www.linkedin.com/help/lms/answer/5753)

**대상 데이터를 보내기 전에 해시하려면 어떻게 해야  [!DNL LinkedIn]합니까?**

[!DNL LinkedIn] 는 PII(개인 식별 정보)가 명확하게 전송되지 않도록 요구합니다. 따라서 [!DNL LinkedIn]에 대해 활성화된 대상은 이메일 주소 또는 전화 번호와 같은 *해시된* 식별자에서 키잉할 수 있습니다.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/linkedin.md#id-matching-requirements)을 참조하십시오.

**어떤 유형의 ID를 활성화할 수  [!DNL LinkedIn]있습니까?**

[!DNL LinkedIn Matched Audiences] 에서는 다음 ID 활성화를 지원합니다.해시된 이메일,  [!DNL GAID]및  [!DNL IDFA]
