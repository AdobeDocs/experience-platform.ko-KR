---
keywords: 플랫폼;대상;대상 작업 영역;작업 영역;ui;대상 ui;카탈로그;대상 카탈로그;platform;destinations;destinations;destinations workspace;workspace;ui;destinations ui;catalog;destinations catalog catalog
title: 대상 작업 공간 개요
description: 대상 작업 공간은 아래의 섹션에 설명된 4개의 섹션인 카탈로그, 찾아보기, 계정 및 시스템 보기로 구성됩니다.
seo-description: Adobe Experience Platform의 왼쪽 탐색 막대에서 대상을 선택하여 대상 작업 영역에 액세스합니다.
translation-type: tm+mt
source-git-commit: 37b0ec0e04c45cb065eca9d262249016e80655ef
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 2%

---


# 대상 작업 공간 개요 {#destinations-workspace}

Adobe Experience Platform의 왼쪽 탐색 막대에서 **[!UICONTROL 대상]**&#x200B;을 선택하여 [!UICONTROL 대상] 작업 영역에 액세스합니다.

[!UICONTROL 대상] 작업 공간은 아래 섹션에 설명된 4개의 섹션, [!UICONTROL 카탈로그], [!UICONTROL 찾아보기], [!UICONTROL 계정] 및 [!UICONTROL 시스템 보기]로 구성됩니다.

