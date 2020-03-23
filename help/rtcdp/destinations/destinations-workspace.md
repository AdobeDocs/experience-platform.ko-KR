---
title: 대상 작업 영역
seo-title: 대상 작업 영역
description: Adobe 실시간 고객 데이터 플랫폼의 경우 왼쪽 탐색 막대에서 대상을 선택하여 대상 작업 영역에 액세스합니다.
seo-description: Adobe 실시간 고객 데이터 플랫폼의 경우 왼쪽 탐색 막대에서 대상을 선택하여 대상 작업 영역에 액세스합니다.
translation-type: tm+mt
source-git-commit: 132bc9787a86045adba559c769b02927a6045b17

---


# 대상 작업 영역 {#destinations-workspace}

Adobe의 실시간 고객 데이터 플랫폼의 왼쪽 탐색 **모음에서** 대상을 선택하여 대상 작업 영역에 액세스합니다.

대상 작업 영역은 카탈로그, **검색**, **계정**, **데이터**&#x200B;흐름 **,**&#x200B;아래 섹션에 설명된 네 가지 섹션으로 구성됩니다.

![대상-개요](/help/rtcdp/destinations/assets/destinations-overview.png)

## 카탈로그 {#catalog}

이 **[!UICONTROL Catalog]** 탭에는 데이터를 보낼 수 있는 Adobe에서 제공하는 모든 대상 목록이 표시됩니다. 카탈로그에서 대상을 선택하여 오른쪽 레일을 엽니다. 여기에서 대상(Connect 대상&#x200B;**)에 대한 연결을 설정하거나 설명서를 참조하여 각**&#x200B;대상에&#x200B;**대한 자세한 정보를 확인할 수**&#x200B;있습니다(문서보기).

![대상 카탈로그 옵션](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

각 대상에 대한 대상 카테고리 및 정보에 대한 자세한 내용은 대상 카탈로그를 [참조하십시오](/help/rtcdp/destinations/destinations-catalog.md).

## 검색 {#browse}

이 **[!UICONTROL Browse]** 탭에는 사용자가 연결을 설정한 대상이 표시됩니다. 토글이 활성화된 대상은 활성으로, 반대의 경우는 활성으로 설정합니다. 세그먼트 > 찾아보기를 선택하고 검사할 세그먼트를 선택하여 데이터가 **흐르는 대상을** 볼 수도 있습니다. 찾아보기 탭에서 각 대상에 대해 제공된 모든 정보는 아래 표를 참조하십시오.

![검색 탭](/help/rtcdp/destinations/assets/browse-tab.png)

| 요소 | 설명 |
---------|----------
| 대상 이름 | 활성화 과정을 위해 제공한 이름을 이 대상으로 보냅니다. |
| 대상 | 활성화 흐름에 대해 선택한 대상 플랫폼. |
| 생성됨 | 대상으로 정품 인증 흐름을 만든 날짜 및 UTC 시간입니다. |
| 연결 유형 | *이메일 마케팅 목적지에만*&#x200B;해당합니다. 저장소 버킷에 대한 연결 유형을 나타냅니다. S3 또는 FTP일 수 있습니다. |
| 사용자 이름 | 대상 흐름에 대해 선택한 계정 자격 증명. |
| 세그먼트 | 이 대상에 대해 활성화되는 세그먼트 수입니다. |
| 상태 | `Active` 또는 `Inactive`. 데이터가 현재 이 대상에 대해 활성화되고 있는지 여부를 나타냅니다. 상태를 편집하려면 활성화 [비활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

오른쪽 레일의 대상에 대한 자세한 정보를 표시하려면 대상 행을 클릭합니다.

![대상 행 클릭](/help/rtcdp/destinations/assets/click-destination-row.png)

이 대상에 대해 활성화된 세그먼트에 대한 정보를 보려면 대상 이름을 선택합니다. 을 **[!UICONTROL Edit activation]** 클릭하여 이 대상으로 전송되는 세그먼트를 수정하거나 추가합니다.

## 계정{#accounts}에서 제공합니다 

탭에서 다양한 대상으로 설정한 연결에 대해 자세히 알아볼 수 있습니다. **[!UICONTROL Accounts]** 각 대상에 대한 모든 정보는 아래 표를 참조하십시오.

![계정 탭](/help/rtcdp/destinations/assets/accounts-tab.png)

| 요소 | 설명 |
---------|----------
| 플랫폼 | 연결을 설정한 대상. |
| 사용자 이름 | [연결 대상 마법사에서](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)선택한 사용자 이름입니다. |
| 흐름 | 대상에 대해 생성된 기본 정보와 연결된 고유한 성공적인 대상 흐름 수를 나타냅니다. |
| 인증됨 | 이 대상에 대한 연결이 인증된 날짜입니다. |

## 데이터 흐름 {#data-flows}

이 **[!UICONTROL Data flows]** 탭에는 실시간 고객 데이터 플랫폼에서 설정한 활성화 흐름을 그래픽으로 표시합니다.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

페이지에 표시된 대상을 선택하고 키를 **[!UICONTROL View flows]** 눌러 각 대상에 대해 설정한 모든 데이터 흐름에 대한 정보를 봅니다.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)