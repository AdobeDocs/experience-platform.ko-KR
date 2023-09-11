---
keywords: Experience Platform;홈;인기 항목;날짜 범위
title: 표준 경고 규칙
description: 이 문서에서는 Experience Platform에서 제공하는 사전 정의된 경고 규칙에 대해 설명합니다.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 9120377f5f2048579d7e2a4740cfcbc56d49d61a
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# 표준 경고 규칙

Adobe Experience Platform은 조직에 대해 활성화할 수 있는 사전 정의된 경고 규칙을 몇 가지 제공합니다. 이 문서에서는 이러한 Adobe 제공 경고 규칙의 세부 사항을 다룹니다. Experience Platform의 경고에 대한 자세한 내용은 [경고 개요](./overview.md).

날짜 [platform UI에서 경고 규칙 보기](./ui.md), 각 규칙에 개별적으로 가입할 수 있습니다. 을 통해 경고를 구독할 때 [I/O 이벤트 알림](./subscribe.md)하지만 경고 규칙은 다른 구독 패키지로 구성됩니다. 아래 표에는 각 규칙이 해당 I/O 이벤트 구독 이름과 함께 표시됩니다.

## 데이터 수집

다음 경고 규칙은 다음과 같습니다 [데이터 수집](../../ingestion/home.md) 및  [소스](../../sources/home.md):

>[!NOTE]
>
>스트리밍 소스는 현재 경고에서 지원되지 않습니다. 배치 출처에 대한 경고 알림만 가입할 수 있습니다.

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 소스 흐름 실행 정보 | 소스 플로우 실행 시작 | 이 경고는 소스 연결이 데이터 처리를 시작할 때 트리거됩니다. |
| 소스 흐름 실행 정보 | 소스 흐름 실행 성공 | 이 경고는 소스 연결에서 데이터가 성공적으로 수집되면 트리거됩니다. |
| 소스 플로우 실행 지연, 실패 및 오류 | 소스 플로우 실행 실패 | 이 경고는 소스 연결에서 데이터를 수집하는 동안 오류가 발생하면 트리거됩니다. |
| 소스 플로우 실행 지연, 실패 및 오류 | 수집 지연 | 이 경고는 일괄 처리 수집 흐름 실행이 처리하는 데 150분 이상 걸릴 때 트리거됩니다. |
| 소스 플로우 실행 지연, 실패 및 오류 | 수집 실패 | 이 경고는 모든 레코드에 대한 실패한 레코드의 비율이 0.5%의 임계값을 초과하는 경우 트리거됩니다. |

{style="table-layout:auto"}

다음 경고 유형을 이전에 구독한 경우 이 경고가 더 이상 사용되지 않으므로 더 이상 경고를 받지 않습니다.

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 소스 플로우 실행 지연, 실패 및 오류 | 수집 부족 | 이 경고는 수집이 7시간 이상 지연되고 플랫폼으로 데이터가 수집되지 않는 경우 메시지를 보냅니다. |

{style="table-layout:auto"}

## ID 서비스

