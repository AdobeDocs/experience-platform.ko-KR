---
keywords: Experience Platform;프로필;실시간 고객 프로필;사용자 인터페이스;UI;사용자 지정;프로필 대시보드;대시보드
title: 대상 대시보드
description: Adobe Experience Platform은 조직의 활성 대상에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 86041e3165d4ea9cb55717f24b002afa084ff420
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 0%

---

# [!UICONTROL 대상] 대시보드

Adobe Experience Platform UI(사용자 인터페이스)는 일별 스냅샷 중에 캡처된 대로 조직의 활성 대상에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 대상 대시보드에 액세스하고 사용하는 방법을 간략하게 설명하고 대시보드에 표시되는 지표에 대한 자세한 정보를 제공합니다.

대상 개요 및 Experience Platform 내에서 사용 가능한 모든 대상 카탈로그를 보려면 [대상 설명서](../../destinations/home.md).

## [!UICONTROL 대상] 대시보드 데이터 {#destinations-dashboard-data}

다음 [!UICONTROL 대상] 대시보드는 Experience Platform 내에서 조직에서 활성화한 대상의 스냅숏을 표시합니다. 스냅샷의 데이터는 스냅샷을 가져온 특정 시점의 데이터와 동일하게 표시됩니다. 즉, 스냅샷은 근사 또는 데이터 샘플이 아니며, 대상 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 생성하기 때문에 데이터가 변경된 사항이나 업데이트는 다음 스냅샷을 가져올 때까지 대시보드에 반영되지 않습니다.

## 대상 대시보드 탐색

Platform UI 내에서 대상 대시보드로 이동하려면 다음을 선택합니다 **[!UICONTROL 대상]** 왼쪽 레일에서 **[!UICONTROL 개요]** 탭을 클릭하여 대시보드를 표시합니다.

