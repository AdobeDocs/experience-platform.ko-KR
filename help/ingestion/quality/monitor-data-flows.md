---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 수집 모니터링
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# 데이터 수집 모니터링

데이터 수집 기능을 사용하면 데이터를 Adobe Experience Platform에 인제스트할 수 있습니다. 다양한 파일 형식(예: CSV)을 사용하여 데이터를 삽입할 수 있는 일괄 처리 섭취 또는 스트리밍 끝점을 실시간으로 사용하여 Platform에 데이터를 수집할 수 있는 스트리밍 섭취 중 하나를 사용할 수 있습니다.

이 사용자 안내서에서는 Adobe Experience Platform 사용자 인터페이스 내에서 데이터를 모니터하는 방법에 대한 단계를 제공합니다. 이 안내서에서는 Adobe ID을 사용하고 Adobe Experience Platform에 액세스해야 합니다.

## 스트리밍 엔드 투 엔드 데이터 통합 모니터링

Experience Platform [UI에서](https://platform.adobe.com)왼쪽 탐색 메뉴에서 **모니터링을** 클릭한 다음 **스트리밍 종단간**&#x200B;을 클릭합니다.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Streaming *end-to-end* monitoring 페이지가 나타납니다. 이 작업 공간은 Platform에서 수신되는 스트리밍 이벤트 속도뿐만 아니라 [실시간 고객 프로파일에서](../../profile/home.md)성공적으로 처리된 스트리밍 이벤트의 비율을 표시하는 그래프, 수신 데이터의 세부 목록을 표시하는 그래프를 제공합니다.

![](../images/quality/monitor-data-flows/list-streams.png)

기본적으로 상단 그래프는 지난 7일 동안의 섭취 비율을 보여줍니다. 강조 표시된 단추를 클릭하여 다양한 기간을 표시하도록 이 날짜 범위를 조정할 수 있습니다.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

아래쪽 그래프는 지난 7일 동안 프로필로 성공적으로 스트리밍된 이벤트의 비율을 보여줍니다. 강조 표시된 단추를 클릭하여 다양한 기간을 표시하도록 이 날짜 범위를 조정할 수 있습니다.

>[!NOTE]
>
>데이터가 이 그래프에 표시되려면 데이터가 프로필에 대해 **명시적으로** 활성화되어 있어야 합니다. 프로필에 대한 스트리밍 데이터를 활성화하는 방법에 대해 알아보려면 [데이터 집합 사용자 안내서를 읽어 보십시오](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

그래프 아래에는 위에 표시된 날짜 범위와 일치하는 모든 스트리밍 통합 레코드 목록이 있습니다. 나열된 각 일괄 처리에는 해당 ID, 데이터 세트 이름, 마지막 업데이트 시 일괄 처리에 있는 레코드 수 및 오류 수(있는 경우)가 표시됩니다. 해당 레코드에 대한 자세한 정보를 보려면 레코드를 클릭하면 됩니다.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### 스트리밍 레코드 보기

성공적으로 스트리밍된 레코드의 세부 정보를 볼 때, 인제스트된 레코드 수, 파일 크기, 인제스트 시작 및 종료 시간 등의 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

실패한 스트리밍 레코드의 세부 정보는 성공적인 레코드와 동일한 정보를 표시합니다.

![](../images/quality/monitor-data-flows/failed-batch.png)

또한 실패한 레코드는 배치를 처리하는 동안 발생한 오류에 대한 세부 사항을 제공합니다. 아래 예에서 카탈로그에서 datasetId를 확인하는 동안 시스템 오류가 발생했습니다.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## 일괄적으로 엔드 투 엔드 데이터 수집 모니터링

Experience Platform [UI의](https://platform.adobe.com)왼쪽 탐색 **메뉴에서** 모니터링을 클릭합니다.

![](../images/quality/monitor-data-flows/click-monitoring.png)

이전에 **인제스트한 배치 목록을 표시하는 일괄 처리 엔드 투 엔드** 모니터링 페이지가 나타납니다. 해당 레코드에 대한 자세한 정보를 보려면 배치를 클릭하면 됩니다.

![](../images/quality/monitor-data-flows/list-batches.png)

### 배치 보기

성공적인 일괄 처리에 대한 세부 사항을 볼 때, 인제스트된 레코드 수, 파일 크기, 인제스트 시작 및 종료 시간과 같은 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/successful-batch.png)

실패한 배치의 세부 사항에는 실패한 레코드 수와 함께 성공적인 배치와 동일한 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

또한 실패한 배치에서는 배치를 처리하는 동안 발생한 오류에 대한 세부 정보를 제공합니다. 아래 예에서, 인제스트된 일괄 처리에서 알 수 없는 필드를 사용했기 때문에 오류가 발생했습니다 `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)