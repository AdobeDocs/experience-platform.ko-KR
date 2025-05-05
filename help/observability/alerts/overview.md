---
keywords: Experience Platform;홈;인기 항목;날짜 범위
title: 경고 개요
description: 경고 규칙이 정의되는 구조를 포함하여 Adobe Experience Platform에서의 다양한 경고에 대해 알아봅니다.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 3%

---

# 경고 개요

>[!NOTE]
>
>경고는 프로덕션 및 개발 샌드박스 모두에서 지원되므로 모든 샌드박스에서 경고에 가입할 수 있습니다. 샌드박스가 재설정되면 모든 구독 경고도 재설정되고 샌드박스가 삭제되면 모든 구독 경고가 삭제됩니다.

Adobe Experience Platform을 사용하면 Adobe Experience Platform 활동과 관련된 이벤트 기반 경고를 구독할 수 있습니다. 경고는 작업이 완료되었는지, 워크플로우 내의 특정 마일스톤에 도달했는지 또는 오류가 발생했는지 확인하기 위해 [[!DNL Observability Insights] API](../api/overview.md)를 폴링하지 않아도 됩니다.

Experience Platform 작업의 특정 조건 세트에 도달하면(예: 시스템이 임계값을 위반한 경우 발생할 수 있는 문제) Experience Platform에서 이를 구독한 조직의 모든 사용자에게 경고 메시지를 전달할 수 있습니다. 이러한 메시지는 경고가 해결될 때까지 사전 정의된 시간 간격 동안 반복될 수 있습니다.

이 문서에서는 경고 규칙이 정의되는 구조를 포함하여 Adobe Experience Platform의 경고에 대한 개요를 제공합니다.

## 일회성 경고와 반복 경고 비교

Experience Platform 경고는 한 번 전송하거나 해결할 때까지 사전 정의된 간격 동안 반복할 수 있습니다. 이러한 각 옵션의 사용 사례는 다음과 같은 점에서 다르기 위한 것입니다.

| 일회성 경고 | 반복 경고 |
| --- | --- |
| 반드시 문제가 있음을 나타내지는 않습니다. | 잠재적으로 원하지 않는 상태를 나타냅니다. |
| 반복하지 않습니다. | 이상 상태가 지속되면 반복할 수 있습니다. |
| 해당 예는 다음과 같습니다.<ul><li>데이터 수집이 완료되었습니다.</li><li>쿼리 실행이 완료되었습니다.</li><li>데이터가 삭제되었습니다.</li></ul> | 해당 예는 다음과 같습니다.<ul><li>수집 기간이 서비스 수준 계약(SLA)을 초과합니다.</li><li>지난 24시간 동안 일일 섭취는 발생하지 않았습니다.</li><li>스트림 프로세서의 오류 속도가 구성된 임계값을 초과합니다.</li><li>총 프로필 수가 권한을 초과합니다.</li></ul> |

{style="table-layout:auto"}

## 경보 해부학

경고는 다음 구성 요소로 나눌 수 있습니다.

| 구성 요소 | 설명 |
| --- | --- |
| **지표** | 실패한 일괄 처리 수집 이벤트 수(`timeseries.ingestion.dataset.batchfailed.count`)와 같이 값이 경고를 트리거하는 Observability [metric](../api/metrics.md#available-metrics). |
| **조건** | 특정 수를 초과하는 카운트 지표와 같이 true로 확인될 경우 경고를 트리거하는 지표와 관련된 조건입니다. 이 조건은 미리 정의된 시간 윈도우(time window)와 연관될 수 있다. |
| **창** | (선택 사항) 경보에 대한 조건은 미리 정의된 시간 윈도우로 제한될 수 있다. 예를 들어 지난 5분 동안 실패한 일괄 처리 수에 따라 경고가 트리거될 수 있습니다. |
| **작업** | 경고가 트리거되면 작업이 수행됩니다. 특히 미리 구성된 웹후크 또는 Experience Platform UI와 같은 게재 채널을 통해 메시지를 적용 가능한 수신자에게 보냅니다. |
| **빈도** | (선택 사항) 해당 조건이 true로 유지되거나 해결되지 않은 경우 정의된 간격으로 작업을 반복하도록 경고를 구성할 수 있습니다. |

{style="table-layout:auto"}

## 경고 수신 및 관리

경고는 다음 두 가지 채널을 통해 수신 및 관리할 수 있습니다.

* [Adobe I/O Events](#events)
* [EXPERIENCE PLATFORM UI](#ui)

### I/O 이벤트 {#events}

활동 모니터링의 효율적인 자동화를 용이하게 하기 위해 구성된 웹후크에 경고를 보낼 수 있습니다. Webhook을 통해 경고를 수신하려면 Adobe Developer Console에서 Experience Platform 경고에 대한 Webhook을 등록해야 합니다. 특정 단계는 [Adobe I/O 이벤트 알림 구독](./subscribe.md)에 대한 안내서를 참조하십시오.

### EXPERIENCE PLATFORM UI {#ui}

Experience Platform UI를 통해 수신된 경고를 보고 경고 규칙을 관리할 수 있습니다. 다음 비디오에서는 이러한 기능에 대해 소개합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3423921?quality=12&learn=on&captions=kor)

Experience Platform UI에서 경고를 사용하여 작업하려면 Adobe Admin Console을 통해 다음 액세스 제어 권한을 활성화해야 합니다.

| 사용 권한 | 설명 |
| --- | --- |
| 경고 보기 | 수신된 경고 메시지를 볼 수 있습니다. |
| 경고 내역 보기* | [!UICONTROL 알림] 탭을 통해 받은 알림 기록을 볼 수 있습니다. |
| 경고 관리* | [!UICONTROL 경고] 탭을 통해 경고 규칙을 활성화 및 비활성화할 수 있습니다. |
| 경고 해결* | [!UICONTROL 경고] 탭을 통해 트리거된 경고를 해결할 수 있습니다. |

{style="table-layout:auto"}

**[!UICONTROL 경고] 탭에 액세스하려면 다른 권한 중 하나와 함께 경고 보기 권한도 부여 받아야 합니다.*

>[!NOTE]
>
>Experience Platform에서 권한을 관리하는 방법에 대한 자세한 내용은 [액세스 제어 설명서](../../access-control/ui/overview.md)를 참조하세요.

경고 보기 권한으로 오른쪽 상단 모서리에서 벨 아이콘(![벨 아이콘](/help/images/icons/bell.png))을 선택하여 받은 경고를 볼 수 있습니다.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> 경고가 트리거된 이유에 대한 자세한 내용을 보려면 경고를 선택하여 관련 대시보드로 이동합니다.

또한 UI의 [!UICONTROL 경고] 탭에서는 개별 사용자가 특정 경고 유형을 구독할 수 있으며 관리자가 경고 규칙을 모두 활성화하거나 비활성화할 수 있습니다. 경고 관리에 대한 자세한 내용은 [UI 안내서](./ui.md)를 참조하세요.

## 다음 단계

이 문서를 읽고 Experience Platform 알림 및 Experience Platform 생태계에서의 역할에 대해 알아보았습니다. 경고를 받고 관리하는 방법은 이 개요 전체에 연결된 프로세스 설명서를 참조하십시오.