다음 경고 규칙은 다음과 같습니다 [ID 서비스](../../identity-service/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| ID 수집 정보 | ID 서비스 흐름 실행 시작 | 이 경고는 ID 서비스 흐름 실행이 데이터 처리를 시작할 때 트리거됩니다. 즉, 수집된 데이터가 데이터 레이크에서 ID 서비스로 로드됩니다. |
| ID 수집 정보 | ID 서비스 흐름 실행 성공 | 이 경고는 데이터가 데이터 레이크에서 ID 서비스로 성공적으로 로드될 때 트리거됩니다. |
| ID 수집 지연, 실패 및 오류 | ID 서비스 흐름 실행 지연 | 이 경고는 ID 서비스 흐름 실행이 처리하는 데 150분 이상 걸릴 때 트리거됩니다. |
| ID 수집 지연, 실패 및 오류 | ID 서비스 흐름 실행 실패 | 이 경고는 ID 서비스로 데이터를 수집하는 동안 오류가 발생하면 트리거됩니다. |

{style="table-layout:auto"}

## 실시간 고객 프로필

다음 경고 규칙은 다음과 같습니다 [실시간 고객 프로필](../../profile/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 프로필 수집 정보 | 프로필 흐름 실행 시작 | 이 경고는 프로필 흐름 실행이 데이터 처리를 시작할 때 트리거됩니다. |
| 프로필 수집 정보 | 프로필 흐름 실행 성공 | 이 경고는 데이터가 데이터 레이크에서 프로필로 성공적으로 로드될 때 트리거됩니다. |
| 프로필 수집 지연, 실패 및 오류 | 프로필 흐름 실행 지연 | 이 경고는 데이터 레이크에서 프로필로 데이터를 로드하는 데 150분 이상 걸릴 때 트리거됩니다. |
| 프로필 수집 지연, 실패 및 오류 | 프로필 흐름 실행 실패 | 이 경고는 프로필로 데이터를 수집하는 동안 오류가 발생하면 트리거됩니다. |

{style="table-layout:auto"}

## 세그먼테이션

다음 경고 규칙은 다음과 같습니다 [세분화 서비스](../../segmentation/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 세그먼트 평가 작업 정보 | 세그먼트 작업 시작 | 이 경고는 세그먼트 평가 작업이 데이터 처리를 시작할 때 트리거됩니다. |
| 세그먼트 평가 작업 정보 | 세그먼트 작업 성공 | 이 경고는 세그먼트 평가 작업이 성공적으로 완료되면 트리거됩니다. |
| 세그먼트 평가 작업 지연, 실패 및 오류 | 세그먼트 작업 지연 | 이 경고는 세그먼트 평가 작업이 완료되는 데 150분 이상 걸릴 때 트리거됩니다. <br> 다음 상태 중 하나가 표시됩니다. <br>- 실행 중 - 실패 또는 지연 조건이 충족되었습니다(활성 상태로 간주함). <br>- 비활성 - 조건이 충족되지 않았거나 해결되지 않았습니다(해결됨 상태로 간주함). |
| 세그먼트 평가 작업 지연, 실패 및 오류 | 세그먼트 작업 실패 | 이 경고는 세그먼트 평가 작업으로 인해 오류가 발생하는 경우 트리거됩니다. |
| 세그먼트 평가 작업 지연, 실패 및 오류 | 세그먼트 정의 비활성화됨 | 이 경고는 내부 오류로 인해 세그먼트 정의가 비활성화될 때 트리거됩니다. 이렇게 하면 Adobe 엔지니어링 팀이 문제를 조사할 수 있는 워 룸이 자동으로 트리거됩니다. 이 경고는 유용한 정보만 제공하기 위한 것이며 사용자의 조치가 필요하지 않습니다. |

{style="table-layout:auto"}

## 대상

다음 경고 규칙은 다음과 같습니다 [대상](../../destinations/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 대상 흐름 실행 정보 | 대상 플로우 실행 시작 | 이 경고는 대상 흐름 실행이 세그먼트 활성화를 시작할 때 트리거됩니다. |
| 대상 흐름 실행 정보 | 대상 흐름 실행 성공 | 이 경고는 세그먼트가 대상에 성공적으로 활성화되면 트리거됩니다. |
| 대상 플로우 실행 지연, 오류 | 대상 흐름 실행 지연 | 이 경고는 대상 흐름 실행이 세그먼트를 활성화하는 데 150분 이상 걸릴 때 트리거됩니다. |
| 대상 플로우 실행 지연, 오류 | 대상 흐름 실행 실패 | 이 경고는 대상에 대한 세그먼트를 활성화하는 동안 오류가 발생하면 트리거됩니다. |
| 대상 플로우 실행 지연, 오류 | 건너뛰기 비율이 임계값을 초과합니다. | 이 경고는 총 ID에 대한 건너뛴 ID 비율이 임계값을 초과하는 경우 트리거됩니다. |

{style="table-layout:auto"}

## 쿼리 서비스

다음 경고 규칙은 다음과 같습니다 [쿼리 서비스](../../query-service/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 쿼리 서비스 예약 쿼리 정보 | 쿼리 서비스 예약 쿼리 시작 | 이 경고는 예약된 쿼리 실행이 시작될 때 트리거됩니다. |
| 쿼리 서비스 예약 쿼리 정보 | 쿼리 서비스 예약 쿼리 성공 | 이 경고는 예약된 쿼리 작업이 성공적으로 완료되면 트리거됩니다. |
| 쿼리 서비스 예약 쿼리 지연, 실패 및 오류 | 쿼리 서비스 예약 쿼리 실패 | 이 경고는 예약된 쿼리 작업이 실패하면 트리거됩니다. |

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
