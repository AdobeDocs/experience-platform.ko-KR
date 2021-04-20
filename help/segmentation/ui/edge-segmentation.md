---
keywords: Experience Platform;홈;인기 항목;에지 세그멘테이션;세그멘테이션 서비스;세그멘테이션 서비스;ui 안내서;스트리밍 가장자리
solution: Experience Platform
title: Edge 세그멘테이션 UI 안내서
topic: ui guide
description: Edge Segmentation은 Platform에서 세그먼트를 즉시 평가하여 동일한 페이지와 다음 페이지 개인화 사용 사례를 활성화하는 기능입니다.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
translation-type: tm+mt
source-git-commit: 36169a42c7f6a73ca9cc165cd338d6a1cf245bfc
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 4%

---

# Edge 세그멘테이션 UI 안내서(베타)

>[!NOTE]
>
>에지 세그먼테이션은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

Edge Segmentation은 Adobe Experience Platform에서 세그먼트를 바로 에지 시 평가하는 기능으로, 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화합니다.

## 에지 세그멘테이션 쿼리 유형

쿼리는 다음 기준을 충족하는 경우 가장자리 세그먼테이션으로 평가할 수 있습니다.

| 쿼리 유형 | 세부 사항 | 예 |
| ---------- | ------- | ------- |
| 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하는 모든 세그먼트 정의 | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| 프로필을 참조하는 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하고 하나 이상의 프로필 속성을 참조하는 세그먼트 정의입니다. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| 주파수 쿼리 | 이벤트를 참조하는 세그먼트 정의 중 적어도 일정 횟수만큼 발생하는 모든 세그먼트 정의입니다. |  |
| 프로필을 참조하는 빈도 쿼리 | 이벤트를 참조하는 세그먼트 정의에는 적어도 일정 횟수만큼 발생하며 하나 이상의 프로필 속성이 있습니다. |  |

쿼리가 위의 쿼리 유형과 일치하는 경우 **[!UICONTROL Evaluate as streaming segment on the edge]** 토글을 켜서 가장자리 세그멘테이션에 사용할 수 있습니다.

![](../images/ui/edge-segmentation/mark-on-edge.png)

다음 쿼리 유형은 현재 가장자리 세그멘테이션에 지원되지 **않습니다.**:

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 상대 시간 창 | 쿼리가 시간 창을 참조하면 가장자리 세그멘테이션을 사용하여 평가할 수 없습니다. |
| 부정 | 쿼리에 부정적인 부분이 있으면 가장자리 세그멘테이션을 사용하여 평가할 수 없습니다. |
| 여러 이벤트 | 쿼리에 이벤트가 두 개 이상 있으면 에지 세그멘테이션을 사용하여 평가할 수 없습니다. |

## 다음 단계

이 사용 안내서에서는 Adobe Experience Platform에서 가장자리 세그먼테이션으로 세그먼트를 평가하는 방법을 설명합니다.

Adobe Experience Platform 사용자 인터페이스 사용에 대한 자세한 내용은 [세그멘테이션 사용자 안내서](./overview.md)를 참조하십시오. 유사한 작업을 수행하고 Adobe Experience Platform 사용자 인터페이스를 사용하여 세그먼트를 작업하는 방법에 대해 알아보려면 [edge 세그멘테이션 API 안내서](../api/edge-segmentation.md)를 방문하십시오.
