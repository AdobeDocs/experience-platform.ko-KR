---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;샘플 쿼리;샘플 쿼리;adobe analytics;home;popular topics;query service;query queries;sample query;adobe analytics
solution: Experience Platform
title: Adobe Analytics 데이터에 대한 샘플 쿼리
topic-legacy: queries
description: 선택한 Adobe Analytics 보고서 세트의 데이터는 XDM ExperienceEvents로 변환되고 데이터 세트로 Adobe Experience Platform으로 수집됩니다. 이 문서에서는 Adobe Experience Platform 쿼리 서비스가 이 데이터를 사용하며 포함된 샘플 쿼리는 Adobe Analytics 데이터 세트에서 사용해야 하는 다양한 사용 사례를 간략하게 설명합니다.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 1%

---

# Adobe Analytics 데이터에 대한 샘플 쿼리

선택한 Adobe Analytics 보고서 세트의 데이터는 [!DNL XDM ExperienceEvent] 클래스를 따르는 데이터로 변환되고 데이터 세트로 Adobe Experience Platform으로 수집됩니다.

이 문서는 Adobe Experience Platform [!DNL Query Service]에서 이 데이터를 사용하는 데 필요한 샘플 쿼리를 포함하여 Adobe Analytics 데이터 세트에서 사용할 수 있는 여러 가지 사용 사례를 요약합니다. [!DNL Experience Events]에 대한 매핑에 대한 자세한 내용은 [분석 필드 매핑](../../sources/connectors/adobe-applications/mapping/analytics.md)의 설명서를 참조하십시오.

## 시작하기

이 문서의 SQL 예제에서는 SQL을 편집하고 평가할 데이터 세트, eVar, 이벤트 또는 시간대를 기반으로 쿼리에 대해 예상되는 매개 변수를 작성해야 합니다. 다음에 나오는 SQL 예제에 `{ }`이 표시될 때마다 매개 변수를 제공합니다.

## 일반적으로 사용되는 SQL 예제

다음 예는 Adobe Analytics 데이터를 분석하기 위해 일반적으로 사용되는 SQL 쿼리를 보여줍니다.

### 지정된 날짜에 대한 시간별 방문자 수

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### 지정된 날짜에 본 페이지 상위 10개

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### 가장 활성화된 사용자 10명

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 사용자 활동별 상위 10개 도시

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 가장 많이 본 제품 10개

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### 총 주문 매출 상위 10개

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {TARGET_TABLE} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### 일별 이벤트 수

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## 머천다이징 변수(제품 구문)


### 제품 구문

Adobe Analytics에서 머천다이징 변수라고 하는 특별히 구성된 변수를 통해 사용자 지정 제품 수준 데이터를 수집할 수 있습니다. eVar 또는 사용자 지정 이벤트를 기반으로 합니다. 이러한 변수와 표준 사용 간의 차이는 해당 히트에 대해 단일 값만 표시하지 않고 히트에서 찾은 각 제품에 대해 별도의 값을 나타낸다는 것입니다.

이러한 변수를 제품 구문 머천다이징 변수라고 합니다. 이를 통해 제품 &quot;할인 금액&quot; 또는 고객의 검색 결과에서 제품의 &quot;페이지에 있는 위치&quot;에 대한 정보 등의 정보를 수집할 수 있습니다.

