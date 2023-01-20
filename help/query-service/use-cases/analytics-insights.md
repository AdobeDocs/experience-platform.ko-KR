---
title: 웹 및 모바일 상호 작용에 대한 Analytics Insights
description: 이 문서에서는 Query Service를 사용하여 수집된 Adobe Analytics 데이터에서 실행 가능한 통찰력을 만드는 방법을 설명합니다.
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# 웹 및 모바일 상호 작용에 대한 Analytics 통찰력

Adobe Experience Platform을 사용하면 XDM(Experience Data Model) 필드를 사용하여 Adobe Analytics 보고서 세트에서 데이터를 수집하여 데이터 세트를 채울 수 있습니다. 이 분석 데이터는 [!DNL XDM ExperienceEvent] 클래스 이름을 지정합니다. 그런 다음 Query Service는 SQL 쿼리를 실행하여 디지털 플랫폼에 대한 사용자의 동작에서 중요한 통찰력을 생성하여 이 데이터를 사용할 수 있습니다.

이 문서에서는 웹 및 모바일 Analytics 데이터를 통해 통찰력을 만들 때 일반적인 사용 사례를 보여주는 다양한 샘플 SQL 쿼리를 제공합니다.

자세한 내용은 [Analytics 필드 매핑 설명서](../../sources/connectors/adobe-applications/mapping/analytics.md) analytics 데이터 수집 및 매핑에 대한 자세한 정보.

## 시작하기

다음 각 사용 사례에 대해 매개 변수가 있는 SQL 쿼리 예는 사용자 정의할 수 있는 템플릿으로 제공됩니다. 표시되는 곳에 매개 변수를 제공합니다. `{ }` 을 참조하십시오.

## 목표

다음 예제에서는 Adobe Analytics 데이터를 분석하는 일반적인 사용 사례에 대한 SQL 쿼리를 보여줍니다.

### 지정된 날짜에 매시간 방문자 수를 생성합니다

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### 지정된 날짜에 가장 많이 본 페이지 10개를 식별합니다

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### 10명의 가장 활성 상태의 사용자 식별

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 사용자 활동을 기반으로 가장 원하는 10개의 도시를 식별합니다

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 가장 많이 본 10개의 제품 식별

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

### 10개의 가장 높은 주문 매출 파악

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
