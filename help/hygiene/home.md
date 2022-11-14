---
title: 데이터 위생 개요
description: Adobe Experience Platform 데이터 위생에서는 오래된 레코드 또는 부정확한 레코드를 업데이트하거나 삭제하여 데이터 주기를 관리할 수 있습니다.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: b76e1bc6d5b346c32ea09612e24b68c6636f7deb
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---

# Adobe Experience Platform의 데이터 위생

>[!IMPORTANT]
>
>데이터 위생은 현재 구입한 조직에서만 사용할 수 있습니다 **Adobe 의료 보호** 또는 **Adobe 개인 정보 보호 및 보안 차단**.

Adobe Experience Platform은 소비자 경험을 오케스트레이션하기 위해 복잡하고 큰 데이터 작업을 관리하는 강력한 도구 세트를 제공합니다. 시간이 지나면서 시스템에 데이터를 수집하면 데이터가 예상대로 사용되고, 잘못된 데이터를 수정해야 할 때 업데이트되고, 조직 정책이 필요하다고 인정하는 경우 삭제되도록 데이터 저장소를 관리하는 것이 점점 더 중요해집니다.

플랫폼의 데이터 위생 기능을 사용하면 다음을 통해 저장된 소비자 데이터를 관리할 수 있습니다.

* 자동화된 데이터 세트 만료 예약
* 수집된 ID를 기반으로 소비자 데이터 삭제

