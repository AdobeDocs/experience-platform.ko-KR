---
keywords: 대상;대상;대상 세부 정보 페이지;대상 세부 정보 페이지
title: 대상 세부 사항 보기
description: '개별 대상에 대한 세부 사항 페이지에서는 대상 세부 사항에 대한 개요를 제공합니다. 대상 세부 사항에는 대상 이름, ID, 대상에 매핑된 세그먼트 및 활성화를 편집하고 데이터 흐름을 활성화 및 비활성화하는 컨트롤이 포함됩니다. '
seo-description: 개별 대상에 대한 세부 사항 페이지에서는 대상 세부 사항에 대한 개요를 제공합니다. 대상 세부 사항에는 대상 이름, ID, 대상에 매핑된 세그먼트 및 활성화를 편집하고 데이터 흐름을 활성화 및 비활성화하는 컨트롤이 포함됩니다.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# 대상 세부 사항 보기

## 개요 {#overview}

Adobe Experience Platform 사용자 인터페이스에서 대상의 속성 및 활동을 보고 모니터링할 수 있습니다. 이러한 세부 사항에는 대상의 이름 및 ID, 대상을 활성화하거나 비활성화하는 컨트롤 등이 포함됩니다. 배치 대상에 대한 세부 사항에는 활성화된 프로필 레코드에 대한 지표와 데이터 흐름 실행 내역이 포함됩니다.

>[!NOTE]
>
>대상 세부 사항 페이지는 [!DNL Platform] [!DNL UI]에 있는 [!UICONTROL 대상] 작업 공간의 일부입니다. 자세한 내용은 [[!UICONTROL 대상] 작업 공간 개요](./destinations-workspace.md)를 참조하십시오.

## 대상 세부 사항 보기 {#view-details}

기존 대상에 대한 자세한 내용을 보려면 아래 절차를 따르십시오.

1. [Experience Platform UI](https://platform.adobe.com/)에 로그인하고 왼쪽 탐색 막대에서 **[!UICONTROL 대상]**&#x200B;을 선택합니다. 기존 대상을 보려면 상단 헤더에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택하십시오.

   ![찾아보기 대상](../assets/ui/details-page/browse-destinations.png)

1. 왼쪽 상단에 있는 필터 아이콘 ![필터-아이콘](../assets/ui/details-page/filter.png)을 선택하여 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상 목록을 제공합니다. 목록에서 둘 이상의 대상을 선택하여 선택한 대상과 연관된 필터링된 데이터 흐름 선택을 볼 수 있습니다.

   ![필터 대상](../assets/ui/details-page/filter-destinations.png)

1. 보려는 대상의 이름을 선택합니다.

   ![대상 선택](../assets/ui/details-page/destination-select.png)

1. 대상에 대한 세부 정보 페이지가 나타나고 사용 가능한 컨트롤이 표시됩니다. 배치 대상의 세부 정보를 볼 경우 모니터링 대시보드도 나타납니다.

   ![대상 세부 사항](../assets/ui/details-page/destination-details.png)

## 오른쪽 레일

오른쪽 레일에는 선택한 대상에 대한 기본 정보가 표시됩니다.

![오른쪽 레일](../assets/ui/details-page/right-sidebar.png)

다음 표는 오른쪽 레일에서 제공하는 컨트롤과 세부 사항을 다룹니다.

| 오른쪽 레일 항목 | 설명 |
| --- | --- |
| [!UICONTROL 활성화] | 대상에 매핑되는 세그먼트를 편집하려면 이 컨트롤을 선택합니다. 자세한 내용은 [대상 데이터를 세그먼트 스트리밍 대상에 활성화](./activate-segment-streaming-destinations.md), [대상 데이터를 배치 프로필 기반 대상으로 활성화](./activate-batch-profile-destinations.md) 및 [대상 데이터를 스트리밍 프로필 기반 대상으로 활성화](./activate-streaming-profile-destinations.md)에 대한 안내서를 참조하십시오. |
| [!UICONTROL 삭제] | 이 데이터 흐름을 삭제하고 이전에 활성화한 세그먼트(있는 경우)의 매핑을 해제할 수 있습니다. |
| [!UICONTROL 대상 이름] | 대상 이름을 업데이트하기 위해 이 필드를 편집할 수 있습니다. |
| [!UICONTROL 설명] | 이 필드를 편집하여 대상에 선택적 설명을 업데이트하거나 추가할 수 있습니다. |
| [!UICONTROL 대상] | 대상이 전송되는 대상 플랫폼을 나타냅니다. 자세한 내용은 [대상 카탈로그](../catalog/overview.md)를 참조하십시오. |
| [!UICONTROL 상태] | 대상이 활성화되었는지 여부를 나타냅니다. |
| [!UICONTROL 마케팅 작업] | 데이터 거버넌스 목적으로 이 대상에 적용되는 마케팅 작업(사용 사례)을 나타냅니다. |
| [!UICONTROL 카테고리] | 대상 유형을 나타냅니다. 자세한 내용은 [대상 카탈로그](../catalog/overview.md)를 참조하십시오. |
| [!UICONTROL 연결 유형] | 대상이 대상으로 전송되는 양식을 나타냅니다. 가능한 값에는 [!UICONTROL 쿠키] 및 [!UICONTROL 프로필 기반]이 포함됩니다. |
| [!UICONTROL 빈도] | 대상이 대상으로 전송되는 빈도를 나타냅니다. 가능한 값에는 [!UICONTROL 스트리밍] 및 [!UICONTROL 일괄 처리]가 포함됩니다. |
| [!UICONTROL ID] | `GAID`, `IDFA` 또는 `email`와 같이 대상에서 허용하는 ID 네임스페이스를 나타냅니다. 허용되는 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/namespaces.md)를 참조하십시오. |
| [!UICONTROL 작성자] | 이 대상을 만든 사용자를 나타냅니다. |
| [!UICONTROL 생성됨] | 이 대상을 만들 때의 UTC 날짜/시간을 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL 활성화됨]/ 비활성화됨 전환

**[!UICONTROL Enabled]/[!UICONTROL Disabled]** 전환을 사용하여 모든 데이터 내보내기를 대상으로 시작 및 일시 중지할 수 있습니다.

![비활성화 토글 사용](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL 데이터 흐름 실행]

[!UICONTROL 데이터 흐름 실행] 탭은 데이터 흐름 실행 시 지표 데이터를 배치 대상으로 제공합니다. 자세한 내용은 [데이터 흐름 모니터링](monitor-dataflows.md)을 참조하십시오.

## [!UICONTROL 활성화 데이터] {#activation-data}

[!UICONTROL 활성화 데이터] 탭에는 시작 날짜와 종료 날짜(해당하는 경우)를 포함하여 대상에 매핑된 세그먼트 목록이 표시됩니다. 특정 세그먼트에 대한 세부 사항을 보려면 목록에서 해당 이름을 선택합니다.

![활성화 데이터](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>세그먼트의 세부 사항 페이지 탐색에 대한 자세한 내용은 [세그멘테이션 UI 개요](../../segmentation/ui/overview.md#segment-details) 를 참조하십시오.
