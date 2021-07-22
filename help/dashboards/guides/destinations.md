---
keywords: Experience Platform;프로필;실시간 고객 프로필;사용자 인터페이스;UI;사용자 지정;프로필 대시보드;대시보드
title: 대상 대시보드
description: Adobe Experience Platform은 조직의 활성 대상에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 41ef7a6e6d3b0ee9afe762b19c8c286ceb361dbb
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

#  대상 대시보드

Adobe Experience Platform UI(사용자 인터페이스)는 일별 스냅샷 중에 캡처된 대로 조직의 활성 대상에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 대상 대시보드에 액세스하고 사용하는 방법을 간략하게 설명하고 대시보드에 표시되는 지표에 대한 자세한 정보를 제공합니다.

대상에 대한 개요와 Experience Platform 내에서 사용 가능한 모든 대상에 대한 카탈로그가 필요하면 [대상 설명서](../../destinations/home.md)를 방문하십시오.

##  대상, 대시보드 데이터 {#destinations-dashboard-data}

[!UICONTROL 대상] 대시보드는 Experience Profile 내에서 조직에서 활성화한 대상의 스냅샷을 표시합니다. 스냅샷의 데이터는 스냅샷을 가져온 특정 시점의 데이터와 동일하게 표시됩니다. 즉, 스냅샷은 근사 또는 데이터 샘플이 아니며, 대상 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 생성하기 때문에 데이터가 변경된 사항이나 업데이트는 다음 스냅샷을 가져올 때까지 대시보드에 반영되지 않습니다.

## 대상 대시보드 탐색

Platform UI 내의 대상 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL 대상]**&#x200B;을 선택한 다음 **[!UICONTROL 개요]** 탭을 선택하여 대시보드를 표시합니다.

>[!NOTE]
>
>조직이 Experience Platform을 처음 사용하고 아직 활성 대상이 없는 경우 [!UICONTROL 대상] 대시보드 및 [!UICONTROL 개요] 탭이 표시되지 않습니다. 대신 왼쪽 탐색에서 [!UICONTROL 대상]을 선택하면 [!UICONTROL 카탈로그] 탭이 표시됩니다. [!UICONTROL Catalog] 탭에 대한 자세한 내용은 [[!UICONTROL 대상] 작업 공간 안내서](../../destinations/ui/destinations-workspace.md)를 참조하십시오.

![](../images/destinations/dashboard-overview.png)

### 대상 대시보드 수정

**[!UICONTROL 대시보드 수정]**&#x200B;을 선택하여 대상 대시보드의 모양을 수정할 수 있습니다. 이를 통해 대시보드에서 위젯을 이동, 추가 및 제거할 수 있을 뿐만 아니라 **[!UICONTROL 위젯 라이브러리]**&#x200B;에 액세스하여 사용 가능한 위젯을 탐색하고 조직에 대한 사용자 지정 위젯을 만들 수 있습니다.

자세한 내용은 [대시보드](../customize/modify.md) 및 [위젯 라이브러리 개요](../customize/widget-library.md) 설명서를 참조하십시오.

## 표준 위젯

Adobe은 대상과 관련된 다양한 지표를 시각화하는 데 사용할 수 있는 여러 표준 위젯을 제공합니다. [!UICONTROL 위젯 라이브러리]를 사용하여 조직과 공유할 사용자 지정 위젯을 만들 수도 있습니다. 사용자 지정 위젯을 만드는 방법에 대한 자세한 내용은 [위젯 라이브러리 개요](../customize/widget-library.md)를 읽어 보십시오.

사용 가능한 각 표준 위젯에 대해 자세히 알아보려면 다음 목록에서 위젯 이름을 선택하십시오.

