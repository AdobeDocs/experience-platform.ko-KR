---
keywords: Experience Platform;홈;자주 찾는 주제;모니터링;모니터링;데이터 흐름;수집 모니터링;데이터 수집;데이터 수집;데이터 수집;레코드 보기;배치 보기;
solution: Experience Platform
title: 데이터 수집 모니터링
description: 이 사용 안내서는 Adobe Experience Platform 사용자 인터페이스 내에서 데이터를 모니터링하는 방법에 대한 단계를 제공합니다. 이 안내서를 사용하려면 Adobe ID가 있어야 하며 Adobe Experience Platform에 액세스할 수 있어야 합니다.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 4%

---

# 데이터 수집 모니터링하기

데이터 수집을 통해 데이터를 Adobe Experience Platform 에 수집할 수 있습니다. 다양한 파일 형식(예: CSV)을 사용하여 데이터를 삽입할 수 있는 일괄 처리 또는 스트리밍 엔드포인트를 [!DNL Experience Platform] 사용하여 실시간으로 데이터를 수집할 수 있는 스트리밍 수집을 사용할 수 있습니다.

이 사용자 안내서에서는 사용자 인터페이스 내에서 데이터를 모니터 방법에 대한 단계를 제공합니다Adobe Experience Platform. 이 안내서를 사용하려면 Adobe ID가 있어야 하며 Adobe Experience Platform에 액세스할 수 있어야 합니다.

## 엔드투엔드 스트리밍 데이터 수집 모니터링 {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="수집 속도"
>abstract="초당 정상적으로 처리된 이벤트 수입니다."
>text="Learn more in the documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-sources.html?lang=ko" text="UI에서 소스의 데이터 흐름 모니터링"

>[!TIP]
>
>특정 날짜의 총 이벤트를 계산하려면 `total events / day = ingestion rate * 60 * 60 * 24` 식을 사용합니다.

[Experience Platform UI](https://platform.adobe.com)에서 왼쪽 탐색 메뉴을 선택한 다음 **[!UICONTROL Monitoring]**&#x200B;을 선택합니다&#x200B;**[!UICONTROL Streaming end-to-end]**.

**[!UICONTROL Streaming end-to-end]** 모니터링 페이지 가 나타납니다. 이 작업 영역 는 에서 수신 [!DNL Experience Platform]한 스트리밍된 이벤트의 비율을 표시하는 그래프와 에서 성공적으로 처리 [[!DNL Real-Time Customer Profile]](../../profile/home.md)한 스트리밍된 이벤트의 비율을 표시하는 그래프와 수신 데이터의 자세한 목록을 제공합니다.

![](../images/quality/monitor-data-flows/list-streams.png)

기본적으로 위쪽 그래프에는 지난 7일 동안의 수집 속도가 표시됩니다. 강조 표시된 버튼을 선택하여 다양한 기간을 표시하도록 이 날짜 범위를 조정할 수 있습니다.

![](../images/quality/monitor-data-flows/events-received.png)

아래쪽 그래프는 지난 7일 동안 성공적으로 처리된 스트리밍 이벤트의 비율을 [!DNL Profile] 보여줍니다. 강조 표시된 버튼을 선택하여 다양한 기간을 표시하도록 이 날짜 범위를 조정할 수 있습니다.

>[!NOTE]
>
>이 그래프에 데이터를 표시하려면 에 대해 **데이터를 명시적으로** 활성화해야 [!DNL Profile]합니다. 에 대한 [!DNL Profile]스트리밍 데이터를 사용하도록 설정하는 방법을 알아보려면 데이터 세트 사용자 안내서[&#x200B; 를 읽어보세요](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

그래프 아래에는 위에 표시된 날짜 범위 에 해당하는 모든 스트리밍 수집 레코드 목록이 있습니다. 나열된 각 배치는 마지막으로 업데이트한 경우 해당 ID, 데이터 세트 이름, 배치의 레코드 수 및 오류 수(있는 경우)를 표시합니다. 레코드에 대한 자세한 내용을 보려면 레코드를 선택할 수 있습니다.

![](../images/quality/monitor-data-flows/streams.png)

### 스트리밍 레코드 보기

성공적으로 스트리밍된 레코드의 세부 정보를 볼 때 수집된 레코드 수, 파일 크기, 수집 시작 및 종료 시간 등의 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/successful-streaming.png)

실패한 스트리밍 레코드의 세부 정보에는 성공한 레코드와 동일한 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/failed-batch.png)

또한 실패한 레코드는 일괄 처리를 처리하는 동안 발생한 오류에 대한 세부 정보를 제공합니다. 아래 예에서는 데이터를 변환하거나 유효성을 검사할 때 구문 분석 오류가 발생했습니다.

>[!NOTE]
>
>수집된 행에 오류가 있는 경우 결과 메시지로 인해 잘못된 XDM이 발생하지 않는 한 이러한 행은 **삭제되지 않습니다** .

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 일괄 처리 엔드투엔드 데이터 수집 모니터링

[[!DNL Experience Platform UI]](https://platform.adobe.com)에서 왼쪽 탐색 메뉴를 선택합니다&#x200B;**[!UICONTROL Monitoring]**.

**[!UICONTROL Batch end-to-end]** 모니터링 페이지 가 나타나고 이전에 수집된 배치 목록이 표시됩니다. 배치를 선택하여 해당 레코드에 대한 자세한 정보를 확인할 수 있습니다.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 배치 보기

성공적인 배치의 세부 정보를 볼 때 수집된 레코드 수, 파일 크기, 수집 시작 및 종료 시간 등의 정보가 표시됩니다.

![](../images/quality/monitor-data-flows/successful-batch.png)

실패한 배치의 상세내역은 실패한 배치 수와 동일한 정보를 표시하며 실패한 레코드 수를 추가합니다.

![](../images/quality/monitor-data-flows/failed-batch.png)

또한 실패한 배치는 배치를 처리하는 동안 발생한 오류에 대한 세부 정보를 제공합니다. 아래 예에는 개인의 최대 ID 수가 있으므로 수집된 배치에 오류가 있습니다.

>[!NOTE]
>
>수집된 행에 오류가 있는 경우 결과 메시지로 인해 잘못된 XDM이 발생하지 않는 한 이러한 행은 **삭제되지 않습니다** .

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