>[!NOTE]
>
>조직에서 Experience Platform을 처음 사용하고 아직 활성 대상이 없는 경우 [!UICONTROL 대상] 대시보드 및 [!UICONTROL 개요] 탭이 표시되지 않습니다. 대신, 선택 [!UICONTROL 대상] 왼쪽 탐색에서 는 [!UICONTROL 카탈로그] 탭. 에 대해 자세히 알아보려면 [!UICONTROL 카탈로그] 탭에서 다음을 참조하십시오 [[!UICONTROL 대상] 작업 공간 안내서](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### 대상 대시보드 수정

을 선택하여 대상 대시보드의 모양을 수정할 수 있습니다 **[!UICONTROL 대시보드 수정]**. 이를 통해 대시보드에서 위젯을 이동, 추가 및 제거할 수 있을 뿐만 아니라 **[!UICONTROL 위젯 라이브러리]** 사용 가능한 위젯을 살펴보고 조직에 대한 사용자 지정 위젯을 만들려면

자세한 내용은 [대시보드 수정](../customize/modify.md) 및 [위젯 라이브러리 개요](../customize/widget-library.md) 설명서 를 참조하십시오.

## 표준 위젯

Adobe은 대상과 관련된 다양한 지표를 시각화하고 데이터 분석에 사용할 수 있는 세그먼트의 완벽성을 평가하는 데 사용할 수 있는 여러 표준 위젯을 제공합니다. 또한 [!UICONTROL 위젯 라이브러리]. 사용자 지정 위젯을 만드는 방법에 대해 자세히 알아보려면 [위젯 라이브러리 개요](../customize/widget-library.md).

사용 가능한 각 표준 위젯에 대해 자세히 알아보려면 다음 목록에서 위젯 이름을 선택하십시오.

* [[!UICONTROL 가장 많이 사용되는 대상]](#most-used-destinations)
* [[!UICONTROL 최근에 만든 대상]](#recently-created-destinations)
* [[!UICONTROL 최근에 활성화된 세그먼트]](#recently-activated-segments)
* [[!UICONTROL 대상별로 최근에 활성화된 세그먼트]](#recently-activated-segments-by-destination)
* [[!UICONTROL 대상 크기 트렌드]](#audience-size-trends)
* [[!UICONTROL ID로 매핑되지 않은 세그먼트]](#unmapped-segments-by-identity)
* [[!UICONTROL ID별로 매핑된 세그먼트]](#mapped-segments-by-identity)
* [[!UICONTROL 일반적인 대상]](#common-audiences)
* [[!UICONTROL 대상 수]](#destinations-count)

### [!UICONTROL 가장 많이 사용되는 대상] {#most-used-destinations}

다음 **[!UICONTROL 가장 많이 사용되는 대상]** 위젯은 마지막 스냅샷을 기준으로 매핑된 세그먼트 수별로 조직의 최상위 대상을 표시합니다. 이 등급을 통해 사용 중인 대상을 파악할 수 있을 뿐만 아니라 활용도가 낮은 대상을 표시할 수도 있습니다.

예를 들어 대상을 어제 구성했지만 세그먼트를 매핑하지 않은 경우 대상이 현재 제대로 활용되지 않고 있는지 확인할 수 있습니다.

세그먼트 수 열에 표시된 매핑된 세그먼트의 수가 마지막 일별 스냅숏을 기준으로 정확합니다. 대상에 새 세그먼트를 매핑하면 다음 스냅샷을 가져올 때까지 카운트가 업데이트되지 않습니다.

위젯에 표시된 목록에서 대상 이름을 선택하면 **[!UICONTROL 찾아보기]** 탭. 선택할 수도 있습니다 **[!UICONTROL 모두 보기]** 로 이동 **[!UICONTROL 찾아보기]** 탭한 다음 대상의 이름을 선택하여 세부 정보를 확인합니다.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL 최근에 만든 대상] {#recently-created-destinations}

다음 **[!UICONTROL 최근에 만든 대상]** 위젯을 사용하면 조직의 가장 최근에 구성된 대상 목록을 볼 수 있습니다.

표시된 생성 날짜가 마지막 일별 스냅샷에 정확합니다. 즉, 새 대상을 만들면 다음 스냅샷을 가져올 때까지 목록에 표시되지 않습니다.

위젯에 표시된 목록에서 대상 이름을 선택하면 **[!UICONTROL 찾아보기]** 탭. 선택할 수도 있습니다 **[!UICONTROL 모두 보기]** 로 이동 **[!UICONTROL 찾아보기]** 탭한 다음 대상의 이름을 선택하여 세부 정보를 확인합니다.

특정 유형의 대상을 구성하는 방법에 대해 자세히 알아보려면 [대상 설명서](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 최근에 활성화된 세그먼트] {#recently-activated-segments}

다음 **[!UICONTROL 최근에 활성화된 세그먼트]** 위젯은 대상에 가장 최근에 매핑된 세그먼트 목록을 제공합니다. 이 목록은 시스템에서 활발하게 사용 중인 세그먼트 및 대상에 대한 스냅숏을 제공하며 잘못된 매핑을 해결하는 데 도움이 될 수 있습니다.

표시된 업데이트 날짜는 세그먼트가 대상에 활성화되고 마지막 일별 스냅숏까지 정확해진 마지막 시간을 표시합니다. 즉, 세그먼트를 대상으로 활성화하면 다음 스냅샷을 만든 후에 업데이트된 날짜가 변경됩니다.

위젯에 표시된 목록에서 세그먼트 이름을 선택하면 세그먼트 세부 사항으로 이동합니다. 선택할 수도 있습니다 **[!UICONTROL 모두 보기]** 세그먼트 찾아보기 탭으로 이동한 다음 세그먼트 이름을 선택하여 세부 사항을 확인합니다.

Experience Platform에서 세그먼트 작업에 대한 자세한 내용은 [세그먼테이션 서비스 개요](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

### [!UICONTROL 대상별로 최근에 활성화된 세그먼트] {#recently-activated-segments-by-destination}

다음 **[!UICONTROL 대상별로 최근에 활성화된 세그먼트]** 위젯은 개요 드롭다운에서 선택한 대상에 따라 가장 최근에 활성화된 상위 5개의 세그먼트를 내림차순으로 표시합니다. 비슷하지만 [!UICONTROL 최근에 활성화된 세그먼트] 위젯이지만 데이터가 표시됨 **전용** 선택한 대상에 적용됩니다.

이 위젯에는 두 개의 지표가 포함되어 있습니다. 세그먼트 이름 및 세그먼트가 대상에 마지막으로 활성화된 날짜입니다. 표시된 데이터는 마지막 일별 스냅샷에서 정확합니다.

표시된 목록에서 세그먼트 이름을 선택하여 세그먼트의 세부 사항을 볼 수 있습니다.

![대상 위젯별로 최근에 활성화된 세그먼트입니다.](../images/destinations/recently-activated-segments-by-destination.png)

### [!UICONTROL 대상 크기 트렌드] {#audience-size-trend}

다음 **[!UICONTROL 대상 크기 트렌드]** 위젯은 해당 대상 계정에 매핑된 세그먼트의 기간 동안 프로필 수의 관계를 나타냅니다. 위젯은 선 그래프를 사용하여 매일 대상 계정으로 보내는 세그먼트에 포함된 프로필 수를 보여줍니다.

지난 30일, 90일 또는 12개월 동안의 대상 트렌드의 기간은 첫 번째 드롭다운 메뉴를 사용하여 조정할 수 있습니다.

두 번째 드롭다운 메뉴에는 대시보드 맨 위에서 선택한 대상 계정으로 전송할 수 있는 모든 사용 가능한 세그먼트가 나열됩니다.

![대상 크기 트렌드 위젯.](../images/destinations/audience-size-trend.png)

### [!UICONTROL ID로 매핑되지 않은 세그먼트] {#unmapped-segments-by-identity}

다음 **[!UICONTROL ID로 매핑되지 않은 세그먼트]** 위젯은 상위 5개 위젯을 나열합니다 **매핑되지 않음** 지정된 대상 및 id에 대한 내림차순 ID 카운트로 정렬된 세그먼트입니다. 선택한 ID를 기반으로 선택한 대상 계정에 매핑하는 데 가장 유용한 세그먼트를 강조 표시합니다.

대상 ID 드롭다운은 사용 가능한 세그먼트를 필터링합니다. 드롭다운에 나열된 필터 ID는 개요 페이지 맨 위에서 선택한 대상 계정에 따라 변경됩니다.

id 열은 위젯 ID 드롭다운에서 선택한 ID에 매핑할 수 있는 세그먼트 내의 소스 ID 수를 계산합니다.

![ID 위젯별로 매핑되지 않은 세그먼트.](../images/destinations/unmapped-segments-by-identity.png)

### [!UICONTROL ID별로 매핑된 세그먼트] {#mapped-segments-by-identity}

이 위젯은 **매핑된** 세그먼트 를 참조하십시오. 목록은 세그먼트 내에 포함된 소스 ID 수에 따라 높기에서 낮이로 정렬됩니다. 카운트할 대상 ID는 위젯 제목 아래의 드롭다운 메뉴에서 선택합니다. 위젯의 드롭다운에서 사용할 수 있는 대상 ID는 개요 대시보드 맨 위에서 선택한 대상 계정 필터에 따라 변경됩니다.

![ID 위젯별 매핑된 세그먼트.](../images/destinations/mapped-segments-by-identity.png)

다음 **[!UICONTROL ID별로 매핑된 세그먼트]** 위젯은 선택한 대상 내에서 캠페인에 대한 프로필 기회를 성공적으로 타깃팅할 가능성이 있는 한 눈에 강조 표시됩니다. 효율적인 타깃팅된 캠페인은 대상으로 전송된 프로필의 수가 아니라 유용하고 실행 가능한 데이터를 제공하기 위해 대상 ID와 일치할 수 있는 소스 ID 수에 따라 다릅니다.

### 일반적인 대상

다음 **[!UICONTROL 일반적인 대상]** 위젯은 페이지 맨 위에서 선택한 대상 계정과 위젯 드롭다운에서 선택한 대상 간에 활성화된 상위 5개 세그먼트 목록을 제공합니다. 세그먼트 목록은 최근에 활성화한 시기에 따라 정렬됩니다. 가장 최근에 활성화된 세그먼트가 맨 위에 표시됩니다.

다음 [!UICONTROL 대상 크기] 열은 나열된 각 세그먼트의 총 프로필 수를 제공합니다.

![공통 대상 위젯.](../images/destinations/common-audiences.png)

### 매핑된 대상 상태

위젯은 최대 20개의 매핑된 세그먼트 목록으로서, 마지막 일별 스냅샷에서 30일 평균 대상 크기보다 하나 이상의 표준 편차의 인자로 해당 대상에 매핑된 대상 크기를 벗어납니다.

간단히 말해서, 지난 30일 동안 평균으로부터 대상 크기의 분산에 대한 계산된 지표를 제공합니다. 이는 현재 대상 크기가 지난 30일 동안 데이터에서 본 과거 표준 편차를 벗어나는지 여부를 비교합니다.

시스템의 모든 대상 크기는 [!UICONTROL 최신 크기] 열.

세그먼트 매핑 프로필 카운트가 지난 30일 동안 평균 매핑된 프로필 크기보다 하나의 표준 편차를 초과하는 경우, 이것은 시스템의 예외 항목을 나타내며 조사해야 합니다.

세그먼트 내의 [!UICONTROL 매핑된 대상 상태] 위젯이 큰 여백에 의해 벗어납니다. 대상 크기 트렌드 차트를 참조하고 예외 항목 세그먼트를 찾아야 합니다. 트렌드는 세그먼트의 상태에 대한 더 많은 통찰력을 제공할 수 있습니다.

![매핑된 대상 상태 위젯.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL 대상 수] (#destinations-count)

다음 [!UICONTROL 대상 수] 위젯은 시스템 내에서 대상을 활성화 및 전달할 수 있는 사용 가능한 총 종단점 수를 제공합니다. 이 번호에는 활성 대상과 비활성 대상이 모두 포함됩니다.

총 개수 아래에서 을 선택합니다. **[!UICONTROL 대상]** 대상 찾아보기 탭으로 이동합니다. 이 페이지에는 날짜로 연결을 설정한 모든 대상이 나열됩니다.

![대상 수 위젯.](../images/destinations/destinations-count.png)

## 다음 단계

이제 이 문서를 따라 대상 대시보드를 찾고 사용 가능한 위젯에 표시되는 지표를 이해할 수 있어야 합니다. Experience Platform에서 대상 작업에 대한 자세한 내용은 [대상 설명서](../../destinations/home.md).
