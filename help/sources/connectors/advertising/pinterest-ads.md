---
keywords: Experience Platform;홈;인기 항목;Pinterest 광고;
title: Pinterest Ads Source 개요
description: API 또는 사용자 인터페이스를 사용하여 Pinterest 광고를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 1%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>[!DNL Pinterest Ads] 원본이 Beta 버전입니다. 베타 레이블 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 서드파티 광고 시스템에서 데이터를 수집하는 기능을 지원합니다. 광고 공급자에 대한 지원은 [!DNL Pinterest Ads]입니다.

[[!DNL Pinterest]](https://www.pinterest.com)은(는) 요리법, 홈 장식, 스타일 영감 및 기타 아이디어를 웹에서 찾을 수 있는 시각적 검색 엔진입니다. 이러한 이미지는 이미지, 애니메이션 GIF 및 비디오를 핀보드 형식으로 사용하여 소규모로 제공됩니다. [[!DNL Pinterest Ads]](https://ads.pinterest.com/)을(를) 사용하면 사업을 확장하고 [!DNL Pinterest]을(를) 사용하여 4억 명에 도달할 수 있습니다.

[!DNL Pinterest Ads]을(를) 사용하면 타깃팅된 광고를 통해 사용자에게 연락하여 제품을 검색하고 구매할 수 있습니다. [!DNL Pinterest Ads]의 Pin은 관련 검색 결과에 추가 노출을 받을 수 있도록 스폰서됩니다. [!DNL Pinterest Business]을(를) 구독한 사용자는 기존의 가장 성과가 좋은 핀을 홍보하거나, 새 이미지나 비디오를 만들거나, 웹 사이트에서 고정된 이미지를 홍보하도록 선택할 수 있습니다. [!DNL Pinterest Ads]에서는 특정 캠페인 목표를 달성하는 데 도움이 되는 몇 가지 광고 형식을 제공합니다.

## [!DNL Pinterest]개 API {#pinterest-apis}

[!DNL Pinterest Ads] 원본은 [!DNL Pinterest] API를 활용하여 모든 성능 및 지표와 함께 [!DNL Pinterest Ads] 데이터를 검색합니다. 지원되는 API 엔드포인트는 다음과 같습니다.

* [Campaign 분석](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [광고 그룹 분석](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [광고 분석](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

[!DNL Pinterest Ads] 원본을 사용하여 [!DNL Pinterest]의 데이터를 Experience Platform으로 가져온 다음 데이터 분석을 실행할 수 있습니다. 데이터는 90일 소급 범위 동안 수집된 날짜부터 반환됩니다. [!DNL Pinterest Ads]은(는) 전달자 토큰을 인증 메커니즘으로 사용하여 [!DNL Pinterest] API와 통신합니다.

## 전제 조건 {#prerequisites}

[!DNL Pinterest Ads] 소스 연결을 만드는 첫 번째 단계는 Pinterest 개발자 계정이 있는지 확인하는 것입니다. 아직 계정이 없는 경우 [등록](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) 페이지를 방문하여 계정을 등록하고 만드십시오.

### [!DNL Pinterest] 앱 설정 및 액세스 토큰 생성 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>UI에서 액세스 토큰을 생성하면 제한된 액세스가 제공되므로 [!DNL Pinterest] API를 사용하여 액세스 토큰을 생성하는 것이 좋습니다. UI를 통해 `pins:read`, `boards:read` 및 `user_accounts:read` 범위에만 액세스할 수 있습니다. 이 제한은 [!DNL Pinterest] API의 Analytics 끝점에 사용하기에 적합하지 않습니다.

액세스 토큰을 생성하려면 [앱 설정](https://developers.pinterest.com/docs/getting-started/set-up-app/) 및 [OAuth 2.0을 사용한 인증](https://developers.pinterest.com/docs/getting-started/authentication/)에 대한 [!DNL Pinterest] 안내서를 읽어 보십시오.

### 필요한 자격 증명 수집 {#gather-required-credentials}

[!DNL Pinterest Ads]을(를) 플랫폼에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 액세스 토큰 | 사용자 계정에 대한 [!DNL Pinterest Ads] 액세스 토큰입니다. 토큰의 사용자 계정은 지정된 [!DNL Pinterest Ad] 계정의 소유자이거나 비즈니스 액세스 권한을 통해 관리자에게 부여된 필수 역할(관리자, 분석가 또는 캠페인 관리자) 중 하나여야 합니다. 액세스 토큰에 대한 자세한 내용은 [[!DNL Pinterest] 액세스 토큰 생성 가이드](https://developers.pinterest.com/docs/getting-started/set-up-app/)를 참조하십시오. |
| 광고 계정 ID | 사업부의 관련 [!DNL Pinterest Ads] 광고 계정 ID. 광고 계정 ID 검색에 대한 정보. 광고 관리자에서 ID를 찾는 방법에 대한 [[!DNL Pinterest] 안내서](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager)를 참조하세요. |
| 캠페인, 광고 그룹 또는 광고 ID | 광고 계정 ID에 해당하는 `campaign`, `ad group` 또는 `ad` ID입니다. 필요한 ID를 얻으려면 **Pinterest Business Hub** > **광고 계정 요약** > **캠페인** / **광고 그룹** / **광고**&#x200B;에 대한 [!DNL Pinterest] 페이지로 이동하여 각 이름 바로 아래에 언급된 필수 ID를 복사하십시오. |

>[!NOTE]
>
>[!DNL Pinterest] API는 각 ID와 연결된 데이터를 검색할 수 있는 개별 API를 제공합니다. 따라서 원하는 ID 유형에 해당하는 ID만 전달해야 합니다.

## 가드레일 {#guardrails}

다음 절에서는 [!DNL Pinterest]의 데이터 보호 기능에 대해 설명합니다.

### [!DNL Pinterest] 날짜 범위 {#pinterest-date-range}

[!DNL Pinterest] API는 지정된 날짜 범위 사이에 분석 데이터를 검색할 수 있도록 `start_date` 및 `end_date` 매개 변수를 모두 지원합니다.

* `start_date`은(는) 현재 날짜보다 90일 이전일 수 없습니다.
* `end_date`은(는) `start_date`에서 90일 이후가 될 수 없습니다.

데이터 흐름을 예약할 때 다음 빈도 및 간격 설정 중 하나를 구성해야 합니다.

| 빈도 | 간격 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

예를 들어, 빈도 및 간격 설정이 `Day=1` 또는 `Hour=24`(으)로 구성된 상태로 수집이 2023년 3월 15일에 설정된 경우 계산이 90일 동안 소급 적용되므로 [!DNL Pinterest] API는 2022년 12월 15일까지만 데이터를 검색합니다.

### [!DNL Pinterest] 시간 범위 {#pinterest-time-range}

[!DNL Pinterest] API는 데이터 검색 방법에 대해 다양한 종류의 시간 세부기간을 지원합니다.

| 시간 세부 기간 | 설명 |
| --- | --- |
| **전체** | 데이터 지표는 지정된 날짜 범위에서 집계됩니다. |
| **일** | 데이터 지표는 매일 분류됩니다. |
| **시간** | 데이터 지표는 시간별로 분류됩니다. |
| **주별** | 데이터 지표는 매주 분류됩니다. |
| **월별** | 데이터 지표는 매월 분류됩니다. |

플랫폼의 경우 [!DNL Pinterest Ads] 소스가 내부적으로 `Day`(으)로 구성됩니다. 즉, 데이터는 매일 집계됩니다. 예를 들어 `impressions recorded`을(를) 지표로 사용하는 경우 세부 기간이 `DAY`(으)로 구성되므로 `day 1`에 `xx` 노출, `day 2`에 `yy` 노출 등이 발생합니다.

>[!IMPORTANT]
>
>Pinterest은 광고, 광고 그룹 또는 광고 캠페인에서 정보를 읽기 위해 API에 대해 매일 1000개의 API 호출 비율 제한을 지정합니다. 기본 API 호출에 적용할 수 있는 속도 제한에 대한 자세한 내용은 [[!DNL Pinterest] 속도 제한에 대한 설명서](https://developers.pinterest.com/docs/reference/ratelimits/)를 참조하세요.

## [!DNL Pinterest Ads]을(를) 플랫폼에 연결 {#connect-to-platform}

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Pinterest Ads]을(를) 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.

### API를 사용하여 [!DNL Pinterest Ads]을(를) 플랫폼에 연결 {#connect-to-platform-using-api}

* [흐름 서비스 API를 사용하여 Pinterest 기본 연결 만들기](../../tutorials/api/create/advertising/pinterest-ads.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 광고 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/advertising.md)

### UI를 사용하여 [!DNL Pinterest Ads]을(를) 플랫폼에 연결 {#connect-to-platform-using-ui}

* [UI에서 Pinterest 소스 연결 만들기](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [UI에서 광고 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/advertising.md)
