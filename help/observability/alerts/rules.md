---
keywords: Experience Platform;홈;인기 항목;날짜 범위
title: 표준 경고 규칙
description: 이 문서에서는 Experience Platform이 제공하는 사전 정의된 경고 규칙을 다룹니다.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 12%

---

# 표준 경고 규칙

Adobe Experience Platform은 조직에 대해 활성화할 수 있는 사전 정의된 여러 경고 규칙을 제공합니다. 아래 표에는 이러한 Adobe 제공 경고 규칙에 대한 세부 사항이 나와 있습니다. Experience Platform의 경고에 대한 일반적인 정보는 [경고 개요](./overview.md)를 참조하십시오.

| 규칙 | 설명 | 평가 빈도 | 반복 창 |
| --- | --- | --- | --- |
| 소스 흐름 실행 성공 | 이 경고는 소스 연결에서 데이터를 성공적으로 수집할 때 트리거됩니다. | N/A | 해당 없음 |
| 소스 흐름 실행 실패 | 이 경고는 소스 연결에서 데이터를 수집하는 동안 오류가 발생하면 트리거됩니다. | 해당 없음 | 해당 없음 |
| 세그먼트 작업 지연 | 이 경고는 세그먼트 작업을 완료하는 데 150분 이상 걸리는 경우 트리거됩니다. | 30초 | 3시간 |
| 세그먼트 정의 사용 안 함 | 이 경고는 세그먼트 정의가 비활성화될 때 트리거됩니다. | 해당 없음 | 해당 없음 |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
