---
keywords: Experience Platform;프로파일;실시간 고객 프로파일;사용자 인터페이스;사용자 정의;프로파일 대시보드;대시보드
title: 대상 대시보드
description: Adobe Experience Platform은 조직의 활성 대상에 대한 중요 정보를 볼 수 있는 대시보드를 제공합니다.
topic-legacy: guide
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# (베타) [!UICONTROL Destinations] 대시보드

>[!IMPORTANT]
>
>이 문서에 설명된 대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 사용자 인터페이스(UI)는 일일 스냅샷 중에 캡처되는 대로 조직의 활성 대상에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 대상 대시보드에 액세스하고 해당 대시보드에 대해 작업하는 방법에 대해 설명하고 대시보드에 표시되는 지표에 대한 자세한 정보를 제공합니다.

대상에 대한 개요 및 Experience Platform 내에서 사용 가능한 모든 대상에 대한 카탈로그를 보려면 [대상 개요](../../destinations/home.md)를 방문하십시오.

## [!UICONTROL Destinations] 대시보드 데이터  {#destinations-dashboard-data}

[!UICONTROL Destinations] 대시보드에는 경험 프로필 내에서 조직에서 활성화한 대상 스냅숏이 표시됩니다. 스냅샷의 데이터는 스냅샷을 촬영한 특정 시점의 데이터와 동일한 데이터를 표시합니다. 즉, 스냅숏은 대략적인 데이터나 샘플이 아니며 대상 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅숏을 만든 이후 데이터에 대한 변경 사항이나 업데이트는 다음 스냅샷을 촬영하기 전까지 대시보드에 반영되지 않습니다.

## 대상 대시보드 탐색

플랫폼 UI 내의 대상 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL Destinations]**&#x200B;을 선택하고 **[!UICONTROL Overview]** 탭을 선택하여 대시보드를 표시합니다.

![](../images/destinations/dashboard-overview.png)

## 사용 가능한 위젯

Experience Platform은 대상과 관련된 여러 지표를 시각화하는 데 사용할 수 있는 여러 개의 위젯을 제공합니다. 자세한 내용을 보려면 아래 위젯 이름을 선택하십시오.

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)

### [!UICONTROL Most used destinations] {#most-used-destinations}

**[!UICONTROL Most used destinations]** 위젯은 마지막 스냅숏을 기준으로 매핑된 세그먼트 수별로 조직의 상위 대상을 표시합니다. 이 등급은 활용되고 있는 대상에 대한 통찰력을 제공하며 활용도가 낮은 대상을 표시합니다.

예를 들어, 대상을 어제 구성했지만 세그먼트에 매핑하지 않은 경우 대상이 현재 활용되지 않음을 확인할 수 있습니다.

세그먼트 수 열에 표시된 매핑된 세그먼트 수는 마지막 일별 스냅숏을 기준으로 정확합니다. 새 세그먼트를 대상에 매핑하면 다음 스냅숏을 만들 때까지 카운트가 업데이트되지 않습니다.

위젯에 표시된 목록에서 대상 이름을 선택하면 **[!UICONTROL Browse]** 탭에서 연결된 대상 세부 사항으로 이동합니다. **[!UICONTROL View All]**&#x200B;을 선택하여 **[!UICONTROL Browse]** 탭으로 이동한 다음 대상의 이름을 선택하여 세부 사항을 볼 수도 있습니다.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

**[!UICONTROL Recently created destinations]** 위젯을 사용하면 조직의 최근 구성된 대상 목록을 볼 수 있습니다.

표시된 작성 날짜는 마지막 일일 스냅숏에 정확합니다. 즉, 새 대상을 만들면 다음 스냅샷을 촬영하기 전까지는 목록에 표시되지 않습니다.

위젯에 표시된 목록에서 대상 이름을 선택하면 **[!UICONTROL Browse]** 탭에서 연결된 대상 세부 사항으로 이동합니다. **[!UICONTROL View All]**&#x200B;을 선택하여 **[!UICONTROL Browse]** 탭으로 이동한 다음 대상의 이름을 선택하여 세부 사항을 볼 수도 있습니다.

특정 유형의 대상을 구성하는 방법에 대한 자세한 내용은 [대상 설명서](../../destinations/home.md)를 참조하십시오.

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

**[!UICONTROL Recently activated segments]** 위젯은 대상에 가장 최근에 매핑된 세그먼트 목록을 제공합니다. 이 목록은 시스템에서 사용 중인 세그먼트 및 대상의 스냅숏을 제공하며 잘못된 매핑을 해결하는 데 도움이 될 수 있습니다.

표시된 업데이트된 날짜는 세그먼트가 대상에 대해 마지막으로 활성화되고 마지막 일별 스냅숏을 정확하게 확인할 수 있는 마지막 시간을 표시합니다. 즉, 세그먼트를 대상에 활성화하면 다음 스냅샷을 촬영하기 전까지 업데이트된 날짜가 변경되지 않습니다.

위젯에 표시된 목록에서 세그먼트 이름을 선택하면 세그먼트 세부 사항으로 이동합니다. **[!UICONTROL View All]**&#x200B;을 선택하여 세그먼트 찾아보기 탭으로 이동한 다음 세그먼트 이름을 선택하여 세부 사항을 볼 수도 있습니다.

Experience Platform에서 세그먼트 작업에 대한 자세한 내용은 [세그멘테이션 서비스 개요](../../segmentation/home.md)를 읽으십시오.

![](../images/destinations/recently-activated-segments.png)

## 다음 단계

이제 이 문서를 따라 대상 대시보드를 찾고 사용 가능한 위젯에 표시되는 지표를 이해할 수 있어야 합니다. Experience Platform에서 대상으로 작업하는 방법에 대한 자세한 내용은 [대상 설명서](../../destinations/home.md)를 참조하십시오.
