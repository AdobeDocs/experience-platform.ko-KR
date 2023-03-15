---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;experienceevent 쿼리;experienceevent 쿼리;경험 이벤트 쿼리;
title: 페이지 보기 횟수별 방문자 나열
description: 경험 이벤트를 사용하여 페이지 보기 수로 구성된 방문자 목록을 검색하는 쿼리를 작성하는 방법을 알아봅니다.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 페이지 보기 횟수별 방문자 나열

이 문서에서는 페이지 보기 수로 구성된 방문자 목록을 검색하는 데 필요한 SQL의 예를 제공합니다. Adobe Experience Platform 쿼리 서비스를 사용하면 다음을 사용하는 쿼리를 작성할 수 있습니다. [!DNL Experience Events] 다양한 사용 사례를 캡처합니다. 경험 이벤트는 사용자가 웹 사이트 또는 서비스와 상호 작용할 때 시스템의 변경할 수 없는 비집계 스냅샷을 캡처하는 XDM(Experience Data Model) ExperienceEvent 클래스로 표시됩니다. 경험 이벤트는 시간 도메인 분석에 사용할 수도 있습니다. 다음을 참조하십시오. [다음 단계 섹션](#next-steps) 다음을 포함하는 더 많은 사용 사례 [!DNL Experience Events] 방문자 보고서를 생성합니다.

XDM에 대한 추가 정보 및 [!DNL Experience Events] 에서 찾을 수 있음 [[!DNL XDM System] 개요](../../xdm/home.md). 쿼리 서비스를 와 결합 [!DNL Experience Events], 사용자 간의 행동 트렌드를 효과적으로 추적할 수 있습니다. 다음 문서에서는 다음과 같은 쿼리의 예를 제공합니다. [!DNL Experience Events].

## 목표

다음 예제에서는 가장 많은 페이지를 본 사용자의 ID 10개를 나열하는 보고서를 만듭니다.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

쿼리 결과는 아래 표에 표시됩니다.

```console
               id                  | pageViews
-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## 다음 단계 {#next-steps}

이 문서를 읽으면 쿼리 서비스를 사용하는 방법을 더 잘 이해할 수 있습니다 [!DNL Experience Events] 를 클릭하여 가장 많은 페이지를 본 사용자를 나열합니다.

다른 방문자 기반 사용 사례에 대해 알려면 다음 사용 사례를 참조하십시오.

- [방문자의 이전 세션을 나열합니다.](./list-visitor-sessions.md)
- [방문자의 롤업 보고서를 봅니다.](./roll-up-report-of-a-visitor.md)
- [일별 이벤트의 트렌드 보고서를 만듭니다.](./trended-report-of-events.md)
