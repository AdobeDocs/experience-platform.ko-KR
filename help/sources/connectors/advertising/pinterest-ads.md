---
keywords: Experience Platform;홈;인기 주제;Pinterest 광고
title: Pinterest 광고 소스 개요
description: API 또는 사용자 인터페이스를 사용하여 Pinterest Ads를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badge: "Beta"
hide: true
hidefromtoc: true
source-git-commit: a16264da68d9e5e9aeac86b1a3083c701407febb
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>다음 [!DNL Pinterest Ads] 소스가 베타 버전입니다. 다음 문서를 참조하십시오. [소스 개요](../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 광고 시스템에서 데이터 섭취를 지원합니다. 광고 공급자에 대한 지원에는 다음이 포함됩니다 [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) 는 웹에서 조리법, 집 장식, 스타일 영감 및 기타 아이디어를 찾기 위한 시각적 검색 엔진입니다. 이러한 이미지는 이미지, 애니메이션 GIF 및 핀보드 형식의 비디오를 사용하여 작은 규모로 표시됩니다. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) 을 통해 비즈니스 규모 확대 및 [!DNL Pinterest].

사용 [!DNL Pinterest Ads]를 사용하면 타겟팅된 광고를 통해 사용자에게 연락하여 제품을 찾고 구매할 수 있습니다. 핀 위치 [!DNL Pinterest Ads] 는 관련 검색 결과에서 추가 노출을 받도록 스폰서됩니다. 에 가입한 사용자 [!DNL Pinterest Business] 기존 최고 성능의 핀을 홍보하거나, 새 이미지나 비디오를 만들거나, 웹 사이트에서 고정된 이미지를 홍보하도록 선택할 수 있습니다. [!DNL Pinterest Ads] 에서는 특정 캠페인 목표를 충족하는 데 도움이 되는 몇 가지 광고 형식을 제공합니다.

## [!DNL Pinterest] API {#pinterest-apis}

다음 [!DNL Pinterest Ads] 소스 는 [!DNL Pinterest] 검색할 API [!DNL Pinterest Ads] 모든 성능 및 지표와 함께 데이터를 전송할 수 있습니다. 지원되는 API 엔드포인트는 다음과 같습니다.

