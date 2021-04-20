---
keywords: Experience Platform;홈;인기 항목;스트리밍 세그멘테이션;세그멘테이션 서비스;세그멘테이션 서비스;ui guide;
solution: Experience Platform
title: 스트리밍 세그멘테이션 UI 안내서
topic: ui guide
description: Adobe Experience Platform의 스트리밍 세분화를 통해 거의 실시간으로 세분화를 수행하고 데이터 풍부함에 초점을 맞출 수 있습니다. 스트리밍 세분화를 통해 데이터가 Platform(플랫폼)으로 유입되므로 세분화 작업을 예약하고 실행할 필요가 없습니다. 이 기능을 사용하면 이제 데이터가 플랫폼에 전달되면 대부분의 세그먼트 규칙을 평가할 수 있으므로 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
translation-type: tm+mt
source-git-commit: e1ae20412f449c991f53fdd0f095d0c3a6de262c
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 스트리밍 세분화

>[!NOTE]
>
>다음 문서에서는 UI를 사용하여 스트리밍 세그멘테이션을 사용하는 방법을 설명합니다. API를 사용한 스트리밍 세그멘테이션 사용에 대한 자세한 내용은 [스트리밍 세그멘테이션 API 안내서](../api/streaming-segmentation.md)를 참조하십시오.

[!DNL Adobe Experience Platform]의 스트리밍 세그먼테이션을 통해 고객은 데이터 풍부함에 주력하면서 거의 실시간으로 세그먼테이션을 수행할 수 있습니다. 스트리밍 세그먼테이션을 통해 이제 스트리밍 데이터가 [!DNL Platform]에 도달하면 세그먼트 자격이 부여되므로 세그먼테이션 작업을 예약하고 실행할 필요가 없습니다. 이 기능을 사용하면 이제 데이터가 [!DNL Platform]에 전달되므로 대부분의 세그먼트 규칙을 평가할 수 있습니다. 즉, 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.

>[!NOTE]
>
>스트리밍 세그먼테이션은 플랫폼으로 스트리밍된 데이터를 평가하는 데에만 사용할 수 있습니다. 즉, 일괄 처리를 통해 처리된 데이터는 스트리밍 세그멘테이션을 통해 평가되지 않고 야간 예약된 세그먼트 작업과 함께 평가됩니다.
>
>또한 스트리밍 세그멘테이션으로 평가된 세그먼트가 배치 세그멘테이션을 사용하여 평가되는 다른 세그먼트를 기반으로 하는 경우 이상적인 멤버십과 실제 멤버십 간에 이동할 수 있습니다. 예를 들어 세그먼트 A가 세그먼트 B를 기반으로 하고 세그먼트 B가 일괄 세그먼테이션을 사용하여 평가되는 경우 세그먼트 B는 24시간마다 업데이트되므로 세그먼트 B 업데이트와 다시 동기화될 때까지 실제 데이터에서 더 멀리 이동합니다.

## 스트리밍 세그멘테이션 쿼리 유형

