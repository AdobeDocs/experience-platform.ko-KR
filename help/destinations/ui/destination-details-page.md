---
keywords: 대상;대상;대상 세부 정보 페이지;대상 세부 정보 페이지
title: 대상 세부 사항 보기
description: '개별 대상에 대한 세부 사항 페이지에서는 대상 세부 사항에 대한 개요를 제공합니다. 대상 세부 사항에는 대상 이름, ID, 대상에 매핑된 세그먼트, 활성화를 편집하고 데이터 흐름을 활성화 및 비활성화하기 위한 컨트롤이 포함됩니다. '
seo-description: 개별 대상에 대한 세부 사항 페이지에서는 대상 세부 사항에 대한 개요를 제공합니다. 대상 세부 사항에는 대상 이름, ID, 대상에 매핑된 세그먼트, 활성화를 편집하고 데이터 흐름을 활성화 및 비활성화하기 위한 컨트롤이 포함됩니다.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
translation-type: tm+mt
source-git-commit: cc432f7c07f0f82deec653864154016638ec8138
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 대상 세부 사항 보기

## 개요 {#overview}

Adobe Experience Platform 사용자 인터페이스에서 대상의 속성 및 활동을 보고 모니터링할 수 있습니다. 이러한 세부 사항에는 대상의 이름 및 ID, 대상을 활성화 또는 비활성화하는 컨트롤 등이 포함됩니다. 일괄 처리 대상에 대한 세부 사항에는 활성화된 프로필 레코드에 대한 지표 및 데이터 흐름 실행 내역이 포함됩니다.

>[!NOTE]
>
>대상 세부 사항 페이지는 [!DNL Platform] [!DNL UI]의 [!UICONTROL Destinations] 작업 영역에 속합니다. 자세한 내용은 [[!UICONTROL Destinations] 작업 영역 개요](./destinations-workspace.md)를 참조하십시오.

## 대상 세부 사항 보기 {#view-details}

기존 대상에 대한 자세한 내용을 보려면 아래 단계를 따르십시오.

1. [Experience Platform UI](https://platform.adobe.com/)에 로그인하고 왼쪽 탐색 막대에서 **[!UICONTROL Destinations]**&#x200B;를 선택합니다. 상단 헤더에서 **[!UICONTROL Browse]**&#x200B;을 선택하여 기존 대상을 봅니다.

   ![검색 대상](../assets/ui/details-page/browse-destinations.png)

1. 정렬 패널을 시작하려면 왼쪽 상단에 있는 필터 아이콘 ![필터 아이콘](../assets/ui/details-page/filter.png)을 선택합니다. 정렬 패널은 모든 대상 목록을 제공합니다. 목록에서 대상을 두 개 이상 선택하여 선택한 대상과 연결된 데이터 흐름 필터링된 선택을 볼 수 있습니다.

   ![필터 대상](../assets/ui/details-page/filter-destinations.png)

1. 보려는 대상의 이름을 선택합니다.

   ![대상 선택](../assets/ui/details-page/destination-select.png)

1. 대상에 대한 세부 사항 페이지가 나타나고 사용 가능한 컨트롤이 표시됩니다. 배치 대상의 세부 사항을 보는 경우 모니터링 대시보드도 나타납니다.

   ![대상 세부 사항](../assets/ui/details-page/destination-details.png)

## 오른쪽 레일

오른쪽 레일에는 선택한 대상에 대한 기본 정보가 표시됩니다.

![오른쪽 레일](../assets/ui/details-page/right-sidebar.png)

다음 표에서는 오른쪽 레일에서 제공하는 컨트롤과 세부 사항을 설명합니다.

| 오른쪽 레일 항목 | 설명 |
| --- | --- |
| [!UICONTROL Activate] | 대상에 매핑되는 세그먼트를 편집하려면 이 컨트롤을 선택합니다. 자세한 내용은 [대상](./activate-destinations.md)에 세그먼트 활성화에 대한 안내서를 참조하십시오. |
| [!UICONTROL Delete] | 이 데이터 흐름을 삭제하고 이전에 활성화한 세그먼트(있는 경우)를 매핑 해제할 수 있습니다. |
| [!UICONTROL Destination name] | 대상 이름을 업데이트하려면 이 필드를 편집할 수 있습니다. |
| [!UICONTROL Description] | 대상에 선택적 설명을 업데이트하거나 추가하기 위해 이 필드를 편집할 수 있습니다. |
| [!UICONTROL Destination] | 대상이 전송되는 대상 플랫폼을 나타냅니다. 자세한 내용은 [대상 카탈로그](../catalog/overview.md)를 참조하십시오. |
| [!UICONTROL Status] | 대상이 활성화되었는지 여부를 나타냅니다. |
| [!UICONTROL Marketing actions] | 데이터 거버넌스 목적으로 이 대상에 적용되는 마케팅 작업(사용 사례)을 나타냅니다. |
| [!UICONTROL Category] | 대상 유형을 나타냅니다. 자세한 내용은 [대상 카탈로그](../catalog/overview.md)를 참조하십시오. |
| [!UICONTROL Connection type] | 대상을 대상으로 보내는 양식을 나타냅니다. 가능한 값은 [!UICONTROL Cookie] 및 [!UICONTROL Profile-based]입니다. |
| [!UICONTROL Frequency] | 대상이 대상으로 전송되는 빈도를 나타냅니다. 가능한 값은 [!UICONTROL Streaming] 및 [!UICONTROL Batch]입니다. |
| [!UICONTROL Identity] | 대상이 허용하는 ID 네임스페이스를 나타냅니다(예: `GAID`, `IDFA` 또는 `email`). 허용되는 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/namespaces.md)를 참조하십시오. |
| [!UICONTROL Created by] | 이 대상을 만든 사용자를 나타냅니다. |
| [!UICONTROL Created] | 이 대상을 만들 때의 UTC datetime을 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] 토글

**[!UICONTROL Enabled]/[!UICONTROL Disabled]** 토글을 사용하여 대상에 대한 모든 데이터 내보내기를 시작 및 일시 중지할 수 있습니다.

![토글 비활성화 사용](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

[!UICONTROL Dataflow runs] 탭은 데이터 흐름 실행에 대한 지표 데이터를 일괄 처리 대상으로 제공합니다. 자세한 내용은 [데이터 흐름 모니터링](monitor-dataflows.md)을 참조하십시오.

## [!UICONTROL Activation data] {#activation-data}

[!UICONTROL Activation data] 탭에는 시작 날짜 및 종료 날짜(해당하는 경우)를 포함하여 대상에 매핑된 세그먼트 목록이 표시됩니다. 특정 세그먼트에 대한 세부 사항을 보려면 목록에서 해당 이름을 선택합니다.

![정품 인증 데이터](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>세그먼트의 세부 사항 페이지를 탐색하는 방법에 대한 자세한 내용은 [세그멘테이션 UI 개요](../../segmentation/ui/overview.md#segment-details)를 참조하십시오.
