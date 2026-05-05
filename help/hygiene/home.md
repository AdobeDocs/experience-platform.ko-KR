---
title: 고급 데이터 수명주기 관리 개요
description: 고급 데이터 수명 주기 관리를 사용하면 오래되거나 부정확한 레코드를 업데이트하거나 삭제하여 데이터의 수명 주기를 관리할 수 있습니다.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: adba9d3cd979f655f477d2d80ed3e55e96fbe486
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 1%

---

# Adobe Experience Platform의 고급 데이터 수명주기 관리

Adobe Experience Platform은 소비자 경험을 조정하기 위해 크고 복잡한 데이터 작업을 관리하는 강력한 도구 세트를 제공합니다. 시간이 지나면서 데이터가 시스템에 수집되면 데이터가 예상대로 사용되고, 잘못된 데이터를 수정해야 할 때 업데이트되고, 조직 정책에서 필요하다고 판단할 때 삭제되도록 데이터 저장소를 관리하는 것이 점점 더 중요해집니다.

이러한 활동은 [[!UICONTROL Data Lifecycle] UI 작업 영역](#ui) 또는 [데이터 위생 API](#api)를 사용하여 수행할 수 있습니다. 데이터 라이프사이클 작업이 실행되면 각 프로세스 단계에서 투명도가 업데이트됩니다. 각 작업 유형이 시스템에 표시되는 방법에 대한 자세한 내용은 [타임라인 및 투명도](#timelines-and-transparency)의 섹션을 참조하십시오.

>[!NOTE]
>
>Advanced Data Lifecycle Management는 [데이터 세트 만료 끝점](./api/dataset-expiration.md)을 통해 데이터 세트 삭제를 지원하고 [작업 주문 끝점](./api/workorder.md)을 통해 기본 ID를 사용하여 ID 삭제(행 수준 데이터)를 지원합니다. Experience Platform UI를 통해 [데이터 세트 만료](./ui/dataset-expiration.md) 및 [레코드 삭제](./ui/record-delete.md)을 관리할 수도 있습니다. 자세한 내용은 연결된 설명서 를 참조하십시오. 데이터 수명 주기는 일괄 삭제를 지원하지 않습니다.

## [!UICONTROL Data Lifecycle] UI 작업 영역 {#ui}

Experience Platform UI의 [!UICONTROL Data Lifecycle] 작업 영역을 사용하면 데이터 라이프사이클 작업을 구성하고 예약할 수 있으므로 레코드가 예상대로 유지될 수 있습니다.

UI에서 데이터 라이프사이클 작업을 관리하는 자세한 단계는 [데이터 라이프사이클 UI 안내서](./ui/overview.md)를 참조하십시오.

## 데이터 위생 API {#api}

[!UICONTROL Data Lifecycle] UI는 데이터 수명 주기 활동을 자동화하려는 경우 엔드포인트를 직접 사용할 수 있는 데이터 위생 API 위에 구축됩니다. 자세한 내용은 [데이터 위생 API 안내서](./api/overview.md)를 참조하십시오.

## 타임라인 및 투명도 {#timelines-and-transparency}

[레코드 삭제](./ui/record-delete.md) 및 데이터 세트 만료 요청은 각각 고유한 처리 타임라인이 있으며 해당 워크플로우의 주요 지점에 투명도 업데이트를 제공합니다.

>[!TIP]
>
>추가 참조 정보의 경우
>- 할당량 제한에 대해 현재 사용량을 모니터링하려면 [할당량 참조 안내서](./api/quota.md)를 참조하세요.
>- 자격 규칙, 월별 상한, SLA 타임라인 및 예외 처리 정책에 대해서는 [UI(할당량 기록)](./ui/record-delete.md#quotas) 및 [API(작업 주문 할당량 가이드)](./api/workorder.md#quotas)를 참조하십시오.

[데이터 세트 만료 요청](./ui/dataset-expiration.md)을 만들 때 다음이 수행됩니다.

| 단계 | 예약된 만료 후 시간 | 설명 |
| --- | --- | --- |
| 요청이 제출됨 | 0시간 | 데이터 관리자 또는 개인 정보 보호 분석가는 주어진 시간에 만료되도록 데이터 세트에 대한 요청을 제출합니다. 요청이 제출되면 [!UICONTROL Data Lifecycle UI]에 표시되고 예약된 만료 시간까지 보류 중인 상태로 유지되며 그 이후에는 요청이 실행됩니다. |
| 데이터 세트가 데이터 레이크에서 삭제됩니다. | 1시간 | UI의 [데이터 집합 인벤토리 페이지](../catalog/datasets/user-guide.md)에서 데이터 집합이 삭제됩니다. 데이터 레이크 내의 데이터는 소프트 삭제만 되며, 프로세스가 끝날 때까지 유지된 후 하드 삭제됩니다. |
| 프로필 서비스에서 데이터 세트 삭제 | 3시간 | 이 시점에서부터 배치 및 스트리밍 세분화, 미리보기 또는 예측, 내보내기 및 엔티티 액세스를 포함한 작업은 더 이상 이 데이터 세트의 데이터를 읽지 않습니다. 프로필 서비스 내의 데이터는 삭제만 가능하며 프로세스가 끝날 때까지 유지된 후 하드 삭제됩니다. |
| 프로필 수 및 대상자 업데이트됨 | 48시간 | 영향을 받는 프로필이 모두 업데이트되면 모든 관련 [대상](../segmentation/home.md)이 새 크기를 반영하도록 업데이트됩니다. 제거된 데이터 세트 및 세그먼트화 중인 속성에 따라 삭제로 인해 각 대상의 크기가 증가하거나 감소할 수 있습니다. 이때 전체 프로필 수에 대한 결과 변경 내용은 [대시보드 위젯](../dashboards/guides/profiles.md#profile-count-trend) 및 기타 보고서에 반영됩니다. |
| 여정 및 대상 업데이트됨 | 50시간 | 관련 세그먼트의 변경 사항에 따라 [여정](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=ko), [캠페인](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=ko) 및 [대상](../destinations/home.md)이 업데이트됩니다. |
| 하드 삭제 완료 | 15일 | 데이터 세트와 관련된 모든 데이터는 데이터 레이크 및 프로필 서비스에서 하드 삭제됩니다. 데이터 집합을 삭제한 [데이터 주기 작업의 상태](./ui/browse.md#view-details)가 이를 반영하도록 업데이트됩니다. |

{style="table-layout:auto"}

### 삭제 타임라인 기록 {#record-delete-transparency}

[레코드 삭제 요청](./ui/record-delete.md)이 제출된 후 다음이 수행됩니다.

>[!NOTE]
>
>시간은 대략적이며 시스템 로드, 배치 예약 및 권한 계층에 따라 다릅니다. 엔드 투 엔드 SLA(표준 30일, Privacy and Security Shield 또는 Healthcare Shield의 경우 15일)가 영업 약속입니다.

| 단계 | 어림잡아 시간 | 설명 |
| --- | --- | --- |
| 요청이 제출되고 일괄 처리됨 | 1-15일 | 작업 주문이 만들어지고 대기 중입니다. 요청은 처리 시작 전 최대 14일 동안 큐에 추가되고 일괄 처리될 수 있습니다. 일괄 처리는 삭제가 즉시 수행되지 않는 주요 원인입니다. |
| 다운스트림 시스템에서 삭제 요청 처리 | 16-25일 | 다운스트림 서비스는 레코드 삭제 요청을 수신하고 실행합니다. |
| 버퍼 — 무결성 검사 및 재제출 | 25-30일 | 버퍼 창을 사용하면 SLA 창이 닫히기 전에 실패한 작업을 무결성 검사 및 다시 제출할 수 있습니다. 모든 시스템이 삭제를 확인하면 작업 주문 상태가 `completed`(으)로 업데이트됩니다. |

{style="table-layout:auto"}

자격 기반 큐 기간 및 최대 SLA 값에 대해서는 [식별자 제출을 위한 처리 타임라인](./ui/record-delete.md#sla-processing-timelines)을 참조하십시오.

## 다음 단계 {#next-steps}

이 문서에서는 Experience Platform의 데이터 라이프사이클 기능에 대한 개요를 제공합니다. UI에서 데이터 위생 요청을 시작하려면 [데이터 수명 주기 UI 안내서](./ui/overview.md)를 참조하세요. 프로그래밍 방식으로 데이터 수명 주기 작업을 만들려면 [데이터 위생 API 안내서](./api/overview.md)를 참조하세요.
