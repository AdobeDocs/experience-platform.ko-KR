---
title: 대상 작업 공간
seo-title: 대상 작업 공간
description: Adobe 실시간 고객 데이터 Platform의 왼쪽 탐색 막대에서 대상을 선택하여 대상 작업 영역에 액세스합니다.
seo-description: Adobe 실시간 고객 데이터 Platform의 왼쪽 탐색 막대에서 대상을 선택하여 대상 작업 영역에 액세스합니다.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 3%

---


# 대상 작업 공간 {#destinations-workspace}

Adobe 실시간 고객 데이터 Platform의 왼쪽 탐색 막대에서 **[!UICONTROL 대상]** 을 선택하여 대상 작업 [!UICONTROL 영역에] 액세스합니다.

작업 [!UICONTROL 공간은] 아래 섹션에 설명된 네 개의 섹션, **[!UICONTROL 카탈로그]**, **[!UICONTROL 검색]**&#x200B;계정, ********&#x200B;및 System ViewFacebook으로 구성됩니다.

![대상-개요](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL 카탈로그] {#catalog}

[ **[!UICONTROL 카탈로그]** ] 탭에는 데이터를 보낼 수 있는 Adobe에서 제공하는 모든 대상 목록이 표시됩니다.

페이지의 검색 기능을 사용하여 카테고리 컨트롤을 사용하여 특정 대상 또는 필터 대상을 **[!UICONTROL 찾습니다]** .

카탈로그에서 대상을 선택하여 오른쪽 레일을 엽니다. 여기에서 대상(**[!UICONTROL Connect 대상]**)에 대한 연결을 설정하거나, 기존 대상 연결(**[!UICONTROL 찾아보기 대상]**)을 보거나, 설명서를 보고 각 대상에 대한 자세한 정보(**[!UICONTROL 보기 설명서]**)를 확인할 수 있습니다.

![대상 카탈로그 옵션](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

각 대상에 대한 대상 카테고리 및 정보에 대한 자세한 내용은 [대상 카탈로그를 참조하십시오](/help/rtcdp/destinations/destinations-catalog.md).

## [!UICONTROL 찾아보기] {#browse}

[ **[!UICONTROL 찾아보기]** ] 탭에는 연결을 설정한 대상이 표시됩니다. 토글을 **[!UICONTROL 활성화한]** 대상은 대상을 활성으로, 그 반대의 경우는 활성으로 설정합니다. 세그먼트 > 찾아보기 **[!UICONTROL 를 선택하고 검사할 세그먼트를 선택하여 데이터]** 가 **[!UICONTROL 흐르는 대상을]** 볼 수도 있습니다. 검색 탭에서 각 대상에 대해 제공되는 모든 정보는 아래 표를 참조하십시오.

![검색 탭](/help/rtcdp/destinations/assets/browse-tab.png)

| 요소 | 설명 |
---------|----------
| 이름 | 활성화 과정을 위해 입력한 이름입니다. |
| [!UICONTROL 대상] | 정품 인증 과정을 위해 선택한 대상 플랫폼입니다. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상: S3 또는 FTP일 수 있습니다.</li><li>실시간 광고 대상: 서버 간</li></ul> |
| [!UICONTROL 사용자 이름] | 대상 플로우에 대해 선택한 계정 자격 증명. |
| [!UICONTROL 세그먼트] | 이 대상에 대해 활성화된 세그먼트 수입니다. |
| [!UICONTROL 작성일] | 대상으로 활성화 흐름을 만든 날짜 및 UTC 시간입니다. |
| [!UICONTROL 상태] | `Active` 또는 `Inactive`. 데이터가 현재 이 대상에 활성화되고 있는지 여부를 나타냅니다. 상태를 편집하려면 활성화 [비활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

오른쪽 레일의 대상에 대한 자세한 정보를 표시하려면 대상 행을 클릭합니다.

![대상 행 클릭](/help/rtcdp/destinations/assets/click-destination-row.png)

이 대상에 대해 활성화된 세그먼트에 대한 정보를 보려면 대상 이름을 선택합니다. 활성화 **[!UICONTROL 편집을]** 클릭하여 이 대상에 전송되는 세그먼트를 수정하거나 추가합니다.

## [!UICONTROL 계정] {#accounts}

계정 **[!UICONTROL 탭에서]** 다양한 대상으로 설정한 연결에 대해 자세히 알아볼 수 있습니다. 각 대상에 대한 모든 정보는 아래 표를 참조하십시오.

![계정 탭](/help/rtcdp/destinations/assets/accounts-tab.png)

| 요소 | 설명 |
---------|----------
| [!UICONTROL 플랫폼] | 연결을 설정한 대상. |
| [!UICONTROL 연결 유형] | 저장소 버킷 또는 대상에 대한 연결 유형을 나타냅니다. <ul><li>이메일 마케팅 대상: S3 또는 FTP일 수 있습니다.</li><li>실시간 광고 대상: 서버 간</li><li>Amazon S3 클라우드 스토리지 대상: 액세스 키 </li><li>SFTP 클라우드 스토리지 대상: SFTP에 대한 기본 인증</li></ul> |
| [!UICONTROL 사용자 이름] | 연결 대상 마법사에서 선택한 [사용자 이름입니다](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination). |
| [!UICONTROL 데이터 흐름] | 대상에 대해 만들어진 기본 정보와 연결된 고유한 성공한 대상 흐름 수를 나타냅니다. |
| [!UICONTROL 인증됨] | 이 대상에 대한 연결이 승인된 날짜입니다. |
| [!UICONTROL 상태] | `Active` 또는 `Inactive`. 데이터가 현재 이 대상에 활성화되고 있는지 여부를 나타냅니다. 상태를 편집하려면 활성화 [비활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL 시스템 보기] {#system-view}

[ **[!UICONTROL 시스템 보기]** ] 탭에는 실시간 고객 데이터 Platform에서 설정한 활성화 흐름을 그래픽으로 표시합니다.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

페이지에 표시되는 대상을 선택하고 **[!UICONTROL 보기 흐름을]** 눌러 각 대상에 대해 설정한 모든 연결에 대한 정보를 확인합니다.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)