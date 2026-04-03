---
title: 에지 세분화 모니터링
description: 모니터링 대시보드를 사용하여 에지 세분화 처리량을 관찰하는 방법을 알아봅니다.
exl-id: 7abba7e8-1f2d-4a21-a93f-8bda7aa4d849
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---

# 에지 세분화 모니터링

Adobe Experience Platform UI의 모니터링 대시보드를 사용하여 조직 내에서 에지 세분화를 실시간으로 모니터링할 수 있습니다. 이 기능을 사용하여 Edge 데이터의 처리량에 대한 투명도를 높입니다.

## 시작

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [데이터스트림](../../datastreams/overview.md): 데이터스트림을 사용하면 Experience Platform Edge Network을 데이터 세트에 연결할 수 있습니다.
* [기능](../../landing/license-usage-and-guardrails/capacity.md): Experience Platform에서 기능은 조직이 보호 기능을 초과했는지 여부를 알려주고 이러한 문제를 해결하는 방법에 대한 정보를 제공합니다.
* [Edge 세그멘테이션](../../segmentation/methods/edge-segmentation.md): Edge 세그멘테이션은 Adobe Experience Platform의 세그먼트 정의를 즉시 [엣지에서](../../landing/edge-and-hub-comparison.md)평가하는 기능으로, 동일한 페이지와 다음 페이지 개인화 사용 사례를 활성화합니다.

## 액세스 {#access}

에지 세분화 처리량에 대한 모니터링 대시보드에 액세스하려면 **[!UICONTROL Monitoring]** 섹션 내에서 **[!UICONTROL Data management]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Edge]**&#x200B;을(를) 선택하십시오.

![모니터 에지 세분화 대시보드에 액세스하는 메서드가 강조 표시되어 있습니다.](/help/dataflows/assets/ui/monitor-edge/access.png)

모니터링 대시보드가 나타납니다. 이것은 에지 스트리밍 처리량에 대한 모니터링 지표, 에지 스트리밍 처리량을 표시하는 그래프 및 데이터스트림 보기를 보여 줍니다. 이러한 지표는 서비스, 에지 및 날짜별로 필터링할 수 있습니다.

![모니터링 대시보드의 필터링 옵션이 강조 표시됩니다.](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>**을(를) 선택하면**&#x200B;전용[!UICONTROL Edge segmentation throughput]의 데이터 스트림 보기를 볼 수 있습니다.

서비스로 필터링하면 처리량 정보를 보려는 서비스를 선택할 수 있습니다. 여기에는 Edge 세그멘테이션, 데이터 수집, Target, Adobe Journey Optimizer, Offer Decisioning, 사용자 지정 개인화된 대상, 이벤트 전달, Adobe Analytics 및 Adobe Audience Manager과 같은 서비스가 포함됩니다.

가장자리로 필터링하면 정보를 보려는 가장자리를 선택할 수 있습니다. 지원되는 가장자리에는 미국 동부 해안, 미국 서부 해안, 유럽, 인도, 싱가포르, 호주, 일본 및 스위스가 포함됩니다. 여러 모서리를 선택하여 한 번에 볼 수 있습니다.

날짜별로 필터링하는 경우 이벤트를 필터링할 날짜 범위를 선택할 수 있습니다. 이 시간표는 최대 30일로 설정할 수 있습니다. 또는 미리 구성된 시간 범위 [!UICONTROL Last 6 hours], [!UICONTROL Last 12 hours], [!UICONTROL Last 24 hours], [!UICONTROL Last 7 days] 및 [!UICONTROL Last 30 days] 중 하나를 사용할 수 있습니다.

## 에지 처리량에 대한 지표 모니터링

지표 테이블은 선택한 서비스의 에지 처리량에 대한 정보를 제공합니다. 각 열에 대한 자세한 내용은 다음 표를 참조하십시오.

| 지표 | 설명 |
| ------ | ----------- |
| 요청 수신됨 | 일정 기간 내 선택한 에지에서 받은 요청 수입니다. |
| 최대 처리량 | 일정 기간 동안 선택한 에지에서 받은 요청의 가장 높은 비율입니다. |

{style="table-layout:auto"}

## 에지 세그멘테이션 처리량에 대한 그래프 모니터링

모니터링 그래프는 허용된 최대 용량과 비교하여 할당된 기간 내에 선택한 에지가 받은 초당 레코드를 보여 줍니다.

![에지 세분화 처리량 그래프가 표시됩니다.](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## 데이터 스트림 보기

>[!NOTE]
>
>Edge 세그멘테이션 처리량을 필터링하는 경우 데이터 스트림 보기를 **만**&#x200B;사용할 수 있습니다.

데이터 스트림 보기 섹션에는 샌드박스 가장자리를 통과한 최신 데이터 스트림 목록이 표시됩니다.

![나열된 데이터 스트림에 대한 정보를 표시하는 데이터 스트림 보기가 표시됩니다.](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| 필드 | 설명 |
| ----- | ----------- |
| 데이터 스트림 이름 | 데이터 스트림의 이름. |
| 데이터 세트 | 데이터 스트림이 속한 데이터 세트의 이름입니다. |
| 서비스 활성화됨 | 데이터 스트림이 사용되는 서비스의 이름입니다. |
| 요청 | 데이터 스트림을 통과한 요청 수입니다. |
| 최대 처리량 | 데이터 스트림을 통과한 요청의 가장 높은 비율입니다. |
