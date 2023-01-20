---
title: Analytics 데이터의 머천다이징 변수 반환 및 사용
description: Analytics 데이터 세트의 머천다이징 변수에 액세스하기 위해 XDM 필드 및 샘플 쿼리를 제공하는 방법을 알아봅니다.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# 분석 데이터의 머천다이징 변수 반환 및 사용

Query Service를 사용하여 Adobe Analytics에서 데이터 세트로 Adobe Experience Platform에 수집한 데이터를 관리합니다. 다음 섹션에서는 Analytics 데이터 세트의 머천다이징 변수에 액세스하는 데 사용할 수 있는 샘플 쿼리를 제공합니다. 자세한 내용은 설명서 를 참조하십시오 [Adobe Analytics 데이터를 수집 및 매핑하는 방법](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=ko-KR) Analytics 소스

## 머천다이징 변수 {#merchandising-variables}

머천다이징 변수는 다음 두 구문 중 하나를 따를 수 있습니다.

* **제품 구문**: eVar 값을 제품에 연결합니다. 
* **전환 변수 구문**: 결합 이벤트가 발생하는 경우에만 eVar을 제품과 연결합니다. 바인딩 이벤트처럼 동작하는 이벤트를 선택할 수 있습니다.

## 제품 구문 {#product-syntax}

Adobe Analytics에서 머천다이징 변수라고 특별히 구성된 변수를 통해 사용자 지정 제품 수준 데이터를 수집할 수 있습니다. 이는 eVar 또는 사용자 지정 이벤트를 기반으로 합니다. 이러한 변수와 일반적인 사용 방식의 차이점은 히트에 대한 단일 값만 아니라 히트에 있는 각 제품에 대해 별도의 값을 나타낸다는 것입니다.

이러한 변수를 제품 구문 머천다이징 변수라고 합니다. 이를 통해 제품 당 &quot;할인 금액&quot; 또는 고객 검색 결과에 있는 제품의 &quot;페이지 위치&quot;에 대한 정보와 같은 정보를 수집할 수 있습니다.

