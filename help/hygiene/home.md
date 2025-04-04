---
title: 고급 데이터 수명주기 관리 개요
description: 고급 데이터 수명 주기 관리를 사용하면 오래되거나 부정확한 레코드를 업데이트하거나 삭제하여 데이터의 수명 주기를 관리할 수 있습니다.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# Adobe Experience Platform의 고급 데이터 수명주기 관리

Adobe Experience Platform은 소비자 경험을 조정하기 위해 크고 복잡한 데이터 작업을 관리하는 강력한 도구 세트를 제공합니다. 시간이 지나면서 데이터가 시스템에 수집되면 데이터가 예상대로 사용되고, 잘못된 데이터를 수정해야 할 때 업데이트되고, 조직 정책에서 필요하다고 판단할 때 삭제되도록 데이터 저장소를 관리하는 것이 점점 더 중요해집니다.

<!-- Experience Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

이러한 활동은 [[!UICONTROL 데이터 수명 주기] UI 작업 공간](#ui) 또는 [데이터 위생 API](#api)를 사용하여 수행할 수 있습니다. 데이터 라이프사이클 작업이 실행되면 각 프로세스 단계에서 투명도가 업데이트됩니다. 각 작업 유형이 시스템에 표시되는 방법에 대한 자세한 내용은 [타임라인 및 투명도](#timelines-and-transparency)의 섹션을 참조하십시오.

>[!NOTE]
>
>Advanced Data Lifecycle Management는 [데이터 세트 만료 끝점](./api/dataset-expiration.md)을 통해 데이터 세트 삭제를 지원하고 [작업 주문 끝점](./api/workorder.md)을 통해 기본 ID를 사용하여 ID 삭제(행 수준 데이터)를 지원합니다. Experience Platform UI를 통해 [데이터 세트 만료](./ui/dataset-expiration.md) 및 [레코드 삭제](./ui/record-delete.md)을 관리할 수도 있습니다. 자세한 내용은 연결된 설명서 를 참조하십시오. 데이터 수명 주기는 일괄 삭제를 지원하지 않습니다.

## [!UICONTROL 데이터 수명 주기] UI 작업 영역 {#ui}

Experience Platform UI의 [!UICONTROL 데이터 수명 주기] 작업 영역을 사용하면 데이터 수명 주기 작업을 구성하고 예약할 수 있으므로 레코드가 예상대로 유지될 수 있습니다.

UI에서 데이터 라이프사이클 작업을 관리하는 자세한 단계는 [데이터 라이프사이클 UI 안내서](./ui/overview.md)를 참조하십시오.

## 데이터 위생 API {#api}

[!UICONTROL 데이터 수명 주기] UI는 데이터 수명 주기 활동을 자동화하려는 경우 엔드포인트를 직접 사용할 수 있는 데이터 위생 API 위에 구축됩니다. 자세한 내용은 [데이터 위생 API 안내서](./api/overview.md)를 참조하십시오.

## 타임라인 및 투명도 {#timelines-and-transparency}

[레코드 삭제](./ui/record-delete.md) 및 데이터 세트 만료 요청은 각각 고유한 처리 타임라인이 있으며 해당 워크플로우의 주요 지점에 투명도 업데이트를 제공합니다.

[데이터 세트 만료 요청](./ui/dataset-expiration.md)을 만들 때 다음이 수행됩니다.

| 단계 | 예약된 만료 후 시간 | 설명 |
| --- | --- | --- |
| 요청이 제출됨 | 0시간 | 데이터 관리자 또는 개인 정보 보호 분석가는 주어진 시간에 만료되도록 데이터 세트에 대한 요청을 제출합니다. 요청이 제출되면 [!UICONTROL 데이터 수명 주기 UI]에 표시되고 예약된 만료 시간까지 보류 중인 상태로 유지되며 그 이후에는 요청이 실행됩니다. |
| 데이터 세트에 삭제 플래그가 지정되었습니다. | 0-2시간 | 요청이 실행되면 데이터 세트에 삭제 플래그가 지정됩니다. Amazon Web Services(AWS) 데이터 저장소를 사용하는 경우 이 프로세스는 최대 2시간이 소요됩니다. 이 시간 동안 일괄 처리 및 스트리밍 세분화, 미리 보기 또는 예측, 내보내기 및 액세스와 같은 작업은 이 데이터 세트를 무시합니다. |
| 데이터 세트 삭제 | 3시간 | **데이터 집합이 삭제 플래그가 지정된 후 1시간**, 시스템에서 완전히 제거됩니다. 이때 UI의 [데이터 집합 인벤토리 페이지](../catalog/datasets/user-guide.md)에서 데이터 집합이 삭제됩니다. 그러나 데이터 레이크 내의 데이터는 이 단계에서 소프트 삭제되며, 하드 삭제 프로세스가 완료될 때까지 유지됩니다. |
| 프로필 개수 업데이트됨 | 30시간 | 삭제되는 데이터 세트의 내용에 따라 구성 요소 속성이 모두 해당 데이터 세트에 연결되어 있는 경우 일부 프로필이 시스템에서 제거될 수 있습니다. 데이터 세트가 삭제된 후 30시간이 경과하면 전체 프로필 수에 대한 결과 변경 사항이 [대시보드 위젯](../dashboards/guides/profiles.md#profile-count-trend) 및 기타 보고서에 반영됩니다. |
| 대상자 업데이트됨 | 48시간 | 영향을 받는 프로필이 모두 업데이트되면 모든 관련 [대상](../segmentation/home.md)이 새 크기를 반영하도록 업데이트됩니다. 제거된 데이터 세트 및 세그먼트화 중인 속성에 따라 삭제의 결과로 각 대상의 크기가 증가 또는 감소할 수 있습니다. |
| 여정 및 대상 업데이트됨 | 50시간 | 관련 세그먼트의 변경 사항에 따라 [여정](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [캠페인](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html) 및 [대상](../destinations/home.md)이 업데이트됩니다. |
| 하드 삭제 완료 | 15일 | 데이터 세트와 관련된 모든 데이터는 데이터 레이크에서 하드 삭제됩니다. 데이터 집합을 삭제한 [데이터 주기 작업의 상태](./ui/browse.md#view-details)가 이를 반영하도록 업데이트됩니다. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Amazon Web Services(AWS)의 데이터 세트 삭제는 변경 사항이 완전히 적용되기 전에 약 3시간의 지연 시간이 적용됩니다. 여기에는 데이터 세트가 삭제에 플래그가 지정되는 데 최대 2시간이 포함된 다음 시스템에서 완전히 삭제되기 전에 추가 1시간이 포함됩니다. 반면 Azure 데이터 레이크를 사용하는 Experience Platform 인스턴스에 대한 삭제 요청은 비즈니스 기능 전반에 걸쳐 즉각적인 변경을 초래합니다.
>
>AWS 사용자의 경우 이 지연은 배치 세분화, 스트리밍 세분화, 미리보기, 예상, 내보내기 및 데이터 액세스에 영향을 줄 수 있습니다. Azure Data Lake 사용자는 즉시 업데이트를 경험하므로 이 지연 시간은 AWS을 사용하는 고객에게만 영향을 줍니다. AWS 사용자의 경우 삭제 요청이 영향을 받는 모든 시스템을 통해 완전히 전파되는 데 최대 3시간이 걸릴 수 있습니다. 그에 따라 기대치를 조정하십시오.


<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## 다음 단계

이 문서에서는 Experience Platform의 데이터 라이프사이클 기능에 대한 개요를 제공합니다. UI에서 데이터 위생 요청을 시작하려면 [UI 안내서](./ui/overview.md)를 참조하세요. 프로그래밍 방식으로 데이터 수명 주기 작업을 만드는 방법에 대해 알아보려면 [데이터 위생 API 안내서](./api/overview.md)를 참조하세요.
