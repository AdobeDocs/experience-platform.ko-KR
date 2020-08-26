---
product: experience-platform
audience: user
user-guide-title: Adobe Experience Platform 데이터 통합 도움말
user-guide-description: Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Platform services.
translation-type: tm+mt
source-git-commit: bd3c31e7d39f7f66d755356a3dbb754e97c196fb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 7%

---


# Adobe Experience Platform Data Ingestion {#ingestion}

- [데이터 통합 개요](home.md)
- 스트리밍 통합 {#streaming}
   - [개요](streaming-ingestion/overview.md)
   - [Kafka 커넥터](streaming-ingestion/kafka.md)
   - [문제 해결](streaming-ingestion/troubleshooting.md)
- 일괄 처리{#batch}
   - [개요](batch-ingestion/overview.md)
   - [일괄 처리 API](batch-ingestion/api-overview.md)
   - [부분 일괄 처리](batch-ingestion/partial.md)
   - [문제 해결](batch-ingestion/troubleshooting.md)
- 자습서 {#tutorials}
   - [XDM에 CSV 파일 매핑](tutorials/map-a-csv-file.md)
   - [UI를 사용하여 일괄 처리 데이터 인제스트](tutorials/ingest-batch-data.md)
   - [인증된 스트리밍 연결 만들기](tutorials/create-authenticated-streaming-connection.md)
   - [스트리밍 연결(API) 만들기](tutorials/create-streaming-connection.md)
   - [스트리밍 연결 만들기(UI)](tutorials/create-streaming-connection-ui.md)
   - [스트리밍 레코드 데이터](tutorials/streaming-record-data.md)
   - [스트리밍 시계열 데이터](tutorials/streaming-time-series-data.md)
   - [여러 메시지 스트리밍](tutorials/streaming-multiple-messages.md)
- 데이터 수집 품질 및 모니터링{#quality}
   - [개요](quality/overview.md)
   - [데이터 흐름 모니터링](quality/monitor-data-flows.md)
   - [실패한 배치 검색](quality/retrieve-failed-batches.md)
   - [스트리밍 통합 유효성 검사](quality/streaming-validation.md)
   - [데이터 수집 이벤트 가입](quality/subscribe-events.md)
- [소스 커넥터](source-connectors.md)
- [API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [플랫폼 릴리스 정보](https://www.adobe.com/go/platform-release-notes-en)