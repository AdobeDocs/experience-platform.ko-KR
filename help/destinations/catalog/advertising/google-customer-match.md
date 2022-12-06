---
keywords: google customer match;Google 고객 일치;Google Customer Match
title: Google Customer Match 연결
description: Google Customer Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 검색, 쇼핑, Gmail 및 YouTube과 같은 Google이 소유하고 운영하는 속성에서 고객에게 도달하고 다시 참여합니다.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: b189f1b0fe29ebefb3cba9c4f820022a772ce297
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 1%

---

# [!DNL Google Customer Match] 연결

## 개요 {#overview}

[Google 고객 일치](https://support.google.com/google-ads/answer/6379332?hl=en) 을 사용하면 온라인 및 오프라인 데이터를 사용하여 다음과 같은 Google의 소유물과 운영 속성에서 고객에게 도달하고 다시 참여하도록 할 수 있습니다. [!DNL Search], [!DNL Shopping], [!DNL Gmail], 및 [!DNL YouTube].

![Adobe Experience Platform UI의 Google 고객 일치 대상.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 사용 사례 {#use-cases}

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Google Customer Match] 대상 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 사용 사례 #1

스포츠 의류 브랜드는 기존 고객에게 [!DNL Google Search] 및 [!DNL Google Shopping] 과거 구매 및 탐색 내역을 기반으로 오퍼와 항목을 개인화하려면 다음을 수행하십시오. 의류 브랜드는 자체 CRM의 이메일 주소를 Experience Platform에 수집하고 자체 오프라인 데이터에서 세그먼트를 작성할 수 있습니다. 그런 다음 이러한 세그먼트를 [!DNL Google Customer Match] 을 사용하여 [!DNL Search] 및 [!DNL Shopping], 광고 비용 최적화.

### 사용 사례 #2

한 유명 기술 회사가 새 휴대폰을 출시했다. 이 새로운 휴대폰 모델을 홍보하기 위해, 그들은 이전 모델의 휴대폰을 소유하고 있는 고객에게 휴대폰의 새로운 기능과 기능에 대한 인식을 유도하려고 노력하고 있다.

릴리스를 승격하려면 이메일 주소를 식별자로 사용하여 CRM 데이터베이스의 이메일 주소를 Experience Platform에 업로드합니다. 세그먼트는 이전 전화 모델을 소유한 고객을 기반으로 만들어집니다. 그런 다음 세그먼트가 로 전송됩니다 [!DNL Google Customer Match]을 가리키도록 업데이트하여, 현재 고객, 이전 휴대폰 모델을 소유한 고객 및 유사한 고객을 [!DNL YouTube].

## 데이터 거버넌스 [!DNL Google Customer Match] 대상 {#data-governance}

Experience Platform의 일부 대상에는 대상 플랫폼으로 전송되거나 대상 플랫폼에서 수신되는 데이터에 대한 특정 규칙과 의무가 있습니다. 귀하는 데이터의 제한 및 의무와 Adobe Experience Platform 및 대상 플랫폼에서 해당 데이터를 사용하는 방법을 이해할 책임이 있습니다. Adobe Experience Platform은 이러한 데이터 사용 의무 중 일부를 관리하는 데 도움이 되는 데이터 거버넌스 도구를 제공합니다. [추가 정보](../../../data-governance/labels/overview.md) 데이터 거버넌스 도구 및 정책에 대해 설명합니다.

## 지원되는 ID {#supported-identities}

[!DNL Google Customer Match] 은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 이 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 타겟 ID를 선택합니다. |
| phone_sha256_e.164 | SHA256 알고리즘으로 해시된 E164 형식의 전화 번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원합니다. 다음 [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션에서 그리고 일반 텍스트와 해시된 전화 번호에 적합한 네임스페이스를 각각 사용합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 다음 [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 섹션에서 그리고 개별 텍스트 및 해시된 이메일 주소에 적절한 네임스페이스를 각각 사용합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| user_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스이면 이 타겟 ID를 선택합니다. |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 에서 사용되는 식별자(이름, 전화번호 등)로 세그먼트(대상)의 모든 구성원을 내보냅니다 [!DNL Google Customer Match] 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Google Customer Match] 계정 사전 요구 사항 {#google-account-prerequisites}

설정하기 전 [!DNL Google Customer Match] Experience Platform의 대상에서 Google의 사용 정책을 읽고 준수하도록 하십시오 [!DNL Customer Match]에 요약된 [Google 지원 설명서](https://support.google.com/google-ads/answer/6299717).

다음으로, [!DNL Google] 계정이 [!DNL Standard] 또는 더 높은 권한 수준. 자세한 내용은 [Google 광고 설명서](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 자세한 내용

### 허용 목록 {#allowlist}

만들기 전 [!DNL Google Customer Match] Experience Platform의 대상, [!DNL Google Ads] 계정은 [Google 고객 일치 정책](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

준수 계정이 있는 고객은 Google에 의해 자동으로 나열될 수 있습니다.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL Google] 에서는 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상이 [!DNL Google Customer Match] 키오프 가능 *해시* 이메일 주소 또는 전화 번호와 같은 식별자.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

### 전화 번호 해싱 요구 사항 {#phone-number-hashing-requirements}

에서 전화 번호를 활성화하는 방법에는 두 가지가 있습니다 [!DNL Google Customer Match]:

* **원시 전화 번호 수집**: 전화 번호를 [!DNL E.164] 포맷 [!DNL Platform]활성화되면 자동으로 해시됩니다. 이 옵션을 선택하는 경우 항상 원시 전화 번호를 `Phone_E.164` 네임스페이스.
* **해시된 전화 번호 수집**: 에 수집하기 전에 전화 번호를 미리 해시할 수 있습니다. [!DNL Platform]. 이 옵션을 선택하는 경우 해시된 휴대폰 번호를 항상 `PHONE_SHA256_E.164` 네임스페이스.

>[!NOTE]
>
>에 수집된 전화 번호 `Phone` 네임스페이스는에서 활성화할 수 없습니다. [!DNL Google Customer Match].

### 이메일 해싱 요구 사항 {#hashing-requirements}

전자 메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 명확히 전자 메일 주소를 사용하여 다음을 보유할 수 있습니다. [!DNL Platform] 활성화 시 해시합니다.

Google의 해시 요구 사항 및 활성화 기타 제한에 대한 자세한 내용은 Google 설명서에서 다음 섹션을 참조하십시오.

* [[!DNL Customer Match] 이메일 주소, 주소 또는 사용자 ID 포함](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 고려 사항](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [전화 번호와 고객 일치](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [모바일 장치 ID와 고객 일치](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Experience Platform에서 이메일 주소 섭취에 대한 자세한 내용은 [배치 수집 개요](../../../ingestion/batch-ingestion/overview.md) 그리고 [스트리밍 수집 개요](../../../ingestion/streaming-ingestion/overview.md).

이메일 주소를 직접 해시하도록 선택하는 경우, 위의 링크에 설명된 Google의 요구 사항을 충족하는지 확인하십시오.

### 사용자 지정 네임스페이스 사용 {#custom-namespaces}

를 사용하기 전에 `User_ID` 데이터를 Google에 보낼 네임스페이스 는 [!DNL gTag]. 자세한 내용은 [Google 공식 설명서](https://support.google.com/google-ads/answer/9199250) 자세한 정보

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상 연결의 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상 연결에 대한 설명을 제공합니다.
* **[!UICONTROL 계정 ID]**: your [Google 광고 고객 ID](https://support.google.com/google-ads/answer/1704344?hl=en). ID의 형식은 xxx-xxx-xxxx입니다. 를 사용하는 경우 [!DNL Google Ads Manager Account (My Client Center)], 관리자 계정 ID를 사용하지 마십시오. 를 사용하십시오 [Google 광고 고객 ID](https://support.google.com/google-ads/answer/1704344?hl=en) 을 가리키도록 업데이트하는 것이 좋습니다.

>[!IMPORTANT]
>
> * 다음 **[!UICONTROL PII와 결합]** 마케팅 작업은 기본적으로 [!DNL Google Customer Match] 대상을 제거할 수 없습니다.


### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

에서 **[!UICONTROL 세그먼트 예약]** 단계에서는 다음을 제공해야 합니다 [!UICONTROL 앱 ID] 보내기 [!DNL IDFA] 또는 [!DNL GAID] 세그먼트를 [!DNL Google Customer Match].

![Google Customer Match 앱 ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

를 찾는 방법에 대한 자세한 내용 [!DNL App ID]를 참조하려면 [Google 공식 설명서](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### 매핑 예: 의 대상 데이터 활성화 [!DNL Google Customer Match] {#example-gcm}

이는 의 대상 데이터를 활성화할 때 올바른 ID 매핑의 예입니다 [!DNL Google Customer Match].

소스 필드 선택:

* 을(를) 선택합니다 `Email` 사용 중인 이메일 주소가 해시되지 않은 경우 소스 ID로 네임스페이스 를 지정합니다.
* 을(를) 선택합니다 `Email_LC_SHA256` 데이터 수집 시 고객 이메일 주소를 해시한 경우 소스 ID로 네임스페이스 [!DNL Platform]에 따라 [!DNL Google Customer Match] [이메일 해싱 요구 사항](#hashing-requirements).
* 을(를) 선택합니다 `PHONE_E.164` 네임스페이스 는 데이터가 해시되지 않은 전화 번호로 구성된 경우 소스 id로 사용됩니다. [!DNL Platform] 이(가) [!DNL Google Customer Match] 요구 사항.
* 을(를) 선택합니다 `Phone_SHA256_E.164` 데이터 수집 시 해시된 전화번호를 소스 ID로 네임스페이스 [!DNL Platform]에 따라 [!DNL Facebook] [전화 번호 해싱 요구 사항](#phone-number-hashing-requirements).
* 을(를) 선택합니다 `IDFA` 데이터가 [!DNL Apple] 장치 ID.
* 을(를) 선택합니다 `GAID` 데이터가 [!DNL Android] 장치 ID.
* 을(를) 선택합니다 `Custom` 네임스페이스 는 데이터가 다른 유형의 식별자로 구성된 경우 소스 id로 사용됩니다.

대상 필드 선택:

* 을(를) 선택합니다 `Email_LC_SHA256` 소스 네임스페이스가 `Email` 또는 `Email_LC_SHA256`.
* 을(를) 선택합니다 `Phone_SHA256_E.164` 소스 네임스페이스가 `PHONE_E.164` 또는 `Phone_SHA256_E.164`.
* 을(를) 선택합니다 `IDFA` 또는 `GAID` 소스 네임스페이스가 타겟 ID인 경우 네임스페이스가 네임스페이스입니다 `IDFA` 또는 `GAID`.
* 을(를) 선택합니다 `User_ID` 네임스페이스 는 소스 네임스페이스가 사용자 지정 네임스페이스일 때 타겟 id로 사용됩니다.

![ID 매핑](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

해시되지 않은 네임스페이스의 데이터는 [!DNL Platform] 활성화 시.

속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.

![ID 매핑 변환](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## 세그먼트 활성화가 성공했는지 확인 {#verify-activation}

활성화 흐름을 완료한 후 로 전환합니다. **[!UICONTROL Google 광고]** 계정이 필요합니다. 활성화된 세그먼트는 Google 계정에 고객 목록으로 표시됩니다. 세그먼트 크기에 따라 일부 대상은 제공할 활성 사용자가 100명 이상 없는 한 채우지 않습니다.

세그먼트를 둘 다에 매핑 시 [!DNL IDFA] 및 [!DNL GAID] 모바일 ID, [!DNL Google Customer Match] 각 ID 매핑에 대해 별도의 세그먼트를 만듭니다. 사용자 [!DNL Google Ads] 계정에는 두 개의 다른 세그먼트가 표시되며, 하나에는 [!DNL IDFA], 및 [!DNL GAID] 매핑.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

이 오류는 고객 계정이 [전제 조건](#google-account-prerequisites). 이 문제를 해결하려면 Google에 문의하여 계정이 허용 목록에 추가되어 다음에 대해 구성되어 있는지 확인하십시오 [!DNL Standard] 또는 더 높은 권한 수준. 자세한 내용은 [Google 광고 설명서](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 자세한 내용

## 추가 리소스 {#additional-resources}

* [Google 고객 일치 통합 - 비디오 자습서](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