제품 구문 사용에 대한 자세한 내용은 다음 문서를 참조하십시오. Adobe Analytics [제품 구문을 사용하여 eVar 구현](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

아래 섹션에서는 의 머천다이징 변수에 액세스하는 데 필요한 XDM 필드에 대해 간략하게 설명합니다 [!DNL Analytics] 데이터 세트:

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: 액세스하는 배열의 색인입니다.
* `evar#`: 액세스하는 특정 eVar 변수입니다.

### 사용자 정의 이벤트

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: 액세스하는 배열의 색인입니다.
* `event#`: 액세스하는 특정 사용자 지정 이벤트 변수입니다.

## 제품 구문 사용 사례 {#product-use-cases}

다음 사용 사례는 머천다이징 eVar을 `productListItems` SQL을 사용하는 배열입니다.

### 머천다이징 eVar 및 이벤트 반환

아래 쿼리는 의 첫 번째 제품에 대한 머천다이징 eVar 및 이벤트를 반환합니다. `productListItems` 배열입니다.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

### productListItems 배열을 확장하고 각 제품에 대한 머천다이징 eVar 및 이벤트를 반환합니다.

다음 쿼리는 `productListItems` 를 배열하고 각 머천다이징 eVar 및 제품별 이벤트를 반환합니다. 다음 `_id` 원래 히트에 대한 관계를 보여주는 필드가 포함되어 있습니다. 다음 `_id` 값은 데이터 세트에 대한 고유한 기본 키입니다.

>[!NOTE]
>
>분해 함수는 배열 요소를 여러 행으로 구분합니다. null 값은 제외합니다.

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> 현재 데이터 세트에 없는 필드를 검색하려고 하면 &quot;해당 구조체 필드 없음&quot; 오류가 발생합니다. 오류 메시지에서 반환되는 이유를 평가하여 사용 가능한 필드를 식별한 다음 쿼리를 업데이트하고 다시 실행합니다.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 전환 변수 구문 {#conversion-variable-syntax}

Adobe Analytics에 있는 다른 유형의 머천다이징 변수는 전환 변수 구문입니다. products 변수에서 eVar 값을 설정할 수 없을 때 전환 변수 구문이 사용됩니다. 이 시나리오는 일반적으로 페이지에 머천다이징 채널 또는 검색 방법 컨텍스트가 없음을 의미합니다. 이 경우 사용자가 제품 페이지에 도착하기 전에 머천다이징 변수를 설정해야 하며 값은 결합 이벤트가 발생할 때까지 지속됩니다.

예를 들어, 아래 제품 검색 시나리오는 제품과 관련된 전환 또는 이벤트가 발생하기 전에 페이지에 필요한 데이터를 표시할 수 있는 방법을 보여줍니다.

1. 사용자가 &quot;winter hat&quot;에 대해 내부 검색을 수행하여 변환 구문을 활성화한 머천다이징 eVar6을 &quot;internal search:winter hat&quot;로 설정합니다.
2. 사용자가 &quot;와플 비니&quot;를 클릭하고 제품 세부 사항 페이지에 도달합니다.\
   a. 여기에 착륙하면 `Product View` &#39;와플 비니&#39; 이벤트 12.99달러\
   나. 이후 `Product View` 가 결합 이벤트로 구성되면 제품 &quot;waffle beanie&quot;가 이제 &quot;internal search:winter hat&quot;이라는 eVar6 값에 연결됩니다. &quot;와플 비니&quot; 제품이 수집되면 &quot;내부 검색:겨울 모자&quot;와 연관된다. 이 문제는 eVar 만료 설정에 도달하거나, 새 eVar6 값이 설정되고, 해당 제품과 함께 결합 이벤트가 다시 발생할 때까지 발생합니다.
3. 사용자가 장바구니에 제품을 추가하여 `Cart Add` 이벤트.
4. 사용자는 전환 구문이 활성화된 머천다이징 eVar6을 &quot;내부 검색:섬머 셔츠&quot;로 설정하는 &quot;여름 셔츠&quot;에 대한 다른 내부 검색을 수행합니다.
5. 사용자가 &quot;스포츠 티셔츠&quot;를 선택하고 제품 세부 사항 페이지에 도달합니다.\
   a. 여기에 착륙하면 `Product View` &quot;스포츠 티셔츠 $19.99에 행사.\
   나. 로서의 `Product View` 이벤트가 결합 이벤트인 경우, 제품 &quot;sporty t-shirts&quot;가 이제 &quot;internal search:summer shirt&quot;의 eVar6 값에 바인딩됩니다. 이전 제품 &quot;와플 비니&quot;는 여전히 &quot;internal search:wflf beanie&quot;라는 eVar6 값에 결합되어 있습니다.
6. 사용자가 장바구니에 제품을 추가하여 `Cart Add` 이벤트.
7. 사용자가 두 제품을 모두 체크 아웃합니다.

보고 시 주문, 매출, 제품 보기 및 장바구니 추가는 eVar6에 대해 보고할 수 있으며 바운드된 제품의 활동에 일치합니다.

| eVar6(제품 검색 방법) | 매출 | 주문 | 제품 보기 | 장바구니 추가 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 내부 검색:여름 셔츠 | 19.99 | 1 | 1 | 1 |
| 내부 검색:winter hat | 12.99 | 1 | 1 | 1 |

전환 변수 구문을 사용하는 방법에 대한 자세한 내용은 Adobe Analytics 설명서를 참조하십시오. [전환 변수 구문을 사용하여 eVar 구현](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

아래에 표시되는 는 XDM 필드에서 전환 변수 구문을 생성하는 것입니다 [!DNL Analytics] 데이터 세트:

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: 액세스하는 특정 eVar 변수입니다.

#### 제품

```console
productListItems[#].sku
```

* `#`: 액세스하는 배열의 색인입니다.

## 전환 변수는 사례를 사용합니다 {#conversion-variable-use-cases}

아래 사용 사례는 전환 변수 구문이 필요한 시나리오를 반영합니다.

### 특정 제품 및 이벤트 쌍에 값을 바인딩합니다

아래 쿼리는 값을 특정 제품 및 이벤트 쌍에 바인딩합니다. 이 예에서 값은 제품 보기 이벤트에 바인딩됩니다.

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

### 각 제품의 후속 발생 시 바인딩된 값을 유지합니다

아래의 샘플 쿼리는 각 제품의 후속 발생 시 바인딩된 값을 유지합니다. 가장 낮은 하위 쿼리는 선언된 바인딩 이벤트의 제품과의 값 관계를 설정합니다. 다음 하위 쿼리는 각 제품과 후속 상호 작용에서 해당 바인딩된 값의 속성을 수행합니다. 최상위 SELECT는 결과를 집계하여 보고를 생성합니다.

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```

## 다음 단계

이 문서를 읽은 후에는 제품 구문을 사용하여 머천다이징 eVar을 반환하고 전환 변수 구문을 사용하여 특정 제품에 값을 바인딩하는 방법을 더 잘 이해할 수 있어야 합니다.

아직 읽지 않았다면 다음을 읽어야 합니다 [웹 및 모바일 상호 작용 설명서에 대한 Analytics 인사이트](./analytics-insights.md) 다음. 일반적인 사용 사례를 제공하고 Query Service를 사용하여 웹 및 모바일 Adobe Analytics 데이터를 통해 실행 가능한 통찰력을 만드는 방법을 보여줍니다.
