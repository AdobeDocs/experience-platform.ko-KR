---
keywords: 대상; 질문; faq; faq; 대상 faq
title: 자주 묻는 질문
description: Adobe Experience Platform 대상에 대해 가장 자주 묻는 질문에 대한 답변
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: dff460f0b0d365d3d643744544642d9f9488e18a
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 2%

---

# 자주 묻는 질문 {#faq}

## 개요 {#overview}

이 문서에서는 Adobe Experience Platform 대상에 대한 FAQ에 대한 답변을 제공합니다. 기타 관련 질문 및 문제 해결 [!DNL Platform] 모든 상황에서 발생하는 서비스를 포함한 서비스 [!DNL Platform] API, 다음을 참조하십시오. [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

## 일반 대상 질문 {#general}

### Experience Platform UI와 내보낸 CSV 파일에서 다른 프로필 수가 표시되는 이유는 무엇입니까?

+++답변 Experience Platform이 세그먼테이션을 수행하는 방식으로 인해 발생하는 일반적인 비헤이비어입니다.

스트리밍 세분화는 하루 종일 스트리밍 대상의 프로필 수를 업데이트하는 반면, 배치 세분화는 24시간마다 한 번씩 배치 대상의 프로필 수를 업데이트합니다.

대상자 내보내기 일정이 세분화 일정과 다를 경우 프로필은 UI와 내보낸 프로필 간에 계산됩니다 [!DNL CSV] 특히 스트리밍 대상과 관련된 파일은 다를 수 있습니다.

다음을 참조하십시오. [세그먼테이션 서비스 설명서](../segmentation/home.md) 을 참조하십시오.
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

### 에서 대상자를 활성화하려면 먼저 무엇을 해야 합니까 [!DNL Facebook Custom Audiences]?

+++대상자를 다음으로 보내려면 먼저 답변하십시오. [!DNL Facebook], 다음 요구 사항을 충족하는지 확인하십시오.

* 사용자 [!DNL Facebook] 사용자 계정에는 **[!DNL Manage campaigns]** 사용하려는 광고 계정에 대해 권한이 활성화되었습니다.
* 다음 **Adobe Experience Cloud** 비즈니스 계정을 의 광고 파트너로 추가해야 합니다. [!DNL Facebook Ad Account]. `business ID=206617933627973`를 사용하십시오. 다음을 참조하십시오 [비즈니스 관리자에 파트너 추가](https://www.facebook.com/business/help/1717412048538897) 자세한 내용은 Facebook 설명서 를 참조하십시오.

  >[!IMPORTANT]
  >
  > Adobe Experience Cloud에 대한 권한을 구성할 때 다음을 활성화해야 합니다 **캠페인 관리** 권한. 이 단계는 [!DNL Adobe Experience Platform] 통합에 필요합니다.
* 읽기 및 서명 [!DNL Facebook Custom Audiences] 서비스 약관. 이렇게 하려면 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`로 이동하십시오. 여기서 `accountID`는 [!DNL Facebook Ad Account ID]입니다.
+++

### 에 앱 또는 픽셀을 추가해야 합니까? [!DNL Facebook] 광고주 계정이요?

+++아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.
+++

### facebook에서 Adobe Experience Platform의 정보를 처리하는 데 시간이 얼마나 걸립니까?

+++2021년 3월 현재 답변, [!DNL Facebook Custom Audiences] 에서 받은 정보를 처리하려면 최대 1시간이 필요합니다. [!DNL Platform].
+++

### 사용할 수 있습니까 [!DNL Facebook Custom Audiences] 기타 대상의 대상 타깃팅 [!DNL Facebook] 앱, 예 [!DNL Instagram]?

+++Amswer 다음을 사용할 수 있습니다. [!DNL Facebook Custom Audiences] 에서 지원하는 Facebook 앱 제품군의 대상 타겟팅 [!DNL Facebook Custom Audiences], 포함 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], 및 [!DNL Messenger]. 광고주가 캠페인을 실행할 앱의 선택은 의 배치 수준에서 표시됩니다. [!DNL Facebook Ads Manager].
+++

### 차이점이 무엇입니까 [!DNL Facebook Custom Audiences] 연결 및 [!DNL Facebook Pixel] 확장?

+++답변: [!DNL Facebook Custom Audiences] 연결 사용 [!DNL Platform] 대상자를 (으)로 보낼 때 ID [!DNL Facebook], 반면에 [[!DNL Facebook Pixel] 연결](../destinations/catalog/advertising/facebook-pixel.md) 를 사용합니다. [!DNL Facebook] 웹 사이트에 통합된 픽셀.

이 두 가지 통합은 상호 보완적입니다. 두 가지 모두를 사용하여 대상 범위를 개선할 수 있습니다. 예를 들어 [!DNL Facebook Pixel] 계정을 만들지 않은 웹 사이트 방문자를 예견하는 데 사용되는 확장 프로그램입니다. [!DNL Facebook Custom Audiences] 을(를) 통해 다음을 기반으로 기존 고객을 타겟팅할 수 있습니다. [!DNL Platform] id입니다.
+++

### Adobe Experience Platform 통합 대상 [!DNL Facebook Custom Audiences] 더 이상 자격이 없는 경우 대상에서 자격을 박탈하는 사용자를 지원합니다?**

+++답변 예, 통합에서 사용자 제거를 지원합니다. [!DNL Facebook Custom Audiences] 더 이상 자격이 없을 때.
+++

### 대상 데이터를에 보내기 전에 해시하려면 어떻게 해야 합니까? [!DNL Facebook]?

+++답변
[!DNL Facebook] 을 사용하려면 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상자는에 대해 활성화됩니다. [!DNL Facebook] 키 사용 안 함 *해시됨* 이메일 주소 또는 전화번호 등 식별자.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/facebook.md#id-matching-requirements).
+++

### 에서 활성화할 수 있는 ID 종류 [!DNL Facebook Custom Audiences]?

+++답변
[!DNL Facebook Custom Audiences] 은(는) 해시된 이메일, 해시된 전화번호, [!DNL GAID], [!DNL IDFA]및 사용자 지정 외부 ID입니다.
+++

### 별도의 Facebook 계정에 대해 Platform UI에서 여러 Facebook 대상을 만들 수 있습니까?

+++예 라고 답하십시오. Experience Platform의 Facebook 대상은 Facebook의 광고 계정으로 1:1입니다. 회사의 각 Facebook 광고 계정에 대해 별도의 Facebook 대상을 만들 수 있습니다. 다음 [대상 연결 자습서](/help/destinations/ui/connect-destination.md) 플랫폼 UI에서 각각의 새로운 Facebook 대상에 대한 별도의 Facebook 계정에 연결합니다. 연결할 수 있는 Facebook 광고 계정 수에는 제한이 없습니다.
+++

## Google Customer Match {#google-customer-match}

### 대상을 Google Customer Match로 내보낼 때 Google 인터페이스의 대상 이름 끝에 추가된 숫자가 표시되는 이유는 무엇입니까?

+++답변 Google을 사용하려면 대상 이름이 고유해야 합니다. 지금 보시는 숫자는 다음과 같습니다 [UNIX 타임스탬프](https://www.unixtimestamp.com/) 그리고 동일한 대상을 여러 Google 대상에 매핑한 경우 대상 이름을 고유하게 유지하기 위해 추가됩니다.
+++

## LinkedIn과 일치하는 대상 {#linkedin}

### 에 앱 또는 픽셀을 추가해야 합니까? [!DNL LinkedIn] 광고주 계정이요?

+++아니요. 픽셀 기반 통합이 아니므로 광고주 계정에 픽셀을 추가할 필요가 없습니다.
+++

### 에서 대상자를 활성화하려면 먼저 무엇을 해야 합니까 [!DNL LinkedIn Matched Audiences]?

+++사용하기 전에 답변 [!UICONTROL LinkedIn 일치 대상] 대상, 다음을 확인하십시오. [!DNL LinkedIn Campaign Manager] 계정이 다음을 보유함: [!DNL Creative Manager] 권한 수준 이상입니다.

을(를) 편집하는 방법에 대해 알아보려면 [!DNL LinkedIn Campaign Manager] 사용자 권한, 참조 [광고 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753) linkedIn 설명서에서 확인할 수 있습니다.
+++

### 대상 데이터를에 보내기 전에 해시하려면 어떻게 해야 합니까? [!DNL LinkedIn]?

+++답변
[!DNL LinkedIn] 을 사용하려면 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상자는에 대해 활성화됩니다. [!DNL LinkedIn] 키 사용 안 함 *해시됨* 이메일 주소 또는 전화번호 등 식별자.

ID 일치 요구 사항에 대한 자세한 내용은 [ID 일치 요구 사항](catalog/social/linkedin.md#id-matching-requirements).
+++

### 에서 활성화할 수 있는 ID 종류 [!DNL LinkedIn]?

+++답변
[!DNL LinkedIn Matched Audiences] 은(는) 해시된 이메일, [!DNL GAID], 및 [!DNL IDFA].

+++

## Adobe Target 및 사용자 지정 개인화 대상을 통한 동일 페이지 및 다음 페이지 개인화 {#same-next-page-personalization}

### Experience Platform Web SDK를 사용하여 대상과 속성을 Adobe Target으로 전송해야 합니까?

+++아니요, [웹 SDK](../edge/home.md) 대상자를 활성화하기 위해 이 필요하지 않음: [Adobe Target](catalog/personalization/adobe-target-connection.md).

그러나 다음과 같은 경우에는 [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) 는 Web SDK 대신 사용되며 다음 세션 개인화만 지원됩니다.

대상 [동일 페이지 및 다음 페이지 개인화](ui/activate-edge-personalization-destinations.md) 사용 사례는 다음 중 하나를 사용해야 합니다. [웹 SDK](../edge/home.md) 또는 [Edge Network Server API](../server-api/overview.md). 다음에서 설명서를 참조하십시오. [Edge 대상으로 대상자 활성화](ui/activate-edge-personalization-destinations.md) 구현 세부 사항.
+++

### Real-time Customer Data Platform에서 Adobe Target 또는 사용자 지정 개인화 대상으로 보낼 수 있는 속성 수에 제한이 있습니까?

+++예, 같은 페이지 및 다음 페이지 개인화 사용 사례는 Adobe Target 또는 사용자 지정 개인화 대상에 대한 대상자를 활성화할 때 샌드박스당 최대 30개의 속성을 지원합니다. 에서 활성화 가드레일에 대한 자세한 내용을 참조하십시오. [보호 기능 설명서](guardrails.md#edge-destinations-activation).
+++

### 활성화에는 어떤 유형의 속성(예: 배열, 맵 등)이 지원됩니까?

+++대답 현재 다음과 같은 정적 단일 값 속성만 지원됩니다. `person.name.firstName`. 배열 속성은 현재 지원되지 않습니다.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Experience Platform에서 대상자를 만들면 Edge 세그멘테이션 사용 사례에 해당 대상자를 사용할 수 있는 데 얼마나 걸립니까?

+++응답 대상 정의는 [에지 네트워크](../edge/home.md) 한 시간이면 됩니다. 그러나 대상이 이 첫 번째 시간 내에 활성화되면 대상의 자격이 되었을 일부 방문자를 놓칠 수 있습니다.
+++

### Adobe Target에서 활성화된 속성은 어디에서 볼 수 있습니까?

+++응답 속성은 의 Target에서 사용할 수 있습니다. [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) 및 [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html) 오퍼.
+++

### 데이터스트림 없이 대상을 만든 다음 나중에 동일한 대상에 데이터스트림을 추가할 수 있습니까?

+++답변 현재 대상 UI를 통해 지원되지 않습니다. 이 경우 도움이 필요한 경우 Adobe 담당자에게 문의하십시오.
+++

### Adobe Target 대상을 삭제하면 어떻게 됩니까?

+++대답: 대상을 삭제하면 대상 아래에 매핑된 모든 대상 및 특성이 Adobe Target에서 삭제되고 Edge Network에서도 제거됩니다.
+++

### Edge Network Server API를 사용하여 통합이 작동합니까?

+++예, Edge Network Server API는 사용자 지정 개인화 대상에서 작동합니다. 프로필 속성에 중요한 데이터가 포함될 수 있으므로 이 데이터를 보호하려면 사용자 지정 개인화 대상에서 데이터 수집에 Edge Network Server API를 사용해야 합니다. 또한 모든 API 호출은 [인증된 컨텍스트](../server-api/authentication.md).
+++

### 에지 상에서 활성 상태인 병합 정책을 하나만 가질 수 있습니다. 다른 병합 정책을 사용하는 대상을 작성하고 이를 스트리밍 대상으로 Adobe Target에 보낼 수 있습니까?

+++아니요. Adobe Target에 활성화하려는 모든 대상은 Active-On-Edge를 사용해야 합니다 [병합 정책](../profile/merge-policies/ui-guide.md).
+++

### 데이터 사용 레이블 및 적용 (DULE) 및 동의 정책이 적용됩니까?

+++예 라고 답하십시오. 다음 [데이터 거버넌스 및 동의 정책](../data-governance/home.md) 선택한 마케팅 액션과 연관되어 만들어지면 선택한 속성의 활성화를 제어합니다.
+++

### 다음 [!DNL Adobe Target] 및 [!DNL Custom Personalization] 대상 [!DNL HIPAA]규정을 준수합니까?

+++답변
[!DNL Adobe Target] 은(는) 아님 [!DNL HIPPA]과 호환 [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). 고객은 다음에 대해 자체 법률팀에 확인해야 합니다 [!DNL HIPPA]-를 통해 에지 개인화를 사용하기 전에 사용자 지정 최적화 채널에 대한 준비 [!DNL Adobe Target] 또는 [!DNL Custom Personalization] 대상.

동의 정책 관리를 규모에 맞게 적용해야 하는 사용 사례의 경우 고객은 다음을 구매해야 합니다 [!DNL Adobe Privacy & Security Shield]. [!DNL Adobe Privacy & Security Shield] 기능은 고급 기능 세트로 판매되며 별도로 구입할 수 없습니다.

이 서비스에는 고객 관리 키와 높아진 임계값이 포함되어 있어 고객 데이터 수명주기를 관리할 수 있습니다.

다음 [!DNL Adobe Target] 및 [!DNL Custom Personalization] 대상이 와 통합됨 [Experience Platform 데이터 사용 레이블](../data-governance/labels/overview.md) 및 [동의 정책 시행 서비스](../data-governance/enforcement/overview.md). 이러한 기능은 모든 고객이 사용할 수 있습니다.




+++

