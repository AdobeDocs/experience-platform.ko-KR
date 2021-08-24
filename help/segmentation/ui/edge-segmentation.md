---
keywords: Experience Platform;홈;인기 항목;에지 세그멘테이션;세그멘테이션 서비스;세그멘테이션 서비스;ui 안내서;스트리밍 에지;
solution: Experience Platform
title: Edge Segmentation UI 안내서
topic-legacy: ui guide
description: Edge Segmentation은 Platform의 세그먼트를 즉시 평가하여 동일한 페이지와 다음 페이지 개인화 사용 사례를 가능하게 하는 기능입니다.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8f2540902cdcff99627393429424dbfe1de2d3da
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 3%

---

# Edge segmentation UI 안내서(베타)

>[!NOTE]
>
>Edge 세그먼테이션은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

Edge Segmentation은 Adobe Experience Platform의 세그먼트를 즉시 평가하여 동일한 페이지와 다음 페이지 개인화 사용 사례를 가능하게 하는 기능입니다.

## 에지 세그멘테이션 쿼리 유형

쿼리는 다음 기준을 충족하는 경우 에지 세그먼테이션으로 평가할 수 있습니다.

| 쿼리 유형 | 세부 사항 | 예 |
| ---------- | ------- | ------- |
| 수신 히트 | 시간 제한 없이 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| 프로필을 참조하는 수신 히트 | 시간 제한 없이 단일 수신 이벤트를 참조하는 모든 세그먼트 정의와 하나 이상의 프로필 속성을 참조합니다. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| 24시간의 시간 창이 있는 수신 히트 | 24시간 이내에 단일 수신 이벤트를 참조하는 모든 세그먼트 정의 |  |
| 24시간의 시간 창이 있는 프로필을 참조하는 수신 히트 | 24시간 이내에 단일 수신 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의 |  |

쿼리가 위의 쿼리 유형과 일치하는 경우 에지 세그멘테이션을 사용하여 자동으로 평가됩니다.

다음 쿼리 유형은 현재 에지 세그먼테이션에 지원되지 않는 **입니다.**

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 여러 이벤트 | 쿼리에 두 개 이상의 이벤트가 포함된 경우 에지 세그멘테이션을 사용하여 평가할 수 없습니다. |
| 빈도 쿼리 | 특정 횟수 이상 발생하는 이벤트를 참조하는 모든 세그먼트 정의입니다. |  |
| 프로필을 참조하는 빈도 쿼리 | 특정 횟수 이상 발생하는 이벤트를 참조하며 하나 이상의 프로필 속성을 갖는 모든 세그먼트 정의입니다. |  |

## 다음 단계

이 사용 안내서에서는 Adobe Experience Platform에서 에지 세그먼테이션을 사용하여 세그먼트를 평가하는 방법을 설명합니다.

Adobe Experience Platform 사용자 인터페이스 사용에 대한 자세한 내용은 [세그먼테이션 사용 안내서](./overview.md)를 참조하십시오. 유사한 작업을 수행하고 Adobe Experience Platform 사용자 인터페이스를 사용하여 세그먼트를 작업하는 방법에 대해 알아보려면 [Edge Segmentation API 안내서](../api/edge-segmentation.md)를 참조하십시오.