![대상-개요](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 카탈로그] {#catalog}

**[!UICONTROL 카탈로그]** 탭에는 데이터를 보낼 수 있는 플랫폼에서 사용할 수 있는 모든 대상 목록이 표시됩니다.

플랫폼 사용자 인터페이스는 대상 카탈로그 페이지에 다양한 검색 및 필터 옵션을 제공합니다.

* 페이지의 검색 기능을 사용하여 특정 대상을 찾습니다.
* [!UICONTROL 범주] 컨트롤을 사용하여 대상을 필터링합니다.
* [!UICONTROL 모든 대상]과 [!UICONTROL 내 대상] 간을 전환합니다. **[!UICONTROL 모든 대상]**&#x200B;을 선택하면 사용 가능한 모든 플랫폼 대상이 표시됩니다. **[!UICONTROL 내 대상]**&#x200B;을 선택하면 사용자가 연결을 설정한 대상만 볼 수 있습니다.
* **[!UICONTROL 연결]** 및/또는 **[!UICONTROL 확장]**&#x200B;을 보려면 선택합니다. 두 카테고리 간의 차이를 이해하려면 [대상 유형과 카테고리](../destination-types.md)를 참조하십시오.

![대상 필터링 및 검색 데모](../assets/ui/workspace/destinations-search-and-filter.gif)

대상 카드에는 **[!UICONTROL Configure]** 또는 **[!UICONTROL Activate]** 컨트롤과 추가 옵션을 표시하는 보조 컨트롤이 포함되어 있습니다. 이러한 모든 내용은 아래에 설명되어 있습니다.

| 제어 | 설명 |
---------|----------
|  구성 | 대상에 대한 연결을 만들 수 있습니다. |
| [!UICONTROL 활성화] | 대상에 대한 연결을 설정했으면 세그먼트를 활성화할 수 있습니다. |
| [!UICONTROL 계정 보기] | 대상에 대해 연결한 계정을 봅니다. |
| [!UICONTROL 데이터 흐름 보기] | 대상에 대해 존재하는 데이터 활성화 흐름을 봅니다. |
| [!UICONTROL 설명서 보기] | 특정 대상에 대한 문서 페이지에 대한 링크를 열고 자세한 정보를 확인하고 설정을 도와줍니다. |

![대상 카드의 컨트롤](../assets/ui/workspace/destination-card-options.png)

카탈로그에서 대상 카드를 선택하여 오른쪽 레일을 엽니다.  여기에서 대상에 대한 설명을 볼 수 있습니다. 오른쪽 레일은 위 표에 설명된 것과 동일한 컨트롤, 대상에 대한 설명, 대상 카테고리 및 유형을 표시합니다.

![대상 카탈로그 옵션](../assets/ui/workspace/destination-right-rail.png)

각 대상에 대한 대상 카테고리 및 정보에 대한 자세한 내용은 [대상 카탈로그](../catalog/overview.md) 및 [대상 유형 및 카테고리](../destination-types.md)를 참조하십시오.

## [!UICONTROL 계정] {#accounts}

**[!UICONTROL 계정]** 탭에서 다양한 대상으로 설정한 연결에 대해 자세히 알아볼 수 있습니다. 각 대상에 대한 모든 정보는 아래 표를 참조하십시오.

>[!TIP]
>
>**[!UICONTROL 플랫폼]** 열에 있는 ![데이터 추가 단추](../assets/ui/workspace/add-data-symbol.png) 단추를 사용하여 해당 계정에 대한 새 대상 연결을 만듭니다.

![계정 탭](../assets/ui/workspace/edit-account-destinations.png)

| 요소 | 설명 |
---------|----------
| [!UICONTROL 플랫폼] | 연결을 설정한 대상. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상:S3 또는 FTP일 수 있습니다.</li><li>실시간 광고 대상:서버 간</li><li>Amazon S3 클라우드 스토리지 대상:액세스 키 </li><li>SFTP 클라우드 스토리지 대상:SFTP에 대한 기본 인증</li></ul> |
| [!UICONTROL 사용자 이름] | [연결 대상 마법사](../catalog/email-marketing/overview.md#connect-destination)에서 선택한 사용자 이름입니다. |
| [!UICONTROL 대상] | 대상에 대해 만들어진 기본 정보와 연결된 고유한 성공적인 대상 흐름 수를 나타냅니다. |
| [!UICONTROL 인증됨] | 이 대상에 대한 연결이 허가된 날짜입니다. |

또한 계정 정보를 편집하거나 업데이트할 수 있습니다. 계정의 정보를 편집하려면 **[!UICONTROL 플랫폼]** 열에서 ![계정 편집 단추](../assets/ui/workspace/pencil-icon.png)를 선택합니다.

`OAuth2` 연결 유형을 사용하는 계정의 경우 **[!UICONTROL OAuth]**&#x200B;에 다시 연결을 선택하여 계정 자격 증명을 갱신할 수 있습니다.

![Oauth 이미지](../assets/ui/workspace/reconnect-oauth.png)

`Access Key` 또는 `ConnectionString` 연결 유형을 사용하는 계정의 경우 액세스 ID, 비밀 키 또는 연결 문자열 등의 정보를 포함하여 계정 인증 정보를 편집할 수 있습니다.

![계정 정보 이미지](../assets/ui/workspace/edit-account-details.png)

계정 세부 사항 편집이 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택하여 업데이트를 완료합니다.

## [!UICONTROL 찾아보기] {#browse}

**[!UICONTROL 찾아보기]** 탭에는 사용자가 연결을 설정한 대상이 표시됩니다. **[!UICONTROL Enabled]** 토글이 켜져 있는 대상(대상을 활성으로 또는 그 반대로 설정합니다. 또한 **[!UICONTROL 세그먼트]** > **[!UICONTROL 찾아보기]**&#x200B;를 선택하고 검사할 세그먼트를 선택하여 데이터가 흐르는 대상을 볼 수도 있습니다. 찾아보기 탭의 각 대상에 대해 제공되는 모든 정보는 아래 표를 참조하십시오.

>[!TIP]
>
> * **[!UICONTROL 이름]** 열에 있는 ![세그먼트 추가 단추](../assets/ui/workspace/add-data-symbol.png) 단추를 사용하여 해당 대상에 대한 추가 세그먼트를 활성화합니다.
> * 대상에 대한 기존 연결을 삭제하려면 **[!UICONTROL 이름]** 열에 있는 ![대상 삭제 단추](../assets/ui/workspace/delete-destination-symbol.png) 단추를 사용합니다.


![검색 탭](../assets/ui/workspace/browse-tab.png)

| 요소 | 설명 |
---------|----------
| 이름 | 활성화 과정을 위해 입력한 이름이 이 대상으로 전송됩니다. 동일한 열에는 2개의 컨트롤이 있습니다. 및 [!UICONTROL 대상 삭제]를 활성화합니다. |
| 마지막 흐름 실행 상태 | 마지막 데이터 흐름 실행의 상태입니다. 데이터 흐름 실행에 대한 자세한 내용은 [대상 세부 사항 보기](destination-details-page.md)를 참조하십시오. |
| 마지막 흐름 실행 날짜 | 마지막 데이터 흐름 실행이 발생한 시간 및 날짜입니다. 데이터 흐름 실행에 대한 자세한 내용은 [대상 세부 사항 보기](destination-details-page.md)를 참조하십시오. |
| [!UICONTROL 대상] | 정품 인증 과정에 대해 선택한 대상 플랫폼입니다. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상:S3, FTP 또는 [!DNL Azure Blob]일 수 있습니다.</li><li>실시간 광고 대상:서버 간</li><li>스트리밍 대상:[!DNL Azure Event Hubs] 또는 [!DNL Amazon Kinesis]일 수 있습니다.</li></ul> |
| [!UICONTROL 사용자 이름] | 대상 플로우에 대해 선택한 계정 자격 증명입니다. |
| [!UICONTROL 활성화 데이터] | 이 대상에 대해 활성화되는 세그먼트 수를 나타냅니다. 활성화된 세그먼트에 대한 자세한 내용을 보려면 이 컨트롤을 선택합니다. 활성화된 세그먼트에 대한 자세한 내용은 대상 세부 정보 페이지에서 [활성화 데이터](/help/destinations/ui/destination-details-page.md#activation-data)를 참조하십시오. |
| [!UICONTROL 작성일] | 대상으로 활성화 흐름이 만들어진 날짜 및 UTC 시간입니다. |
| [!UICONTROL 상태] | `Active` 또는 `Inactive`. 데이터가 현재 이 대상에 대해 활성화되고 있는지 여부를 나타냅니다. 상태를 편집하려면 [활성화 비활성화](./activate-destinations.md#disable-activation)를 참조하십시오. |

오른쪽 레일의 대상에 대한 자세한 정보를 표시하려면 대상 행을 클릭합니다.

![대상 행 클릭](../assets/ui/workspace/click-destination-row.png)

이 대상에 대해 활성화된 세그먼트에 대한 정보를 보려면 대상 이름을 선택합니다. **[!UICONTROL 활성화 편집]**&#x200B;을 클릭하여 이 대상으로 전송되는 세그먼트를 수정하거나 추가합니다.

## [!UICONTROL 시스템 보기] {#system-view}

**[!UICONTROL 시스템 보기]** 탭에는 Adobe Experience Platform에서 설정한 활성화 흐름의 그래픽 표현이 표시됩니다.

![데이터 흐름1](../assets/ui/workspace/data-flows1.png)

페이지에 표시되는 대상을 선택하고 **[!UICONTROL 흐름 보기]**&#x200B;를 클릭하여 각 대상에 대해 설정한 모든 연결에 대한 정보를 봅니다.

![데이터 흐름2](../assets/ui/workspace/data-flows2.png)