---
keywords: 플랫폼;대상;대상 작업 공간;작업 공간;ui;대상 ui;카탈로그;대상 카탈로그
title: 대상 작업 공간
description: 대상 작업 영역은 개요, 카탈로그, 찾아보기, 계정 및 시스템 보기, 5개의 섹션으로 구성됩니다. 이러한 내용은 아래 섹션에 설명되어 있습니다.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 2%

---

# 대상 작업 공간 {#destinations-workspace}

Adobe Experience Platform에서 **[!UICONTROL 대상]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 대상] 작업 공간.

다음 [!UICONTROL 대상] 작업 공간은 다섯 개의 섹션으로 구성됩니다. [!UICONTROL 개요], [!UICONTROL 카탈로그], [!UICONTROL 찾아보기], [!UICONTROL 계정], 및 [!UICONTROL 시스템 보기]아래의 섹션에 설명되어 있습니다.

![대상 - 개요](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 개요] {#overview}

다음 **[!UICONTROL 개요]** 탭이 표시됩니다 [!UICONTROL 대상] 대시보드, 조직의 대상 데이터와 관련된 주요 지표를 제공합니다. 자세한 내용은 [[!UICONTROL 대상] 대시보드 안내서](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>조직에서 Experience Platform을 처음 사용하고 아직 활성 대상이 없는 경우 [!UICONTROL 대상] 대시보드 및 [!UICONTROL 개요] 탭이 표시되지 않습니다. 대신, 선택 [!UICONTROL 대상] 왼쪽 탐색에서 는 [[!UICONTROL 카탈로그] 탭](#catalog).

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL 카탈로그] {#catalog}

다음 **[!UICONTROL 카탈로그]** 탭에는 [!DNL Platform]: 로 데이터를 보낼 수 있습니다.

다음 [!DNL Platform] 사용자 인터페이스는 대상 카탈로그 페이지의 여러 검색 및 필터 옵션을 제공합니다.

* 페이지에서 검색 기능을 사용하여 특정 대상을 찾습니다.
* 을 사용하여 대상 필터링 [!UICONTROL 카테고리] 제어.
* 전환 [!UICONTROL 모든 대상] 및 [!UICONTROL 내 대상]. 선택 시 **[!UICONTROL 모든 대상]**, 모두 사용 가능 [!DNL Platform] 대상이 표시됩니다. 선택 시 **[!UICONTROL 내 대상]**&#x200B;를 입력하면 연결을 설정한 대상만 볼 수 있습니다.
* 보려는 선택 **[!UICONTROL 연결]** 및/또는 **[!UICONTROL 확장]**. 두 범주 간의 차이를 이해하려면 다음을 참조하십시오 [대상 유형 및 카테고리](../destination-types.md).

![카탈로그](../assets/ui/workspace/catalog.png)

대상 카드에 **[!UICONTROL 설정]** 또는 **[!UICONTROL 세그먼트 활성화]** 컨트롤 및 더 많은 옵션을 제공하는 보조 컨트롤 이러한 컨트롤은 아래에 설명되어 있습니다.

| 제어 | 설명 |
|---------|----------|
| [!UICONTROL 설정] | 대상에 대한 연결을 만들 수 있습니다. |
| [!UICONTROL 세그먼트 활성화] | 대상에 대한 연결을 설정한 후에는 세그먼트를 활성화할 수 있습니다. |
| [!UICONTROL 계정 보기] | 대상에 대해 연결한 계정을 봅니다. |
| [!UICONTROL 데이터 흐름 보기] | 대상에 대해 존재하는 데이터 활성화 흐름을 봅니다. |
| [!UICONTROL 설명서 보기] | 자세한 내용을 알고 설정하는 데 도움이 되도록 특정 대상에 대한 설명서 페이지에 대한 링크를 엽니다. |

{style=&quot;table-layout:auto&quot;}

![대상 카드의 컨트롤](../assets/ui/workspace/destination-card-options.png)

카탈로그에서 대상 카드를 선택하여 오른쪽 레일을 엽니다. 여기에서 대상에 대한 설명을 볼 수 있습니다. 오른쪽 레일은 대상에 대한 설명, 대상 카테고리 및 유형의 표시를 포함하여 위의 표에 설명된 것과 동일한 컨트롤을 제공합니다.

![대상 카탈로그 옵션](../assets/ui/workspace/destination-right-rail.png)

대상 카테고리 및 각 대상에 대한 정보에 대한 자세한 내용은 [대상 카탈로그](../catalog/overview.md) 및 [대상 유형 및 카테고리](../destination-types.md).

## [!UICONTROL 계정] {#accounts}

다음 **[!UICONTROL 계정]** 탭에는 다양한 대상으로 설정한 연결에 대한 세부 사항이 표시되며, 기존 계정 세부 사항을 업데이트하거나 삭제할 수 있습니다. 각 대상 계정에서 얻을 수 있는 모든 정보는 아래 표를 참조하십시오.

>[!TIP]
>
> * 에서 세 점을 선택합니다 [!UICONTROL 플랫폼] 열 및 ![세그먼트 활성화 단추](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 세그먼트 활성화&#x200B;]**세그먼트를 해당 대상에 전송하는 단추.
> * 에서 세 점을 선택합니다 [!UICONTROL 플랫폼] 열 및 ![세부 사항 편집 단추](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL 세부 사항 편집&#x200B;]**버튼 대상 [업데이트](update-accounts.md) 기존 대상 계정의 세부 정보입니다.
> * 에서 세 점을 선택합니다 [!UICONTROL 플랫폼] 열 및 ![삭제 단추](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 삭제&#x200B;]**버튼 대상 [delete](delete-destination-account.md) 기존 대상 계정.


![계정 탭](../assets/ui/workspace/destination-account-options.png)

| 요소 | 설명 |
|---|---|
| [!UICONTROL 플랫폼] | 연결을 설정한 대상입니다. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 계정 연결 유형을 나타냅니다. 대상에 따라 인증 옵션은 다음과 같습니다. <ul><li>이메일 마케팅 대상: S3, FTP 또는 Azure Blob일 수 있습니다.</li><li>실시간 광고 대상의 경우: 서버 간</li><li>Amazon S3 클라우드 스토리지 대상의 경우: 액세스 키 </li><li>SFTP 클라우드 스토리지 대상: SFTP에 대한 기본 인증</li><li>OAuth 1 또는 OAuth 2 인증</li><li>베어러 토큰 인증</li></ul> |
| [!UICONTROL 사용자 이름] | 에서 선택한 사용자 이름 [대상 마법사 연결](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL 대상] | 대상에 대해 생성된 기본 정보와 연결된 고유한 성공적인 대상 데이터 흐름의 수를 나타냅니다. |
| [!UICONTROL 인증됨] | 이 대상에 대한 연결이 허용된 날짜입니다. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL 찾아보기] {#browse}

다음 **[!UICONTROL 찾아보기]** 탭에는 연결을 설정한 대상이 표시됩니다. 을 사용하는 대상 **[!UICONTROL 활성화/비활성화]** 대상을 각각 활성 또는 비활성으로 설정 켜기/끄기를 전환합니다. 을 선택하여 데이터가 흐름된 대상을 볼 수도 있습니다 **[!UICONTROL 세그먼트]** > **[!UICONTROL 찾아보기]** 검사할 세그먼트를 선택합니다. 의 각 대상에 대해 제공된 모든 정보는 아래 표를 참조하십시오. [!UICONTROL 찾아보기] 탭:

>[!TIP]
>
> * 에서 세 점을 선택합니다 [!UICONTROL 이름] 열 및 ![세그먼트 활성화 단추](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 세그먼트 활성화&#x200B;]**세그먼트를 해당 대상에 전송하는 단추.
> * 에서 세 점을 선택합니다 [!UICONTROL 이름] 열 및 ![삭제 단추](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 삭제&#x200B;]**버튼 대상 [제거](delete-destinations.md) 대상에 대한 기존 연결.
> * 에서 세 점을 선택합니다 [!UICONTROL 이름] 열 및 ![모니터링 단추에서 보기](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL 모니터링에서 보기&#x200B;]**단추를 클릭하여 이 대상에 대한 활성화 정보를 봅니다. [대시보드 모니터링](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * 에서 세 점을 선택합니다 [!UICONTROL 이름] 열 및 ![경고 구독 ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL 경고 구독&#x200B;]**대상 데이터 흐름 경고를 구독하는 단추. 경고를 구독하면 흐름 실행 상태, 성공 또는 실패와 관련된 메시지를 받을 수 있습니다. 자세한 내용은 [컨텍스트 내 대상 경고 구독](alerts.md) 대상 데이터 흐름 경고에 대한 자세한 정보..


![찾아보기 탭](../assets/ui/workspace/browse-tab.png)

| 요소 | 설명 |
|---------|----------|
| 이름 | 활성화 플로우에 대해 제공한 이름을 이 대상으로 합니다. 동일한 열에는 두 개의 컨트롤이 있습니다. [!UICONTROL 활성화 ] 및 [!UICONTROL 대상 삭제]. |
| [!UICONTROL 마지막 흐름 실행 상태] | 마지막 데이터 흐름 실행의 상태입니다. 자세한 내용은 [대상 세부 사항 보기](destination-details-page.md) dataflow 실행에 대한 자세한 내용은 다음을 참조하십시오. |
| [!UICONTROL 마지막 흐름 실행 날짜] | 마지막 데이터 흐름 실행이 발생한 시간 및 날짜입니다. 자세한 내용은 [대상 세부 사항 보기](destination-details-page.md) dataflow 실행에 대한 자세한 내용은 다음을 참조하십시오. |
| [!UICONTROL 대상] | 활성화 플로우에 대해 선택한 대상 플랫폼입니다. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상: S3, FTP 또는 [!DNL Azure Blob].</li><li>실시간 광고 대상의 경우: 서버 간.</li><li>스트리밍 대상의 경우: 다음을 수행할 수 있습니다. [!DNL Azure Event Hubs] 또는 [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL 사용자 이름] | 대상 플로우에 대해 선택한 계정 자격 증명입니다. |
| [!UICONTROL 활성화 데이터] | 이 대상에 활성화된 세그먼트 수를 나타냅니다. 활성화된 세그먼트에 대한 자세한 내용을 보려면 이 컨트롤을 선택하십시오. 을(를) 참조하십시오. [활성화 데이터](/help/destinations/ui/destination-details-page.md#activation-data) 를 참조하십시오. |
| [!UICONTROL 생성됨] | 대상으로 활성화 흐름이 만들어진 날짜 및 UTC 시간입니다. 활성화 흐름을 가장 최근 첫 번째 또는 가장 오래된 순서로 정렬하려면 위쪽/아래쪽 화살표 기호를 선택합니다. |
| [!UICONTROL 상태] | `Enabled` 또는 `Disabled`. 데이터를 이 대상에 활성화할지 여부를 나타냅니다. |

오른쪽 레일에서 대상에 대한 자세한 정보를 표시하려면 대상 행을 클릭합니다.

![대상 행 클릭](../assets/ui/workspace/click-destination-row.png)

대상 이름을 선택하여 이 대상에 활성화된 세그먼트에 대한 정보를 확인합니다. 클릭 **[!UICONTROL 활성화 편집]** 을 추가하여 이 대상으로 전송되는 세그먼트를 수정하거나 추가합니다.

## [!UICONTROL 시스템 보기] {#system-view}

다음 **[!UICONTROL 시스템 보기]** 탭에는 Adobe Experience Platform에서 설정한 활성화 흐름의 그래픽 표현이 표시됩니다.

![데이터 흐름1](../assets/ui/workspace/data-flows1.png)

페이지에 표시되는 대상을 선택하고 를 클릭합니다 **[!UICONTROL 데이터 흐름 보기]** 를 클릭하여 각 대상에 대해 설정한 모든 연결에 대한 정보를 확인합니다.

![Data-flow2](../assets/ui/workspace/data-flows2.png)
