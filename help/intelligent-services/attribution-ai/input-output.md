---
keywords: Experience Platform;getting started;Attribution ai;popular topics;Attribution ai input;Attribution ai output;
solution: Experience Platform
title: Attribution AI 입력 및 출력
topic: Input and Output data for Attribution AI
description: 다음 문서에서는 Attribution AI에서 사용되는 다양한 입력 및 출력 개요를 설명합니다.
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '2075'
ht-degree: 3%

---


# [!DNL Attribution AI] 입력 및 출력

다음 문서에서는 사용되는 다양한 입력 및 출력 개요를 설명합니다 [!DNL Attribution AI].

## [!DNL Attribution AI] 입력 데이터

[!DNL Attribution AI] 데이터 [!DNL Consumer Experience Event] 를 사용하여 알고리즘 점수를 계산합니다. 자세한 내용 [!DNL Consumer Experience Event]은 Intelligent Services에서 사용할 [데이터 준비 설명서를 참조하십시오](../data-preparation.md).

Attribution AI에 대해 [!DNL Consumer Experience Event] (CEE) 스키마의 모든 열이 필수는 아닙니다.

>[!NOTE]
>
> 다음 9개의 열은 필수 열이며, 추가 열은 선택 사항이지만, [!DNL Customer AI] 및 같은 다른 Adobe 솔루션에 동일한 데이터를 사용하려면 권장/필요합니다 [!DNL Journey AI].

| 필수 열 | Needed for |
| --- | --- |
| 기본 ID 필드 | 터치포인트/전환 |
| 타임스탬프 | 터치포인트/전환 |
| Channel._type | 터치포인트 |
| Channel.mediaAction | 터치포인트 |
| Channel.mediaType | 터치포인트 |
| Marketing.trackingCode | 터치포인트 |
| Marketing.campaignname | 터치포인트 |
| Marketing.campaigngroup | 터치포인트 |
| 상거래 | 전환 |

일반적으로 속성은 &quot;커머스&quot;에서 주문, 구매 및 체크아웃과 같은 전환 열에서 실행됩니다. &quot;채널&quot; 및 &quot;마케팅&quot; 열은 유용한 인사이트를 위해 접점을 정의하는 데 적극 권장됩니다. 하지만 위의 열과 함께 다른 추가 열을 포함하여 전환 또는 터치포인트 정의로 구성할 수 있습니다.

아래 열은 필수는 아니지만 사용 가능한 정보가 있는 경우 CEE 스키마에 포함하는 것이 좋습니다.

**추가 권장 열:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### 이전 데이터

>[!IMPORTANT]
>
> Attribution AI이 작동하는 데 필요한 최소 데이터 양은 다음과 같습니다.
> - 좋은 모델을 실행하려면 최소 3개월(90일)의 데이터를 제공해야 합니다.
> - 최소 1000개의 전환이 필요합니다.


Attribution AI은 모델 트레이닝에 대한 입력으로 내역 데이터를 필요로 합니다. 필요한 데이터 기간은 주로 두 가지 주요 요인에 의해 결정됩니다.트레이닝 창 및 뒤로 보기 창 트레이닝 기간이 짧을수록 최근 트렌드에 더 민감하게 반응하는 반면 트레이닝 기간이 길수록 모델이 안정적이고 정확해집니다. 비즈니스 목표를 가장 잘 나타내는 내역 데이터로 목표를 모델링하는 것이 중요합니다.

