---
keywords: 플랫폼;대상;대상 작업 영역;작업 영역;ui;대상 ui;카탈로그;대상 카탈로그;
title: 대상 작업 영역
description: 대상 작업 영역은 개요, 카탈로그, 찾아보기, 계정 및 시스템 보기의 5개 섹션으로 구성되어 있습니다. 아래 섹션에 설명되어 있습니다.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a2420f86e650ce1ca8a5dc01d9a29548663d3f7c
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 1%

---

# 대상 작업 영역 {#destinations-workspace}

Adobe Experience Platform의 왼쪽 탐색 모음에서 **[!UICONTROL 대상]**&#x200B;을 선택하여 [!UICONTROL 대상] 작업 영역에 액세스합니다.

[!UICONTROL 대상] 작업 영역은 아래 섹션에 설명된 5개의 섹션, [!UICONTROL 개요], [!UICONTROL 카탈로그], [!UICONTROL 찾아보기], [!UICONTROL 계정] 및 [!UICONTROL 시스템 보기]로 구성됩니다.

![대상 개요 대시보드에 3개의 위젯이 표시됨](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 개요] {#overview}

**[!UICONTROL 개요]** 탭에는 조직의 대상 데이터와 관련된 주요 지표를 제공하는 [!UICONTROL 대상] 대시보드가 표시됩니다. 자세한 내용은 [[!UICONTROL 대상] 대시보드 가이드](../../dashboards/guides/destinations.md)를 참조하세요.

>[!NOTE]
>
>조직이 Experience Platform을 처음 사용하고 아직 활성 대상이 없는 경우 [!UICONTROL 대상] 대시보드 및 [!UICONTROL 개요] 탭이 표시되지 않습니다. 대신 왼쪽 탐색에서 [!UICONTROL 대상]을 선택하면 [[!UICONTROL 카탈로그] 탭](#catalog)이 표시됩니다.

![대상 대시보드 개요 탭](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL 카탈로그] {#catalog}

**[!UICONTROL 카탈로그]** 탭에는 데이터를 보낼 수 있는 [!DNL Experience Platform]에서 사용 가능한 모든 대상 목록이 표시됩니다.

[!DNL Experience Platform] 사용자 인터페이스는 대상 카탈로그 페이지에서 여러 검색 및 필터 옵션을 제공합니다.

* 페이지의 검색 기능을 사용하여 특정 대상을 찾습니다.
* [!UICONTROL Categories] 컨트롤을 사용하여 대상을 필터링합니다.
* [!UICONTROL 모든 대상]과(와) [!UICONTROL 내 대상] 사이를 전환합니다. **[!UICONTROL 모든 대상]**&#x200B;을 선택하면 사용 가능한 모든 [!DNL Experience Platform] 대상이 표시됩니다. **[!UICONTROL 내 대상]**&#x200B;을 선택하면 연결을 설정한 대상만 표시됩니다.
* **[!UICONTROL 연결]** 및/또는 **[!UICONTROL 확장]** 유형을 보려면 선택하십시오. 두 범주의 차이점을 이해하려면 [대상 형식 및 범주](../destination-types.md)를 읽어 보세요.

![몇 가지 광고 및 클라우드 저장소 대상을 표시하는 대상 카탈로그입니다.](../assets/ui/workspace/catalog.png)

대상 카드에는 기본 및 보조 제어 옵션이 있습니다. 기본 컨트롤에는 [!UICONTROL 설정], [!UICONTROL 활성화], [!UICONTROL 대상 활성화] 또는 [!UICONTROL 데이터 세트 내보내기]가 포함됩니다. 보조 컨트롤을 사용하여 옵션을 볼 수 있습니다. 이러한 컨트롤은 아래에 설명되어 있습니다.

| 제어 | 설명 |
|---------|----------|
| [!UICONTROL 설정] | 대상에 대한 연결을 만들 수 있습니다. |
| [!UICONTROL 활성화] | 대상에 대한 연결이 설정되면 대상을 활성화하거나 데이터 세트를 이 대상으로 내보낼 수 있습니다. |
| [!UICONTROL 대상자 활성화] | 대상에 대한 연결이 설정되면 이 대상에 대한 대상을 활성화할 수 있습니다. |
| [!UICONTROL 데이터 세트 내보내기] | 대상에 대한 연결이 설정되면 데이터 세트를 이 대상으로 내보낼 수 있습니다. |
| [!UICONTROL 계정 보기] | 대상에 대해 연결한 계정을 봅니다. |
| [!UICONTROL 데이터 흐름 보기] | 대상에 대해 존재하는 데이터 활성화 플로우를 봅니다. |
| [!UICONTROL 설명서 보기] | 자세한 내용을 알고 설정하는 데 도움이 되도록 해당 특정 대상의 설명서 페이지에 대한 링크를 엽니다. |

{style="table-layout:auto"}

대상 카드의 ![컨트롤](../assets/ui/workspace/destination-card-options.png)

카탈로그에서 대상 카드를 선택하여 오른쪽 레일을 엽니다. 여기에서 대상에 대한 설명을 볼 수 있습니다. 오른쪽 레일은 대상 설명, 대상 범주 및 유형 표시를 포함하여 위 표에 설명된 것과 동일한 컨트롤을 제공합니다.

![대상 카탈로그 옵션](../assets/ui/workspace/destination-right-rail.png)

대상 범주 및 각 대상에 대한 자세한 내용은 [대상 카탈로그](../catalog/overview.md) 및 [대상 유형 및 범주](../destination-types.md)를 참조하십시오.

## [!UICONTROL 계정] {#accounts}

**[!UICONTROL 계정]** 탭에는 다양한 대상으로 설정한 연결에 대한 세부 정보가 표시되며, 이를 통해 기존 계정 세부 정보를 업데이트하거나 삭제할 수 있습니다. 각 대상 계정에서 확인할 수 있는 모든 정보는 아래 표를 참조하십시오.

>[!TIP]
>
> * [!UICONTROL Platform] 열에서 줄임표(`...`)를 선택하고 ![컨트롤 활성화](/help/images/icons/data-add.png)**[!UICONTROL 활성화&#x200B;]**/**[!UICONTROL &#x200B;대상 활성화&#x200B;]**/**[!UICONTROL &#x200B;데이터 세트 내보내기&#x200B;]**&#x200B;컨트롤을 사용하여 대상 또는 데이터 세트를 해당 대상으로 내보냅니다.
> * [!UICONTROL 플랫폼] 열에서 줄임표(`...`)를 선택하고 ![세부 정보 편집 컨트롤](/help/images/icons/edit.png)**[!UICONTROL 세부 정보 편집&#x200B;]**&#x200B;컨트롤을 사용하여 기존 대상 계정의 세부 정보를 [업데이트](update-accounts.md)합니다.
> * [!UICONTROL Platform] 열에서 줄임표(`...`)를 선택하고 ![Delete 컨트롤](/help/images/icons/delete.png)**[!UICONTROL Delete &#x200B;]**&#x200B;컨트롤을 사용하여 기존 대상 계정을 [삭제](delete-destination-account.md)합니다.

![계정 탭](../assets/ui/workspace/destination-account-options.png)

| 요소 | 설명 |
|---|---|
| [!UICONTROL 대상] | 연결을 설정한 대상 커넥터입니다. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 계정 연결 유형을 나타냅니다. 대상에 따라 인증 옵션은 다음과 같습니다. <ul><li>이메일 마케팅 대상의 경우: S3, FTP 또는 Azure Blob일 수 있습니다.</li><li>실시간 광고 대상: 서버 간</li><li>Amazon S3 클라우드 스토리지 대상의 경우: 액세스 키 </li><li>SFTP 클라우드 스토리지 대상의 경우: SFTP에 대한 기본 인증</li><li>OAuth 1 또는 OAuth 2 인증</li><li>전달자 토큰 인증</li></ul> |
| [!UICONTROL 사용자 이름] | [대상 연결 워크플로](../catalog/email-marketing/overview.md#connect-destination)에서 선택한 사용자 이름입니다. |
| [!UICONTROL 연결] | 대상에 대해 만들어진 기본 정보와 연결된 성공한 고유 대상 데이터 흐름 수를 나타냅니다. |
| [!UICONTROL 인증 날짜] | 이 대상에 대한 연결이 승인된 날짜입니다. |
| [!UICONTROL 만료 날짜] | 이 대상에 대한 연결 인증이 만료되는 날짜입니다. <br>**중요**: 이 열은 현재 [Facebook](../catalog/social/facebook.md) 연결에만 사용할 수 있습니다. |

{style="table-layout:auto"}

## [!UICONTROL 찾아보기] {#browse}

**[!UICONTROL 찾아보기]** 탭에는 연결을 설정한 대상이 표시됩니다. **[!UICONTROL 사용/사용 안 함]** 토글이 켜진 대상은 각각 활성 또는 비활성으로 설정합니다. **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**&#x200B;를 선택하고 검사할 대상을 선택하여 데이터가 흐르는 대상을 볼 수도 있습니다. [!UICONTROL 찾아보기] 탭에서 각 대상에 대해 제공된 모든 정보를 보려면 아래 표를 참조하십시오.

>[!TIP]
>
> * [!UICONTROL 이름] 열에서 줄임표(`...`)를 선택하고 ![대상 활성화 컨트롤](/help/images/icons/data-add.png)**[!UICONTROL 활성화&#x200B;]**&#x200B;컨트롤을 사용하여 대상 또는 데이터 집합을 해당 대상으로 내보냅니다.
> * [!UICONTROL 이름] 열에서 줄임표(`...`)를 선택하고 ![삭제 컨트롤](/help/images/icons/delete.png)**[!UICONTROL 삭제&#x200B;]**&#x200B;컨트롤을 사용하여 대상에 대한 기존 연결을 [제거](delete-destinations.md)합니다.
> * [!UICONTROL 이름] 열에서 줄임표(`...`)를 선택하고 ![모니터링 제어에서 보기](/help/images/icons/monitoring.png)**[!UICONTROL 모니터링에서 보기&#x200B;]**&#x200B;제어를 사용하여 [모니터링 대시보드](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard)에서 이 대상에 대한 활성화 정보를 봅니다.
> * [!UICONTROL 이름] 열에서 줄임표(`...`)를 선택하고 ![경고 구독 ](/help/images/icons/alert-add.png)**[!UICONTROL 경고 구독&#x200B;]**&#x200B;컨트롤을 사용하여 대상 데이터 흐름 경고를 구독합니다. 경고를 구독하면 플로우 실행의 상태, 성공 또는 실패와 관련된 메시지를 받을 수 있습니다. 대상 데이터 흐름 경고에 대한 자세한 내용은 [컨텍스트 내 대상 경고 구독](alerts.md)을 참조하십시오.

![탭 찾아보기](../assets/ui/workspace/browse-tab.png)

| 요소 | 설명 |
|---------|----------|
| 이름 | 이 대상에 대한 활성화 흐름에 제공한 이름입니다. 같은 열에 [!UICONTROL 활성화] 및 [!UICONTROL 대상 삭제] 컨트롤이 있습니다. |
| 데이터 유형 | 대상 연결에서 지원하는 데이터 유형입니다. 지원되는 데이터 유형: <ul><li>**[!UICONTROL 고객]**</li><li>**[!UICONTROL 잠재 고객]**</li><li>**[!UICONTROL 계정]**</li><li>**[!UICONTROL 데이터 세트]**</li></ul> |
| [!UICONTROL 마지막 데이터 흐름 실행 상태] | 마지막 데이터 흐름 실행의 상태입니다. 데이터 흐름 실행에 대한 자세한 내용은 [대상 세부 정보 보기](destination-details-page.md)를 참조하십시오. |
| [!UICONTROL 마지막 데이터 흐름 실행 날짜] | 마지막 데이터 흐름 실행이 발생한 시간 및 날짜. 데이터 흐름 실행에 대한 자세한 내용은 [대상 세부 정보 보기](destination-details-page.md)를 참조하십시오. |
| [!UICONTROL 대상] | 활성화 흐름에 대해 선택한 대상 플랫폼입니다. |
| [!UICONTROL 계정 만료일] | 이 대상에 대한 연결 인증이 만료되는 날짜입니다. <br>**중요**: 이 열은 현재 [Facebook](../catalog/social/facebook.md) 연결에만 사용할 수 있습니다. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상의 경우: S3, FTP 또는 [!DNL Azure Blob]일 수 있습니다.</li><li>실시간 광고 대상: 서버 간.</li><li>스트리밍 대상의 경우: [!DNL Azure Event Hubs] 또는 [!DNL Amazon Kinesis]일 수 있습니다.</li></ul> |
| [!UICONTROL 사용자 이름] | 대상 흐름에 대해 선택한 계정 자격 증명입니다. |
| [!UICONTROL 활성화 데이터] | 이 대상에 대해 활성화 중인 대상 수를 나타냅니다. 활성화된 대상자에 대한 자세한 내용을 확인하려면 이 컨트롤을 선택하십시오. 활성화된 대상에 대한 자세한 내용은 대상 세부 정보 페이지의 [활성화 데이터](/help/destinations/ui/destination-details-page.md#activation-data)를 참조하십시오. |
| [!UICONTROL 생성일] | 대상으로의 활성화 흐름이 생성된 날짜와 UTC 시간. 활성화 흐름을 가장 최근 첫 번째 또는 가장 오래된 순으로 정렬하려면 위쪽/아래쪽 화살표 기호를 선택합니다. |
| [!UICONTROL 상태] | `Enabled` 또는 `Disabled`. 이 대상에 대해 데이터가 활성화되는지 여부를 나타냅니다. |

대상 ID, 설명, 활성화된 대상 수 등과 같은 대상 정보를 오른쪽 레일에 표시하려면 대상 행을 클릭합니다.

![대상 행 클릭](../assets/ui/workspace/click-destination-row.png)

대상 이름을 선택하여 이 대상에 활성화된 대상에 대한 정보를 확인합니다. 이 대상으로 전송 중인 대상을 수정하거나 추가하려면 **[!UICONTROL 활성화 편집]**&#x200B;을 클릭하세요.

## [!UICONTROL 시스템 보기] {#system-view}

**[!UICONTROL 시스템 보기]** 탭에는 Adobe Experience Platform에서 설정한 활성화 흐름이 그래픽으로 표시됩니다.

![데이터 흐름1](../assets/ui/workspace/data-flows1.png)

페이지에 표시된 대상을 선택하고 **[!UICONTROL 데이터 흐름 보기]**&#x200B;를 클릭하여 각 대상에 대해 설정한 모든 연결에 대한 정보를 확인합니다.

![데이터 흐름2](../assets/ui/workspace/data-flows2.png)
