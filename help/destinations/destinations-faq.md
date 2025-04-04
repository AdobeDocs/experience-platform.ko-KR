---
keywords: 대상; 질문; faq; faq; 대상 faq
title: 자주 묻는 질문
description: Adobe Experience Platform 대상에 대해 가장 자주 묻는 질문에 대한 답변
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 0%

---

# 자주 묻는 질문 {#faq}

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 대상에 대한 FAQ에 대한 답변을 제공합니다. 모든 [!DNL Experience Platform] API에서 발생한 문제를 포함하여 다른 [!DNL Experience Platform] 서비스와 관련된 질문 및 문제 해결은 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

## 일반 대상 질문 {#general}

### Experience Platform UI와 내보낸 CSV 파일에서 다른 프로필 수가 표시되는 이유는 무엇입니까?

+++답변
이는 Experience Platform이 세그먼테이션을 수행하는 방식으로 인해 발생하는 일반적인 비헤이비어입니다.

스트리밍 세분화는 하루 종일 스트리밍 대상의 프로필 수를 업데이트하는 반면, 배치 세분화는 24시간마다 한 번씩 배치 대상의 프로필 수를 업데이트합니다.

대상 내보내기 일정이 세분화 일정과 다를 경우 특히 스트리밍 대상의 경우 UI와 내보낸 [!DNL CSV] 파일 간의 프로필 수가 달라집니다.

자세한 내용은 [세그먼테이션 서비스 설명서](../segmentation/home.md)를 참조하세요.
+++

### 업데이트된 대상을 동일한 대상으로 비활성화하고 다시 활성화하면 낮은 일치율이 표시되는 이유는 무엇입니까?

+++답변

스트리밍 대상에서 대상 비활성화 및 제거는 동일한 스트리밍 대상으로 대상 재활성화 시 채우기를 트리거하지 않습니다.

**예**

스트리밍 대상에 대해 10개의 프로필로 구성된 대상을 활성화했습니다.

대상을 활성화한 후에는 대상 구성을 변경하려고 하므로 대상을 비활성화하고 모집단 기준을 변경하여 100개의 프로필로 대상 모집단을 유도합니다.

업데이트된 대상을 동일한 대상으로 다시 활성화하지만 트리거된 채우기가 없으므로 대상에 추가 90개의 프로필이 수신되지 않습니다.

**솔루션**

모든 프로필이 대상으로 전송되도록 하려면 새 구성으로 새 대상을 만든 다음 대상에 대해 활성화해야 합니다.

+++

### 대상이 대상에서 제거되면 대상이 제거되었음을 나타내는 신호가 대상으로 전송됩니까?

+++답변

아니요. 타겟 시스템의 Experience Platform 대상과 고객 인스턴스 사이에는 종속성이 없습니다. 수신 측에서 타겟 시스템에서 볼 수 있는 유일한 표시는 해당 대상 데이터의 수신을 중단했다는 것입니다.

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### [!DNL Facebook Custom Audiences]에서 대상을 활성화하려면 먼저 무엇을 해야 합니까?

+++답변
대상자를 [!DNL Facebook]&#x200B;(으)로 보내려면 먼저 다음 요구 사항을 충족하는지 확인하십시오.

* [!DNL Facebook] 사용자 계정에는 사용할 광고 계정에 대해 **[!DNL Manage campaigns]** 권한이 활성화되어 있어야 합니다.
* **Adobe Experience Cloud** 비즈니스 계정을 [!DNL Facebook Ad Account]의 광고 파트너로 추가해야 합니다. `business ID=206617933627973` 사용. 자세한 내용은 Facebook 설명서의 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897)를 참조하십시오.

  >[!IMPORTANT]
  >
  > Adobe Experience Cloud에 대한 권한을 구성할 때는 **캠페인 관리** 권한을 활성화해야 합니다. [!DNL Adobe Experience Platform] 통합에 필요합니다.