교육 [창 구성은](./user-guide.md#training-window) 발생 시간에 따라 모델 교육에 포함되도록 설정된 전환 이벤트를 필터링합니다. 현재 최소 교육 기간은 1/4입니다(90일). 조회 [창에서는](./user-guide.md#lookback-window) 전환 이벤트와 관련된 전환 이벤트 터치포인트 전 며칠을 포함해야 하는지 나타내는 시간대를 제공합니다. 이 두 개념은 함께 애플리케이션에 필요한 입력 데이터(일 단위 측정)의 양을 결정합니다.

기본적으로 Attribution AI은 교육 창을 최근 2분기(6개월)로 정의하고 조회 창을 56일로 정의합니다. 즉, 모델은 지난 2분기 동안 발생한 정의된 모든 전환 이벤트를 고려하여 연관된 전환 이벤트 56일 전에 발생한 모든 접점을 찾습니다.

**공식**:

필요한 최소 데이터 길이 = 교육 창 + 조회 창

>[!TIP]
>
> 기본 구성이 있는 응용 프로그램에 필요한 데이터의 최소 길이는 다음과 같습니다.2분기(180일) + 56일 = 236일

예 :

- 지난 90일(3개월) 이내에 발생한 전환 이벤트를 추적하고 전환 이벤트 4주 전에 발생한 모든 터치포인트를 추적하려고 합니다. 입력 데이터 기간은 지난 90일 + 28일(4주)에 걸쳐 지속되어야 합니다. 트레이닝 기간은 90일이며 조회 기간은 118일입니다.

## Attribution AI 출력 데이터

Attribution AI은 다음을 출력합니다.

- [세부적인 원시 점수](#raw-granular-scores)
- [집계된 점수](#aggregated-attribution-scores)

**출력 스키마 예:**

![](./images/input-output/schema_output.gif)

### 세부적인 원시 점수 {#raw-granular-scores}

Attribution AI은 모든 점수 열을 기준으로 점수를 슬라이스하여 가릴 수 있도록 최대한 세분화된 수준의 속성 점수를 출력합니다. UI에서 이러한 점수를 보려면 원시 점수 경로 [보기 섹션을 참조하십시오](#raw-score-path). API를 사용하여 점수를 다운로드하려면 Attribution AI [문서의](./download-scores.md) 다운로드 점수를 참조하십시오.

>[!NOTE]
>
> 다음 중 하나가 참인 경우에만 점수 출력 데이터 세트의 입력 데이터 세트에서 원하는 보고 열을 볼 수 있습니다.
> - 보고 열은 터치포인트 또는 전환 정의 구성의 일부로 구성 페이지에 포함됩니다.
> - 보고 열은 추가 점수 데이터 집합 열에 포함됩니다.


다음 표에서는 원시 점수 예제 출력에서 스키마 필드에 대해 간략하게 설명합니다.

| 열 이름(DataType) | Nullable | 설명 |
| --- | --- | --- |
| timestamp(DateTime) | False | 전환 이벤트나 관찰이 발생한 시간입니다. <br> **예:** 2020-06-09T00:01:51.000Z |
| identityMap(맵) | True | CEE XDM 형식과 유사한 사용자의 identityMap. |
| eventType(문자열) | True | 이 시계열 레코드의 기본 이벤트 유형입니다. <br> **예:** &quot;주문&quot;, &quot;구매&quot;, &quot;방문&quot; |
| eventMergeId(문자열) | True | 본질적으로 동일한 이벤트이거나 병합해야 하는 여러 개의 상호 [!DNL Experience Events] 관계를 지정하거나 병합하는 ID입니다. 이것은 수집하기 전에 데이터 프로듀서가 채워야 합니다. <br> **예:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id(문자열) | False | 시간 시리즈 이벤트의 고유 식별자입니다. <br> **예:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId(개체) | False | 촉각 ID에 해당하는 최상위 수준의 개체 컨테이너입니다. <br> **예:** _atsdsnrmmsv2 |
| your_schema_name(객체) | False | 전환 이벤트와 관련된 모든 터치포인트 이벤트와 해당 메타데이터의 점수 행을 만듭니다. <br> **예:** Attribution AI 점수 - 모델 이름__2020 |
| 세그멘테이션(문자열) | True | 모델이 만들어지는 지리 특성 등의 전환 세그먼트입니다. 세그먼트가 없는 경우 세그먼트는 conversionName과 동일합니다. <br> **예:** ORDER_US |
| conversionName(문자열) | True | 설정 중에 구성된 전환의 이름입니다. <br> **예:** 주문, 리드, 방문 |
| 전환(객체) | False | 전환 메타데이터 열. |
| dataSource(문자열) | True | 데이터 소스에 대한 전역 고유 식별 <br> **예:** Adobe Analytics |
| eventSource(문자열) | True | 실제 이벤트가 발생한 소스입니다. <br> **예:** Adobe.com |
| eventType(문자열) | True | 이 시계열 레코드의 기본 이벤트 유형입니다. <br> **예:** 주문 |
| geo(문자열) | True | 전환이 전달된 지리적 위치입니다 `placeContext.geo.countryCode`. <br> **예:** 미국 |
| priceTotal (Double) | True | 전환을 통해 얻은 매출 <br> **예:** 99.9 |
| 제품(문자열) | True | 제품 자체의 XDM 식별자입니다. <br> **예:** RX 1080ti |
| productType(문자열) | True | 이 제품 보기에 대해 사용자에게 표시되는 제품의 표시 이름입니다. <br> **예:** 고름 |
| 수량(정수) | True | 전환 중 구매한 수량. <br> **예:** 1080ti |
| receivedTimestamp(DateTime) | True | 전환의 타임스탬프를 수신했습니다. <br> **예:** 2020-06-09T00:01:51.000Z |
| skuId(문자열) | True | 공급업체에서 정의한 제품의 고유 식별자인 SKU(Stock Keeping Unit). <br> **예:** MJ-03-XS-Black |
| timestamp(DateTime) | True | 전환의 타임스탬프. <br> **예:** 2020-06-09T00:01:51.000Z |
| passThrough(객체) | True | 추가 점수 데이터 집합 사용자가 모델을 구성하는 동안 지정한 열입니다. |
| commerce_order_purchaseCity(문자열) | True | 추가 점수 데이터 집합 열을 참조하십시오. <br> **예:** city :산호세 |
| customerProfile(개체) | False | 모델을 작성하는 데 사용되는 사용자의 ID 세부 정보입니다. |
| identity (객체) | False | 및 같은 모델을 빌드하는 데 사용된 사용자의 세부 사항을 `id` 포함합니다 `namespace`. |
| id(문자열) | True | 쿠키 ID, AID 또는 MCID와 같은 사용자의 ID <br> **예:** 1734876272540865644688320891369597404 |
| namespace(문자열) | True | 경로를 빌드하고 모델을 만드는 데 사용되는 ID 네임스페이스입니다. <br> **예:** aaid |
| 터치포인트 세부(개체 배열) | True | 터치포인트 발생 또는 타임스탬프별로 정렬된 전환으로 연결되는 터치포인트 세부 사항 목록 |
| touchpointName(문자열) | True | 설정 중에 구성된 터치포인트의 이름입니다. <br> **예:** PAID_SEARCH_CLICK |
| 점수(개체) | True | 이 전환에 대한 터치포인트 기여도를 점수로 지정합니다. 이 개체 내에서 생성된 점수에 대한 자세한 내용은 [집계된 기여도](#aggregated-attribution-scores) 점수 섹션을 참조하십시오. |
| touchPoint(개체) | True | 터치포인트 메타데이터를 참조하십시오. 이 개체 내에서 생성된 점수에 대한 자세한 내용은 [집계된 점수](#aggregated-scores) 섹션을 참조하십시오. |

### 원시 점수 경로 보기(UI) {#raw-score-path}

UI에서 원시 점수의 경로를 볼 수 있습니다. 먼저 플랫폼 UI에서 **[!UICONTROL 스키마를]** 선택한 다음 검색 **[!UICONTROL 탭 내에서 속성 AI 점수 스키마를 검색하고 선택합니다]** .

![스키마 선택](./images/input-output/schemas_browse.png)

그런 다음 UI의 **[!UICONTROL 구조]** 창 내에서 필드를 선택하면 **[!UICONTROL 필드 속성]** 탭이열립니다. Within **[!UICONTROL Field 속성]** 은 원시 점수에 매핑되는 경로 필드입니다.

![스키마 선택](./images/input-output/field_properties.png)


### 집계된 기여도 분석 점수 {#aggregated-attribution-scores}

날짜 범위가 30일 미만인 경우 플랫폼 UI에서 집계된 점수를 CSV 형식으로 다운로드할 수 있습니다.

Attribution AI은 두 가지 속성 점수, 알고리즘 및 규칙 기반 점수를 지원합니다.

Attribution AI은 두 가지 다른 유형의 알고리즘 점수, 증분 및 영향을 생성합니다. 영향을 받는 점수는 각 마케팅 접점이 담당하는 전환의 일부입니다. 점수는 마케팅 접점에 의해 직접적으로 발생하는 한계적 영향의 양입니다. 증분 점수와 영향을 받는 점수 간의 주요 차이점은 증분 점수가 기준선 효과를 고려한다는 것입니다. 전환은 단순히 이전 마케팅 접점에서만 발생한다고 간주하지 않습니다.

다음은 Adobe Experience Platform UI에서 나오는 Attribution AI 스키마 출력 예입니다.

![](./images/input-output/schema_screenshot.png)

이러한 각 속성 점수에 대한 자세한 내용은 아래 표를 참조하십시오.

| 기여도 점수 | 설명 |
| ----- | ----------- |
| 영향(알고리즘) | 영향을 받은 점수는 각 마케팅 접점이 담당하는 전환의 일부입니다. |
| 증분(알고리즘) | 증분 점수는 마케팅 접점에 의해 직접적으로 발생하는 한계 영향의 양입니다. |
| 첫 번째 터치 | 전환 경로의 초기 접점에 모든 크레딧을 할당하는 규칙 기반 속성 점수입니다. |
| 마지막 터치 | 전환에 가장 가까운 터치포인트에 모든 크레딧을 할당하는 규칙 기반 속성 점수입니다. |
| 선형 | 전환 경로의 각 접점에 동일한 크레딧을 할당하는 규칙 기반 속성 점수입니다. |
| U자형 | 첫 번째 터치포인트에 크레딧의 40%, 마지막 터치포인트에 크레딧의 40%를 할당하는 규칙 기반 기여도 분석 점수와 나머지 20%가 동일하게 분할되는 다른 터치포인트를 함께 제공합니다. |
| 시간 감소 | 접점이 전환에 가까운 규칙 기반 기여도 점수는 전환으로부터 더 먼 시간에 접하는 접점보다 더 많은 크레딧을 받습니다. |

**원시 점수 참조(속성 점수)**

아래 표는 속성 점수를 원시 점수에 매핑합니다. Raw 점수를 다운로드하려면 Attribution AI [설명서의](./download-scores.md) 다운로드 점수를 참조하십시오.

| 기여도 점수 | 원시 점수 참조 열 |
| --- | --- |
| 영향(알고리즘) | _tenantID.your_schema_name.element.touchpoint.algorithmicAffinted |
| 증분(알고리즘) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicAffinted |
| 첫 번째 터치 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 마지막 터치 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| 선형 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U자형 | _tenantID.your_schema_name.touchpointDetail.element.touchpoint.uShape |
| 시간 감소 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.deparageUnits |

### 집계된 점수 {#aggregated-scores}

날짜 범위가 30일 미만인 경우 플랫폼 UI에서 집계된 점수를 CSV 형식으로 다운로드할 수 있습니다. 이러한 각 집계 열에 대한 자세한 내용은 아래 표를 참조하십시오.

| 열 이름 | 제한 | Nullable | 설명 |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | 사용자 정의 및 고정 형식 | False | 고객 이벤트 날짜(YYYY-MM-DD 형식) <br> **예**:2016-05-02 |
| mediatochpoints_date(DateTime) | 사용자 정의 및 고정 형식 | True | 미디어 터치포인트 날짜(YYYY-MM-DD 형식) <br> **예**:2017-04-21 |
| 세그먼트(문자열) | 계산됨 | False | 전환 세그먼트(예: 모델이 만들어지는 지리 특성). 세그먼트가 없는 경우 세그먼트는 conversion_scope와 동일합니다. <br> **예**:ORDER_AMER |
| conversion_scope(문자열) | 사용자 정의 | False | 사용자가 구성한 전환의 이름입니다. <br> **예**:주문 |
| touchpoint_scope(문자열) | 사용자 정의 | True | 사용자가 구성한 터치포인트의 이름 <br> **예**:PAID_SEARCH_CLICK |
| 제품(문자열) | 사용자 정의 | True | 제품의 XDM 식별자입니다. <br> **예**:CC |
| product_type(문자열) | 사용자 정의 | True | 이 제품 보기에 대해 사용자에게 표시되는 제품의 표시 이름입니다. <br> **예**:gpus, 랩탑 |
| geo(문자열) | 사용자 정의 | True | 전환이 전달된 지리적 위치(placeContext.geo.countryCode) <br> **예**:미국 |
| event_type(문자열) | 사용자 정의 | True | 이 시계열 레코드의 기본 이벤트 유형 <br> **예**:유료 전환 |
| media_type(문자열) | ENUM | False | 미디어 유형이 유료, 소유 또는 획득 중 어느 것인지 설명합니다. <br> **예**:유료, 소유 |
| channel(문자열) | ENUM | False | XDM에서 유사한 속성을 갖는 채널의 가편집 분류를 제공하는 데 사용되는 `channel._type` [!DNL Consumer Experience Event] 속성입니다. <br> **예**:검색 |
| 작업(문자열) | ENUM | False | 이 `mediaAction` 속성은 경험 이벤트 미디어 작업 유형을 제공하는 데 사용됩니다. <br> **예**:클릭 |
| campaign_group(문자열) | 사용자 정의 | True | 여러 캠페인이 &#39;50%_DISCOUNT&#39;와 같이 함께 그룹화되는 캠페인 그룹의 이름입니다. <br> **예**:상업 |
| campaign_name(문자열) | 사용자 정의 | True | &#39;50%_DISCOUNT_USA&#39; 또는 &#39;50%_DISCOUNT_ASIA&#39;와 같은 마케팅 캠페인을 식별하는 데 사용되는 캠페인 이름. <br> **예**:추수감사절 세일 |

**원시 점수 참조(집계)**

아래 표는 집계된 점수를 원시 점수에 매핑합니다. Raw 점수를 다운로드하려면 Attribution AI [설명서의](./download-scores.md) 다운로드 점수를 참조하십시오. UI 내에서 원시 점수 경로를 보려면 이 문서 내의 원시 점수 경로 [보기 섹션을](#raw-score-path) 방문하십시오.

| 열 이름 | 원시 점수 참조 열 |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| 세그먼트 | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| toupoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| 제품 | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| geo | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 조치 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |


## 다음 단계 {#next-steps}

데이터를 준비하고 모든 자격 증명 및 스키마를 준비했으면 [Attribution AI 사용 안내서를 따라 시작하십시오](./user-guide.md). 이 안내서에서는 Attribution AI 인스턴스를 만드는 과정을 안내합니다.