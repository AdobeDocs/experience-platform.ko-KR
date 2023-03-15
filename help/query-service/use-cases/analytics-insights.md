---
title: 웹 및 모바일 상호 작용에 대한 Analytics Insights
description: 이 문서에서는 쿼리 서비스를 사용하여 수집된 Adobe Analytics 데이터에서 실행 가능한 통찰력을 만드는 방법을 설명합니다.
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# 웹 및 모바일 상호 작용에 대한 Analytics 통찰력

Adobe Experience Platform에서는 XDM(경험 데이터 모델) 필드를 사용하여 Adobe Analytics 보고서 세트에서 데이터를 수집하여 데이터 세트를 채울 수 있습니다. 이 분석 데이터는 다음 내용에 부합하도록 수정됩니다. [!DNL XDM ExperienceEvent] 클래스. 그런 다음 쿼리 서비스에서 SQL 쿼리를 실행하여 이 데이터를 사용하여 디지털 플랫폼에 대한 사용자 동작으로부터 중요한 통찰력을 생성할 수 있습니다.

이 문서에서는 웹 및 모바일 Analytics 데이터에서 통찰력을 생성할 때 일반적인 사용 사례를 보여 주는 다양한 샘플 SQL 쿼리를 제공합니다.

다음을 참조하십시오. [Analytics 필드 매핑 설명서](../../sources/connectors/adobe-applications/mapping/analytics.md) analytics 데이터 수집 및 매핑에 대한 자세한 내용은 를 참조하십시오.

## 시작하기

다음 각 사용 사례에 대해 사용자 정의할 템플릿으로 매개 변수가 있는 SQL 쿼리 예제가 제공됩니다. 표시되는 모든 위치에 매개 변수를 제공합니다. `{ }` 평가하려는 데이터 세트, eVar, 이벤트 또는 시간대에 대한 SQL 예제.

## 목표

다음 예는 Adobe Analytics 데이터를 분석하는 일반적인 사용 사례에 대한 SQL 쿼리를 보여 줍니다.

### 주어진 날짜에서 매 시간마다 방문자 수 생성

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### 주어진 일에 가장 많이 본 페이지 10개 식별

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### 가장 활동적인 10명의 사용자 식별

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 사용자 활동을 기반으로 가장 원하는 10개 도시를 식별합니다

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 가장 많이 본 10개 제품 식별

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

### 10개의 가장 높은 주문 수익 파악

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