* [!DNL Facebook Custom Audiences] 서비스 약관을 읽고 서명합니다. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`(으)로 이동하십시오. 여기서 `accountID`은(는) [!DNL Facebook Ad Account ID]입니다.
+++

### [!DNL Facebook] 광고주 계정에 앱 또는 픽셀을 추가해야 합니까?

+++답변
아니. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.
+++

### Facebook에서 Adobe Experience Platform의 정보를 처리하는 데 시간이 얼마나 걸립니까?

+++답변
2021년 3월부터 [!DNL Facebook Custom Audiences]이(가) [!DNL Experience Platform]에서 받은 정보를 처리하려면 최대 한 시간이 필요합니다.
+++

### [!DNL Instagram]과(와) 같은 다른 [!DNL Facebook] 앱에서 대상 타깃팅에 [!DNL Facebook Custom Audiences]을(를) 사용할 수 있습니까?

+++앰셔어
[!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] 및 [!DNL Messenger]을(를) 포함하여 [!DNL Facebook Custom Audiences]에서 지원하는 Facebook의 앱 제품군에서 대상 타깃팅에 [!DNL Facebook Custom Audiences] 대상을 사용할 수 있습니다. 광고주가 캠페인을 실행할 앱의 선택은 [!DNL Facebook Ads Manager]의 배치 수준에서 표시됩니다.
+++

### [!DNL Facebook Custom Audiences] 연결과 [!DNL Facebook Pixel] 확장 간의 차이점은 무엇입니까?

+++답변
[!DNL Facebook Custom Audiences] 연결에서는 대상을 [!DNL Facebook]에 보낼 때 [!DNL Experience Platform] ID를 사용하는 반면 [[!DNL Facebook Pixel] 연결](../destinations/catalog/advertising/facebook-pixel.md)에서는 웹 사이트에 통합된 [!DNL Facebook] 픽셀을 사용합니다.

이 두 가지 통합은 상호 보완적입니다. 두 가지 모두를 사용하여 대상 범위를 개선할 수 있습니다. 예를 들어 계정을 만들지 않은 웹 사이트 방문자를 예상하는 데 [!DNL Facebook Pixel] 확장을 사용할 수 있지만, [!DNL Facebook Custom Audiences]은(는) [!DNL Experience Platform]개의 ID를 기반으로 기존 고객을 타깃팅하는 데 도움이 될 수 있습니다.
+++

### [!DNL Facebook Custom Audiences]과(와) Adobe Experience Platform 통합은 더 이상 자격이 없는 사용자가 대상자로부터 자격을 박탈하는 것을 지원합니까?**

+++답변
예. 통합은 더 이상 자격이 없는 사용자를 [!DNL Facebook Custom Audiences]에서 제거할 수 있도록 지원합니다.
+++

### 대상 데이터를 [!DNL Facebook]에 보내기 전에 해시하려면 어떻게 해야 합니까?

+++답변
[!DNL Facebook]을(를) 사용하려면 PII(개인 식별 정보)를 명확하게 보내지 않아야 합니다. 따라서 [!DNL Facebook]에 대해 활성화된 대상은 이메일 주소 또는 전화 번호와 같은 *hashed* 식별자에서 벗어날 수 있습니다.

ID 일치 요구 사항에 대한 자세한 설명은 [ID 일치 요구 사항](catalog/social/facebook.md#id-matching-requirements)을 참조하십시오.
+++

### [!DNL Facebook Custom Audiences]에서 활성화할 수 있는 ID 종류

+++답변
[!DNL Facebook Custom Audiences]은(는) 해시된 이메일, 해시된 전화번호, [!DNL GAID], [!DNL IDFA] 및 사용자 지정 외부 ID와 같은 ID의 활성화를 지원합니다.
+++

### 별도의 Facebook 계정에 대해 Experience Platform UI에서 여러 Facebook 대상을 만들 수 있습니까?

+++답변
예. Experience Platform의 Facebook 대상은 Facebook의 광고 계정에 1:1입니다. 회사의 각 Facebook 광고 계정에 대해 별도의 Facebook 대상을 만들 수 있습니다. [대상 연결 자습서](/help/destinations/ui/connect-destination.md)를 따라 Experience Platform UI에서 각 새 Facebook 대상에 대해 별도의 Facebook 계정에 연결합니다. 연결할 수 있는 Facebook 광고 계정 수에는 제한이 없습니다.
+++

## Google 고객 일치 타겟팅 {#google-customer-match}

### 대상을 Google Customer Match로 내보낼 때 Google 인터페이스의 대상 이름 끝에 추가된 숫자가 표시되는 이유는 무엇입니까?

+++답변
Google에서는 대상 이름이 고유해야 합니다. 표시되는 숫자는 [UNIX 타임스탬프](https://www.unixtimestamp.com/)이며 동일한 대상을 여러 Google 대상에 매핑한 경우 대상 이름을 고유하게 유지하기 위해 추가됩니다.
+++

## LinkedIn 일치하는 대상 {#linkedin}

### [!DNL LinkedIn] 광고주 계정에 앱 또는 픽셀을 추가해야 합니까?

+++답변
아니. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.
+++

### [!DNL LinkedIn Matched Audiences]에서 대상을 활성화하려면 먼저 무엇을 해야 합니까?

+++답변
[!UICONTROL LinkedIn 일치하는 대상] 대상을 사용하려면 먼저 [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상이 있는지 확인하십시오.

[!DNL LinkedIn Campaign Manager] 사용자 권한을 편집하는 방법에 대해 알아보려면 LinkedIn 설명서에서 [Advertising 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753)를 참조하십시오.
+++

### 대상 데이터를 [!DNL LinkedIn]에 보내기 전에 해시하려면 어떻게 해야 합니까?

+++답변
[!DNL LinkedIn]을(를) 사용하려면 PII(개인 식별 정보)를 명확하게 보내지 않아야 합니다. 따라서 [!DNL LinkedIn]에 대해 활성화된 대상은 이메일 주소 또는 전화 번호와 같은 *hashed* 식별자에서 벗어날 수 있습니다.

ID 일치 요구 사항에 대한 자세한 설명은 [ID 일치 요구 사항](catalog/social/linkedin.md#id-matching-requirements)을 참조하십시오.
+++

### [!DNL LinkedIn]에서 활성화할 수 있는 ID 종류

+++답변
[!DNL LinkedIn Matched Audiences]은(는) 해시된 이메일, [!DNL GAID] 및 [!DNL IDFA] id의 활성화를 지원합니다.

+++

## Adobe Target 및 사용자 지정 Personalization 대상을 통한 동일 페이지 및 다음 페이지 개인화 {#same-next-page-personalization}

### Experience Platform Web SDK을 사용하여 대상과 속성을 Adobe Target으로 전송해야 합니까?

+++답변
아니요. [웹 SDK](../web-sdk/home.md)은(는) 대상자를 [Adobe Target](catalog/personalization/adobe-target-connection.md)에 활성화하기 위해 필요하지 않습니다.

그러나 Web SDK 대신 [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html)을(를) 사용하면 다음 세션 개인화만 지원됩니다.

[동일 페이지 및 다음 페이지 개인화](ui/activate-edge-personalization-destinations.md) 사용 사례의 경우 [Web SDK](../web-sdk/home.md) 또는 [Edge Network Server API](../server-api/overview.md)를 사용해야 합니다. 자세한 구현 정보는 [Edge 대상으로 대상 활성화](ui/activate-edge-personalization-destinations.md)에 대한 설명서를 참조하십시오.
+++

### Real-time Customer Data Platform에서 Adobe Target 또는 사용자 지정 Personalization 대상으로 보낼 수 있는 속성 수에 제한이 있습니까?

+++답변
예. 동일 페이지 및 다음 페이지 개인화 사용 사례는 Adobe Target 또는 사용자 지정 Personalization 대상으로 대상을 활성화할 때 샌드박스당 최대 30개의 속성을 지원합니다. 활성화 보호 기능에 대한 자세한 내용은 [보호 기능 설명서](guardrails.md#edge-destinations-activation)를 참조하세요.
+++

### 활성화에는 어떤 유형의 속성(예: 배열, 맵 등)이 지원됩니까?

+++답변
현재 `person.name.firstName`과(와) 같은 정적 단일 값 특성만 지원됩니다. 배열 속성은 현재 지원되지 않습니다.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Experience Platform에서 대상을 만들면 Edge 세그멘테이션 사용 사례에 해당 대상을 사용할 수 있는 데 얼마나 걸립니까?

+++답변
대상 정의가 최대 1시간 후에 [Edge Network](../web-sdk/home.md)에 전파됩니다. 그러나 대상이 이 첫 번째 시간 내에 활성화되면 대상의 자격이 되었을 일부 방문자를 놓칠 수 있습니다.
+++

### Adobe Target에서 활성화된 속성은 어디에서 볼 수 있습니까?

+++답변
[JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) 및 [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html) 오퍼의 Target에서 특성을 사용할 수 있습니다.
+++

### 데이터스트림 없이 대상을 만든 다음 나중에 동일한 대상에 데이터스트림을 추가할 수 있습니까?

+++답변
대상 UI를 통해서는 현재 지원되지 않습니다. 이 경우 도움이 필요한 경우 Adobe 담당자에게 문의하십시오.
+++

### Adobe Target 대상을 삭제하면 어떻게 됩니까?

+++답변
대상을 삭제하면 대상 아래에 매핑된 모든 대상 및 특성이 Adobe Target에서 삭제되며, Edge Network에서도 제거됩니다.
+++

### 통합은 Edge Network Server API를 사용하여 작동합니까?

+++답변
예. Edge Network 서버 API는 사용자 지정 Personalization 대상에서 작동합니다. 프로필 속성에 중요한 데이터가 포함될 수 있으므로 이 데이터를 보호하려면 사용자 지정 Personalization 대상에서 데이터 수집을 위해 Edge Network Server API를 사용해야 합니다. 또한 모든 API 호출은 [인증된 컨텍스트](../server-api/authentication.md)에서 수행되어야 합니다.
+++

### 에지 상에서 활성 상태인 병합 정책을 하나만 가질 수 있습니다. 다른 병합 정책을 사용하는 대상을 작성하고 이를 스트리밍 대상으로 Adobe Target에 보낼 수 있습니까?

+++답변
아니. Adobe Target에 활성화하려는 모든 대상은 Active-On-Edge [병합 정책](../profile/merge-policies/ui-guide.md)을 사용해야 합니다.
+++

### 데이터 사용 레이블 및 적용 (DULE) 및 동의 정책이 적용됩니까?

+++답변
예. 선택한 마케팅 작업과 관련하여 만들어지고 연결된 [데이터 거버넌스 및 동의 정책](../data-governance/home.md)은(는) 선택한 특성의 활성화를 제어합니다.
+++

### [!DNL Adobe Target] 및 [!DNL Custom Personalization] 대상이 [!DNL HIPAA]을(를) 준수합니까?

+++답변
[!DNL Adobe Target]이(가) [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html)과(와) 호환되지 않습니다. [!DNL HIPPA] 고객은 [!DNL Adobe Target] 또는 [!DNL Custom Personalization] 대상을 통해 Edge 개인화를 사용하기 전에 사용자 지정 최적화 채널에 대한 [!DNL HIPPA] 준비 상태를 자체 법률팀에 확인해야 합니다.

동의 정책 관리를 규모에 맞게 적용해야 하는 사용 사례의 경우 고객은 [!DNL Adobe Privacy & Security Shield]을(를) 구매해야 합니다. [!DNL Adobe Privacy & Security Shield] 기능은 고급 기능 세트로 판매되며 별도로 구입할 수 없습니다.

이 서비스에는 고객 관리 키와 높아진 임계값이 포함되어 있어 고객 데이터 수명주기를 관리할 수 있습니다.

[!DNL Adobe Target] 및 [!DNL Custom Personalization] 대상은 [Experience Platform 데이터 사용 레이블](../data-governance/labels/overview.md) 및 [동의 정책 시행 서비스](../data-governance/enforcement/overview.md)와 통합됩니다. 이러한 기능은 모든 고객이 사용할 수 있습니다.




+++

