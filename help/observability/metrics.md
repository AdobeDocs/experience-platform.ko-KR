---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 사용 가능한 지표
topic: developer guide
translation-type: tm+mt
source-git-commit: ff299a69a81f00cad3e90a83f7411e4b15d4f850

---


# 사용 가능한 지표 목록

다음 표는 Observability Insights에 의해 노출된 모든 지표를 플랫폼 서비스로 분류합니다. 각 지표에는 설명 및 승인된 ID 쿼리 매개 변수가 포함되어 있습니다.

## 데이터 통합

다음 표에서는 Adobe Experience Platform 데이터 수집에 대한 지표에 대해 간략히 설명합니다. 굵게 표시된 **지표는** 스트리밍 통합 지표입니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 생성된 총 데이터 집합 수입니다. | N/A |
| timeseries.ingestion.dataset.size | 데이터 세트 하나 또는 모든 데이터 세트에 대해 수집되는 모든 데이터의 누적 크기입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.ingestion.dataset.dailysize | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 일별 사용 기반으로 데이터 인제스트 크기 | 데이터 집합 ID(선택 사항) |
| timeseries.ingestion.dataset.batchfailed.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 실패한 일괄 처리 수입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.ingestion.dataset.batchsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 인제스트된 배치 수입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.ingestion.dataset.recordsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.total.messages.rate** | 하나의 데이터 집합 또는 모든 데이터 집합에 대한 총 메시지 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.valid.messages.rate** | 하나의 데이터 집합 또는 모든 데이터 집합에 대해 유효한 총 메시지 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.invalid.messages.rate** | 하나의 데이터 집합 또는 모든 데이터 집합에 대해 잘못된 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.category.type.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;유형&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.category.range.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;범위&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.category.format.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;형식&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.category.pattern.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;패턴&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.category.presence.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;존재&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.category.enum.count** | 하나의 데이터 집합 또는 모든 데이터 집합에 대해 잘못된 &quot;열거형&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timelines.data.collection.validation.category.unclased.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;분류되지 않은&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timeselines.data.collection.validation.category.unknown.count** | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;알 수 없음&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| **timelines.data.collection.inlet.total.messages.received** | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대해 받은 총 메시지 수입니다. | 입구 ID(옵션) |
| **timeselines.data.collection.total.messages.size.received** | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대해 수신된 데이터의 전체 크기입니다. | 입구 ID(옵션) |
| **timelines.data.collection.inlet.success** | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대한 성공적인 HTTP 호출의 총 수입니다. | 입구 ID(옵션) |
| **timeselines.data.collection.inlet.failure** | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대한 실패한 HTTP 호출의 총 수입니다. | 입구 ID(옵션) |

## ID 서비스

다음 표에서는 Adobe Experience Platform ID Service에 대한 지표에 대해 간략히 설명합니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 ID 서비스가 데이터 소스에 쓴 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.identity.dataset.recordfailed.count | ID 서비스에서 한 데이터 세트 또는 모든 데이터 세트에 대해 실패한 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 네임스페이스에 대해 인제스트된 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 네임스페이스에 의해 실패한 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 네임스페이스로 건너뛴 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | IMS 조직에 대한 ID 그래프에 저장된 고유 ID 수. | N/A |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 네임스페이스에 대한 ID 그래프에 저장된 고유 ID의 수입니다. | 네임스페이스 ID(**필수**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | IMS 조직에 대한 ID 그래프에 저장된 고유한 그래프 ID의 수입니다. | N/A |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS에 대한 ID 그래프에 저장된 고유 ID의 수입니다. 특정 그래프 강도(&quot;알 수 없음&quot;, &quot;약함&quot; 또는 &quot;강함&quot;)에 대한 조직입니다. | 그래프 강도(**필수**) |

## 개인 정보 서비스

다음 표는 Adobe Experience Platform Privacy Service에 대한 지표에 대해 간략히 설명합니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | GDPR에서 만든 총 작업 수입니다. | ENV(**필수**) |
| timeseries.gdpr.jobs.completedjobs.count | GDPR에서 완료된 총 작업 수입니다. | ENV(**필수**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR의 총 오류 작업 수입니다. | ENV(**필수**) |

## 쿼리 서비스

다음 표에서는 Adobe Experience Platform 쿼리 서비스에 대한 지표에 대해 간략히 설명합니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 반복되지 않는 총 예약된 쿼리 수입니다. | N/A |
| timeseries.queryservice.query.scheduledrecurring.count | 반복 예약된 총 쿼리 수입니다. | N/A |
| timeseries.queryservice.query.batchquery.count | 실행된 일괄 처리 쿼리의 총 수입니다. | N/A |
| timeseries.queryservice.query.scheduledquery.count | 실행된 총 예약된 쿼리 수입니다. | N/A |
| timeseries.queryservice.query.interactivequery.count | 실행된 대화형 쿼리의 총 수입니다. | N/A |
| timeseries.queryservice.query.batchfrompsqlquery.count | PSQL에서 실행된 배치 쿼리의 총 수입니다. | N/A |

## 실시간 고객 프로필

다음 표에서는 실시간 고객 프로필에 대한 지표에 대해 간략히 설명합니다.

| 인사이트 지표 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 프로필별로 데이터 레이크에서 읽은 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.profiles.dataset.recordsuccess.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 프로필별로 데이터 소스에 기록된 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.profiles.dataset.recordfailed.count | 한 데이터 세트 또는 모든 데이터 세트에 대해 프로필에 의해 실패한 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.profiles.dataset.batchsuccess.count | 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 프로필 배치 수입니다. | 데이터 집합 ID(선택 사항) |
| timeseries.profiles.dataset.batchfailed.count | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 실패한 프로필 배치 수입니다. | 데이터 집합 ID(선택 사항) |
| platform.ups.ingest.streaming.request.m1_rate | 수신 요청 비율입니다. | IMS 조직 |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 통합 성공률 | IMS 조직 |
| platform.ups.ingest.streaming.records.created.m15_rate | 데이터 세트에 대해 수집되는 새 레코드 비율입니다. | 데이터 집합 ID |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 데이터 세트에 대한 만들기 요청에 대해 순서가 잘못되어 타임스탬프가 지정된 레코드의 비율입니다. | 데이터 집합 ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 데이터 세트에 대한 마지막 레코드 만들기 요청에 대한 타임스탬프 | 데이터 집합 ID |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 데이터 세트에 대한 업데이트 요청에 대해 순서가 잘못되어 타임스탬프가 지정된 레코드의 비율입니다. | 데이터 집합 ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 데이터 세트에 대한 마지막 업데이트 레코드 요청에 대한 타임스탬프 | 데이터 집합 ID |
| platform.ups.ingest.streaming.record.size.m1_rate | 평균 레코드 크기. | IMS 조직 |
| platform.ups.ingest.streaming.records.updated.m15_rate | 데이터 세트에 대해 인제스트된 레코드에 대한 업데이트 요청 비율입니다. | 데이터 집합 ID |
