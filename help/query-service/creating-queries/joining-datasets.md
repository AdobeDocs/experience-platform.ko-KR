---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: 데이터 집합 참여
topic: queries
type: Tutorial
description: 데이터 세트를 결합하면 쿼리에 다른 데이터 집합의 데이터를 포함할 수 있습니다. 이 예에서는 사용자 지정 운영 체제 데이터 세트를 사용하여 운영 체제 ID를 운영 체제 값에 매핑합니다.
translation-type: tm+mt
source-git-commit: 37356db1666b0c800119b1e254940ad72550848a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 2%

---


# 데이터 집합 참여

데이터 세트를 결합하면 쿼리에 다른 데이터 집합의 데이터를 포함할 수 있습니다. 이 예에서는 사용자 지정 운영 체제 데이터 세트를 사용하여 값을 값 `operatingsystemID` 에 `operatingsystem` 매핑합니다.

데이터 세트:
- your_analytics_table
- custom_operating_system_lookup

페이지 보기 횟수로 상위 50개 운영 체제에 대한 `SELECT` 설명을 만듭니다.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![이미지](../images/queries/joining-datasets/select-operating-systems.png)