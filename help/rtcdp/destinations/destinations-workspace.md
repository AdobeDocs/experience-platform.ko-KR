---
keywords: RTCDP;rtcdp
title: 대상 작업 공간
seo-title: 대상 작업 공간
description: 대상 작업 공간은 아래의 섹션에 설명된 네 개의 섹션인 카탈로그, 찾아보기, 계정 및 시스템 보기로 구성됩니다.
seo-description: 실시간 고객 데이터 플랫폼의 경우 왼쪽 탐색 막대에서 대상을 선택하여 대상 작업 영역에 액세스합니다.
translation-type: tm+mt
source-git-commit: a3e35dee98b7b2758a4246a63bb0e1bde6b2f165
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 2%

---


# 대상 작업 공간 {#destinations-workspace}

실시간 고객 데이터 플랫폼의 경우 왼쪽 탐색 막대에서 **[!UICONTROL 대상]** 을 선택하여 대상 작업 [!UICONTROL 영역에] 액세스합니다.

작업 [!UICONTROL 공간은] 아래 섹션에 설명된 네 개의 섹션, [!UICONTROL 카탈로그], [!UICONTROL 검색]계정, 및 System ViewFacebook으로 구성됩니다.

![대상-개요](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL 카탈로그] {#catalog}

[ **[!UICONTROL 카탈로그]** ] 탭에는 데이터를 보낼 수 있는 실시간 CDP에서 사용할 수 있는 모든 대상 목록이 표시됩니다.

실시간 CDP 사용자 인터페이스는 대상 카탈로그 페이지에 다양한 검색 및 필터 옵션을 제공합니다.

* 페이지의 검색 기능을 사용하여 특정 대상을 찾습니다.
* 카테고리 컨트롤을 사용하여 [!UICONTROL 대상을] 필터링합니다.
* 모든 [!UICONTROL 대상] 및 [!UICONTROL 내 대상 간을 전환합니다]. 모든 **[!UICONTROL 대상을]** 선택하면 사용 가능한 모든 실시간 CDP 대상이 표시됩니다. 내 **[!UICONTROL 대상을]** 선택하면 사용자가 연결을 설정한 대상만 볼 수 있습니다.
* 연결 및/ **[!UICONTROL 또는 확장]** 기능을 보려면 **[!UICONTROL 선택합니다]**. 두 카테고리 간의 차이를 이해하려면 [대상 유형과 카테고리를 참조하십시오](/help/rtcdp/destinations/destination-types.md).

![대상 필터링 및 검색 데모](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

대상 카드에는 **[!UICONTROL 구성]** 또는 **[!UICONTROL 활성화]** 컨트롤과 더 많은 옵션을 표시하는 보조 컨트롤이 포함되어 있습니다. 다음은 모두 아래에 설명되어 있습니다.

| 컨트롤 | 설명 |
---------|----------
|  구성 | 대상에 대한 연결을 만들 수 있습니다. |
| [!UICONTROL 활성화] | 대상에 대한 연결을 설정했으면 세그먼트를 활성화할 수 있습니다. |
| [!UICONTROL 계정 보기] | 대상에 대해 연결한 계정을 봅니다. |
| [!UICONTROL 데이터 흐름 보기] | 대상에 대해 존재하는 데이터 활성화 흐름을 봅니다. |
| [!UICONTROL 설명서 보기] | 특정 대상에 대한 문서 페이지에 대한 링크를 열고 자세한 내용을 확인하고 설정을 지원합니다. |

![대상 카드의 컨트롤](/help/rtcdp/destinations/assets/destination-card-options.png)

카탈로그에서 대상 카드를 선택하여 오른쪽 레일을 엽니다.  여기, 대상에 대한 설명을 볼 수 있습니다. 오른쪽 레일은 위 표에 설명된 것과 동일한 컨트롤, 대상에 대한 설명, 대상 카테고리 및 유형의 표시를 제공합니다.

![대상 카탈로그 옵션](/help/rtcdp/destinations/assets/destination-right-rail.png)

각 대상에 대한 대상 카테고리 및 정보에 대한 자세한 내용은 [대상 카탈로그](/help/rtcdp/destinations/destinations-catalog.md) 및 [대상 유형 및 카테고리를 참조하십시오](/help/rtcdp/destinations/destination-types.md).

## [!UICONTROL 계정] {#accounts}

계정 **[!UICONTROL 탭에서]** 다양한 대상으로 설정한 연결에 대해 자세히 알아볼 수 있습니다. 각 대상에 대한 모든 정보는 아래 표를 참조하십시오.

>[!TIP]
>
>[ ![플랫폼](/help/rtcdp/destinations/assets/add-data-symbol.png) ] 열의 [데이터 추가] 단추 **** 단추를 사용하여 해당 계정에 대한 새 대상 연결을 만듭니다.

![계정 탭](./assets/workspace/edit-account-destinations.png)

| 요소 | 설명 |
---------|----------
| [!UICONTROL 플랫폼] | 연결을 설정한 대상. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상:S3 또는 FTP일 수 있습니다.</li><li>실시간 광고 대상:서버 간</li><li>Amazon S3 클라우드 스토리지 대상:액세스 키 </li><li>SFTP 클라우드 스토리지 대상:SFTP에 대한 기본 인증</li></ul> |
| [!UICONTROL 사용자 이름] | 연결 대상 마법사에서 선택한 [사용자 이름입니다](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination). |
| [!UICONTROL 대상] | 대상에 대해 만들어진 기본 정보와 연결된 고유한 성공한 대상 흐름 수를 나타냅니다. |
| [!UICONTROL 인증됨] | 이 대상에 대한 연결이 승인된 날짜입니다. |

또한 계정 정보를 편집하거나 업데이트할 수 있습니다. [ ![플랫폼](./assets/workspace/pencil-icon.png) ] 열에서 [계정 편집] 단추 **** 를 선택하여 계정 정보를 편집합니다.

연결 유형을 사용하는 계정의 경우 `OAuth2` OAuth **[!UICONTROL 재연결을 선택하여 계정 자격 증명을]** 갱신할 수 있습니다.

![Oauth 이미지](./assets/workspace/reconnect-oauth.png)

액세스 ID, 비밀 키 또는 연결 문자열 등의 정보를 포함하여 `Access Key` 또는 `ConnectionString` 연결 유형을 사용하는 계정의 계정 인증 정보를 편집할 수 있습니다.

![계정 정보 이미지](./assets/workspace/edit-account-details.png)

계정 세부 사항 편집이 끝나면 **[!UICONTROL 저장을 선택하여]** 업데이트를 완료합니다.

## [!UICONTROL 찾아보기] {#browse}

[ **[!UICONTROL 찾아보기]** ] 탭에는 연결을 설정한 대상이 표시됩니다. 활성화 **[!UICONTROL 토글이]** 켜져 있는 대상은 대상을 활성으로 또는 그 반대로 설정합니다. 세그먼트 > 찾아보기 **[!UICONTROL 를 선택하고 검사할 세그먼트를 선택하여 데이터]** 가 **[!UICONTROL 흐르는 대상을]** 볼 수도 있습니다. 검색 탭에서 각 대상에 대해 제공되는 모든 정보는 아래 표를 참조하십시오.

>[!TIP]
>
>이름 ![열의 데이터 추가 단추](/help/rtcdp/destinations/assets/add-data-symbol.png) 단추 **[!UICONTROL 를]** 사용하여 해당 대상에 대한 추가 세그먼트를 활성화합니다.

![검색 탭](/help/rtcdp/destinations/assets/browse-tab.png)

| 요소 | 설명 |
---------|----------
| 이름 | 활성화 과정을 위해 입력한 이름입니다. |
| [!UICONTROL 대상] | 정품 인증 과정을 위해 선택한 대상 플랫폼입니다. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상:S3 또는 FTP일 수 있습니다.</li><li>실시간 광고 대상:서버 간</li></ul> |
| [!UICONTROL 사용자 이름] | 대상 플로우에 대해 선택한 계정 자격 증명. |
| [!UICONTROL 세그먼트] | 이 대상에 대해 활성화된 세그먼트 수입니다. |
| [!UICONTROL 작성일] | 대상으로 활성화 흐름을 만든 날짜 및 UTC 시간입니다. |
| [!UICONTROL 상태] | `Active` 또는 `Inactive`. 데이터가 현재 이 대상에 활성화되고 있는지 여부를 나타냅니다. 상태를 편집하려면 활성화 [비활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

오른쪽 레일의 대상에 대한 자세한 정보를 표시하려면 대상 행을 클릭합니다.

![대상 행 클릭](/help/rtcdp/destinations/assets/click-destination-row.png)

이 대상에 대해 활성화된 세그먼트에 대한 정보를 보려면 대상 이름을 선택합니다. 활성화 **[!UICONTROL 편집을]** 클릭하여 이 대상에 전송되는 세그먼트를 수정하거나 추가합니다.

## [!UICONTROL 시스템 보기] {#system-view}

[ **[!UICONTROL 시스템 보기]** ] 탭에는 실시간 고객 데이터 플랫폼에서 설정한 활성화 흐름을 그래픽으로 표시합니다.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

페이지에 표시되는 대상을 선택하고 **[!UICONTROL 보기 흐름을]** 눌러 각 대상에 대해 설정한 모든 연결에 대한 정보를 확인합니다.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)