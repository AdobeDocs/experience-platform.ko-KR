---
keywords: google 고객 일치;Google 고객 일치;Google Customer Match
title: Google Customer Match 연결
description: 'Google Customer Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 Google이 소유하거나 운영하는 속성(예: Search, Shopping, Gmail, YouTube)에서 고객에게 도달하고 다시 참여하도록 할 수 있습니다.'
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---

# [!DNL Google Customer Match] 연결

## 개요 {#overview}

[Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 다음과 같이 Google의 소유 및 운영 속성에서 고객에게 도달하고 다시 참여하도록 할 수 있습니다.  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail]및  [!DNL YouTube].

![Adobe Experience Platform UI의 Google Customer Match 대상](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 사용 사례

[!DNL Google Customer Match] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 샘플 사용 사례가 여기에 있습니다.

### 사용 사례 #1

운동용 의류 브랜드에서는 [!DNL Google Search] 및 [!DNL Google Shopping]을 통해 기존 고객에게 도달하여 과거 구매 및 탐색 내역을 기반으로 오퍼와 항목을 개인화하려고 합니다. 의류 브랜드는 자체 CRM의 이메일 주소를 Experience Platform에 수집하고 자체 오프라인 데이터에서 세그먼트를 작성할 수 있습니다. 그런 다음 이러한 세그먼트를 [!DNL Search] 및 [!DNL Shopping]에서 사용할 [!DNL Google Customer Match]로 보내어 광고 비용을 최적화할 수 있습니다.

### 사용 사례 #2

한 유명 기술 회사가 새 휴대폰을 출시했다. 이 새로운 휴대폰 모델을 홍보하기 위해, 그들은 이전 모델의 휴대폰을 소유하고 있는 고객에게 휴대폰의 새로운 기능과 기능에 대한 인식을 유도하려고 노력하고 있다.

릴리스를 승격하려면 이메일 주소를 식별자로 사용하여 CRM 데이터베이스의 이메일 주소를 Experience Platform에 업로드합니다. 세그먼트는 이전 전화 모델을 소유한 고객을 기반으로 만들어집니다. 그런 다음 세그먼트가 [!DNL Google Customer Match]에 전송되므로 이 회사는 현재 고객, 이전 전화 모델을 소유한 고객 및 [!DNL YouTube]에서 유사한 고객을 타깃팅할 수 있습니다.

## [!DNL Google Customer Match] 대상에 대한 데이터 거버넌스 {#data-governance}

Experience Platform의 일부 대상에는 대상 플랫폼으로 전송되거나 대상 플랫폼에서 수신되는 데이터에 대한 특정 규칙과 의무가 있습니다. 귀하는 데이터의 제한 및 의무와 Adobe Experience Platform 및 대상 플랫폼에서 해당 데이터를 사용하는 방법을 이해할 책임이 있습니다. Adobe Experience Platform은 이러한 데이터 사용 의무 중 일부를 관리하는 데 도움이 되는 데이터 거버넌스 도구를 제공합니다. [데이터 ](../../../data-governance/labels/overview.md) 거버넌스 도구 및 정책에 대해 자세히 알아보십시오.

## 지원되는 ID {#supported-identities}

[!DNL Google Customer Match] 은 아래 표에 설명된 id의 활성화를 지원합니다. [id](/help/identity-service/namespaces.md)에 대해 자세히 알아보십시오.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 이 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 타겟 ID를 선택합니다. |
| phone_sha256_e.164 | SHA256 알고리즘으로 해시된 E164 형식의 전화 번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침에 따라 일반 텍스트 및 해시된 전화 번호에 적합한 네임스페이스를 각각 사용하십시오. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션의 지침에 따라 일반 텍스트 및 해시된 이메일 주소에 적합한 네임스페이스를 각각 사용하십시오. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| user_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스이면 이 타겟 ID를 선택합니다. |

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - 대상에 사용된 식별자(이름, 전화 번호 및 기타)로 세그먼트(대상)의 모든 멤버를  [!DNL Google Customer Match] 내보냅니다.

## [!DNL Google Customer Match] 계정 사전 요구 사항 {#google-account-prerequisites}

Experience Platform에서 [!DNL Google Customer Match] 대상을 설정하기 전에 [Google 지원 설명서](https://support.google.com/google-ads/answer/6299717)에 설명된 [!DNL Customer Match] 사용에 대한 Google의 정책을 읽고 준수하도록 하십시오.

그런 다음 [!DNL Google] 계정이 [!DNL Standard] 이상의 액세스 수준에 대해 구성되어 있는지 확인합니다. 자세한 내용은 [Google 광고 설명서](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1)를 참조하십시오.

### 허용 목록 {#allowlist}

Experience Platform에서 [!DNL Google Customer Match] 대상을 만들기 전에 [!DNL Google Ads] 계정이 [Google Customer Match 정책](https://support.google.com/google-ads/answer/6299717/customer-match-policy)을(를) 준수하는지 확인하십시오.

호환 계정이 있는 고객은 Google에서 자동으로 나열할 수 있습니다.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL Google] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 [!DNL Google Customer Match]에 활성화된 대상은 이메일 주소 또는 전화 번호와 같이 *해시된* 식별자를 사용할 수 있습니다.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

## 전화 번호 해싱 요구 사항 {#phone-number-hashing-requirements}

[!DNL Google Customer Match]에서 전화 번호를 활성화하는 방법에는 두 가지가 있습니다.

* **원시 전화 번호 수집**: 원시 전화 번호를  [!DNL E.164] 형식으로  [!DNL Platform]수집할 수 있으며 활성화 시 자동으로 해시됩니다. 이 옵션을 선택하는 경우 반드시 원시 전화 번호를 항상 `Phone_E.164` 네임스페이스에 수집하십시오.
* **해시된 전화 번호 수집**: 에 수집하기 전에 전화 번호를 미리 해시할 수 있습니다 [!DNL Platform]. 이 옵션을 선택하는 경우 해시된 전화 번호를 항상 `PHONE_SHA256_E.164` 네임스페이스에 수집해야 합니다.

>[!NOTE]
>
>`Phone` 네임스페이스에 수집된 전화 번호는 [!DNL Google Customer Match]에서 활성화할 수 없습니다.

## 이메일 해싱 요구 사항 {#hashing-requirements}

전자 메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 명확히 전자 메일 주소를 사용할 수 있으며 [!DNL Platform] 해시 처리할 수 있습니다.

Google의 해시 요구 사항 및 활성화 기타 제한에 대한 자세한 내용은 Google 설명서의 다음 섹션을 참조하십시오.

* [[!DNL Customer Match] 이메일 주소, 주소 또는 사용자 ID 포함](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 고려 사항](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [전화 번호와 고객 일치](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [모바일 장치 ID와 고객 일치](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Experience Platform에서 이메일 주소를 수집하는 방법에 대한 자세한 내용은 [일괄 처리 수집 개요](../../../ingestion/batch-ingestion/overview.md) 및 [스트리밍 수집 개요](../../../ingestion/streaming-ingestion/overview.md)를 참조하십시오.

이메일 주소를 직접 해시하도록 선택하는 경우, 위의 링크에 설명된 Google의 요구 사항을 충족하는지 확인하십시오.

## 사용자 지정 네임스페이스 사용 {#custom-namespaces}

`User_ID` 네임스페이스를 사용하여 Google에 데이터를 보내려면 먼저 [!DNL gTag] 을 사용하여 자체 식별자를 동기화해야 합니다. 자세한 내용은 [Google 공식 설명서](https://support.google.com/google-ads/answer/9199250)를 참조하십시오.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 이 대상 연결의 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상 연결에 대한 설명을 제공합니다.
* **[!UICONTROL 계정 ID]**: Google 고객 클라이언트 ID입니다. ID의 형식은 xxx-xxx-xxxx입니다.

>[!IMPORTANT]
>
> * **[!UICONTROL PII와 결합]** 마케팅 작업은 기본적으로 [!DNL Google Customer Match] 대상에 대해 선택되므로 제거할 수 없습니다.


## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 세그먼트 내보내기 대상으로 대상 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

**[!UICONTROL 세그먼트 예약]** 단계에서 [!DNL IDFA] 또는 [!DNL GAID] 세그먼트를 [!DNL Google Customer Match]에 보낼 때 [!UICONTROL 앱 ID]를 제공해야 합니다.

![Google Customer Match 앱 ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

[!DNL App ID]을 찾는 방법에 대한 자세한 내용은 [Google 공식 설명서](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid)를 참조하십시오.

## 세그먼트 활성화가 성공했는지 확인 {#verify-activation}

활성화 흐름을 완료한 후 **[!UICONTROL Google 광고]** 계정으로 전환하십시오. 활성화된 세그먼트는 Google 계정에 고객 목록으로 표시됩니다. 세그먼트 크기에 따라 일부 대상은 제공할 활성 사용자가 100명 이상 없는 한 채우지 않습니다.

세그먼트를 [!DNL IDFA] 및 [!DNL GAID] 모바일 ID에 모두 매핑하면 [!DNL Google Customer Match] 는 각 ID 매핑에 대해 별도의 세그먼트를 만듭니다. [!DNL Google Ads] 계정에는 [!DNL IDFA] 및 [!DNL GAID] 매핑에 대한 세그먼트와, 각각 다른 두 개의 세그먼트가 표시됩니다.

## 추가 리소스 {#additional-resources}

* [Google Customer Match 통합 - 비디오 자습서](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
