---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;experienceevent 쿼리;experienceevent 쿼리;경험 이벤트 쿼리;
title: 특정 방문자에 대한 롤업 보고서 보기
description: 다음 문서에서는 Adobe Experience Platform 쿼리 서비스의 Experience 이벤트와 관련된 쿼리의 예를 제공합니다.
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# 특정 방문자에 대한 롤업 보고서 보기

이 문서에서는 특정 사용자에 대한 여러 분석 속성에서 데이터를 집계하고 해당 데이터를 하나의 보고서에 함께 확인하는 SQL 예제를 제공합니다. Adobe Experience Platform 쿼리 서비스를 사용하면 [!DNL Experience Events]을(를) 사용하는 쿼리를 작성하여 다양한 사용 사례를 캡처할 수 있습니다. 경험 이벤트는 사용자가 웹 사이트 또는 서비스와 상호 작용할 때 시스템의 변경할 수 없는 비집계 스냅샷을 캡처하는 XDM(Experience Data Model) ExperienceEvent 클래스로 표시됩니다. 경험 이벤트는 시간 도메인 분석에 사용할 수도 있습니다. 방문자 보고서를 생성하는 데 [!DNL Experience Events]이(가) 포함된 사용 사례는 [다음 단계 섹션](#next-steps)을 참조하세요.

XDM 및 [!DNL Experience Events]에 대한 자세한 내용은 [[!DNL XDM System] 개요](../../xdm/home.md)를 참조하세요. 쿼리 서비스를 [!DNL Experience Events]과(와) 결합하여 사용자 간의 동작 트렌드를 효과적으로 추적할 수 있습니다. 다음 문서에서는 [!DNL Experience Events]과(와) 관련된 쿼리의 예를 제공합니다.

## 목표

다음 SQL 예는 지정된 사용자에 대한 다양한 분석 값의 집계 보고서를 보는 방법을 보여 줍니다.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews, 
SUM(_experience.analytics.event1to100.event1.value) as A, 
SUM(_experience.analytics.event1to100.event2.value) as B, 
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

쿼리 결과는 아래 표에 표시됩니다.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## 다음 단계 {#next-steps}

이 문서를 읽으면 [!DNL Experience Events]과(와) 함께 쿼리 서비스를 사용하여 지정된 사용자에 대한 분석 값의 집계 보고서를 보는 방법에 대해 더 잘 이해할 수 있습니다.

다른 방문자 기반 사용 사례에 대해 알려면 다음 사용 사례를 참조하십시오.

- [페이지 보기 횟수별로 구성된 방문자 목록을 검색합니다.](./visitors-by-number-of-page-views.md)
- [방문자의 이전 세션을 나열합니다.](./list-visitor-sessions.md)
- [일별 이벤트의 트렌드 보고서를 만듭니다.](./trended-report-of-events.md)
