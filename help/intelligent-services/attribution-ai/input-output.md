---
keywords: Experience Platform;시작;속성 ai;인기 항목;속성(attribution ai) ai input;속성(attribution ai) ai output
solution: Experience Platform, Intelligent Services
title: Attribution AI의 입력 및 출력
topic-legacy: Input and Output data for Attribution AI
description: 다음 문서에서는 Attribution AI에서 사용되는 다양한 입력 및 출력 개요를 설명합니다.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 3%

---

# [!DNL Attribution AI]에 입력 및 출력

다음 문서에서는 [!DNL Attribution AI]에서 사용되는 다양한 입력 및 출력 개요를 설명합니다.

## [!DNL Attribution AI] 입력 데이터

Attribution AI은 다음 데이터 집합 중 하나를 분석하여 알고리즘 점수를 계산하는 방식으로 작동합니다.

- CEE(Consumer Experience Event) 데이터 세트
- [Analytics 소스 커넥터를 사용하는 Adobe Analytics 데이터 집합](../../sources/tutorials/ui/create/adobe-applications/analytics.md)

>[!IMPORTANT]
>
>Adobe Analytics 소스 커넥터는 데이터를 채우는 데 최대 4주가 걸릴 수 있습니다. 최근에 커넥터를 설정하는 경우 데이터 세트에 Attribution AI에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. [내역 데이터](#data-requirements) 섹션을 검토하여 정확한 알고리즘 점수를 계산하는 데 충분한 데이터가 있는지 확인하십시오.

[!DNL Consumer Experience Event](CEE) 스키마 설정에 대한 자세한 내용은 [지능형 서비스 데이터 준비](../data-preparation.md) 안내서를 참조하십시오. Adobe Analytics 데이터 매핑에 대한 자세한 내용은 [분석 필드 매핑](../../sources/connectors/adobe-applications/analytics.md) 설명서를 참조하십시오.

[!DNL Consumer Experience Event](CEE) 스키마의 모든 열이 Attribution AI에 필수는 아닙니다.

>[!NOTE]
>
> 다음 9개의 열은 필수이며, [!DNL Customer AI] 및 [!DNL Journey AI] 같은 다른 Adobe 솔루션에 대해 동일한 데이터를 사용하려면 추가 열이 선택 사항이지만 권장/필요합니다.

| 필수 열 | 필요 |
| --- | --- |
| 기본 ID 필드 | 터치포인트/전환 |
| 타임스탬프 | 터치포인트/전환 |
| Channel._type | 터치포인트 |
| Channel.mediaAction | 터치포인트 |
| Channel.mediaType | 터치포인트 |
| Marketing.trackingCode | 터치포인트 |
| Marketing.campaignname | 터치포인트 |
| Marketing.campaigngroup | 터치포인트 |
| Commerce | 전환 |

일반적으로 속성은 &quot;상거래&quot; 아래의 주문, 구매 및 체크아웃과 같은 전환 열에서 실행됩니다. &quot;채널&quot; 및 &quot;마케팅&quot; 열은 유용한 인사이트를 위해 접점을 정의하는 데 적극 권장됩니다. 하지만 위의 열과 함께 다른 추가 열을 포함하여 전환 또는 터치포인트 정의로 구성할 수 있습니다.

아래 열은 필요하지 않지만 사용 가능한 정보가 있는 경우 CEE 스키마에 포함하는 것이 좋습니다.

**추가 권장 열:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### 이전 데이터 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI이 작동하는 데 필요한 최소 데이터 양은 다음과 같습니다.
> - 좋은 모델을 실행하려면 최소 3개월(90일)의 데이터를 제공해야 합니다.
> - 최소 1,000개의 전환이 필요합니다.


Attribution AI은 모델 트레이닝에 대한 입력으로 내역 데이터를 필요로 합니다. 필요한 데이터 기간은 주로 다음 두 가지 주요 요인에 의해 결정됩니다.트레이닝 창 및 룩백 창 짧은 교육 창을 통해 입력하면 최신 트렌드에 더 민감하며 트레이닝 기간이 길면 보다 안정적이고 정확한 모델을 생성할 수 있습니다. 비즈니스 목표를 가장 잘 나타내는 내역 데이터로 목표를 모델링하는 것이 중요합니다.

[교육 창 구성](./user-guide.md#training-window)은 발생 시간에 따라 모델 교육에 포함되도록 설정된 전환 이벤트를 필터링합니다. 현재 최소 교육 기간은 1/4입니다(90일). [전환 창](./user-guide.md#lookback-window)은 이 전환 이벤트와 관련된 전환 이벤트 접점의 이전 일 수를 나타내는 기간을 제공합니다. 이 두 개념은 함께 애플리케이션에 필요한 입력 데이터의 양(일 단위 측정)을 결정합니다.

기본적으로 Attribution AI은 교육 창을 가장 최근 2분기(6개월)로 정의하고 전환 기간은 56일로 봅니다. 즉, 모델은 지난 2분기 동안 발생한 정의된 모든 전환 이벤트를 고려하고 연관된 전환 이벤트 이전 56일 이내에 발생한 모든 접점을 찾습니다.

**공식**:

필요한 최소 데이터 길이 = 교육 창 + 조회 창

>[!TIP]
>
> 기본 구성이 있는 응용 프로그램에 필요한 최소 데이터 길이는 다음과 같습니다.2분기(180일) + 56일 = 236일

예 :

- 지난 90일(3개월) 이내에 발생한 전환 이벤트를 적용하고 전환 이벤트 4주 전에 발생한 모든 접점을 추적하려는 경우 입력 데이터 기간은 지난 90일 + 28일(4주)에 걸쳐 지속되어야 합니다. 트레이닝 기간은 90일이며 조회 기간은 총 118일입니다.

## Attribution AI 출력 데이터

Attribution AI은 다음을 출력합니다.

- [세부적인 원시 점수](#raw-granular-scores)
- [집계된 점수](#aggregated-attribution-scores)

**출력 스키마 예:**

![](./images/input-output/schema_output.gif)

### 원시 정밀한 점수 {#raw-granular-scores}

Attribution AI은 점수 열을 기준으로 점수를 슬라이스하여 가릴 수 있도록 최대한 세분화된 수준으로 기여도 점수를 출력합니다. UI에서 이러한 점수를 보려면 [원시 점수 경로 보기](#raw-score-path)의 섹션을 참조하십시오. API를 사용하여 점수를 다운로드하려면 Attribution AI](./download-scores.md) 문서의 [다운로드 스코어를 방문하십시오.

>[!NOTE]
>
> 다음 중 하나가 참인 경우에만 점수 출력 데이터 세트의 입력 데이터 세트에서 원하는 보고 열을 볼 수 있습니다.
> - 보고 열은 터치포인트 또는 전환 정의 구성의 일부로 구성 페이지에 포함됩니다.
> - 보고 열은 추가 점수 데이터 세트 열에 포함됩니다.


다음 표에서는 원시 점수(예: 출력)의 스키마 필드에 대해 간략히 설명합니다.

| 열 이름(DataType) | Null 허용 | 설명 |
| --- | --- | --- |
| timestamp(DateTime) | False | 전환 이벤트나 관찰이 발생한 시간입니다.<br> **예:** 2020-06-09T00:01:51.000Z |
| identityMap(맵) | True | CEE XDM 형식과 유사한 사용자의 identityMap입니다. |
| eventType(문자열) | True | 이 시계열 레코드에 대한 기본 이벤트 유형입니다.<br> **예:** &quot;주문&quot;, &quot;구매&quot;, &quot;방문&quot; |
| eventMergeId(문자열) | True | 기본적으로 동일한 이벤트이거나 병합해야 하는 여러 [!DNL Experience Events]의 상호 연관시키거나 병합하는 ID입니다. 수집하기 전에 데이터 프로듀서가 채울 목적으로 만들어진 것입니다.<br> **예:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id(문자열) | False | 시간 시리즈 이벤트에 대한 고유 식별자입니다.<br> **예:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId(개체) | False | 촉각 ID에 해당하는 최상위 개체 컨테이너입니다. <br> **예:** _atsdsnrmmsv2 |
| your_schema_name(객체) | False | 전환 이벤트와 관련된 모든 터치포인트 이벤트와 해당 메타데이터의 점수 행을 만듭니다.<br> **예:** Attribution AI 점수 - 모델 이름__2020 |
| 세그멘테이션(문자열) | True | 모델이 기준이 되는 지리 특성 등의 전환 세그먼트입니다. 세그먼트가 없는 경우 세그먼트는 conversionName과 같습니다.<br> **예:** ORDER_US |
| conversionName(문자열) | True | 설정 중에 구성된 전환의 이름입니다.<br> **예:** 주문, 리드, 방문 |
| 전환(객체) | False | 전환 메타데이터 열. |
| dataSource(문자열) | True | 데이터 소스의 전역적 고유 식별<br> **예:** Adobe Analytics |
| eventSource(문자열) | True | 실제 이벤트가 발생한 소스.<br> **예:** Adobe.com |
| eventType(문자열) | True | 이 시계열 레코드에 대한 기본 이벤트 유형입니다.<br> **예:** 순서 |
| geo(문자열) | True | 전환이 `placeContext.geo.countryCode`으로 전달된 지리적 위치입니다. <br> **예:** 미국 |
| priceTotal (Double) | True | 전환 <br>을(를) 통해 얻은 매출 **예:** 99.9 |
| 제품(문자열) | True | 제품 자체의 XDM 식별자입니다.<br> **예:** RX 1080 ti |
| productType(문자열) | True | 이 제품 보기에 대해 사용자에게 표시되는 제품의 표시 이름입니다.<br> **예:** Gpu |
| 수량(정수) | True | 전환 중 구매한 수량.<br> **예:** 1 1080ti |
| receivedTimestamp(DateTime) | True | 전환의 타임스탬프를 수신했습니다.<br> **예:** 2020-06-09T00:01:51.000Z |
| skuId(문자열) | True | 공급업체에서 정의한 제품의 고유 식별자인 SKU(Stock Keeping Unit)입니다.<br> **예:** MJ-03-XS-Black |
| timestamp(DateTime) | True | 전환의 타임스탬프.<br> **예:** 2020-06-09T00:01:51.000Z |
| passThrough(객체) | True | 모델을 구성하는 동안 사용자가 지정한 추가 점수 데이터 세트 열. |
| commerce_order_purchaseCity (String) | True | 추가 점수 데이터 집합 열을 참조하십시오.<br> **예:** city :산호세 |
| customerProfile(개체) | False | 모델을 작성하는 데 사용되는 사용자의 ID 세부 사항입니다. |
| id(객체) | False | `id` 및 `namespace` 등의 모델을 작성하는 데 사용되는 사용자의 세부 정보를 포함합니다. |
| id(문자열) | True | 쿠키 ID, AID 또는 MCID 등과 같은 사용자의 ID <br> **예:** 17348762725408656344688320891369597404 |
| namespace (문자열) | True | 경로를 빌드하여 모델을 만드는 데 사용되는 ID 네임스페이스입니다.<br> **예:** aid |
| touchpointsDetail(개체 배열) | True | 터치포인트 발생 또는 타임스탬프별로 정렬된 전환으로 연결되는 터치포인트 세부 사항 목록. |
| touchpointName(문자열) | True | 설정 중에 구성된 터치포인트의 이름입니다.<br> **예:** PAID_SEARCH_CLICK |
| 점수(개체) | True | 이 전환에 대한 터치포인트 기여도를 점수로 지정합니다. 이 개체 내에서 생성된 점수에 대한 자세한 내용은 [집계된 속성 점수](#aggregated-attribution-scores) 섹션을 참조하십시오. |
| touchPoint(개체) | True | 터치포인트 메타데이터를 참조하십시오. 이 개체 내에서 생성된 점수에 대한 자세한 내용은 [집계된 점수](#aggregated-scores) 섹션을 참조하십시오. |

### 원시 점수 경로 보기(UI) {#raw-score-path}

UI에서 원시 점수에 대한 경로를 볼 수 있습니다. 먼저 플랫폼 UI에서 **[!UICONTROL Schemas]**&#x200B;을 선택한 다음 **[!UICONTROL Browse]** 탭 내에서 속성 AI 점수 스키마를 검색하고 선택합니다.

![스키마 선택](./images/input-output/schemas_browse.png)

그런 다음 UI의 **[!UICONTROL Structure]** 창 내에서 필드를 선택합니다. **[!UICONTROL Field properties]** 탭이 열립니다. **[!UICONTROL Field properties]** 내에는 원시 점수에 매핑되는 경로 필드가 있습니다.

![스키마 선택](./images/input-output/field_properties.png)


### 집계된 속성 점수 {#aggregated-attribution-scores}

날짜 범위가 30일 미만인 경우 플랫폼 UI에서 집계된 점수를 CSV 형식으로 다운로드할 수 있습니다.

Attribution AI은 두 가지 속성 점수, 알고리즘 및 규칙 기반 점수를 지원합니다.

Attribution AI은 2가지 유형의 알고리즘 점수, 증분 및 영향을 생성합니다. 영향을 받은 점수는 각 마케팅 접점이 담당하는 전환의 일부입니다. 점수는 마케팅 접점으로 인해 직접적으로 발생할 수 없는 영향의 양입니다. 증분 점수와 영향을 받는 점수 간의 주요 차이점은 증분 점수가 기준 효과를 고려한다는 것입니다. 전환은 단순히 이전 마케팅 접점에 의한 것이라고 간주하지 않습니다.

다음은 Adobe Experience Platform UI에서 Attribution AI 스키마 출력 예를 빠르게 살펴보는 예제입니다.

![](./images/input-output/schema_screenshot.png)

이러한 각 속성 점수에 대한 자세한 내용은 아래 표를 참조하십시오.

| 속성 점수 | 설명 |
| ----- | ----------- |
| 영향(알고리즘) | 영향을 받은 점수는 각 마케팅 접점이 담당하는 전환의 일부입니다. |
| 증분(알고리즘) | 점수는 마케팅 접점으로 인해 직접적으로 발생할 수 없는 영향의 양입니다. |
| 첫 번째 터치 | 전환 경로의 초기 접점에 모든 크레딧을 할당하는 규칙 기반 속성 점수입니다. |
| 마지막 터치 | 전환에 가장 가까운 터치포인트에 모든 크레딧을 할당하는 규칙 기반 속성 점수입니다. |
| 선형 | 전환 경로의 각 접점에 동일한 크레딧을 할당하는 규칙 기반 속성 점수입니다. |
| U자형 | 첫 번째 터치포인트에 크레딧의 40%, 마지막 터치포인트에 크레딧의 40%를 할당하는 규칙 기반 기여도 분석 점수와 나머지 20%를 동일하게 분할하는 다른 터치포인트도 있습니다. |
| 시간 감소 | 전환에 가까운 터치포인트에서 전환으로부터 더 먼 시간에 떨어진 터치포인트보다 더 많은 크레딧을 받는 규칙 기반 기여도 점수입니다. |

**원시 점수 참조(속성 점수)**

아래 표는 속성 점수를 원시 점수에 매핑합니다. 원시 점수를 다운로드하려면 Attribution AI](./download-scores.md) 설명서의 [다운로드 점수를 참조하십시오.

| 속성 점수 | 원시 점수 참조 열 |
| --- | --- |
| 영향(알고리즘) | _tenantID.your_schema_name.element.touchpoint.algorithmicAffinted |
| 증분(알고리즘) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInferred |
| 첫 번째 터치 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 마지막 터치 | _tenantID.your_schema_name.touchpointsDetail.element.touch.lastTouch |
| 선형 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U자형 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| 시간 감소 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decisionUnits |

### 집계된 점수 {#aggregated-scores}

날짜 범위가 30일 미만인 경우 플랫폼 UI에서 집계된 점수를 CSV 형식으로 다운로드할 수 있습니다. 이러한 각 집계 열에 대한 자세한 내용은 아래 표를 참조하십시오.

| 열 이름 | 제한 | Null 허용 | 설명 |
| --- | --- | --- | --- |
| custom_date (DateTime) | 사용자 정의 형식 및 고정 형식 | False | YYYY-MM-DD 형식의 고객 이벤트 날짜.<br> **예**:2016-05-02 |
| mediatouchpoints_date (DateTime) | 사용자 정의 형식 및 고정 형식 | True | 미디어 터치포인트 날짜(YYYY-MM-DD 형식 <br>) **예**:2017-04-21 |
| 세그먼트(문자열) | 계산됨 | False | 모델이 기준이 되는 지역 세그먼테이션과 같은 전환 세그먼트. 세그먼트가 없는 경우 세그먼트는 conversion_scope와 같습니다.<br> **예**:ORDER_AMER |
| conversion_scope(문자열) | 사용자 정의 | False | 사용자가 구성한 전환의 이름입니다.<br> **예**:주문 |
| touchpoint_scope(문자열) | 사용자 정의 | True | <br> 사용자가 구성한 터치포인트의 이름 **예**:PAID_SEARCH_CLICK |
| 제품(문자열) | 사용자 정의 | True | 제품의 XDM 식별자입니다.<br> **예**:CC |
| product_type(문자열) | 사용자 정의 | True | 이 제품 보기에 대해 사용자에게 표시되는 제품의 표시 이름입니다.<br> **예**:노트북 |
| geo(문자열) | 사용자 정의 | True | 전환이 전달된 지리적 위치(placeContext.geo.countryCode) <br> **예**:미국 |
| event_type(문자열) | 사용자 정의 | True | 이 시계열 레코드 <br>에 대한 기본 이벤트 유형 **예**:유료 전환 |
| media_type(문자열) | 열거형 | False | 미디어 유형이 유료, 소유 또는 획득 중 어느 것인지 설명합니다.<br> **예**:유료, 소유 |
| channel(문자열) | 열거형 | False | [!DNL Consumer Experience Event] XDM에서 비슷한 속성을 가진 채널의 가급적 분류를 제공하는 데 사용되는 `channel._type` 속성<br> **예**:검색 |
| action(문자열) | 열거형 | False | `mediaAction` 속성은 경험 이벤트 미디어 작업 유형을 제공하는 데 사용됩니다.<br> **예**:클릭 |
| campaign_group(문자열) | 사용자 정의 | True | 여러 캠페인을 &#39;50%_DISCOUNT&#39;와 같이 함께 그룹화하는 캠페인 그룹의 이름입니다. <br> **예**:기업 |
| campaign_name(문자열) | 사용자 정의 | True | &#39;50%_DISCOUNT_USA&#39; 또는 &#39;50%_DISCOUNT_ASIA&#39;와 같은 마케팅 캠페인을 식별하는 데 사용되는 캠페인 이름입니다. <br> **예**:추수감사절 세일 |

**원시 점수 참조(집계됨)**

아래 표는 집계된 점수를 원시 점수에 매핑합니다. 원시 점수를 다운로드하려면 Attribution AI](./download-scores.md) 설명서의 [다운로드 점수를 참조하십시오. UI 내에서 원시 점수 경로를 보려면 이 문서 내의 [원시 점수 경로 보기](#raw-score-path)를 방문하십시오.

| 열 이름 | 원시 점수 참조 열 |
| --- | --- |
| custom_revents_date | timestamp |
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
| 액션 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |


## 다음 단계 {#next-steps}

데이터를 준비하고 자격 증명과 스키마를 모두 준비했으면 [Attribution AI 사용자 안내서](./user-guide.md)를 따라 시작합니다. 이 안내서에서는 Attribution AI 인스턴스를 만드는 과정을 안내합니다.
