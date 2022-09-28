---
keywords: Experience Platform;홈;인기 항목;날짜 범위
title: 표준 경고 규칙
description: 이 문서에서는 Experience Platform이 제공하는 사전 정의된 경고 규칙을 다룹니다.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: f707a6338ad72578328b363792010fa50ea9ce88
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 3%

---

# 표준 경고 규칙

Adobe Experience Platform은 조직에 대해 활성화할 수 있는 사전 정의된 여러 경고 규칙을 제공합니다. 이 문서에서는 이러한 Adobe 제공 경고 규칙에 대한 세부 사항을 다룹니다. Experience Platform의 경고에 대한 일반적인 정보는 [경고 개요](./overview.md).

When [플랫폼 UI에서 경고 규칙 보기](./ui.md)각 규칙에 개별적으로 가입할 수 있습니다. 경고 구독 시 [I/O 이벤트 알림](./subscribe.md)그러나 경고 규칙은 다른 구독 패키지로 구성되어 있습니다. 아래 표에는 각 규칙이 해당 I/O 이벤트 구독 이름과 함께 표시됩니다.

## 데이터 수집

다음 경고 규칙은 다음과 같습니다 [데이터 수집](../../ingestion/home.md) 및  [소스](../../sources/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 소스 흐름 실행 정보 | 소스 흐름 실행 시작 | 이 경고는 소스 연결에서 데이터 처리를 시작할 때 트리거됩니다. |
| 소스 흐름 실행 정보 | 소스 흐름 실행 성공 | 이 경고는 소스 연결에서 데이터를 성공적으로 수집할 때 트리거됩니다. |
| 소스 흐름 실행 지연, 오류 및 오류 | 소스 흐름 실행 실패 | 이 경고는 소스 연결에서 데이터를 수집하는 동안 오류가 발생하면 트리거됩니다. |
| 소스 흐름 실행 지연, 오류 및 오류 | 수집 지연 | 이 경고는 배치 수집 흐름 실행을 처리하는 데 150분 이상 걸릴 때 트리거됩니다. |
| 소스 흐름 실행 지연, 오류 및 오류 | 수집 실패 | 이 경고는 모든 레코드에 대한 실패한 레코드 비율이 임계값 0.5%를 초과할 때 트리거됩니다. |

{style=&quot;table-layout:auto&quot;}

이전에 다음 경고 유형을 구독한 경우, 이 경고가 더 이상 사용되지 않으므로 더 이상 경고를 받지 않습니다.

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 소스 흐름 실행 지연, 오류 및 오류 | 수집 부족 | 이 경고는 수집이 7시간 이상 지연되고 Platform에 데이터를 수집하지 않는 경우 메시지를 보냅니다. |

{style=&quot;table-layout:auto&quot;}

## ID 서비스

다음 경고 규칙은 다음과 같습니다 [ID 서비스](../../identity-service/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| ID 수집 정보 | ID 서비스 흐름 실행 시작 | 이 경고는 Identity Service 흐름 실행이 데이터 처리를 시작할 때 트리거됩니다. 즉, 수집된 데이터가 Data Lake에서 Identity 서비스로 로드되고 있습니다. |
| ID 수집 정보 | ID 서비스 흐름 실행 성공 | 이 경고는 Data Lake에서 Identity 서비스로 데이터가 성공적으로 로드되면 트리거됩니다. |
| ID 수집 지연, 오류 및 오류 | ID 서비스 흐름 실행 지연 | 이 경고는 ID 서비스 흐름 실행을 처리하는 데 150분 이상 걸릴 때 트리거됩니다. |
| ID 수집 지연, 오류 및 오류 | ID 서비스 흐름 실행 실패 | 이 경고는 데이터를 Identity 서비스로 수집하는 동안 오류가 발생하면 트리거됩니다. |

{style=&quot;table-layout:auto&quot;}

## 실시간 고객 프로필

다음 경고 규칙은 다음과 같습니다 [실시간 고객 프로필](../../profile/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 프로필 수집 정보 | 프로필 흐름 실행 시작 | 이 경고는 프로필 흐름 실행이 데이터 처리를 시작할 때 트리거됩니다. |
| 프로필 수집 정보 | 프로필 흐름 실행 성공 | 이 경고는 데이터가 데이터 레이크에서 프로필에 성공적으로 로드되면 트리거됩니다. |
| 프로필 수집 지연, 오류 및 오류 | 프로필 흐름 실행 지연 | 이 경고는 Data Lake에서 Profile로 데이터를 로드하는 데 150분 이상 걸릴 때 트리거됩니다. |
| 프로필 수집 지연, 오류 및 오류 | 프로필 흐름 실행 실패 | 이 경고는 데이터를 프로필에 수집하는 동안 오류가 발생하면 트리거됩니다. |

{style=&quot;table-layout:auto&quot;}

## 세그먼테이션

다음 경고 규칙은 다음과 같습니다 [세분화 서비스](../../segmentation/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 세그먼트 평가 작업 정보 | 세그먼트 작업 시작 | 이 경고는 세그먼트 평가 작업이 데이터 처리를 시작할 때 트리거됩니다. |
| 세그먼트 평가 작업 정보 | 세그먼트 작업 성공 | 이 경고는 세그먼트 평가 작업이 성공적으로 완료되면 트리거됩니다. |
| 세그먼트 평가 작업 지연, 오류 및 오류 | 세그먼트 작업 지연 | 이 경고는 세그먼트 평가 작업을 완료하는 데 150분 이상 걸리는 경우 트리거됩니다. |
| 세그먼트 평가 작업 지연, 오류 및 오류 | 세그먼트 작업 실패 | 이 경고는 세그먼트 평가 작업으로 인해 오류가 발생할 때 트리거됩니다. |
| 세그먼트 평가 작업 지연, 오류 및 오류 | 세그먼트 정의 사용 안 함 | 이 경고는 내부 오류로 인해 세그먼트 정의가 비활성화될 때 트리거됩니다. Adobe 엔지니어링 팀이 이 문제를 조사하도록 자동으로 전쟁 공간을 트리거합니다. 이 경보는 정보용으로만 사용되며 사용자의 작업이 필요하지 않습니다. |

{style=&quot;table-layout:auto&quot;}

## 대상

다음 경고 규칙은 다음과 같습니다 [대상](../../destinations/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 대상 흐름 실행 정보 | 대상 흐름 실행 시작 | 이 경고는 대상 흐름 실행이 세그먼트 활성화를 시작할 때 트리거됩니다. |
| 대상 흐름 실행 정보 | 대상 흐름 실행 성공 | 이 경고는 세그먼트가 대상에 성공적으로 활성화되면 트리거됩니다. |
| 대상 흐름 실행 지연, 오류 및 오류 | 대상 흐름 실행 지연 | 이 경고는 대상 흐름 실행이 세그먼트를 활성화하는 데 150분 이상 걸릴 때 트리거됩니다. |
| 대상 흐름 실행 지연, 오류 및 오류 | 대상 흐름 실행 실패 | 이 경고는 세그먼트를 대상에 활성화하는 동안 오류가 발생하면 트리거됩니다. |
| 대상 흐름 실행 지연, 오류 및 오류 | 건너가기가 임계값을 초과합니다. | 이 경고는 건너뛴 ID와 총 ID의 비율이 임계값을 초과하는 경우 트리거됩니다. |

{style=&quot;table-layout:auto&quot;}

## 쿼리 서비스

다음 경고 규칙은 다음과 같습니다 [쿼리 서비스](../../query-service/home.md):

| I/O 이벤트 구독 | 경고 규칙 | 설명 |
| --- | --- | --- |
| 쿼리 서비스 임시 정보 | 쿼리 서비스 Ad Hoc 성공 | 이 경고는 임시 스키마 작업이 성공적으로 완료되면 트리거됩니다. |
| 쿼리 서비스 애드혹 지연, 오류 및 오류 | 쿼리 서비스 임시 실패 | 이 경고는 임시 스키마 작업이 실패할 때 트리거됩니다. |
| 쿼리 서비스 예약된 쿼리 정보 | 쿼리 서비스 예약된 쿼리 시작 | 이 경고는 예약된 쿼리 실행이 시작되면 트리거됩니다. |
| 쿼리 서비스 예약된 쿼리 정보 | 쿼리 서비스 예약된 쿼리 성공 | 이 경고는 예약된 쿼리 작업이 성공적으로 완료되면 트리거됩니다. |
| 쿼리 서비스 예약된 쿼리 지연, 오류 및 오류 | 쿼리 서비스 예약 쿼리 실패 | 이 경고는 예약된 쿼리 작업이 실패하면 트리거됩니다. |

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
