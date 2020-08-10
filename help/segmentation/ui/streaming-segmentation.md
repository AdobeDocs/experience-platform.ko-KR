---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 스트리밍 세분화
topic: ui guide
translation-type: tm+mt
source-git-commit: 2adadad855edd01436a6961cc9be3e58e6483732
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# 스트리밍 세분화

>[!NOTE]
>
>다음 문서에서는 UI를 사용하여 스트리밍 세그멘테이션을 사용하는 방법을 설명합니다. API를 사용한 스트리밍 세그멘테이션 사용에 대한 자세한 내용은 [스트리밍 세그멘테이션 API 안내서를 참조하십시오](../api/streaming-segmentation.md).

스트리밍 세그먼테이션을 통해 [!DNL Adobe Experience Platform] 고객은 데이터 풍부함에 주력하면서 거의 실시간으로 세분화할 수 있습니다. 이제 스트리밍 세분화를 통해 데이터가 유입되면 세그먼트 자격 조건 [!DNL Platform]이 높아져 세분화 작업을 예약하고 실행할 필요가 없습니다. 이 기능을 사용하면 이제 데이터가 전달될 때 대부분의 세그먼트 규칙을 평가할 수 [!DNL Platform]있으므로, 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.

## 스트리밍 세그멘테이션 쿼리 유형

>[!NOTE]
>
>스트리밍 세그멘테이션이 작동하려면 조직의 예약된 세그멘테이션을 활성화해야 합니다. 예약된 세그멘테이션 활성화에 대한 자세한 내용은 세그멘테이션 사용자 안내서 [의 스트리밍 세그멘테이션 섹션을 참조하십시오](./overview.md#scheduled-segmentation).

쿼리는 다음 기준을 충족하는 경우 스트리밍 세그멘테이션으로 자동으로 평가됩니다.

| 쿼리 유형 | 세부 사항 | 예 |
| ---------- | ------- | ------- |
| 들어오는 히트 | 시간 제한 없이 들어오는 단일 이벤트를 참조하는 모든 세그먼트 정의 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 상대 시간 창 내의 들어오는 히트 | 지난 7일 **이내에 들어오는 단일 이벤트를 참조하는 모든 세그먼트 정의**. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 프로필 전용 | 프로필 속성만 참조하는 모든 세그먼트 정의 |  |
| 프로필을 참조하는 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하는 세그먼트 정의 및 하나 이상의 프로필 속성. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 상대 시간 창 내의 프로파일을 참조하는 들어오는 히트 | 지난 7일 **이내에 들어오는 단일 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의**. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 프로파일을 참조하는 여러 이벤트 | 지난 24시간 **** 이내에 여러 이벤트를 참조하고 (선택 사항) 하나 이상의 프로필 속성을 포함하는 세그먼트 정의입니다. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

다음 섹션에는 스트리밍 세그멘테이션에 사용할 수 **없는** 세그먼트 정의 예가 나와 있습니다.

| 쿼리 유형 | 세부 사항 | 예 |
| ---------- | ------- | ------- |
| 상대 시간 창 내의 들어오는 히트 | 세그먼트 정의가 **지난 7일 기간 내에** 없는 **들어오는 이벤트를 참조한 경우**. 예를 들어 **지난 2주**&#x200B;이내에 | ![](../images/ui/streaming-segmentation/relative-hit-failure.png) |
| 상대 창 내의 프로파일을 참조하는 들어오는 히트 | 다음 옵션은 스트리밍 세그멘테이션을 지원하지 **않습니다** .<ul><li>**지난 7일 기간** ****&#x200B;내에 들어오는 이벤트</li><li>세그먼트 또는 트레이트를 포함하는 [!DNL Adobe Audience Manager (AAM)] 세그먼트 정의</li></ul> | ![](../images/ui/streaming-segmentation/profile-relative-failure.png) |
| 프로파일을 참조하는 여러 이벤트 | 다음 옵션은 스트리밍 세그멘테이션을 지원하지 **않습니다** .<ul><li>지난 24시간 이내에 **발생하지** 않는 ****&#x200B;이벤트.</li><li>Adobe Audience Manager(AAM) 세그먼트 또는 트레이트를 포함하는 세그먼트 정의입니다.</li></ul> | ![](../images/ui/streaming-segmentation/event-history-failure.png) |
| 다중 엔티티 쿼리 | 다중 엔티티 쿼리는 전체적으로 스트리밍 세그먼테이션에서 **지원되지 않습니다** . |  |

또한 스트리밍 세그먼테이션을 수행할 때 다음과 같은 지침이 적용됩니다.

| 쿼리 유형 | 지침 |
| ---------- | -------- |
| 단일 이벤트 쿼리 | 뒤쪽 창은 **7일로 제한됩니다**. |
| 이벤트 내역이 있는 쿼리 | <ul><li>뒤쪽 창은 **하루로 제한됩니다**.</li><li>이벤트 간에 엄격한 시간 순서 지정 조건이 **있어야** 합니다.</li><li>이벤트 간의 간단한 시간 순서(전과 후)만 허용됩니다.</li><li>개별 이벤트는 무효화할 **수** 없습니다. 하지만 전체 쿼리는 무효화할 **수** 있습니다.</li></ul> |

## 스트리밍 세분화 세그먼트 세부 사항

스트리밍 가능 세그먼트를 만든 후 해당 세그먼트의 세부 사항을 볼 수 있습니다.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

특히 **[!UICONTROL 전체 적격 대상자 크기에]** 대한 세부 사항이 표시됩니다. 작업이 지난 24시간 이내에 실행된 경우 추가된 대상자에 대한 라인 차트 외에 **[!UICONTROL 작업의 전체 적격 대상]** 크기가 표시됩니다. 그렇지 않으면 **[!UICONTROL 시각화 트렌드 라인 외에 총 예상 대상]** 크기가 표시됩니다.

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