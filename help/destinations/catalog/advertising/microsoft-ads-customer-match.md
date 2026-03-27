---
keywords: advertising; microsoft ads; customer match;
title: Microsoft Ads 고객 일치 연결
description: Microsoft Ads Customer Match 대상을 사용하여 이메일 주소로 고객을 일치시키고 검색 및 대상 광고를 포함하여 Microsoft Advertising 네트워크에서 고객과 다시 교류합니다.
badge: label="Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4d405ffb-f600-463b-a215-44e806b6d139
source-git-commit: 40a9ea68fd855b2f0d92a4fa336f1b68142f0649
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 14%

---

# [!DNL Microsoft Ads Customer Match] 연결 {#microsoft-ads-customer-match-destination}

>[!AVAILABILITY]
>
>이 대상 커넥터는 현재 사용할 수 없습니다. 액세스 권한을 받으려면 Adobe 담당자에게 문의하십시오.

## 개요 {#overview}

[!DNL Microsoft Ads Customer Match] 대상을 사용하여 이메일 주소로 고객을 일치시키고 검색 및 대상 광고를 포함하여 [!DNL Microsoft Advertising Network]에서 고객과 다시 교류하십시오. [!DNL Microsoft Advertising] 계정을 [!DNL Real-Time CDP]에 연결하여 Experience Platform에서 직접 고객 일치 목록 생성 및 관리를 자동화합니다.

## 사용 사례 {#use-cases}

[!DNL Microsoft Ads Customer Match] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 기능을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### 개인화된 오퍼로 기존 고객 재타겟팅 {#use-case-1}

전자 상거래 브랜드는 [!DNL Microsoft Search] 및 [!DNL Microsoft Audience Network]을(를) 통해 기존 고객에게 연락하여 과거 구매 및 검색 기록을 기반으로 오퍼를 개인화하려고 합니다. 브랜드는 자체 CRM의 이메일 주소를 Experience Platform으로 수집하고, 자체 오프라인 데이터에서 대상을 만들고, 이러한 대상을 [!DNL Microsoft Ads Customer Match]에 보내 검색 및 대상 광고 전반에 걸쳐 사용할 수 있도록 함으로써 광고 비용을 최적화할 수 있습니다.

### 기존 고객에게 새 제품 홍보 {#use-case-2}

한 기술 회사가 새로운 제품을 출시했고 이전에 관련 제품을 구매한 고객들 사이에서 인지도를 끌어내고 싶어한다. CRM 데이터베이스의 이메일 주소를 식별자로 사용하여 Experience Platform에 업로드합니다. 관련 제품을 소유한 고객을 기반으로 대상을 만듭니다. 이러한 대상은 [!DNL Microsoft Ads Customer Match]&#x200B;(으)로 전송되므로 회사는 현재 고객과 [!DNL Microsoft Advertising Network]의 유사한 고객을 타깃팅할 수 있습니다.

## 지원되는 ID {#supported-identities}

[!DNL Microsoft Ads Customer Match]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| `email` | 일반 텍스트 이메일 주소 | 매핑 단계에서는 일반 텍스트(해시되지 않은) 전자 메일 주소만 **소스** 필드로 지원됩니다. 사전 해시된 소스 필드는 지원되지 않습니다. Experience Platform은 전자 메일 주소를 [!DNL Microsoft Ads]&#x200B;(으)로 내보내기 전에 항상 해시합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 예 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li> CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience),</li><li> 유사 대상, </li><li> 페더레이션 대상, </li><li> [!DNL Adobe Journey Optimizer]과(와) 같은 다른 Experience Platform 앱에서 생성된 대상, </li><li> 등. </li></ul> |

{style="table-layout:auto"}

대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
|--------------------|-----------|-------------|-----------|
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필을 기반으로 마케팅 캠페인을 위해 특정 사용자 그룹을 타깃팅할 수 있습니다. | 빈번한 구매자, 장바구니 포기 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | [!DNL Adobe Experience Platform] 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | [!DNL Microsoft Ads Customer Match] 대상에 사용된 식별자(이메일 주소)를 사용하여 대상자의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

