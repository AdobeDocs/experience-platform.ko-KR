---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: 스트리밍 세분화
topic: ui guide
description: Adobe Experience Platform의 스트리밍 세분화를 통해 거의 실시간으로 데이터를 세분화할 수 있습니다. 이제 스트리밍 세분화를 통해 데이터가 플랫폼에 유입되면 세그먼트 자격이 부여되므로 세분화 작업을 예약하고 실행할 필요가 없습니다. 이 기능을 사용하면 이제 데이터가 플랫폼으로 전달되면 대부분의 세그먼트 규칙을 평가할 수 있습니다. 즉, 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.
translation-type: tm+mt
source-git-commit: 578579438ca1d6a7a8c0a023efe2abd616a6dff2
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---


# 스트리밍 세분화

>[!NOTE]
>
>다음 문서에서는 UI를 사용하여 스트리밍 세그멘테이션을 사용하는 방법을 설명합니다. API를 사용한 스트리밍 세그멘테이션 사용에 대한 자세한 내용은 [스트리밍 세그멘테이션 API 안내서를 참조하십시오](../api/streaming-segmentation.md).

스트리밍 세그먼테이션을 통해 [!DNL Adobe Experience Platform] 고객은 데이터 풍부함에 주력하면서 거의 실시간으로 세분화할 수 있습니다. 스트리밍 세분화를 통해 이제 데이터가 스트리밍되는 즉시 세그먼트 자격 조건 [!DNL Platform]이 충족되므로 세분화 작업을 예약하고 실행할 필요가 없습니다. 이 기능을 사용하면 이제 데이터가 전달될 때 대부분의 세그먼트 규칙을 평가할 수 [!DNL Platform]있으므로, 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.

>[!NOTE]
>
>스트리밍 세그먼테이션은 플랫폼으로 스트리밍되는 데이터를 평가하는 데에만 사용할 수 있습니다. 즉, 일괄 처리를 통해 수집되는 데이터는 스트리밍 세그멘테이션을 통해 평가되지 않으며, 야간 세그먼트화된 작업과 함께 평가됩니다.

## 스트리밍 세그멘테이션 쿼리 유형

>[!NOTE]
>
>스트리밍 세그멘테이션이 작동하려면 조직의 예약된 세그멘테이션을 활성화해야 합니다. 예약된 세그멘테이션 활성화에 대한 자세한 내용은 세그멘테이션 사용자 안내서 [의 스트리밍 세그멘테이션 섹션을 참조하십시오](./overview.md#scheduled-segmentation).

쿼리는 다음 기준을 충족하는 경우 스트리밍 세그멘테이션으로 자동으로 평가됩니다.

| 쿼리 유형 | 세부 사항 | 예 |
| ---------- | ------- | ------- |
| 들어오는 히트 | 시간 제한 없이 들어오는 단일 이벤트를 참조하는 모든 세그먼트 정의 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 상대 시간 창 내의 들어오는 히트 | 단일 들어오는 이벤트를 참조하는 세그먼트 정의입니다. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 프로필 전용 | 프로필 속성만 참조하는 모든 세그먼트 정의 |  |
| 프로필을 참조하는 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하는 세그먼트 정의 및 하나 이상의 프로필 속성. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 상대 시간 창 내의 프로파일을 참조하는 들어오는 히트 | 단일 들어오는 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의입니다. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 프로파일을 참조하는 여러 이벤트 | 지난 24시간 **** 이내에 여러 이벤트를 참조하고 (선택 사항) 하나 이상의 프로필 속성을 포함하는 세그먼트 정의입니다. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

다음 섹션에는 스트리밍 세그멘테이션에 사용할 수 **없는** 세그먼트 정의 예가 나와 있습니다.

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 상대 창 내의 프로파일을 참조하는 들어오는 히트 | 세그먼트 또는 트레이트를 포함하는 [!DNL Adobe Audience Manager (AAM)] 세그먼트 정의 |
| 프로파일을 참조하는 여러 이벤트 | Adobe Audience Manager(AAM) 세그먼트 또는 트레이트를 포함하는 세그먼트 정의입니다. |
| 다중 엔티티 쿼리 | 다중 엔티티 쿼리는 전체적으로 스트리밍 세그먼테이션에서 **지원되지 않습니다** . |

또한 스트리밍 세그먼테이션을 수행할 때 다음과 같은 지침이 적용됩니다.

| 쿼리 유형 | 지침 |
| ---------- | -------- |
| 단일 이벤트 쿼리 | 룩백 창에는 제한이 없습니다. |
| 이벤트 내역이 있는 쿼리 | <ul><li>뒤쪽 창은 **하루로 제한됩니다**.</li><li>이벤트 간에 엄격한 시간 순서 지정 조건이 **있어야** 합니다.</li><li>이벤트 간의 간단한 시간 순서(전과 후)만 허용됩니다.</li><li>개별 이벤트는 무효화할 **수** 없습니다. 하지만 전체 쿼리는 무효화할 **수** 있습니다.</li></ul> |

세그먼트 정의가 수정되어 더 이상 스트리밍 세그멘테이션의 기준을 충족하지 않을 경우 세그먼트 정의가 &quot;스트리밍&quot;에서 &quot;일괄 처리&quot;로 자동 전환됩니다.

## 스트리밍 세분화 세그먼트 세부 사항

스트리밍 가능 세그먼트를 만든 후 해당 세그먼트의 세부 사항을 볼 수 있습니다.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

특히 **[!UICONTROL 전체 적격 대상자 크기에]** 대한 세부 사항이 표시됩니다. 자격이 **[!UICONTROL 있는 총 대상 크기는]** 마지막으로 완료된 세그먼트 작업 실행의 전체 적격 대상 수를 보여줍니다. 지난 24시간 이내에 세그먼트 작업이 완료되지 않은 경우 대신 예상에서 대상 수를 가져옵니다.

아래에는 지난 24시간 동안 자격이 있고 결격 처리된 세그먼트의 수가 표시되는 선 그래프가 표시됩니다. 드롭다운을 조정하여 지난 24시간, 지난 주 또는 지난 30일을 표시할 수 있습니다.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

정보 버블을 선택하여 마지막 세그먼트 평가에 대한 추가 정보를 찾을 수 있습니다.

![](../images/ui/streaming-segmentation/info-bubble.png)

세그먼트 정의에 대한 자세한 내용은 [세그먼트 정의 세부 정보에 대한 이전 섹션을 참조하십시오](#segment-details).

## 스트리밍 세분화 비디오 데모

다음 비디오는 스트리밍 세그멘테이션에 대한 이해를 지원하기 위한 것입니다. 고객 경험의 예를 보여주고 [!DNL Platform] 인터페이스에서 주요 기능을 빠르게 둘러봅니다.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## 다음 단계

이 사용 안내서에서는 Adobe Experience Platform에서 스트리밍이 가능한 세그먼트 정의가 작동하는 방식과 스트리밍이 가능한 세그먼트를 모니터링하는 방법을 설명합니다.

Adobe Experience Platform 사용자 인터페이스 사용에 대한 자세한 내용은 세그멘테이션 사용자 [안내서를 참조하십시오](./overview.md).