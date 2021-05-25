---
keywords: 대상;질문FAQfaq;대상 faq
title: Experience Cloud 핵심 서비스에 대한
seo-title: Experience Cloud 핵심 서비스에 대한
description: Adobe Experience Platform 대상에 대해 자주 묻는 질문과 대답(FAQ)입니다
seo-description: Adobe Experience Platform 대상에 대해 자주 묻는 질문과 대답(FAQ)입니다
source-git-commit: 47b3ef28281e3480e8b194486845f4fb4326b7d4
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 6%

---


# Experience Cloud 핵심 서비스에 대한 {#faq}

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 대상에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 모든 [!DNL Platform] API에서 발생한 서비스 등 다른 [!DNL Platform] 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**에서 대상을 활성화하기 전에 어떻게 해야 합니까 [!DNL Facebook Custom Audiences]?**

대상 세그먼트를 [!DNL Facebook]에 보내려면 먼저 다음 요구 사항을 충족하는지 확인하십시오.

* 사용하려는 광고 계정에 대해 **[!DNL Manage campaigns]** 사용 권한이 활성화되어 있어야 합니다.[!DNL Facebook]
* **Adobe Experience Cloud** 비즈니스 계정은 [!DNL Facebook Ad Account]에서 광고 파트너로서 추가해야 합니다.  `business ID=206617933627973`. 자세한 내용은 Facebook 설명서의 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897)를 참조하십시오.
   >[!IMPORTANT]
   >
   > Adobe Experience Cloud에 대한 권한을 구성할 때 **캠페인 관리** 권한을 활성화해야 합니다. 이 단계는 [!DNL Adobe Experience Platform] 통합에 필요합니다.
* [!DNL Facebook Custom Audiences] 서비스 약관을 읽고 서명하십시오. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`로 이동하십시오. 여기서 `accountID`는 [!DNL Facebook Ad Account ID]입니다.

**내 광고주 계정에 앱이나 픽셀을 추가해야  [!DNL Facebook] 합니까?**

아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.

**facebook은 Adobe Experience Platform에서 정보를 처리하는 데 얼마나 걸립니까?**

2021년 3월 현재 [!DNL Facebook Custom Audiences]은 [!DNL Platform]에서 수신한 정보를 처리하는 데 최대 1시간이 필요합니다.

**과 같은 다른 앱 [!DNL Facebook Custom Audiences] 에서 대상 타깃팅 [!DNL Facebook] 에 을 사용할 수  [!DNL Instagram]있습니까?**

[!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] 및 [!DNL Messenger]를 포함하여 [!DNL Facebook Custom Audiences]에서 지원하는 Facebook의 앱 제품군에서 대상 타깃팅에 [!DNL Facebook Custom Audiences] 대상을 사용할 수 있습니다. 캠페인을 실행할 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.

**연결과 확장의  [!DNL Facebook Custom Audiences] 차이점은  [!DNL Facebook Pixel] 무엇입니까?**

[!DNL Facebook Custom Audiences] 연결은 대상자를 [!DNL Facebook]에 보낼 때 [!DNL Platform] ID를 사용하는 반면, [[!DNL Facebook Pixel] 연결](../destinations/catalog/advertising/facebook-pixel.md)은 웹 사이트에 통합된 [!DNL Facebook] 픽셀을 사용합니다.

이 두 가지 통합은 상호 보완적입니다. 두 가지 모두를 사용하여 대상 범위를 개선할 수 있습니다. 예를 들어 [!DNL Facebook Pixel] 확장을 사용하여 계정을 만들지 않은 웹 사이트 방문자를 예상할 수 있지만 [!DNL Facebook Custom Audiences] 은 [!DNL Platform] ID를 기반으로 기존 고객을 타깃팅하는 데 도움이 될 수 있습니다.

**Adobe Experience Platform과  [!DNL Facebook Custom Audiences] 통합하면 대상이 더 이상 해당 대상에 적합하지 않을 때 대상에서 자격을 상실합니까?**

예. 통합은 더 이상 자격이 없는 사용자를 [!DNL Facebook Custom Audiences]에서 제거할 수 있도록 지원합니다.

**전송하기 전에 대상 데이터를 해시하려면 어떻게 해야  [!DNL Facebook]합니까?**

[!DNL Facebook] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 [!DNL Facebook]에 활성화된 대상은 이메일 주소 또는 전화 번호와 같이 *해시된* 식별자를 사용할 수 있습니다.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/facebook.md#id-matching-requirements)을 참조하십시오.

**에서 활성화할 수 있는 ID는 무엇입니까 [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 은 다음 ID의 활성화를 지원합니다.해시된 이메일, 해시된 전화번호,  [!DNL GAID] [!DNL IDFA], 및 사용자 지정 외부 ID.

## linkedIn 일치하는 대상 {#linkedin}

**내 광고주 계정에 앱이나 픽셀을 추가해야  [!DNL LinkedIn] 합니까?**

아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.

**에서 대상을 활성화하기 전에 어떻게 해야 합니까 [!DNL LinkedIn Matched Audiences]?**

[!UICONTROL LinkedIn Matched Audience] 대상을 사용하려면 먼저 [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상이 있는지 확인하십시오.

[!DNL LinkedIn Campaign Manager] 사용자 권한을 편집하는 방법에 대한 자세한 내용은 LinkedIn 설명서에서 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753)를 참조하십시오.

**전송하기 전에 대상 데이터를 해시하려면 어떻게 해야  [!DNL LinkedIn]합니까?**

[!DNL LinkedIn] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 [!DNL LinkedIn]에 활성화된 대상은 이메일 주소 또는 전화 번호와 같이 *해시된* 식별자를 사용할 수 있습니다.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/linkedin.md#id-matching-requirements)을 참조하십시오.

**에서 활성화할 수 있는 ID는 무엇입니까 [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 은 다음 ID의 활성화를 지원합니다.해시된 이메일,  [!DNL GAID] 및  [!DNL IDFA].