대상 데이터를 [!DNL Microsoft Ads]에 보내려면 활성 [!DNL Microsoft Advertising] 계정이 있어야 합니다. 계정 만들기에 대한 자세한 내용은 [Microsoft Advertising 설명서](https://help.ads.microsoft.com/#apex/ads/en/53090/0)를 참조하세요.

### 고객 일치 약관에 동의 {#accept-customer-match-terms}

이 대상을 통해 대상을 활성화하기 전에 먼저 [!DNL Microsoft Advertising] 계정에서 고객 일치 목록을 수동으로 만들어야 합니다. 이 초기 수동 작성은 고객 일치 약관을 수락하는 데 필요합니다. 이렇게 하면 Experience Platform에서 보낸 대상자를 자동으로 만들 수 있습니다. 이 단계를 완료하지 않으면 대상을 활성화할 때 오류가 발생할 수 있습니다.

### 작업 계정(MS Entra) IT 관리자 승인 {#work-account-admin-approval}

Microsoft 작업 계정(Microsoft Entra 계정이라고도 함)으로 인증하는 경우 [!DNL Microsoft Advertising]에 연결하기 전에 조직의 IT 관리자가 승인을 받아야 할 수 있습니다.

작업 계정을 사용하여 인증하려고 하면 **승인 필요** 페이지로 리디렉션될 수 있습니다. 이 페이지에서는 앱 연결 정당성을 요청하고 `ads.manage`을(를) 포함한 필수 권한을 나열합니다. 요청을 제출하면 IT 관리자가 이를 검토하라는 알림을 받게 됩니다. 요청이 제출되었다는 확인 이메일도 받게 됩니다.

IT 관리자가 Azure 포털에서 요청을 승인하면 Experience Platform으로 돌아가서 작업 계정을 사용하여 인증할 수 있습니다. 지침은 Microsoft 설명서 를 참조하십시오.

* [관리자 동의 요청을 검토하고 조치를 취합니다](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/review-admin-consent-requests)
* [관리자 동의 워크플로 구성](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-admin-consent-workflow)
* [사용자가 애플리케이션에 동의하는 방법 구성](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-user-consent)

IT 관리자가 아직 요청을 승인하지 않은 경우 다음 오류로 인해 인증이 실패합니다. `AADSTS650052: The app needs access to a service ('https://ads.microsoft.com') that your organization has not subscribed to or enabled. Contact your IT Admin to review the configuration of your service subscriptions.`

### 계정 구성 {#account-configuration}

대상을 구성할 때는 다음 정보를 제공해야 합니다.

* [!UICONTROL Customer ID]: 정수 형식의 [!DNL Microsoft Ads] CID(고객 ID)입니다. 고객 ID를 찾는 방법에 대한 지침은 [Microsoft Advertising 설명서](https://learn.microsoft.com/ko-kr/advertising/guides/get-started?view=bingads-13#get-ids)를 참조하세요.
* [!UICONTROL Customer Account ID]: [!DNL Microsoft Ads] 고객 계정 ID입니다. 고객 계정 ID를 찾는 방법에 대한 지침은 [Microsoft Advertising 설명서](https://learn.microsoft.com/ko-kr/advertising/guides/get-started?view=bingads-13#get-ids)를 참조하세요.

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 대상 세부 정보 입력 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_id"
>title="Customer ID"
>abstract="관리자 계정 ID라고도 하는 Microsoft Advertising 고객 ID입니다. 여러 광고주 계정(고객 계정 ID)을 가질 수 있는 Microsoft Advertising의 최상위 ID입니다."
>additional-url="https://learn.microsoft.com/ko-kr/advertising/guides/get-started?view=bingads-13#get-ids" text="고객 ID 찾기"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_account_id"
>title="고객 계정 ID"
>abstract="광고주 계정 ID라고도 하는 Microsoft Advertising 고객 계정 ID입니다. 고객 ID에서 특정 광고주 계정을 식별합니다."
>additional-url="https://learn.microsoft.com/ko-kr/advertising/guides/get-started?view=bingads-13#get-ids" text="고객 계정 ID 찾기"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_membership_duration"
>title="멤버십 기간"
>abstract="사용자가 고객 일치 목록에 남아 있는 일 수입니다. 허용되는 값은 1일에서 390일 사이입니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_list_availability"
>title="고객 일치 목록 가용성"
>abstract="고객 일치 목록을 단일 광고주 계정에서 사용할 수 있는지 아니면 관리자 계정의 모든 계정에서 사용할 수 있는지 선택합니다. 고객 ID를 선택하여 고객 ID 아래의 모든 광고주 계정에서 목록을 사용할 수 있도록 합니다. 고객 계정 ID를 선택하여 특정 고객 계정 ID로 목록을 제한합니다."
>additional-url="https://help.ads.microsoft.com/apex/index/3/en/56727" text="Microsoft Advertising의 대상자 목록 공유에 대해 자세히 알아보기"

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Customer ID]**: [!DNL Microsoft Ads] CID(고객 ID)입니다. 고객 ID를 찾는 방법에 대한 지침은 [Microsoft Advertising 설명서](https://learn.microsoft.com/ko-kr/advertising/guides/get-started?view=bingads-13#get-ids)를 참조하세요.
* **[!UICONTROL Customer Account ID]**: [!DNL Microsoft Ads] 고객 계정 ID입니다. 고객 계정 ID를 찾는 방법에 대한 지침은 [Microsoft Advertising 설명서](https://learn.microsoft.com/ko-kr/advertising/guides/get-started?view=bingads-13#get-ids)를 참조하세요.
* **[!UICONTROL Membership Duration]**: 사용자가 고객 일치 목록에 남아 있는 일 수입니다. 허용되는 값은 1일에서 390일 사이입니다.
* **[!UICONTROL Customer Match List Availability]**: 고객 일치 목록의 사용 가능 여부를 선택합니다. [!DNL Microsoft Advertising]에서 고객 ID에는 여러 고객 계정 ID(광고주 계정)가 있을 수 있습니다. 고객 ID의 모든 광고주 계정에서 목록을 사용할 수 있도록 하려면 **[!UICONTROL Customer ID (all advertising accounts)]**&#x200B;을(를) 선택하고, 위에서 제공한 특정 고객 계정 ID로 목록을 제한하려면 **[!UICONTROL Customer Account ID (single advertising account)]**&#x200B;을(를) 선택하십시오. 자세한 내용은 [Microsoft Advertising 설명서](https://help.ads.microsoft.com/apex/index/3/en/56727)를 참조하세요.

  ![Microsoft Ads Customer Match 대상에 대한 대상 세부 정보 필드를 보여주는 Platform UI 이미지입니다.](../../assets/catalog/advertising/microsoft-ads-customer-match/destination-details.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* 대상으로 *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 매핑 {#mapping}

**[!UICONTROL Mapping]** 단계에서는 소스 프로필의 전자 메일 ID를 [!DNL Microsoft Ads Customer Match]의 대상 ID에 매핑해야 합니다.

* **Source 필드**: 프로필의 전자 메일 ID를 매핑할 소스 필드로 `IdentityMap: Email`을(를) 선택합니다. 또는 `personalEmail.address`과(와) 같은 XDM 특성을 소스 필드로 선택할 수 있습니다.
* **대상 필드**: `Identity: email`을(를) 대상 필드로 선택합니다.

>[!IMPORTANT]
>
>일반 텍스트(해시되지 않은) 이메일 주소를 **소스** 필드로 매핑해야 합니다. `Emails (SHA256, lowercased)`과(와) 같은 사전 해시된 소스 ID는 지원되지 않습니다. Experience Platform은 전자 메일 주소를 [!DNL Microsoft Ads]&#x200B;(으)로 내보내기 전에 항상 해시합니다.

![IdentityMap 전자 메일이 ID 전자 메일에 매핑된 매핑 단계를 표시하는 UI 이미지입니다.](../../assets/catalog/advertising/microsoft-ads-customer-match/mapping.png)

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL Microsoft Ads Customer Match] 대상으로 내보냈는지 확인하려면 [!DNL Microsoft Advertising] 계정을 확인하세요. 활성화가 성공하면 계정에 대상자가 고객 일치 목록으로 채워집니다.

## 추가 리소스 {#additional-resources}

자세한 내용은 [Microsoft Advertising 도움말 센터](https://help.ads.microsoft.com/)를 참조하십시오.