제품 구문 사용에 대한 자세한 내용은 제품 구문](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax)을 사용하여 eVar 구현에 대한 Adobe Analytics 설명서를 참조하십시오.[

아래 섹션에서는 [!DNL Analytics] 데이터 세트에 있는 머천다이징 변수에 액세스하는 데 필요한 XDM 필드에 대해 간략하게 설명합니다.

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`:액세스하는 배열의 인덱스입니다.
- `evar#`:액세스하는 특정 eVar 변수.

#### 사용자 지정 이벤트

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`:액세스하는 배열의 인덱스입니다.
- `event#`:액세스하는 특정 사용자 지정 이벤트 변수.

#### 샘플 쿼리

다음은 `productListItems`에 있는 첫 번째 제품에 대한 머천다이징 eVar 및 이벤트를 반환하는 샘플 쿼리입니다.

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

다음 쿼리는 `productListItems` 배열을 분해하고 제품당 각 머천다이징 eVar 및 이벤트를 반환합니다. 원래 히트에 대한 관계를 표시하기 위해 `_id` 필드가 포함됩니다. `_id` 값은 데이터 세트에 대한 고유한 기본 키입니다.

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
> 현재 데이터 세트에 없는 필드를 검색하려고 하면 &quot;해당 구조체 필드 없음&quot; 오류가 발생합니다. 오류 메시지에서 반환된 이유를 평가하여 사용 가능한 필드를 식별한 다음 쿼리를 업데이트하고 다시 실행합니다.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 전환 구문

Adobe Analytics에 있는 다른 유형의 머천다이징 변수는 전환 구문입니다. 제품 구문을 사용하면 해당 값이 제품과 동시에 수집되지만, 이 경우 데이터가 동일한 페이지에 있어야 합니다. 제품과 관련된 전환 또는 관심 이벤트가 발생하기 전에 페이지에서 데이터가 발생하는 시나리오도 있습니다. 예를 들어 제품 검색 방법의 사용 사례를 고려하십시오.

1. 전환 구문이 활성화된 머천다이징 eVar6을 &quot;내부 검색:겨울 모자&quot;로 설정하는 &quot;겨울 모자&quot;에 대한 내부 검색을 수행합니다.
2. 사용자가 &quot;와플 비니&quot;를 클릭하고 제품 세부 정보 페이지에 랜딩합니다.\
   a.여기에 착륙하면 &quot;와플 비니&quot; 이벤트가 $12.99에 발생합니다.`Product View`\
   b.`Product View`은(는) 바인딩 이벤트로 구성되므로 이제 &quot;와플 비니&quot; 제품은 &quot;internal search:winter hat&quot;의 eVar6 값에 바인딩됩니다. &quot;와플 비니&quot; 제품을 수집할 때마다 (1) 만료 설정에 도달하거나 (2) 새 eVar6 값이 설정되고 해당 제품에 결합 이벤트가 다시 발생할 때까지 &quot;internal search:winter hat&quot;과 연결됩니다.
3. 사용자가 장바구니에 제품을 추가하여 `Cart Add` 이벤트를 실행합니다.
4. 사용자는 전환 구문이 활성화된 머천다이징 eVar6을 &quot;내부 검색:여름 셔츠&quot;로 설정하는 &quot;여름 셔츠&quot;에 대한 다른 내부 검색을 수행합니다.
5. 사용자가 &quot;sporty t-shirt&quot;를 클릭하고 제품 세부 정보 페이지에 표시합니다.\
   a.여기에 착륙하면 &quot;19.99달러에 스포츠 티셔츠의 `Product View` 이벤트가 발생합니다.\
   b.`Product View` 이벤트는 여전히 바인딩 이벤트로, 이제 &quot;sporty t-shirt&quot; 제품이 &quot;internal search:summer shirt&quot;의 eVar6 값에 바인딩되며 이전 제품 &quot;waffle beanie&quot;는 여전히 &quot;internal search:waffle beanie&quot;의 eVar6 값으로 바인딩됩니다.
6. 사용자가 장바구니에 제품을 추가하여 `Cart Add` 이벤트를 실행합니다.
7. 사용자가 두 제품을 모두 체크 아웃합니다.

보고 시 주문, 매출, 제품 보기 및 장바구니 추가는 eVar6에 대해 보고할 수 있으며 해당 제품의 활동에 맞게 조정됩니다.

| eVar6(제품 검색 방법) | 매출 | 주문 | 제품 보기 | 장바구니 추가 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 내부 검색:여름 셔츠 | 19.99 | 1 | 1 | 1 |
| 내부 검색:겨울 모자 | 12.99 | 1 | 1 | 1 |

전환 구문 사용에 대한 자세한 내용은 전환 구문](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax)을 사용하여 eVar 구현에 대한 Adobe Analytics 설명서를 참조하십시오.[

다음은 [!DNL Analytics] 데이터 세트에 전환 구문을 생성하는 XDM 필드입니다.

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`:액세스하는 특정 eVar 변수.

#### 제품

```console
productListItems[#].sku
```

- `#`:액세스하는 배열의 인덱스입니다.

#### 샘플 쿼리

다음은 제품 보기 이벤트의 특정 제품 및 이벤트 쌍에 값을 바인딩하는 샘플 쿼리입니다.

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

각 제품의 후속 발생 시 바인딩된 값을 유지하는 샘플 쿼리는 다음과 같습니다. 가장 낮은 하위 쿼리는 선언된 바인딩 이벤트의 제품과 값 관계를 설정합니다. 다음 하위 쿼리는 각 제품과 상호 작용한 이후에 해당 바인딩된 값에 대한 속성을 수행합니다. 최상위 수준 선택 항목은 결과를 집계하여 보고를 생성합니다.

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