* [Campaign 분석](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [광고 그룹 분석](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [광고 분석](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

를 사용하십시오 [!DNL Pinterest Ads] 데이터를 가져올 소스 [!DNL Pinterest] Experience Platform을 위해 데이터 분석을 실행할 수 있습니다. 데이터는 오래된 90일 범위 동안 수집일로부터 반환됩니다. [!DNL Pinterest Ads] 는 bearer 토큰을 인증 메커니즘으로 사용하여 와 통신합니다 [!DNL Pinterest] API.

## 사전 요구 사항 {#prerequisites}

웹 사이트를 작성하는 첫 번째 단계 [!DNL Pinterest Ads] 소스 연결은 Pinterest 개발자 계정이 있는지 확인하는 것입니다. 아직 없는 경우 [등록](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) 페이지를 사용하여 계정을 등록하고 만듭니다.

### 설정 [!DNL Pinterest] 앱 및 액세스 토큰 생성 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>을 사용하는 것이 좋습니다 [!DNL Pinterest] UI에서 액세스 토큰을 생성하면 제한된 액세스가 제공되므로 액세스 토큰을 생성하는 API입니다. UI를 통해 다음 범위에만 액세스할 수 있습니다. `pins:read`, `boards:read` 및 `user_accounts:read`. 이 제한은 의 analytics 종단점에서 사용하는 경우에는 적합하지 않습니다 [!DNL Pinterest] API.

액세스 토큰을 생성하려면 [!DNL Pinterest] 안내서 [앱 설정](https://developers.pinterest.com/docs/getting-started/set-up-app/) 및 [OAuth 2.0을 사용하여 인증](https://developers.pinterest.com/docs/getting-started/authentication/).

### 필요한 자격 증명 수집 {#gather-required-credentials}

연결하려면 [!DNL Pinterest Ads] 플랫폼에 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 액세스 토큰 | 다음 [!DNL Pinterest Ads] 사용자 계정에 대한 액세스 토큰. 토큰의 사용자 계정은 지정된 토큰의 소유자라야 합니다 [!DNL Pinterest Ad] 계정을 사용하거나 비즈니스 액세스를 통해 필요한 역할 중 하나를 부여하십시오. 관리자, 분석가 또는 캠페인 관리자. 액세스 토큰에 대한 자세한 내용은 [[!DNL Pinterest] 액세스 토큰 생성에 대한 안내서](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| 광고 계정 ID | 관련 [!DNL Pinterest Ads] 비즈니스 단위의 계정 ID를 추가합니다. 광고 계정 ID 검색에 대한 정보입니다. 다음 방문 [[!DNL Pinterest] 광고 관리자에서 ID 찾기에 대한 안내서](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campaign, 광고 그룹 또는 광고 ID | 다음 `campaign`, `ad group`, 또는 `ad` 광고 계정 ID에 해당하는 ID입니다. 필요한 ID를 얻으려면 [!DNL Pinterest] 페이지 **Pinterest 비즈니스 허브** > **광고 계정 요약** > **캠페인** / **광고 그룹** / **광고** 및 각 이름 바로 아래에 언급된 필수 ID를 복사합니다. |

>[!NOTE]
>
>다음 [!DNL Pinterest] API는 각 ID와 연결된 데이터를 검색하기 위한 개별 API를 제공합니다. 따라서 관심이 있는 ID 유형에 해당하는 ID만 전달해야 합니다.

## 가드레일 {#guardrails}

다음 섹션에서는 [!DNL Pinterest].

### [!DNL Pinterest] 날짜 범위 {#pinterest-date-range}

다음 [!DNL Pinterest] API는 둘 다 지원합니다 `start_date` 그리고 `end_date` 지정된 날짜 범위 간에 analytics 데이터를 검색하는 매개 변수입니다.

* 다음 `start_date` 는 현재 날짜보다 90일 이상 앞에 있을 수 없습니다.
* 다음 `end_date` 는 이후 90일을 초과할 수 없습니다. `start_date`.

데이터 흐름을 예약할 때 다음 빈도 및 간격 설정 중 하나를 구성해야 합니다.

| 빈도 | 간격 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

예를 들어 수집이 2023년 3월 15일에 로 설정된 경우 빈도 및 간격 설정이 로 구성된 경우 `Day=1` 또는 `Hour=24`, 그런 다음 [!DNL Pinterest] 계산은 90일 동안 소급 적용되므로 API는 2022년 12월 15일까지만 데이터를 검색합니다.

### [!DNL Pinterest] 시간 범위 {#pinterest-time-range}

다음 [!DNL Pinterest] API는 데이터를 검색하는 방법에 대해 다양한 종류의 시간 세부기간을 지원합니다.

| 시간 세부기간 | 설명 |
| --- | --- |
| **합계** | 데이터 지표는 지정된 날짜 범위에 대해 집계됩니다. |
| **일** | 데이터 지표는 일별로 분류됩니다. |
| **시간** | 데이터 지표는 시간별로 분류됩니다. |
| **주별** | 데이터 지표는 주별 단위로 분류됩니다. |
| **월별** | 데이터 지표는 월별 기준으로 분류됩니다. |

플랫폼의 경우 [!DNL Pinterest Ads] 소스가 내부적으로 `Day`: 데이터가 일별로 집계됨을 의미합니다. 예를 들어 `impressions recorded` 지표로, 세부기간이 `DAY`를 호출하면 `xx` 노출 횟수 `day 1`, `yy` 노출 횟수 `day 2` 기타.

>[!IMPORTANT]
>
>Pinterest은 광고, 광고 그룹 또는 광고 캠페인에서 정보를 읽기 위해 API에 매일 1000개의 API 호출의 비율 제한을 지정합니다. 기본 API 호출에 적용할 수 있는 비율 제한에 대한 자세한 내용은 [[!DNL Pinterest] 비율 제한 설명서](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connect [!DNL Pinterest Ads] 플랫폼 {#connect-to-platform}

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Pinterest Ads] API 또는 사용자 인터페이스를 사용하여 플랫폼:

### Connect [!DNL Pinterest Ads] API를 사용하여 플랫폼 구현 {#connect-to-platform-using-api}

* [Flow Service API를 사용하여 Pinterest 기본 연결 만들기](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Flow Service API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [Flow Service API를 사용하여 광고 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/advertising.md)

### Connect [!DNL Pinterest Ads] UI를 사용하여 플랫폼 구현 {#connect-to-platform-using-ui}

* [UI에서 Pinterest 소스 연결 만들기](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [UI에서 광고 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/advertising.md)
