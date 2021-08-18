---
keywords: 플랫폼;대상;대상 작업 공간;작업 공간;ui;대상 ui;카탈로그;대상 카탈로그
title: 대상 작업 공간
description: 대상 작업 영역은 카탈로그, 찾아보기, 계정 및 시스템 보기의 네 섹션으로 구성됩니다. 이러한 내용은 아래 섹션에 설명되어 있습니다.
seo-description: Adobe Experience Platform의 왼쪽 탐색 막대에서 대상 을 선택하여 대상 작업 공간에 액세스합니다.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a97b235e2d8834f6be002923be9cdbca5f08495b
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 2%

---

# 대상 작업 공간 {#destinations-workspace}

Adobe Experience Platform의 왼쪽 탐색 막대에서 **[!UICONTROL 대상]**&#x200B;을 선택하여 [!UICONTROL 대상] 작업 공간에 액세스합니다.

[!UICONTROL 대상] 작업 공간은 아래 섹션에 설명된 5개 섹션, [!UICONTROL 개요], [!UICONTROL 카탈로그], [!UICONTROL 찾아보기], [!UICONTROL 계정] 및 [!UICONTROL 시스템 보기]로 구성됩니다.

![대상 - 개요](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 개요] {#overview}

**[!UICONTROL 개요]** 탭에는 조직의 대상 데이터와 관련된 주요 지표를 제공하는 [!UICONTROL 대상] 대시보드가 표시됩니다. 자세한 내용은 [[!UICONTROL 대상] 대시보드 안내서](../../dashboards/guides/destinations.md)를 참조하십시오.

>[!NOTE]
>
>조직이 Experience Platform을 처음 사용하고 아직 활성 대상이 없는 경우 [!UICONTROL 대상] 대시보드 및 [!UICONTROL 개요] 탭이 표시되지 않습니다. 대신 왼쪽 탐색에서 [!UICONTROL 대상]을 선택하면 [[!UICONTROL 카탈로그] 탭](#catalog)이 표시됩니다.

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL 카탈로그] {#catalog}

**[!UICONTROL 카탈로그]** 탭에는 [!DNL Platform]에서 데이터를 보낼 수 있는 모든 대상 목록이 표시됩니다.

[!DNL Platform] 사용자 인터페이스는 대상 카탈로그 페이지에서 다음과 같은 몇 가지 검색 및 필터 옵션을 제공합니다.

* 페이지에서 검색 기능을 사용하여 특정 대상을 찾습니다.
* [!UICONTROL Categories] 컨트롤을 사용하여 대상을 필터링합니다.
* [!UICONTROL 모든 대상] 및 [!UICONTROL 내 대상] 간을 전환합니다. **[!UICONTROL 모든 대상]**&#x200B;을 선택하면 사용 가능한 모든 [!DNL Platform] 대상이 표시됩니다. **[!UICONTROL 내 대상]**&#x200B;을 선택하면 연결을 설정한 대상만 볼 수 있습니다.
* **[!UICONTROL 연결]** 및/또는 **[!UICONTROL 확장]**&#x200B;을 보려면 선택하십시오. 두 범주 간의 차이를 이해하려면 [대상 유형과 카테고리](../destination-types.md)를 참조하십시오.

![대상 필터링 및 검색 데모](../assets/ui/workspace/destinations-search-and-filter.gif)

대상 카드에 **[!UICONTROL Configure]** 또는 **[!UICONTROL Activate]** 컨트롤과 추가 옵션을 표시하는 보조 컨트롤이 있습니다. 이러한 컨트롤은 아래에 설명되어 있습니다.

| 제어 | 설명 |
|---------|----------|
|  구성 | 대상에 대한 연결을 만들 수 있습니다. |
| [!UICONTROL 활성화] | 대상에 대한 연결을 설정한 후에는 세그먼트를 활성화할 수 있습니다. |
| [!UICONTROL 계정 보기] | 대상에 대해 연결한 계정을 봅니다. |
| [!UICONTROL 데이터 흐름 보기] | 대상에 대해 존재하는 데이터 활성화 흐름을 봅니다. |
| [!UICONTROL 설명서 보기] | 자세한 내용을 알고 설정하는 데 도움이 되도록 특정 대상에 대한 설명서 페이지에 대한 링크를 엽니다. |

{style=&quot;table-layout:auto&quot;}

![대상 카드의 컨트롤](../assets/ui/workspace/destination-card-options.png)

카탈로그에서 대상 카드를 선택하여 오른쪽 레일을 엽니다. 여기에서 대상에 대한 설명을 볼 수 있습니다. 오른쪽 레일은 대상에 대한 설명, 대상 카테고리 및 유형의 표시를 포함하여 위의 표에 설명된 것과 동일한 컨트롤을 제공합니다.

![대상 카탈로그 옵션](../assets/ui/workspace/destination-right-rail.png)

대상 카테고리 및 각 대상에 대한 정보에 대한 자세한 내용은 [대상 카탈로그](../catalog/overview.md) 및 [대상 유형 및 카테고리](../destination-types.md)를 참조하십시오.

## [!UICONTROL 계정] {#accounts}

**[!UICONTROL 계정]** 탭은 다양한 대상으로 설정한 연결에 대한 세부 정보를 보여주며 기존 연결 세부 정보를 업데이트할 수 있도록 해줍니다. 자세한 지침은 [계정 업데이트](update-accounts.md)를 참조하십시오.

## [!UICONTROL 찾아보기] {#browse}

**[!UICONTROL 찾아보기]** 탭에는 연결을 설정한 대상이 표시됩니다. **[!UICONTROL Enabled/Disabled]** 토글이 설정된 대상은 각각 활성 또는 비활성 상태로 설정합니다. 또한 **[!UICONTROL 세그먼트]** > **[!UICONTROL 찾아보기]**&#x200B;를 선택하고 검사할 세그먼트를 선택하여 데이터가 흐르는 대상을 볼 수도 있습니다. 찾아보기 탭에서 각 대상에 대해 제공되는 모든 정보는 아래 표를 참조하십시오.

>[!TIP]
>
> * [!UICONTROL 이름] 열에서 세 점을 선택하고 ![세그먼트 추가 단추](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 활성화&#x200B;]**단추를 사용하여 세그먼트를 해당 대상에 보냅니다.
> * [!UICONTROL 이름] 열에서 세 점을 선택하고 ![대상 삭제 단추](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 삭제&#x200B;]**단추를 사용하여 대상에 대한 기존 연결을 [제거](delete-destinations.md)합니다.


![찾아보기 탭](../assets/ui/workspace/browse-tab.png)

| 요소 | 설명 |
|---------|----------|
| 이름 | 활성화 플로우에 대해 제공한 이름을 이 대상으로 합니다. 동일한 열에는 두 개의 컨트롤이 있습니다.  및 [!UICONTROL 대상 삭제]. |
| [!UICONTROL 마지막 흐름 실행 상태] | 마지막 데이터 흐름 실행의 상태입니다. 데이터 흐름 실행에 대한 자세한 내용은 [대상 세부 정보 보기](destination-details-page.md)를 참조하십시오. |
| [!UICONTROL 마지막 흐름 실행 날짜] | 마지막 데이터 흐름 실행이 발생한 시간 및 날짜입니다. 데이터 흐름 실행에 대한 자세한 내용은 [대상 세부 정보 보기](destination-details-page.md)를 참조하십시오. |
| [!UICONTROL 대상] | 활성화 플로우에 대해 선택한 대상 플랫폼입니다. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상: S3, FTP 또는 [!DNL Azure Blob]일 수 있습니다.</li><li>실시간 광고 대상의 경우: 서버 간.</li><li>스트리밍 대상의 경우: [!DNL Azure Event Hubs] 또는 [!DNL Amazon Kinesis]일 수 있습니다.</li></ul> |
| [!UICONTROL 사용자 이름] | 대상 플로우에 대해 선택한 계정 자격 증명입니다. |
| [!UICONTROL 활성화 데이터] | 이 대상에 활성화된 세그먼트 수를 나타냅니다. 활성화된 세그먼트에 대한 자세한 내용을 보려면 이 컨트롤을 선택하십시오. 활성화된 세그먼트에 대한 자세한 내용은 대상 세부 정보 페이지의 [활성화 데이터](/help/destinations/ui/destination-details-page.md#activation-data) 를 참조하십시오. |
| [!UICONTROL 생성됨] | 대상으로 활성화 흐름이 만들어진 날짜 및 UTC 시간입니다. |
| [!UICONTROL 상태] | `Active` 또는 `Inactive`. 데이터를 이 대상에 활성화할지 여부를 나타냅니다. |

오른쪽 레일에서 대상에 대한 자세한 정보를 표시하려면 대상 행을 클릭합니다.

![대상 행 클릭](../assets/ui/workspace/click-destination-row.png)

대상 이름을 선택하여 이 대상에 활성화된 세그먼트에 대한 정보를 확인합니다. **[!UICONTROL 활성화 편집]**&#x200B;을 클릭하여 이 대상으로 전송되는 세그먼트를 수정하거나 추가합니다.

## [!UICONTROL 시스템 보기] {#system-view}

**[!UICONTROL 시스템 보기]** 탭에는 Adobe Experience Platform에서 설정한 활성화 흐름의 그래픽 표현이 표시됩니다.

![데이터 흐름1](../assets/ui/workspace/data-flows1.png)

페이지에 표시되는 대상을 선택하고 **[!UICONTROL 데이터 흐름 보기]**&#x200B;를 클릭하여 각 대상에 대해 설정한 모든 연결에 대한 정보를 확인합니다.

![Data-flow2](../assets/ui/workspace/data-flows2.png)
