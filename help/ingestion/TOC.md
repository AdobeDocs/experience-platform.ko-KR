---
audience: user
user-guide-title: Adobe Experience Platform 데이터 수집 도움말
breadcrumb-title: Data Ingestion 안내서
user-guide-description: 일괄 처리 또는 스트리밍 통합 기능을 통해 데이터를 Experience Platform으로 가져올 수 있습니다.
feature: Data Ingestion
role: Developer
source-git-commit: e828485ad5b0904c9dc66b43d1cdb3c4707885b1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 18%

---


# Adobe Experience Platform 데이터 수집 {#ingestion}

- [데이터 수집 개요](home.md)
- 스트리밍 수집 {#streaming}
   - [개요](streaming-ingestion/overview.md)
   - [Kafka 커넥터](streaming-ingestion/kafka.md)
   - [문제 해결](streaming-ingestion/troubleshooting.md)
- 일괄 처리 수집{#batch}
   - [일괄 처리 수집 API 시작](batch-ingestion/getting-started.md)
   - [API 개요](batch-ingestion/overview.md)
   - [API 개발자 안내서](batch-ingestion/api-overview.md)
   - [부분 일괄 처리 수집](batch-ingestion/partial.md)
   - [문제 해결](batch-ingestion/troubleshooting.md)
- 튜토리얼 {#tutorials}
   - XDM {#map-csv}에 CSV 파일 매핑
      - [개요](./tutorials/map-csv/overview.md)
      - [CSV 파일을 기존 스키마에 매핑](./tutorials/map-csv/existing-schema.md)
      - [AI가 생성한 권장 사항을 사용하여 CSV 파일 매핑](./tutorials/map-csv/recommendations.md)
   - [UI를 사용하여 배치 데이터 수집](tutorials/ingest-batch-data.md)
   - [인증된 스트리밍 연결 만들기](tutorials/create-authenticated-streaming-connection.md)
   - [스트리밍 연결(API) 만들기](tutorials/create-streaming-connection.md)
   - [스트리밍 연결(UI) 만들기](tutorials/create-streaming-connection-ui.md)
   - [레코드 데이터 스트리밍](tutorials/streaming-record-data.md)
   - [시계열 데이터 스트리밍](tutorials/streaming-time-series-data.md)
   - [여러 메시지 스트리밍](tutorials/streaming-multiple-messages.md)
- 데이터 품질 및 모니터링{#quality}
   - [개요](quality/overview.md)
   - [데이터 수집 모니터링](quality/monitor-data-ingestion.md)
   - [오류 진단 검색](quality/error-diagnostics.md)
   - [실패한 일괄 처리 검색](quality/retrieve-failed-batches.md)
   - [스트리밍 수집 유효성 검사](quality/streaming-validation.md)
   - [데이터 수집 알림](quality/subscribe-events.md)
- [데이터 수집 보호](guardrails.md)
- [Source 커넥터](source-connectors.md)
- [일괄 처리 수집 API 참조](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [스트리밍 수집 API 참조](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [플랫폼 릴리스 정보](https://experienceleague.adobe.com/ko/docs/experience-platform/release-notes/latest)
