---
keywords: google 고객 일치;Google 고객 일치;Google 고객 일치
title: Google Customer Match 연결
description: Google Customer Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 검색, 쇼핑, Gmail 및 YouTube과 같은 Google의 소유 및 운영되는 속성에서 고객에게 연락하고 다시 연결할 수 있습니다.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 7d43abd507b5cee2b5c5d90af253d3e9290013a2
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 1%

---

# [!DNL Google Customer Match] 연결

>[!IMPORTANT]
>
> Google은 의 변경 사항을 [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [고객 일치](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)및 [디스플레이 및 비디오 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) 아래에 정의된 준수 및 동의 관련 요구 사항을 지원하기 위해 [디지털 시장법](https://digital-markets-act.ec.europa.eu/index_en) 유럽 연합의 (DMA)[EU 사용자 동의 정책](https://www.google.com/about/company/user-consent-policy/)). 이러한 동의 요건 변경의 시행은 2024년 3월 6일부터 시행될 예정이다.
><br/>
>EU 사용자 동의 정책을 준수하고 유럽 경제 영역(EEA)의 사용자에 대한 대상 목록을 계속 만들려면 광고주와 파트너는 대상 데이터를 업로드할 때 최종 사용자 동의를 전달하는지 확인해야 합니다. Google 파트너인 Adobe은 유럽 연합의 DMA에 따라 이러한 동의 요구 사항을 준수하는 데 필요한 도구를 제공합니다.
><br/>
>Adobe 개인 정보 보호 및 보안 쉴드를 구매하고 [동의 정책](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 동의하지 않은 프로필을 필터링하려면 별도의 조치를 취할 필요가 없습니다.
><br/>
>Adobe Privacy &amp; Security Shield를 구매하지 않은 고객은 [세그먼트 정의](../../../segmentation/home.md#segment-definitions) 내 기능 [세그먼트 빌더](../../../segmentation/ui/segment-builder.md) 기존 Real-Time CDP Google 대상을 중단 없이 계속 사용할 수 있도록 동의하지 않은 프로필을 필터링합니다.

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) 온라인 및 오프라인 데이터를 사용하여 Google의 소유 및 운영 속성에서 고객에게 연락하고 다시 연결할 수 있습니다. 예를 들면 다음과 같습니다. [!DNL Search], [!DNL Shopping], [!DNL Gmail], 및 [!DNL YouTube].

![Adobe Experience Platform UI의 Google Customer Match 대상.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 사용 사례 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Google Customer Match] 대상: 다음은 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 사용 사례 #1

한 스포츠 의류 브랜드는 다음을 통해 기존 고객에게 도달하기를 원합니다. [!DNL Google Search] 및 [!DNL Google Shopping] 과거의 구매 및 검색 기록을 기반으로 오퍼와 항목을 개인화합니다. 의류 브랜드는 자체 CRM에서 Experience Platform으로 이메일 주소를 수집하고 자체 오프라인 데이터에서 대상을 구축할 수 있습니다. 그런 다음 대상자를 (으)로 보낼 수 있습니다. [!DNL Google Customer Match] 다음에 사용될 수 있음 [!DNL Search] 및 [!DNL Shopping], 광고 지출 최적화.

### 사용 사례 #2

한 저명한 기술 회사가 새 전화기를 출시했다. 이 새로운 폰 모델을 홍보하기 위해, 그들은 이전 폰 모델을 소유한 고객들에게 이 폰의 새로운 기능과 기능성에 대한 인지도를 높이고자 한다.

릴리스를 홍보하기 위해 이메일 주소를 식별자로 사용하여 CRM 데이터베이스의 이메일 주소를 Experience Platform에 업로드합니다. 대상은 이전 휴대폰 모델을 소유한 고객을 기반으로 만들어집니다. 그러면 대상자가에 전송됩니다. [!DNL Google Customer Match], 따라서 현재 고객, 이전 휴대폰 모델을 보유한 고객 및 다음과 유사한 고객을 타겟팅할 수 있습니다. [!DNL YouTube].

## 데이터 거버넌스 [!DNL Google Customer Match] 대상 {#data-governance}

Experience Platform의 일부 대상에는 대상 플랫폼으로 보내거나 대상 플랫폼으로부터 받은 데이터에 대한 특정 규칙과 의무가 있습니다. 데이터의 제한 사항 및 의무와 Adobe Experience Platform 및 대상 플랫폼에서 해당 데이터를 사용하는 방법을 이해해야 합니다. Adobe Experience Platform은 이러한 데이터 사용 의무 중 일부를 관리하는 데 도움이 되는 데이터 거버넌스 도구를 제공합니다. [자세히 알아보기](../../../data-governance/labels/overview.md) 데이터 거버넌스 도구 및 정책 정보.

## 지원되는 ID {#supported-identities}

[!DNL Google Customer Match] 는 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/features/namespaces.md).

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| phone_sha256_e.164 | SHA256 알고리즘으로 해시된 E164 형식의 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원됩니다. 의 지침을 따르십시오. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 일반 텍스트와 해시된 전화 번호에 대해 각각 적절한 네임스페이스를 선택하고 사용하십시오. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 의 지침을 따르십시오. [ID 일치 요구 사항](#id-matching-requirements-id-matching-requirements) 일반 텍스트와 해시된 이메일 주소에 각각 적절한 네임스페이스를 섹션으로 지정하고 사용하십시오. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| user_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | 에 사용된 식별자(이름, 전화번호 등)를 사용하여 대상자의 모든 구성원을 내보냅니다. [!DNL Google Customer Match] 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] 계정 사전 요구 사항 {#google-account-prerequisites}

을(를) 설정하기 전에 [!DNL Google Customer Match] 대상 Experience Platform에서 다음에 대한 Google 정책을 읽고 준수하는지 확인하십시오. [!DNL Customer Match], 다음에 요약된 [Google 지원 설명서](https://support.google.com/google-ads/answer/6299717).

다음으로, 다음을 확인합니다. [!DNL Google] 계정이 다음에 대해 구성되었습니다. [!DNL Standard] 또는 더 높은 권한 수준입니다. 다음을 참조하십시오. [Google 광고 설명서](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 을 참조하십시오.

### 허용 목록 {#allowlist}

만들기 전에 [!DNL Google Customer Match] Experience Platform의 대상, [!DNL Google Ads] 계정이 다음을 준수함: [[!DNL Google Customer Match] 정책](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

준수 계정이 있는 고객은 Google에서 자동으로 허용 목록에추가된으로 제공됩니다.

## ID 일치 요구 사항 {#id-matching-requirements}

[!DNL Google] 을 사용하려면 PII(개인 식별 정보)가 명확하게 전송되지 않아야 합니다. 따라서 대상자는에 대해 활성화됩니다. [!DNL Google Customer Match] 키 사용 안 함 *해시됨* 이메일 주소 또는 전화번호 등 식별자.

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다.

### 전화번호 해시 요구 사항 {#phone-number-hashing-requirements}

에서 전화 번호를 활성화하는 방법에는 두 가지가 있습니다 [!DNL Google Customer Match]:

* **원시 전화번호 수집**: 에서 원시 전화 번호를 수집할 수 있습니다. [!DNL E.164] 서식 [!DNL Platform]및 활성화 시 자동으로 해시됩니다. 이 옵션을 선택하는 경우 항상 원시 전화 번호를 `Phone_E.164` 네임스페이스입니다.
* **해시된 전화번호 수집**: 로 수집하기 전에 전화 번호를 사전 해시할 수 있습니다. [!DNL Platform]. 이 옵션을 선택하는 경우 해시된 전화 번호를 항상 `PHONE_SHA256_E.164` 네임스페이스입니다.

>[!NOTE]
>
>에 수집된 전화번호 `Phone` 네임스페이스를에서 활성화할 수 없음 [!DNL Google Customer Match].

### 이메일 해시 요구 사항 {#hashing-requirements}

이메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 Experience Platform에서 이메일 주소를 지우고 다음을 수행할 수 있습니다. [!DNL Platform] 활성화 시 해시합니다.

Google의 해시 요구 사항 및 기타 활성화 제한 사항에 대한 자세한 내용은 Google 설명서의 다음 섹션을 참조하십시오.

* [[!DNL Customer Match] 이메일 주소, 주소 또는 사용자 ID 포함](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 고려 사항](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] 전화 번호 포함](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] 모바일 장치 ID 사용](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Experience Platform에서 이메일 주소 수집에 대한 자세한 내용은 [일괄 처리 수집 개요](../../../ingestion/batch-ingestion/overview.md) 및 [스트리밍 수집 개요](../../../ingestion/streaming-ingestion/overview.md).

이메일 주소를 해시하도록 선택하는 경우 위의 링크에 설명된 Google 요구 사항을 준수해야 합니다.

### 사용자 정의 네임스페이스 사용 {#custom-namespaces}

을(를) 사용하기 전에 `User_ID` 네임스페이스로 데이터를 Google에 보내려면 다음을 사용하여 자체 식별자를 동기화하십시오. [!DNL gTag]. 다음을 참조하십시오. [Google 공식 설명서](https://support.google.com/google-ads/answer/9199250) 을 참조하십시오.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 비디오 개요 {#video-overview}

아래 비디오를 통해 혜택과 Google Customer Match에 대한 데이터 활성화 방법에 대해 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/38180/)

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상 연결의 이름을 제공합니다
* **[!UICONTROL 설명]**: 이 대상 연결에 대한 설명을 제공합니다
* **[!UICONTROL 계정 ID]**: 사용자 [Google Ads 고객 ID](https://support.google.com/google-ads/answer/1704344?hl=en). ID 형식은 xxx-xxx-xxxx 입니다. 를 사용하는 경우 [!DNL Google Ads Manager Account (My Client Center)], 관리자 계정 ID를 사용하지 마십시오. 사용 [Google Ads 고객 ID](https://support.google.com/google-ads/answer/1704344?hl=en) 대신,

>[!IMPORTANT]
>
> * 다음 **[!UICONTROL PII와 결합]** 마케팅 액션은 다음에 대해 기본적으로 선택됩니다. [!DNL Google Customer Match] 대상 및 을(를) 제거할 수 없습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id* 대상에 대해 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

다음에서 **[!UICONTROL 세그먼트 일정]** 단계, 다음을 제공해야 합니다. [!UICONTROL 앱 ID] 전송 시 [!DNL IDFA] 또는 [!DNL GAID] 대상: [!DNL Google Customer Match].

![활성화 워크플로의 세그먼트 예약 단계에서 강조 표시된 Google Customer Match App ID 필드입니다.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

을(를) 찾는 방법에 대한 자세한 내용은 [!DNL App ID]을(를) 참조하십시오. [Google 공식 설명서](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) 또는 Google 담당자에게 문의하십시오.

### 매핑 예:에서 대상 데이터 활성화 [!DNL Google Customer Match] {#example-gcm}

다음에서 대상 데이터를 활성화할 때 올바른 ID 매핑의 예입니다 [!DNL Google Customer Match].

소스 필드 선택:

* 다음 항목 선택 `Email` 사용 중인 이메일 주소가 해시되지 않은 경우 소스 id로서의 네임스페이스.
* 다음 항목 선택 `Email_LC_SHA256` 데이터 수집에 대한 고객 이메일 주소를 해시한 경우 소스 id로서의 네임스페이스 [!DNL Platform]에 따라 [!DNL Google Customer Match] [이메일 해시 요구 사항](#hashing-requirements).
* 다음 항목 선택 `PHONE_E.164` 데이터가 해시되지 않은 전화 번호로 구성된 경우 소스 id로 네임스페이스입니다. [!DNL Platform] 은(는) 다음을 준수하기 위해 전화번호를 해시합니다. [!DNL Google Customer Match] 요구 사항.
* 다음 항목 선택 `Phone_SHA256_E.164` 데이터 수집 시 전화번호를 해시한 경우 소스 id로 네임스페이스 [!DNL Platform]에 따라 [!DNL Facebook] [전화번호 해시 요구 사항](#phone-number-hashing-requirements).
* 다음 항목 선택 `IDFA` 네임스페이스 를 소스 id로 사용 [!DNL Apple] 장치 ID.
* 다음 항목 선택 `GAID` 네임스페이스 를 소스 id로 사용 [!DNL Android] 장치 ID.
* 다음 항목 선택 `Custom` 데이터가 다른 유형의 식별자로 구성된 경우 네임스페이스 를 소스 id로 사용합니다.

대상 필드 선택:

* 다음 항목 선택 `Email_LC_SHA256` 소스 네임스페이스가 다음 중 하나일 때 타겟 ID로서의 네임스페이스 `Email` 또는 `Email_LC_SHA256`.
* 다음 항목 선택 `Phone_SHA256_E.164` 소스 네임스페이스가 다음 중 하나일 때 타겟 ID로서의 네임스페이스 `PHONE_E.164` 또는 `Phone_SHA256_E.164`.
* 다음 항목 선택 `IDFA` 또는 `GAID` 소스 네임스페이스가 다음과 같을 때 타겟 ID로서의 네임스페이스 `IDFA` 또는 `GAID`.
* 다음 항목 선택 `User_ID` 소스 네임스페이스가 사용자 정의 네임스페이스인 경우 네임스페이스를 타겟 ID로.

![활성화 워크플로의 매핑 단계에 표시된 소스 필드와 대상 필드 간의 ID 매핑.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

해시되지 않은 네임스페이스의 데이터는 다음에 의해 자동으로 해시됩니다. [!DNL Platform] 활성화 시.

속성 소스 데이터는 자동으로 해시되지 않습니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다.

![활성화 워크플로의 매핑 단계에서 강조 표시된 변환 제어를 적용합니다.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## 대상자 활성화가 성공했는지 확인 {#verify-activation}

활성화 흐름을 완료한 후 (으)로 전환합니다. **[!UICONTROL Google 광고]** 계정입니다. 활성화된 대상은 Google 계정에 고객 목록으로 표시됩니다. 대상 크기에 따라 제공할 활성 사용자가 100명을 넘지 않는 한 일부 대상은 채워지지 않습니다.

대상자를 두 대상에 매핑할 때 [!DNL IDFA] 및 [!DNL GAID] 모바일 ID, [!DNL Google Customer Match] 는 각 ID 매핑에 대해 별도의 대상을 만듭니다. 사용자 [!DNL Google Ads] account에는 두 개의 서로 다른 세그먼트가 표시되며, 하나는 [!DNL IDFA], 및 용 1개 [!DNL GAID] 매핑.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

이 오류는 고객 계정이 [전제 조건](#google-account-prerequisites). 이 문제를 해결하려면 Google에 문의하고 계정이 허용 목록에 추가되었는지, 그리고 용으로 구성되어 있는지 확인하십시오. [!DNL Standard] 또는 더 높은 권한 수준입니다. 다음을 참조하십시오. [Google 광고 설명서](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 을 참조하십시오.