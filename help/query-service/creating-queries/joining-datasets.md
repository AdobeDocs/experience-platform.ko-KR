---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 집합 참여
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 데이터 집합 참여

데이터 세트를 결합하면 쿼리에 다른 데이터 집합의 데이터를 포함할 수 있습니다. 이 예에서는 사용자 지정 운영 체제 데이터 세트를 사용하여 값을 `operatingsystemID` 매핑합니다 `operatingsystem` .

데이터 집합:
- your_analytics_table
- custom_operating_system_lookup

페이지 보기 횟수로 상위 50개 운영 체제에 대한 설명을 `SELECT` 만듭니다.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE _ACP_YEAR=2018 
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![이미지](../images/queries/joining-datasets/select-operating-systems.png)