>[!NOTE]
>
>스트리밍 세그먼테이션이 작동하려면 조직에 대해 예약된 세그먼테이션을 활성화해야 합니다. 예약된 세그멘테이션 활성화에 대한 자세한 내용은 세그멘테이션 사용자 안내서](./overview.md#scheduled-segmentation)의 [스트리밍 세그멘테이션 섹션을 참조하십시오.

쿼리는 다음 기준을 충족하는 경우 스트리밍 세그먼테이션으로 자동으로 평가됩니다.

| 쿼리 유형 | 세부 사항 | 예 |
| ---------- | ------- | ------- |
| 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하는 모든 세그먼트 정의 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 상대 시간 창 내에서 들어오는 히트 | 단일 들어오는 이벤트를 참조하는 모든 세그먼트 정의 | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 시간 창으로 들어오는 히트 | 시간 창이 있는 단일 들어오는 이벤트를 참조하는 세그먼트 정의입니다. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| 프로필 전용 | 프로필 속성만 참조하는 모든 세그먼트 정의 |  |
| 프로필을 참조하는 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하고 하나 이상의 프로필 속성을 참조하는 세그먼트 정의입니다. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 상대 시간 창 내의 프로파일을 참조하는 들어오는 히트 | 단일 들어오는 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의입니다. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 세그먼트 | 하나 이상의 일괄 처리 또는 스트리밍 세그먼트를 포함하는 모든 세그먼트 정의 | ![](../images/ui/streaming-segmentation/two-batches.png) |
| 프로파일을 참조하는 여러 이벤트 | 지난 24시간 이내에 여러 이벤트 **을 참조하고 (선택 사항) 하나 이상의 프로필 특성이 있는 세그먼트 정의입니다.** | ![](../images/ui/streaming-segmentation/event-history-success.png) |

세그먼트 정의는 다음 시나리오에서 스트리밍 세그먼테이션에 대해 **활성화되지 않습니다.**.

- 세그먼트 정의에는 Adobe Audience Manager(AAM) 세그먼트 또는 트레이트가 포함됩니다.
- 세그먼트 정의에는 여러 엔티티(다중 엔티티 쿼리)가 포함됩니다.

또한 스트리밍 세분화를 수행할 때 다음과 같은 지침이 적용됩니다.

| 쿼리 유형 | 지침 |
| ---------- | -------- |
| 단일 이벤트 쿼리 | 전환 확인 창에는 제한이 없습니다. |
| 이벤트 내역이 있는 쿼리 | <ul><li>조회 창은 **1일**&#x200B;로 제한됩니다.</li><li>이벤트 사이에 엄격한 시간 순서 조건 **이 있어야 합니다**.</li><li>하나 이상의 부정 이벤트가 있는 쿼리가 지원됩니다. 그러나 전체 이벤트 **는 부정일 수 없습니다.**</li></ul> |

세그먼트 정의가 수정되어 더 이상 스트리밍 세그멘테이션의 기준을 충족하지 않을 경우, 세그먼트 정의는 자동으로 &quot;스트리밍&quot;에서 &quot;배치&quot;로 전환됩니다.

## 스트리밍 세분화 세그먼트 세부 사항

스트리밍 가능 세그먼트를 만든 후 해당 세그먼트의 세부 사항을 볼 수 있습니다.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

특히 **[!UICONTROL total qualified audience size]**&#x200B;에 대한 세부 사항이 표시됩니다. **[!UICONTROL Total qualified audience size]**&#x200B;은 마지막으로 완료된 세그먼트 작업 실행의 자격이 있는 총 대상 수를 보여줍니다. 지난 24시간 이내에 세그먼트 작업이 완료되지 않은 경우 대신 예상에서 대상 수를 가져옵니다.

아래에는 지난 24시간 동안 자격이 있고 결격 처리된 세그먼트 수가 표시되는 선 그래프가 있습니다. 드롭다운을 조정하여 지난 24시간, 지난 주 또는 최근 30일을 표시할 수 있습니다.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

정보 버블을 선택하여 마지막 세그먼트 평가에 대한 추가 정보를 찾을 수 있습니다.

![](../images/ui/streaming-segmentation/info-bubble.png)

세그먼트 정의에 대한 자세한 내용은 [세그먼트 정의 세부 사항](#segment-details)의 이전 섹션을 참조하십시오.

## 다음 단계

이 사용 안내서에서는 스트리밍이 활성화된 세그먼트 정의가 Adobe Experience Platform에서 작동하는 방식과 스트리밍이 가능한 세그먼트를 모니터링하는 방법을 설명합니다.

Adobe Experience Platform 사용자 인터페이스 사용에 대한 자세한 내용은 [세그멘테이션 사용자 안내서](./overview.md)를 참조하십시오.
