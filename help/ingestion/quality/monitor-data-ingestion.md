---
keywords: Experience Platform;홈;인기 항목;모니터링;모니터;데이터 흐름;모니터 수집;데이터 수집;데이터 수집;레코드 보기;배치 보기
solution: Experience Platform
title: 데이터 수집 모니터링
topic-legacy: overview
description: 이 사용 안내서에서는 Adobe Experience Platform 사용자 인터페이스 내에서 데이터를 모니터링하는 방법을 제공합니다. 이 안내서를 사용하려면 Adobe ID이 있고 Adobe Experience Platform에 액세스할 수 있어야 합니다.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: 3fadf7006c8ea058e469067b61950ed2d2d12e3f
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 데이터 수집 모니터링

데이터 수집을 사용하면 데이터를 Adobe Experience Platform에 수집할 수 있습니다. 일괄 처리 섭취 를 사용하면 다양한 파일 유형(예: CSV)을 사용하여 데이터를 삽입하거나 스트리밍 수집 기능을 사용하여 실시간으로 데이터를 [!DNL Platform]에 수집할 수 있습니다.

이 사용 안내서에서는 Adobe Experience Platform 사용자 인터페이스 내에서 데이터를 모니터링하는 방법을 제공합니다. 이 안내서를 사용하려면 Adobe ID이 있고 Adobe Experience Platform에 액세스할 수 있어야 합니다.

## 스트리밍 종단 간 데이터 수집 모니터링

[Experience Platform UI](https://platform.adobe.com)의 왼쪽 탐색 메뉴에서 **[!UICONTROL 모니터링]**&#x200B;을 선택하고 **[!UICONTROL 스트리밍 종단간]**&#x200B;을 선택합니다.

**[!UICONTROL 스트리밍 종단 간]** 모니터링 페이지가 나타납니다. 이 작업 공간은 [!DNL Platform]에 의해 수신되는 스트리밍된 이벤트의 비율을 표시하는 그래프, [[!DNL Real-time Customer Profile]](../../profile/home.md)에 의해 성공적으로 처리된 스트리밍된 이벤트의 비율과 들어오는 데이터의 세부 목록을 표시하는 그래프를 제공합니다.

![](../images/quality/monitor-data-flows/list-streams.png)

기본적으로 상단 그래프는 지난 7일 동안의 수집률을 보여줍니다. 강조 표시된 단추를 선택하여 다양한 기간을 표시하도록 이 날짜 범위를 조정할 수 있습니다.

![](../images/quality/monitor-data-flows/events-received.png)

아래 그래프는 지난 7일 동안 [!DNL Profile]에 의해 성공적으로 스트리밍된 이벤트 수를 보여줍니다. 강조 표시된 단추를 선택하여 다양한 기간을 표시하도록 이 날짜 범위를 조정할 수 있습니다.

>[!NOTE]
>
>이 그래프에 데이터를 표시하려면 데이터가 **명시적으로**&#x200B;이(가) [!DNL Profile]에 대해 활성화되어 있어야 합니다. [!DNL Profile]에 대해 스트리밍 데이터를 활성화하는 방법에 대해 알아보려면 [데이터 세트 사용 안내서](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)를 참조하십시오.

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

그래프 아래에는 위에 표시된 날짜 범위에 해당하는 모든 스트리밍 수집 레코드 목록이 있습니다. 나열된 각 배치에는 해당 ID, 데이터 세트 이름, 마지막으로 업데이트되었을 때 배치의 레코드 수 및 오류 수(있는 경우)가 표시됩니다. 해당 레코드에 대한 자세한 정보를 보려면 레코드를 선택할 수 있습니다.

![](../images/quality/monitor-data-flows/streams.png)

### 스트리밍 레코드 보기

성공적으로 스트리밍된 레코드의 세부 정보를 볼 때 수집된 레코드 수, 파일 크기, 수집 시작 및 종료 시간과 같은 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/successful-streaming.png)

실패한 스트리밍 레코드의 세부 정보에 성공한 레코드와 동일한 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/failed-batch.png)

또한 실패한 레코드는 배치를 처리하는 동안 발생한 오류에 대한 세부 정보를 제공합니다. 아래 예에서는 데이터를 변환하거나 유효성을 검사할 때 구문 분석 오류가 발생했습니다.

>[!NOTE]
>
>수집된 행에 오류가 있는 경우, 결과 메시지가 잘못된 XDM을 생성하지 않는 한 이러한 행은 **삭제되지 않습니다.**

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 일괄적으로 엔드 투 엔드 데이터 수집 모니터링

[[!DNL Experience Platform UI]](https://platform.adobe.com)의 왼쪽 탐색 메뉴에서 **[!UICONTROL 모니터링]**&#x200B;을 선택합니다.

이전에 수집된 일괄 처리 목록을 표시하는 **[!UICONTROL 일괄 처리 종료]** 모니터링 페이지가 나타납니다. 해당 레코드에 대한 자세한 정보를 위해 배치를 선택할 수 있습니다.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 배치 보기

성공적인 배치의 세부 사항을 볼 때 수집된 레코드 수, 파일 크기, 수집 시작 및 종료 시간과 같은 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/successful-batch.png)

실패한 배치의 상세내역에는 실패한 레코드 수를 추가하여 성공한 배치와 동일한 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/failed-batch.png)

또한 실패한 배치에서는 배치를 처리하는 동안 발생한 오류에 대한 세부 정보를 제공합니다. 아래 예에는 개인의 최대 ID 수가 있으므로 수집된 일괄 처리에 오류가 발생했습니다.

>[!NOTE]
>
>수집된 행에 오류가 있는 경우, 결과 메시지가 잘못된 XDM을 생성하지 않는 한 이러한 행은 **삭제되지 않습니다.**

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
