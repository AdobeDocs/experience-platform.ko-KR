---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;experienceevent 쿼리;experienceevent 쿼리;Experience Event 쿼리;
title: 사용자의 페이지 보기 나열
description: Experience Events를 사용하여 지정된 사용자가 사용한 마지막 100페이지 목록을 만드는 쿼리를 작성하는 방법을 알아봅니다.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# 사용자의 페이지 보기 나열

이 문서에서는 지정된 사용자가 페이지 보기를 나열하는 데 필요한 SQL의 예를 제공합니다. Adobe Experience Platform 쿼리 서비스를 사용하여 [!DNL Experience Events] 다양한 사용 사례를 캡처합니다. 경험 이벤트는 사용자가 웹 사이트 또는 서비스와 상호 작용할 때 시스템의 변경할 수 없고 집계되지 않은 스냅샷을 캡처하는 XDM(Experience Data Model) ExperienceEvent 클래스로 표시됩니다. 경험 이벤트는 시간 도메인 분석에 사용할 수도 있습니다. 자세한 내용은 [다음 단계 섹션](#next-steps) 를 참조하십시오. [!DNL Experience Events] 방문자 보고서를 생성합니다.

XDM 및 [!DNL Experience Events] 은 [[!DNL XDM System] 개요](../../xdm/home.md). 쿼리 서비스를 [!DNL Experience Events]를 사용하면 사용자 간의 행동 트렌드를 효과적으로 추적할 수 있습니다. 다음 문서에서는 [!DNL Experience Events].

## 목표

다음 예제에서는 지정된 사용자가 본 마지막 100페이지를 나열합니다.

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

이 쿼리의 결과는 아래에 볼 수 있습니다.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 [!DNL Experience Events] 페이지 보기를 지정된 사용자로 나열하려면 다음을 수행하십시오.

다른 방문자 기반 사용 사례에 대해 알아보려면 다음 사용 사례를 참조하십시오.

- [페이지 보기 수로 구성된 방문자 목록을 검색합니다.](./visitors-by-number-of-page-views.md)
- [방문자의 롤업 보고서를 봅니다.](./roll-up-report-of-a-visitor.md)
- [일별 이벤트의 트렌드 보고서를 만듭니다.](./trended-report-of-events.md)