* [[!UICONTROL 가장 많이 사용되는 대상]](#most-used-destinations)
* [[!UICONTROL 최근에 만든 대상]](#recently-created-destinations)
* [[!UICONTROL 최근에 활성화된 세그먼트]](#recently-activated-segments)

### [!UICONTROL 가장 많이 사용되는 대상] {#most-used-destinations}

**[!UICONTROL 가장 많이 사용되는 대상]** 위젯은 마지막 스냅샷을 기준으로 매핑된 세그먼트의 수만큼 조직의 최상위 대상을 표시합니다. 이 등급을 통해 사용 중인 대상을 파악할 수 있을 뿐만 아니라 활용도가 낮은 대상을 표시할 수도 있습니다.

예를 들어 대상을 어제 구성했지만 세그먼트를 매핑하지 않은 경우 대상이 현재 제대로 활용되지 않고 있는지 확인할 수 있습니다.

세그먼트 수 열에 표시된 매핑된 세그먼트의 수가 마지막 일별 스냅숏을 기준으로 정확합니다. 대상에 새 세그먼트를 매핑하면 다음 스냅숏이 수행될 때까지 카운트가 업데이트되지 않습니다.

위젯에 표시된 목록에서 대상 이름을 선택하면 **[!UICONTROL 찾아보기]** 탭에서 연결된 대상 세부 사항으로 이동합니다. **[!UICONTROL 모두 보기]**&#x200B;를 선택하여 **[!UICONTROL 찾아보기]** 탭으로 이동한 다음 대상의 이름을 선택하여 세부 사항을 볼 수도 있습니다.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL 최근에 만든 대상] {#recently-created-destinations}

**[!UICONTROL 최근에 생성된 대상]** 위젯을 사용하면 조직의 가장 최근에 구성된 대상 목록을 볼 수 있습니다.

표시된 생성 날짜가 마지막 일별 스냅샷에 정확합니다. 즉, 새 대상을 만들면 다음 스냅샷을 가져올 때까지 목록에 표시되지 않습니다.

위젯에 표시된 목록에서 대상 이름을 선택하면 **[!UICONTROL 찾아보기]** 탭에서 연결된 대상 세부 사항으로 이동합니다. **[!UICONTROL 모두 보기]**&#x200B;를 선택하여 **[!UICONTROL 찾아보기]** 탭으로 이동한 다음 대상의 이름을 선택하여 세부 사항을 볼 수도 있습니다.

특정 유형의 대상을 구성하는 방법에 대한 자세한 내용은 [대상 설명서](../../destinations/home.md)를 참조하십시오.

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 최근에 활성화된 세그먼트] {#recently-activated-segments}

**[!UICONTROL 최근에 활성화된 세그먼트]** 위젯은 대상에 가장 최근에 매핑된 세그먼트 목록을 제공합니다. 이 목록은 시스템에서 활발하게 사용 중인 세그먼트 및 대상에 대한 스냅숏을 제공하며 잘못된 매핑을 해결하는 데 도움이 될 수 있습니다.

표시된 업데이트 날짜는 세그먼트가 대상에 활성화되고 마지막 일별 스냅숏까지 정확해진 마지막 시간을 표시합니다. 즉, 세그먼트를 대상으로 활성화하면 다음 스냅샷을 만든 후에 업데이트된 날짜가 변경됩니다.

위젯에 표시된 목록에서 세그먼트 이름을 선택하면 세그먼트 세부 사항으로 이동합니다. **[!UICONTROL 모두 보기]**&#x200B;를 선택하여 세그먼트 찾아보기 탭으로 이동한 다음 세그먼트 이름을 선택하여 세부 사항을 볼 수도 있습니다.

Experience Platform에서 세그먼트 작업에 대한 자세한 내용은 [세그멘테이션 서비스 개요](../../segmentation/home.md)를 읽어 보십시오.

![](../images/destinations/recently-activated-segments.png)

## 다음 단계

이제 이 문서를 따라 대상 대시보드를 찾고 사용 가능한 위젯에 표시되는 지표를 이해할 수 있어야 합니다. Experience Platform에서 대상 작업에 대한 자세한 내용은 [대상 설명서](../../destinations/home.md)를 참조하십시오.
