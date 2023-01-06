---
keywords: Experience Platform;시작하기;속성 ai;인기 항목;속성 ai 입력;속성 ai 출력;
feature: Attribution AI
title: Attribution AI의 입력 및 출력
description: 다음 문서에서는 Attribution AI에서 사용되는 다양한 입력 및 출력에 대해 설명합니다.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2504'
ht-degree: 3%

---

# 입력 및 출력 [!DNL Attribution AI]

다음 문서에서는 [!DNL Attribution AI].

## [!DNL Attribution AI] 입력 데이터

Attribution AI은 다음 데이터 세트를 분석하여 알고리즘 점수를 계산하여 작동합니다.

- 을 사용하여 Adobe Analytics 데이터 세트 [Analytics 소스 커넥터](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Experience Platform 스키마의 일반 EE(경험 이벤트) 데이터 세트
- CEE(소비자 경험 이벤트) 데이터 세트

이제 를 기반으로 다른 소스의 여러 데이터 세트를 추가할 수 있습니다 **id 맵** (필드) 각 데이터 세트가 ECID와 같은 동일한 ID 유형(네임스페이스)을 공유하는 경우 ID 및 네임스페이스를 선택하면 결합되는 데이터의 볼륨을 나타내는 ID 열 완결성 지표가 나타납니다. 여러 데이터 세트를 추가하는 방법에 대해 자세히 알아보려면 [Attribution AI 사용 안내서](./user-guide.md#identity).

기본적으로 채널 정보가 항상 매핑되는 것은 아닙니다. 경우에 따라 mediaChannel(필드)이 비어 있으면 필수 열이므로 mediaChannel에 필드를 매핑할 때까지 &quot;계속&quot;을 수행할 수 없습니다. 데이터 세트에서 채널이 검색되면 기본적으로 mediaChannel에 매핑됩니다. 기타 열(예: **미디어 유형** 및 **미디어 작업** 은 여전히 선택 사항입니다.

채널 필드를 매핑한 후에는 &#39;이벤트 정의&#39; 단계를 계속 진행하여 전환 이벤트, 터치 포인트 이벤트를 선택하고 개별 데이터 세트에서 특정 필드를 선택할 수 있습니다.

>[!IMPORTANT]
>
>Adobe Analytics 소스 커넥터에서 데이터를 채우는 데 최대 4주가 걸릴 수 있습니다. 최근에 커넥터를 설정하는 경우 데이터 세트에 Attribution AI에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. 다음 문서를 검토하십시오 [내역 데이터](#data-requirements) 정확한 알고리즘 점수를 계산할 충분한 데이터가 있는지 확인하는 섹션을 추가했습니다.

설정에 대한 자세한 내용 [!DNL Consumer Experience Event] (CEE) 스키마는 [Intelligent Services 데이터 준비](../data-preparation.md) 안내서. Adobe Analytics 데이터 매핑에 대한 자세한 내용은 [Analytics 필드 매핑](../../sources/connectors/adobe-applications/analytics.md) 설명서.

의 일부 열은 [!DNL Consumer Experience Event] (CEE) 스키마는 Attribution AI에 필수입니다.

스키마나 선택한 데이터 세트에서 아래 권장 필드를 사용하여 터치 포인트를 구성할 수 있습니다.

| 권장 열 | 필요한 대상 |
| --- | --- |
| 기본 ID 필드 | 터치 포인트/전환 |
| 타임스탬프 | 터치 포인트/전환 |
| 채널._유형 | 터치 포인트 |
| Channel.mediaAction | 터치 포인트 |
| Channel.mediaType | 터치 포인트 |
| Marketing.trackingCode | 터치 포인트 |
| Marketing.campaignname | 터치 포인트 |
| Marketing.campaigngroup | 터치 포인트 |
| Commerce | 전환 |

일반적으로 속성은 &quot;상거래&quot; 아래의 주문, 구매 및 체크아웃과 같은 전환 열에서 실행됩니다. &quot;채널&quot; 및 &quot;마케팅&quot;에 대한 열은 Attribution AI에 대한 터치포인트를 정의하는 데 사용됩니다(예: `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). 최적의 결과 및 인사이트를 위해서는 가능한 한 많은 전환 및 터치 포인트 열을 포함하는 것이 좋습니다. 또한 위의 열에만 국한되지 않습니다. 다른 권장 열 또는 사용자 지정 열을 전환 또는 터치 포인트 정의로 포함할 수 있습니다.

경험 이벤트(EE) 터치 포인트를 구성하는 것과 관련된 채널 또는 캠페인 정보가 mixin 또는 through 필드 중 하나에 존재하는 한, 데이터 세트에 채널 및 마케팅 Mixin이 명시적으로 있을 필요가 없습니다.

>[!TIP]
>
>CEE 스키마에서 Adobe Analytics 데이터를 사용하는 경우 Analytics에 대한 터치포인트 정보는 일반적으로 `channel.typeAtSource` (예: `channel.typeAtSource = 'email'`).

## 이전 데이터 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI이 작동하는 데 필요한 최소 데이터 양은 다음과 같습니다.
> - 좋은 모델을 실행하려면 최소 3개월(90일)의 데이터를 제공해야 합니다.
> - 전환이 1000개 이상 필요합니다.


Attribution AI은 모델 교육을 위한 입력으로 이전 데이터가 필요합니다. 필요한 데이터 기간은 주로 다음 두 가지 주요 요인에 의해 결정됩니다. 교육 창 및 전환 확인 기간 훈련 기간이 짧은 입력은 최신 트렌드에 더 민감하지만, 교육 기간이 길면 보다 안정적이고 정확한 모델을 생성할 수 있습니다. 비즈니스 목표를 가장 잘 나타내는 이전 데이터로 목표를 모델링하는 것이 중요합니다.

다음 [교육 창 구성](./user-guide.md#training-window) 은(는) 발생 시간에 따라 모델 교육을 위해 포함되도록 설정된 전환 이벤트를 필터링합니다. 현재 최소 교육 기간은 1/4분기(90일)입니다. 다음 [전환 창](./user-guide.md#lookback-window) 은 이 전환 이벤트와 관련된 전환 이벤트 터치포인트를 포함하기 전 일 수를 나타내는 기간을 제공합니다. 이 두 가지 개념은 애플리케이션에 필요한 입력 데이터(일 단위로 측정)의 양을 함께 결정합니다.

기본적으로 Attribution AI은 교육 기간을 가장 최근 2분기(6개월)로 정의하고 전환 확인 기간은 56일로 정의합니다. 다시 말해, 모델은 지난 2분기에 발생한 정의된 모든 전환 이벤트를 고려하고 연관된 전환 이벤트 전 56일 이내에 발생한 모든 터치포인트를 찾습니다.

**공식**:

필요한 최소 데이터 길이 = 교육 창 + 조회 창

>[!TIP]
>
> 기본 구성이 있는 응용 프로그램에 필요한 최소 데이터 길이는 다음과 같습니다. 2분기(180일) + 56일 = 236일.

예:

- 지난 90일(3개월) 내에 발생한 전환 이벤트를 추적하고 전환 이벤트 4주 전에 발생한 모든 터치포인트를 추적하려고 합니다. 입력 데이터 기간은 지난 90일 + 28일(4주)에 걸쳐 지속되어야 합니다. 교육 기간은 90일이며 전환 확인 기간은 총 118일입니다.

## Attribution AI 출력 데이터

Attribution AI은 다음을 출력합니다.

- [원시 세분화된 점수](#raw-granular-scores)
- [집계된 점수](#aggregated-attribution-scores)

**출력 스키마 예:**

![](./images/input-output/schema_output.gif)

### 원시 세분화된 점수 {#raw-granular-scores}

Attribution AI은 모든 점수 열로 점수를 나누고 분류할 수 있도록 가능한 가장 세부적인 수준의 속성 점수를 출력합니다. UI에서 이러한 점수를 보려면 [원시 점수 경로 보기](#raw-score-path). API를 사용하여 점수를 다운로드하려면 [Attribution AI에서 점수 다운로드](./download-scores.md) 문서.

>[!NOTE]
>
> 다음 중 하나가 참인 경우에만 점수 출력 데이터 세트의 입력 데이터 세트에서 원하는 보고 열을 볼 수 있습니다.
> - 보고 열은 터치 포인트 또는 전환 정의 구성의 일부로 구성 페이지에 포함됩니다.
> - 보고 열은 추가 점수 데이터 세트 열에 포함됩니다.


다음 표에서는 원시 점수 예제 출력의 스키마 필드에 대해 설명합니다.

| 열 이름(DataType) | Nullable | 설명 |
| --- | --- | --- |
| timestamp(DateTime) | False | 전환 이벤트 또는 관찰이 발생한 시간입니다. <br> **예:** 2020-06-09T00:01:51.00Z |
| identityMap(맵) | True | CEE XDM 형식과 유사한 사용자의 identityMap입니다. |
| eventType(String) | True | 이 시계열 레코드에 대한 기본 이벤트 유형입니다. <br> **예:** &quot;주문&quot;, &quot;구매&quot;, &quot;방문&quot; |
| eventMergeId(String) | True | 여러 ID를 상호 연결하거나 병합하는 ID [!DNL Experience Events] 이 두 이벤트는 기본적으로 동일한 이벤트나 병합해야 합니다. 이는 섭취 전에 데이터 생성자가 채워주기 위한 것입니다. <br> **예:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id(문자열) | False | 시계열 이벤트에 대한 고유 식별자입니다. <br> **예:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId(Object) | False | 중간 ID에 해당하는 최상위 객체 컨테이너입니다. <br> **예:** _atsdsnrmmsv2 |
| your_schema_name(개체) | False | 전환 이벤트와 함께 점수 행에 연결된 모든 터치 포인트 이벤트 및 메타데이터. <br> **예:** Attribution AI 점수 - 모델 이름__2020 |
| 세그먼테이션(문자열) | True | 모델이 만들어져 있는 지리 특성 등의 전환 세그먼트입니다. 세그먼트가 없는 경우 세그먼트는 conversionName과 동일합니다. <br> **예:** ORDER_US |
| conversionName(문자열) | True | 설정 중에 구성된 전환의 이름입니다. <br> **예:** 주문, 리드, 방문 |
| 변환(개체) | False | 변환 메타데이터 열. |
| dataSource(String) | True | 데이터 소스에 대한 전역적으로 고유한 식별. <br> **예:** Adobe Analytics |
| eventSource (String) | True | 실제 이벤트가 발생한 소스. <br> **예:** Adobe.com |
| eventType(String) | True | 이 시계열 레코드에 대한 기본 이벤트 유형입니다. <br> **예:** 주문 |
| 지역(문자열) | True | 전환이 전달된 지리적 위치입니다 `placeContext.geo.countryCode`. <br> **예:** 미국 |
| priceTotal (Double) | True | 전환을 통해 얻은 매출 <br> **예:** 99.9 |
| product (String) | True | 제품 자체의 XDM 식별자입니다. <br> **예:** RX 1080ti |
| productType(String) | True | 이 제품 보기에 대해 사용자에게 표시되는 제품의 표시 이름입니다. <br> **예:** 고름 |
| 수량(정수) | True | 전환 중 구매한 수량. <br> **예:** 1080ti |
| receivedTimestamp(DateTime) | True | 전환의 타임스탬프를 받았습니다. <br> **예:** 2020-06-09T00:01:51.00Z |
| skuId(문자열) | True | 공급업체에서 정의한 제품의 고유 식별자인 SKU(Stock Keeping Unit). <br> **예:** MJ-03-XS-블랙 |
| timestamp(DateTime) | True | 전환 타임스탬프입니다. <br> **예:** 2020-06-09T00:01:51.00Z |
| passThrough(개체) | True | 모델을 구성하는 동안 사용자가 지정한 추가 점수 데이터 세트 열입니다. |
| commerce_order_purchaseCity(String) | True | 추가 점수 데이터 세트 열. <br> **예:** city: San Jose |
| customerProfile(Object) | False | 모델을 만드는 데 사용되는 사용자의 ID 세부 사항입니다. |
| id(개체) | False | 다음과 같이 모델을 만드는 데 사용되는 사용자의 세부 정보를 포함합니다. `id` 및 `namespace`. |
| id(문자열) | True | 쿠키 ID, Adobe Analytics ID(AAID) 또는 Experience Cloud ID(ECID(MCID 또는 방문자 ID라고도 함) 등과 같은 사용자의 ID입니다. <br> **예:** 17348762725408656344688320891369597404 |
| namespace(문자열) | True | 경로를 빌드하여 모델을 만드는 데 사용되는 ID 네임스페이스입니다. <br> **예:** aaid |
| touchpointsDetail(개체 배열) | True | 주문된 전환으로 이어지는 터치 포인트 세부 사항 목록 | 터치 포인트 발생 또는 타임스탬프. |
| touchpointName(문자열) | True | 설정 중에 구성된 터치 포인트의 이름입니다. <br> **예:** PAID_SEARCH_CLICK |
| 점수(개체) | True | 점수로 이 변환에 대한 터치포인트 기여입니다. 이 객체 내에서 생성된 점수에 대한 자세한 내용은 [집계된 기여도 분석 점수](#aggregated-attribution-scores) 섹션을 참조하십시오. |
| touchPoint(개체) | True | 터치 포인트 메타데이터. 이 객체 내에서 생성된 점수에 대한 자세한 내용은 [집계된 점수](#aggregated-scores) 섹션을 참조하십시오. |

### 원시 점수 경로 보기(UI) {#raw-score-path}

UI에서 원시 점수의 경로를 볼 수 있습니다. 선택 **[!UICONTROL 스키마]** 에서 Platform UI에서 내에서 Attribution AI 점수 스키마를 검색하고 선택합니다 **[!UICONTROL 찾아보기]** 탭.

![스키마 선택](./images/input-output/schemas_browse.png)

다음으로, **[!UICONTROL 구조]** UI의 창, **[!UICONTROL 필드 속성]** 탭이 열립니다. 내 **[!UICONTROL 필드 속성]** 는 원시 점수에 매핑되는 경로 필드입니다.

![스키마 선택](./images/input-output/field_properties.png)

### 집계된 속성 점수 {#aggregated-attribution-scores}

날짜 범위가 30일 미만인 경우 Platform UI에서 CSV 형식으로 집계된 점수를 다운로드할 수 있습니다.

Attribution AI은 속성 점수, 알고리즘 및 규칙 기반 점수의 두 가지 카테고리를 지원합니다.

Attribution AI은 증가율과 영향을 받는 두 가지 유형의 알고리즘 점수를 생성합니다. 영향을 받는 점수는 각 마케팅 터치포인트가 담당하는 전환의 일부입니다. 증분 점수는 마케팅 터치포인트에 의해 직접적으로 발생한 한계 영향의 양입니다. 증분 점수와 영향을 받는 점수의 주요 차이점은 증분 점수가 기준 효과를 고려한다는 것입니다. 전환이 전적으로 이전 마케팅 터치포인트에 의해 발생한다고 가정하지는 않습니다.

다음은 Adobe Experience Platform UI에서 가져온 Attribution AI 스키마 출력 예제를 간략하게 보여주는 예입니다.

![](./images/input-output/schema_screenshot.png)

이러한 각 속성 점수에 대한 자세한 내용은 아래 표를 참조하십시오.

| 속성 점수 | 설명 |
| ----- | ----------- |
| 영향(알고리즘) | 영향을 받는 점수는 각 마케팅 터치포인트가 담당하는 전환의 일부입니다. |
| 증분(알고리즘) | 증분 점수는 마케팅 터치포인트에 의해 직접적으로 발생하는 한계 영향의 양입니다. |
| 첫 번째 터치 | 전환 경로의 초기 터치 포인트에 모든 크레딧을 지정하는 규칙 기반 속성 점수입니다. |
| 마지막 터치 | 전환에 가장 가까운 터치포인트에 모든 크레딧을 할당하는 규칙 기반 속성 점수. |
| 선형 | 전환 경로의 각 터치 포인트에 동일한 크레딧을 할당하는 규칙 기반 속성 점수. |
| U자형 | 첫 번째 터치 포인트에 크레딧의 40% 및 마지막 터치 포인트에 크레딧의 40%를 할당하는 규칙 기반 속성 점수, 나머지 20%를 동일하게 분할하는 다른 터치 포인트가 있습니다. |
| 시간 감소 | 전환과 가까운 터치포인트가 전환에서 더 먼 시간에 있는 터치포인트보다 더 많은 크레딧을 받는 규칙 기반 속성 점수입니다. |

**원시 점수 참조(속성 점수)**

아래 표는 속성 점수를 원시 점수에 매핑합니다. 원시 점수를 다운로드하려면 [Attribution AI에서 점수 다운로드](./download-scores.md) 설명서.

| 속성 점수 | 원시 점수 참조 열 |
| --- | --- |
| 영향(알고리즘) | _tenantID.your_schema_name.element.touchpoint.algorithmicInference |
| 증분(알고리즘) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInstructed |
| 첫 번째 터치 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 마지막 터치 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| 선형 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U자형 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| 시간 감소 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.detailUnits |

### 집계된 점수 {#aggregated-scores}

날짜 범위가 30일 미만인 경우 Platform UI에서 CSV 형식으로 집계된 점수를 다운로드할 수 있습니다. 이러한 각 집계 열에 대한 자세한 내용은 아래 표를 참조하십시오.

| 열 이름 | 제한 | Nullable | 설명 |
| --- | --- | --- | --- |
| customer_events_date (DateTime) | 사용자 정의 및 고정 형식 | False | YYYY-MM-DD 형식의 고객 이벤트 날짜. <br> **예**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | 사용자 정의 및 고정 형식 | True | YYYY-MM-DD 형식의 미디어 터치 포인트 날짜 <br> **예**: 2017-04-21 |
| 세그먼트(문자열) | 계산된 지표 | False | 모델이 만들어져 있는 지리 특성 등의 전환 세그먼트입니다. 세그먼트가 없는 경우 세그먼트는 conversion_scope와 동일합니다. <br> **예**: ORDER_AMER |
| conversion_scope(문자열) | 사용자 정의 | False | 사용자가 구성한 전환의 이름입니다. <br> **예**: 주문 |
| touchpoint_scope(문자열) | 사용자 정의 | True | 사용자가 구성한 터치포인트의 이름입니다 <br> **예**: PAID_SEARCH_CLICK |
| product (String) | 사용자 정의 | True | 제품의 XDM 식별자입니다. <br> **예**: CC |
| product_type(문자열) | 사용자 정의 | True | 이 제품 보기에 대해 사용자에게 표시되는 제품의 표시 이름입니다. <br> **예**: 노트북 |
| 지역(문자열) | 사용자 정의 | True | 전환이 전달되는 지리적 위치(placeContext.geo.countryCode) <br> **예**: 미국 |
| event_type (String) | 사용자 정의 | True | 이 시계열 레코드에 대한 기본 이벤트 유형입니다 <br> **예**: 유료 전환 |
| media_type(문자열) | 열거형 | False | 미디어 유형이 유료, 소유 또는 획득되는지 여부를 설명합니다. <br> **예**: 유료, 소유 |
| 채널(문자열) | 열거형 | False | 다음 `channel._type` 에서 유사한 속성을 갖는 채널을 대략적으로 분류하는 데 사용되는 속성입니다 [!DNL Consumer Experience Event] XDM. <br> **예**: 검색 |
| 작업(문자열) | 열거형 | False | 다음 `mediaAction` 속성은 경험 이벤트 미디어 작업 유형을 제공하는 데 사용됩니다. <br> **예**: 클릭 |
| campaign_group(문자열) | 사용자 정의 | True | 여러 캠페인을 &#39;50%_DISCOUNT&#39;처럼 함께 그룹화하는 캠페인 그룹의 이름입니다. <br> **예**: 상업 |
| campaign_name (문자열) | 사용자 정의 | True | &#39;50%_DISCOUNT_USA&#39; 또는 &#39;50%_DISCOUNT_ASIA&#39;와 같이 마케팅 캠페인을 식별하는 데 사용되는 캠페인의 이름입니다. <br> **예**: 추수감사절 세일 |

**원시 점수 참조(집계됨)**

아래 표는 집계된 점수를 원시 점수에 매핑합니다. 원시 점수를 다운로드하려면 [Attribution AI에서 점수 다운로드](./download-scores.md) 설명서. UI 내에서 원시 점수 경로를 보려면 [원시 점수 경로 보기](#raw-score-path) 이 문서 내에서 사용할 수 있습니다.

| 열 이름 | 원시 점수 참조 열 |
| --- | --- |
| customer_events_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| 세그먼트 | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touch_point_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| 지리적 위치 | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 작업 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Attribution AI은 추가 교육 및 점수를 위해 업데이트된 데이터만 사용합니다. 마찬가지로, 데이터 삭제를 요청하면 Customer AI는 삭제된 데이터를 사용하지 않습니다.
> - Attribution AI은 Platform 데이터 세트를 사용합니다. 브랜드가 수신할 수 있는 소비자 권한 요청을 지원하려면 브랜드는 Platform Privacy Service을 사용하여 소비자 액세스 및 삭제 요청을 제출하여 데이터 레이크, Identity Service 및 실시간 고객 프로필에서 데이터를 제거해야 합니다.
> - 모델의 입출력 작업에 사용하는 모든 데이터 세트는 플랫폼 지침을 따릅니다. Platform 데이터 암호화는 전송 중인 데이터를 위해 적용됩니다. 자세한 내용은 설명서 를 참조하십시오 [데이터 암호화](../../../help/landing/governance-privacy-security/encryption.md)


## 다음 단계 {#next-steps}

데이터를 준비하고 모든 자격 증명과 스키마를 준비했으면 다음을 수행하여 시작하십시오 [Attribution AI 사용 안내서](./user-guide.md). 이 안내서에서는 Attribution AI에 대한 인스턴스를 만드는 과정을 안내합니다.