이러한 활동은 [[!UICONTROL 데이터 위생] UI 작업 공간](#ui) 또는 [데이터 위생 API](#api). 데이터 위생 작업이 실행되면 시스템은 프로세스의 각 단계에서 투명성 업데이트를 제공합니다. 의 섹션을 참조하십시오. [타임라인 및 투명도](#timelines-and-transparency) 시스템에서 각 작업 유형이 표시되는 방식에 대한 자세한 정보.

## [!UICONTROL 데이터 위생] UI 작업 공간 {#ui}

다음 [!UICONTROL 데이터 위생] platform UI의 작업 공간을 사용하면 데이터 위생 작업을 구성하고 예약할 수 있으므로 레코드가 예상대로 유지되는지를 확인할 수 있습니다.

UI에서 데이터 위생 작업을 관리하는 방법에 대한 자세한 단계는 [데이터 위생 UI 안내서](./ui/overview.md).

## 데이터 위생 API {#api}

다음 [!UICONTROL 데이터 위생] UI는 데이터 위생 API를 기반으로 구축되었으며, 데이터 위생 활동을 자동화하려는 경우 직접 사용할 수 있는 종단점입니다. 자세한 내용은 [데이터 위생 API 안내서](./api/overview.md) 추가 정보.

## 타임라인 및 투명도

소비자 삭제 및 데이터 세트 만료 요청에는 각각 고유한 처리 타임라인이 있으며 각 워크플로우의 주요 지점에서 투명도 업데이트를 제공합니다. 각 작업 유형에 대한 자세한 내용은 아래 섹션을 참조하십시오.

### 데이터 집합 만료 {#dataset-expiration-transparency}

다음 작업은 [데이터 세트 만료 요청](./ui/dataset-expiration.md) 이(가) 생성되었습니다.

| 스테이징 | 예약된 만료 후 시간 | 설명 |
| --- | --- | --- |
| 요청이 제출됨 | 0시간 | 데이터 관리자 또는 개인 정보 분석가는 지정된 시간에 데이터 세트가 만료되도록 요청을 제출합니다. 요청이 [!UICONTROL 데이터 위생 UI] 제출되면 및은(는) 예약된 만료 시간까지 보류 중인 상태로 유지되며 그 이후에는 요청이 실행됩니다. |
| 데이터 세트가 삭제됩니다 | 1시간 | 데이터 세트가 [데이터 세트 인벤토리 페이지](../catalog/datasets/user-guide.md) ( UI) 아래에 그룹화됩니다. 데이터 레이크 내의 데이터는 단지 소프트 삭제일 뿐이며, 프로세스가 종료될 때까지 그대로 유지되며, 그 이후에는 삭제되기 어렵습니다. |
| 프로필 수가 업데이트됨 | 30시간 | 삭제할 데이터 세트의 컨텐츠에 따라 모든 구성 요소 속성이 해당 데이터 세트에 연결된 경우 일부 프로필이 시스템에서 제거될 수 있습니다. 데이터 세트가 삭제된 후 30시간 후에 전체 프로필 수의 변경 사항이 [대시보드 위젯](../dashboards/guides/profiles.md#profile-count-trend) 및 기타 보고서. |
| 업데이트된 세그먼트 | 48시간 | 영향을 받는 모든 프로필이 업데이트되면 모든 관련 프로필이 업데이트됩니다 [세그먼트](../segmentation/home.md) 새 크기를 반영하도록 업데이트됩니다. 제거된 데이터 세트와 세그먼트화하는 속성에 따라, 삭제 결과로 각 세그먼트의 크기가 늘리거나 줄일 수 있습니다. |
| 여정 및 대상 업데이트 | 50시간 | [여정](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [캠페인](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), 및 [대상](../destinations/home.md) 은 관련 세그먼트의 변경 사항에 따라 업데이트됩니다. |
| 하드 삭제 완료 | 14일 | 데이터 세트와 관련된 모든 데이터는 데이터 레이크에서 삭제되기 어렵습니다. 다음 [위생 작업 상태](./ui/browse.md#view-details) 삭제한 데이터 세트가 이를 반영하도록 업데이트됩니다. |

{style=&quot;table-layout:auto&quot;}

### 소비자 삭제 {#consumer-delete-transparency}

>[!IMPORTANT]
>
>소비자 삭제는 Adobe Healthcare Shield를 구입한 조직에서만 사용할 수 있습니다.

다음 작업은 [소비자 삭제 요청](./ui/delete-consumer.md) 이(가) 생성되었습니다.

| 스테이징 | 제출 요청 후 시간 | 설명 |
| --- | --- | --- |
| 요청이 제출됨 | 0시간 | 데이터 관리자 또는 개인 정보 분석가가 소비자 삭제 요청을 제출합니다. 요청이 [!UICONTROL 데이터 위생 UI] 제출한 후. |
| 프로필 조회 업데이트 | 3시간 | 삭제된 ID로 인해 발생한 프로필 카운트의 변경 내용은 [대시보드 위젯](../dashboards/guides/profiles.md#profile-count-trend) 및 기타 보고서. |
| 업데이트된 세그먼트 | 24시간 | 프로파일이 제거되면 모든 관련 [세그먼트](../segmentation/home.md) 새 크기를 반영하도록 업데이트됩니다. |
| 여정 및 대상 업데이트 | 26시간 | [여정](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [캠페인](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), 및 [대상](../destinations/home.md) 은 관련 세그먼트의 변경 사항에 따라 업데이트됩니다. |
| 데이터 레이크에서 소프트 삭제된 레코드 | 7일 | 데이터가 데이터 레이크에서 소프트 삭제됩니다. |
| 데이터 진공 완료 | 14일 | 다음 [위생 작업 상태](./ui/browse.md#view-details) 작업이 완료되었음을 나타내는 업데이트로, 즉 데이터 레이크에서 데이터 진공이 완료되었으며 관련 레코드가 삭제되었음을 의미합니다. |

{style=&quot;table-layout:auto&quot;}

## 다음 단계

이 문서에서는 플랫폼의 데이터 위생 기능에 대한 개요를 제공합니다. UI에서 데이터 위생 요청을 시작하려면 다음을 참조하십시오. [UI 안내서](./ui/overview.md). 프로그래밍 방식으로 데이터 위생 작업을 만드는 방법을 알아보려면 [데이터 위생 API 안내서](./api/overview.md)
