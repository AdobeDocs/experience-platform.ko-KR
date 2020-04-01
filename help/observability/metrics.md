---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 사용 가능한 지표
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# 사용 가능한 지표 목록

다음은 Observability Insights에서 각 지표와 관련 플랫폼 서비스, 설명 및 수락된 ID 쿼리 매개 변수를 통해 표시되는 지표 목록입니다.

| 인사이트 지표 | 플랫폼 서비스 | 설명 | ID 쿼리 매개 변수 |
| ---- | ---- | ---- | ---- |
| timelines.ingestion.dataset.new.count | 데이터 통합 | 생성된 총 데이터 집합 수입니다. | N/A |
| timelines.ingestion.dataset.size | 데이터 통합 | 데이터 세트 하나 또는 모든 데이터 세트에 대해 수집되는 모든 데이터의 누적 크기입니다. | 데이터 집합 ID(선택 사항) |
| timelines.ingestion.dataset.dailysize | 데이터 통합 | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 일별 사용 기반으로 데이터 인제스트 크기 | 데이터 집합 ID(선택 사항) |
| timelines.ingestion.dataset.batchfailed.count | 데이터 통합 | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 실패한 일괄 처리 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.ingestion.dataset.batchsuccess.count | 데이터 통합 | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 인제스트된 배치 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.ingestion.dataset.recordsuccess.count | 데이터 통합 | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.total.messages.rate | 데이터 통합(스트리밍) | 하나의 데이터 집합 또는 모든 데이터 집합에 대한 총 메시지 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.valid.messages.rate | 데이터 통합(스트리밍) | 하나의 데이터 집합 또는 모든 데이터 집합에 대해 유효한 총 메시지 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.invalid.messages.rate | 데이터 통합(스트리밍) | 하나의 데이터 집합 또는 모든 데이터 집합에 대해 잘못된 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.category.type.count | 데이터 통합(스트리밍) | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;유형&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.category.range.count | 데이터 통합(스트리밍) | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;범위&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.category.format.count | 데이터 통합(스트리밍) | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;형식&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.category.pattern.count | 데이터 통합(스트리밍) | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;패턴&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.category.presence.count | 데이터 통합(스트리밍) | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;존재&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.category.enum.count | 데이터 통합(스트리밍) | 하나의 데이터 집합 또는 모든 데이터 집합에 대해 잘못된 &quot;열거형&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.data.collection.validation.category.unclased.count | 데이터 통합(스트리밍) | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;분류되지 않은&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timeselines.data.collection.validation.category.unknown.count | 데이터 통합(스트리밍) | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 잘못된 &quot;알 수 없음&quot; 메시지의 총 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.data.collection.inlet.total.messages.received | 데이터 통합(스트리밍) | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대해 받은 총 메시지 수입니다. | 입구 ID(옵션) |
| timeselines.data.collection.total.messages.size.received | 데이터 통합(스트리밍) | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대해 수신된 데이터의 전체 크기입니다. | 입구 ID(옵션) |
| timelines.data.collection.inlet.success | 데이터 통합(스트리밍) | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대한 성공적인 HTTP 호출의 총 수입니다. | 입구 ID(옵션) |
| timeselines.data.collection.inlet.failure | 데이터 통합(스트리밍) | 하나의 데이터 입력부 또는 모든 데이터 입력란에 대한 실패한 HTTP 호출의 총 수입니다. | 입구 ID(옵션) |
| timelines.profiles.dataset.recordabid.count | 실시간 고객 프로필 | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 프로필별로 데이터 레이크에서 읽은 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.profiles.dataset.recordsuccess.count | 실시간 고객 프로필 | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 프로필별로 데이터 소스에 기록된 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.profiles.dataset.recordfailed.count | 실시간 고객 프로필 | 한 데이터 세트 또는 모든 데이터 세트에 대해 프로필에 의해 실패한 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.profiles.dataset.batchsuccess.count | 실시간 고객 프로필 | 데이터 세트 또는 모든 데이터 세트에 대해 수집되는 프로필 배치 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.profiles.dataset.batchfailed.count | 실시간 고객 프로필 | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 실패한 프로필 배치 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.identity.dataset.recordsuccess.count | ID 서비스 | 하나의 데이터 세트 또는 모든 데이터 세트에 대해 ID 서비스가 데이터 소스에 쓴 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.identity.dataset.recordfailed.count | ID 서비스 | ID 서비스에서 한 데이터 세트 또는 모든 데이터 세트에 대해 실패한 레코드 수입니다. | 데이터 집합 ID(선택 사항) |
| timelines.identity.dataset.namespacecode.recordsuccess.count | ID 서비스 | 네임스페이스에 대해 인제스트된 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timelines.identity.dataset.namespacecode.recordfailed.count | ID 서비스 | 네임스페이스에 의해 실패한 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timelines.identity.dataset.namespacecode.recordswithed.count | ID 서비스 | 네임스페이스로 건너뛴 ID 레코드 수입니다. | 네임스페이스 ID(**필수**) |
| timeselines.identity.graph.imsorg.uniqueidity.count | ID 서비스 | IMS 조직에 대한 ID 그래프에 저장된 고유 ID 수. | N/A |
| timelines.identity.graph.imsorg.namespacecode.uniqueidity.count | ID 서비스 | 네임스페이스에 대한 ID 그래프에 저장된 고유 ID의 수입니다. | 네임스페이스 ID(**필수**) |
| timeselines.identity.graph.imsorg.numidgraphs.count | ID 서비스 | IMS 조직에 대한 ID 그래프에 저장된 고유한 그래프 ID의 수입니다. | N/A |
| timelines.identity.graph.imsorg.graphstrength.uniqueidity.count | ID 서비스 | IMS에 대한 ID 그래프에 저장된 고유 ID의 수입니다. 특정 그래프 강도(&quot;알 수 없음&quot;, &quot;약함&quot; 또는 &quot;강함&quot;)에 대한 조직입니다. | 그래프 강도(**필수**) |
| timeselines.gdpr.jobs.totaljobs.count | GDPR | GDPR에서 만든 총 작업 수입니다. | ENV(**필수**) |
| timeselines.gdpr.jobs.completedjobs.count | GDPR | GDPR에서 완료된 총 작업 수입니다. | ENV(**필수**) |
| timeselines.gdpr.jobs.errorjobs.count | GDPR | GDPR의 총 오류 작업 수입니다. | ENV(**필수**) |
| timeselines.queryservice.query.scheduleonce.count | 쿼리 서비스 | 반복되지 않는 총 예약된 쿼리 수입니다. | N/A |
| timeselines.queryservice.query.scheduledrecipe.count | 쿼리 서비스 | 반복 예약된 총 쿼리 수입니다. | N/A |
| timeselines.queryservice.query.batchquery.count | 쿼리 서비스 | 실행된 일괄 처리 쿼리의 총 수입니다. | N/A |
| timeselines.queryservice.query.scheduledquery.count | 쿼리 서비스 | 실행된 총 예약된 쿼리 수입니다. | N/A |
| timeselines.queryservice.query.interactivequery.count | 쿼리 서비스 | 실행된 대화형 쿼리의 총 수입니다. | N/A |
| timeselines.queryservice.query.batchfrompsqlquery.count | 쿼리 서비스 | PSQL에서 실행된 배치 쿼리의 총 수입니다. | N/A |