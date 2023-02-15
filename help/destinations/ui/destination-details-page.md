---
keywords: 대상;대상;대상 세부 정보 페이지;대상 세부 정보 페이지
title: 대상 세부 사항 보기
description: 개별 대상에 대한 세부 사항 페이지에서는 대상 세부 사항에 대한 개요를 제공합니다. 대상 세부 사항에는 대상 이름, ID, 대상에 매핑된 세그먼트 및 활성화를 편집하고 데이터 흐름을 활성화 및 비활성화하는 컨트롤이 포함됩니다.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a84d67e433d70cc6194ca20abc656e4b141d42a6
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# 대상 세부 사항 보기

## 개요 {#overview}

Adobe Experience Platform 사용자 인터페이스에서 대상의 속성 및 활동을 보고 모니터링할 수 있습니다. 이러한 세부 사항에는 대상의 이름 및 ID, 대상을 활성화하거나 비활성화하는 컨트롤 등이 포함됩니다. 세부 정보에는 활성화된 프로필 레코드, 활성화된 ID, 실패 및 제외에 대한 지표 및 데이터 흐름 실행 내역이 포함됩니다.

>[!NOTE]
>
>대상 세부 사항 페이지는 [!UICONTROL 대상] 작업 영역 [!DNL Platform] [!DNL UI]. 자세한 내용은 [[!UICONTROL 대상] 작업 공간 개요](./destinations-workspace.md) 추가 정보.

## 대상 세부 사항 보기 {#view-details}

기존 대상에 대한 자세한 내용을 보려면 아래 절차를 따르십시오.

