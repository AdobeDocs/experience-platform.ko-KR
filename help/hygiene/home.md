---
title: 데이터 위생 개요
description: Adobe Experience Platform 데이터 위생에서는 오래된 레코드 또는 부정확한 레코드를 업데이트하거나 삭제하여 데이터 주기를 관리할 수 있습니다.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# Adobe Experience Platform의 데이터 위생

>[!IMPORTANT]
>
>데이터 위생은 현재 구입한 조직에서만 사용할 수 있습니다 **Adobe 의료 보호** 또는 **Adobe 개인 정보 보호 및 보안 차단**.

Adobe Experience Platform은 소비자 경험을 오케스트레이션하기 위해 복잡하고 큰 데이터 작업을 관리하는 강력한 도구 세트를 제공합니다. 시간이 지나면서 시스템에 데이터를 수집하면 데이터가 예상대로 사용되고, 잘못된 데이터를 수정해야 할 때 업데이트되고, 조직 정책이 필요하다고 인정하는 경우 삭제되도록 데이터 저장소를 관리하는 것이 점점 더 중요해집니다.

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

이러한 활동은 [[!UICONTROL 데이터 위생] UI 작업 공간](#ui) 또는 [데이터 위생 API](#api). 데이터 위생 작업이 실행되면 시스템은 프로세스의 각 단계에서 투명성 업데이트를 제공합니다. 의 섹션을 참조하십시오. [타임라인 및 투명도](#timelines-and-transparency) 시스템에서 각 작업 유형이 표시되는 방식에 대한 자세한 정보.

## [!UICONTROL 데이터 위생] UI 작업 공간 {#ui}

다음 [!UICONTROL 데이터 위생] platform UI의 작업 공간을 사용하면 데이터 위생 작업을 구성하고 예약할 수 있으므로 레코드가 예상대로 유지되는지를 확인할 수 있습니다.

UI에서 데이터 위생 작업을 관리하는 방법에 대한 자세한 단계는 [데이터 위생 UI 안내서](./ui/overview.md).

## 데이터 위생 API {#api}

다음 [!UICONTROL 데이터 위생] UI는 데이터 위생 API를 기반으로 구축되었으며, 데이터 위생 활동을 자동화하려는 경우 직접 사용할 수 있는 종단점입니다. 자세한 내용은 [데이터 위생 API 안내서](./api/overview.md) 추가 정보.

## 타임라인 및 투명도

레코드 삭제 및 데이터 세트 만료 요청에는 각각 고유한 처리 타임라인이 있으며 각 워크플로우의 주요 지점에서 투명도 업데이트를 제공합니다.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

다음 작업은 [데이터 세트 만료 요청](./ui/dataset-expiration.md) 이(가) 생성되었습니다.

| 스테이징 | 예약된 만료 후 시간 | 설명 |
| --- | --- | --- |
| 요청이 제출됨 | 0시간 | 데이터 관리자 또는 개인 정보 분석가는 지정된 시간에 데이터 세트가 만료되도록 요청을 제출합니다. 요청이 [!UICONTROL 데이터 위생 UI] 제출되면 및은(는) 예약된 만료 시간까지 보류 중인 상태로 유지되며 그 이후에는 요청이 실행됩니다. |
| 데이터 세트가 삭제됩니다 | 1시간 | 데이터 세트가 [데이터 세트 인벤토리 페이지](../catalog/datasets/user-guide.md) ( UI) 아래에 그룹화됩니다. 데이터 레이크 내의 데이터는 단지 소프트 삭제일 뿐이며, 프로세스가 종료될 때까지 그대로 유지되며, 그 이후에는 삭제되기 어렵습니다. |
| 프로필 수가 업데이트됨 | 30시간 | 삭제할 데이터 세트의 컨텐츠에 따라 모든 구성 요소 속성이 해당 데이터 세트에 연결된 경우 일부 프로필이 시스템에서 제거될 수 있습니다. 데이터 세트가 삭제된 후 30시간 후에 전체 프로필 수의 변경 사항이 [대시보드 위젯](../dashboards/guides/profiles.md#profile-count-trend) 및 기타 보고서. |
| 업데이트된 세그먼트 | 48시간 | 영향을 받는 모든 프로필이 업데이트되면 모든 관련 프로필이 업데이트됩니다 [세그먼트](../segmentation/home.md) 새 크기를 반영하도록 업데이트됩니다. 제거된 데이터 세트와 세그먼트화하는 속성에 따라, 삭제 결과로 각 세그먼트의 크기가 늘리거나 줄일 수 있습니다. |
| 여정 및 대상 업데이트 | 50시간 | [여정](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [캠페인](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), 및 [대상](../destinations/home.md) 은 관련 세그먼트의 변경 사항에 따라 업데이트됩니다. |
| 하드 삭제 완료 | 14일 | 데이터 세트와 관련된 모든 데이터는 데이터 레이크에서 삭제되기 어렵습니다. 다음 [위생 작업 상태](./ui/browse.md#view-details) 삭제한 데이터 세트가 이를 반영하도록 업데이트됩니다. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## 다음 단계

이 문서에서는 플랫폼의 데이터 위생 기능에 대한 개요를 제공합니다. UI에서 데이터 위생 요청을 시작하려면 다음을 참조하십시오. [UI 안내서](./ui/overview.md). 프로그래밍 방식으로 데이터 위생 작업을 만드는 방법을 알아보려면 [데이터 위생 API 안내서](./api/overview.md)