1. 에 로그인합니다. [Experience Platform UI](https://platform.adobe.com/) 을(를) 선택합니다. **[!UICONTROL 대상]** 왼쪽 탐색 막대에서 을 클릭합니다. 선택 **[!UICONTROL 찾아보기]** 기존 대상을 보려면 상단 헤더에서 클릭하십시오.

   ![찾아보기 대상](../assets/ui/details-page/browse-destinations.png)

1. 필터 아이콘을 선택합니다 ![Filter-icon](../assets/ui/details-page/filter.png) 왼쪽 상단에서 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상 목록을 제공합니다. 목록에서 둘 이상의 대상을 선택하여 선택한 대상과 연관된 필터링된 데이터 흐름 선택을 볼 수 있습니다.

   ![필터 대상](../assets/ui/details-page/filter-destinations.png)

1. 보려는 대상의 이름을 선택합니다.

   ![대상 선택](../assets/ui/details-page/destination-select.png)

1. 대상에 대한 세부 정보 페이지가 나타나고 사용 가능한 컨트롤이 표시됩니다.

   ![대상 세부 사항](../assets/ui/details-page/destination-details.png)

## 오른쪽 레일 {#right-rail}

오른쪽 레일에는 선택한 대상에 대한 기본 정보가 표시됩니다.

![오른쪽 레일](../assets/ui/details-page/right-sidebar.png)

다음 표는 오른쪽 레일에서 제공하는 컨트롤과 세부 사항을 다룹니다.

| 오른쪽 레일 항목 | 설명 |
| --- | --- |
| [!UICONTROL 세그먼트 활성화] | 대상에 매핑되는 세그먼트를 편집하거나 내보내기 일정을 업데이트하거나 매핑된 속성과 ID를 추가 및 제거하려면 이 컨트롤을 선택합니다. 다음 내용을 참조하십시오 [세그먼트 스트리밍 대상에 대상 데이터 활성화](./activate-segment-streaming-destinations.md), [대상자 데이터를 묶음 프로필 기반 대상으로 활성화](./activate-batch-profile-destinations.md), 및 [스트리밍 프로필 기반 대상으로 대상 데이터 활성화](./activate-streaming-profile-destinations.md) 추가 정보. |
| [!UICONTROL 삭제] | 이 데이터 흐름을 삭제하고 이전에 활성화한 세그먼트(있는 경우)의 매핑을 해제할 수 있습니다. |
| [!UICONTROL 대상 이름] | 대상 이름을 업데이트하기 위해 이 필드를 편집할 수 있습니다. |
| [!UICONTROL 설명] | 이 필드를 편집하여 대상에 선택적 설명을 업데이트하거나 추가할 수 있습니다. |
| [!UICONTROL 대상] | 대상이 전송되는 대상 플랫폼을 나타냅니다. 자세한 내용은 [대상 카탈로그](../catalog/overview.md) 추가 정보. |
| [!UICONTROL 상태] | 대상이 활성화되었는지 여부를 나타냅니다. |
| [!UICONTROL 마케팅 작업] | 데이터 거버넌스 목적으로 이 대상에 적용되는 마케팅 작업(사용 사례)을 나타냅니다. |
| [!UICONTROL 범주] | 대상 유형을 나타냅니다. 자세한 내용은 [대상 카탈로그](../catalog/overview.md) 추가 정보. |
| [!UICONTROL 연결 유형] | 대상이 대상으로 전송되는 양식을 나타냅니다. 가능한 값은 다음과 같습니다 [!UICONTROL 쿠키] 및 [!UICONTROL 프로필 기반]. |
| [!UICONTROL 빈도] | 대상이 대상으로 전송되는 빈도를 나타냅니다. 가능한 값은 다음과 같습니다 [!UICONTROL 스트리밍] 및 [!UICONTROL 일괄 처리]. |
| [!UICONTROL 신원] | 대상에서 허용하는 ID 네임스페이스를 나타냅니다(예: ). `GAID`, `IDFA`, 또는 `email`. 허용되는 ID 네임스페이스에 대한 자세한 내용은 [id 네임스페이스 개요](../../identity-service/namespaces.md). |
| [!UICONTROL 작성자] | 이 대상을 만든 사용자를 나타냅니다. |
| [!UICONTROL 생성됨] | 이 대상을 만들 때의 UTC 날짜/시간을 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL 활성화됨]/[!UICONTROL 비활성화됨] 전환 {#enabled-disabled-toggle}

를 사용할 수 있습니다 **[!UICONTROL 활성화됨]/[!UICONTROL 비활성화됨]** 모든 데이터 내보내기를 대상으로 시작 및 일시 중지로 전환합니다.

![데이터 흐름 전환 활성화 또는 비활성화](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL 데이터 흐름 실행] {#dataflow-runs}

다음 [!UICONTROL 데이터 흐름 실행] 탭에서 데이터 흐름 실행에서 일괄 처리 및 스트리밍 대상에 대한 지표 데이터를 제공합니다. 을(를) 참조하십시오. [데이터 흐름 모니터링](monitor-dataflows.md) 자세한 내용 및 지표 정의를 참조하십시오.

>[!NOTE]
>
>* 대상 모니터링 기능은 현재 Experience Platform의 모든 대상에 대해 지원됩니다 *제외* a [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [사용자 지정 개인화](/help/destinations/catalog/personalization/custom-personalization.md) 및 [Experience Cloud 대상](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 대상.
>* 대상 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure 이벤트 허브](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), 및 [HTTP API](/help/destinations/catalog/streaming/http-destination.md) 대상, ID 제외, 실패 및 활성화가 현재 표시되지 않습니다.


![데이터 흐름 실행 보기](../assets/ui/details-page/dataflow-runs.png)

### 데이터 흐름 실행 기간 {#dataflow-runs-duration}

표시된 데이터 흐름 실행 기간에 알려진 문제가 있습니다. 반면에 **[!UICONTROL 처리 기간]** 대부분의 데이터 흐름 실행에 대해 아래 이미지에 표시된 대로 약 4시간 정도가 지정되며, 모든 데이터 흐름 실행에 대한 실제 처리 시간이 훨씬 짧습니다. Experience Platform이 대상에 대한 호출을 다시 시도해야 하는 경우 데이터 흐름 실행 창이 오랫동안 열려 있습니다.

![데이터 흐름 의 이미지는 처리 시간 열이 강조 표시된 채 실행됩니다.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run.png)

## [!UICONTROL 활성화 데이터] {#activation-data}

다음 [!UICONTROL 활성화 데이터] 탭에는 시작 날짜 및 종료 날짜(해당하는 경우) 등 대상에 매핑된 세그먼트 목록과 내보내기 유형, 예약 및 빈도 등 데이터 내보내기에 대한 기타 관련 정보가 표시됩니다. 특정 세그먼트에 대한 세부 사항을 보려면 목록에서 해당 이름을 선택합니다.

>[!TIP]
>
>대상에 매핑된 속성 및 ID에 대한 세부 사항을 보고 편집하려면 을 선택합니다 **[!UICONTROL 세그먼트 활성화]** 에서 [오른쪽 레일](#right-rail).

![활성화 데이터 보기 배치 대상](../assets/ui/details-page/activation-data-batch.png)

![활성화 데이터 보기 스트리밍 대상](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>세그먼트의 세부 사항 페이지 탐색에 대한 자세한 내용은 [세그먼테이션 UI 개요](../../segmentation/ui/overview.md#segment-details).
