---
audience: user
user-guide-title: Adobe Experience Platform 쿼리 서비스 도움말
breadcrumb-title: 쿼리 서비스 안내서
user-guide-description: 표준 SQL을 사용하여 Experience Platform의 데이터 레이크 내에서 데이터를 쿼리합니다.
feature: Queries
source-git-commit: 59fb31697d7a9f132f7e8700422538026ae24b8c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 17%

---


# Adobe Experience Platform 쿼리 서비스 {#query}

- [쿼리 서비스 개요](home.md)
- [Query Service 패키징](packages.md)
- [쿼리 서비스 보호 기능](guardrails.md)
- 데이터 Distiller {#data-distiller}
   - [라이선스 사용](data-distiller/licence-usage.md)
- 시작 {#get-started}
   - [전제 조건](get-started/prerequisites.md)
- 사용 사례 {#use-cases}
   - [찾아보기 포기](use-cases/abandoned-browse.md)
   - [Adobe Target을 사용한 활동 분석](use-cases/activity-analysis-with-adobe-target.md)
   - [속성 분석](use-cases/attribution-analysis.md)
   - [보트 필터링](use-cases/bot-filtering.md)
   - [웹 및 모바일 분석 통찰력](use-cases/analytics-insights.md)
- 쿼리 서비스 API {#api}
   - [시작하기](api/getting-started.md)
   - [쿼리](api/queries.md)
   - [연결 매개 변수](api/connection-parameters.md)
   - [예약된 쿼리](api/scheduled-queries.md)
   - [예약된 쿼리에 대해 실행됩니다](api/runs-scheduled-queries.md)
   - [쿼리 템플릿](api/query-templates.md)
- 쿼리 서비스 UI {#ui}
   - [UI 개요](ui/overview.md)
   - [쿼리 편집기 사용 안내서](ui/user-guide.md)
   - [쿼리 템플릿](ui/query-templates.md)
   - [쿼리 서비스 자격 증명 사용](ui/credentials.md)
   - [쿼리 결과에서 데이터 세트 생성](ui/create-datasets.md)
- [쿼리 모니터링](monitor-queries.md)
- 쿼리 가속 저장소{#query-accelerated-store}
   - [보고 통찰력 데이터 모델](query-accelerated-store/reporting-insights-data-model.md)
- 모범 사례 {#best-practices}
   - [쿼리 실행에 대한 일반 지침](best-practices/writing-queries.md)
   - [데이터 자산 조직에 대한 지침](./best-practices/organize-data-assets.md)
   - [중첩된 데이터 구조를 사용한 작업](best-practices/nested-data-structures.md)
   - [중첩 데이터 구조 평면화](best-practices/flatten-nested-data.md)
   - [익명 블록](best-practices/anonymous-block.md)
   - [증분 로드](best-practices/incremental-load.md)
   - [데이터 중복 제거](best-practices/deduplication.md)
- 파생 특성 {#derived-attributes}
   - [개요](derived-attributes/overview.md)
   - [십진수 사용 사례](derived-attributes/deciles-use-case.md)
- 샘플 쿼리 {#sample-queries}
   - [샘플 경험 이벤트 쿼리](sample-queries/experience-event.md)
   - [샘플 Adobe Analytics 쿼리](sample-queries/adobe-analytics.md)
- SQL 참조 {#sql}
   - [SQL 개요](sql/overview.md)
   - [SQL 구문](sql/syntax.md)
   - [Adobe 정의 함수](sql/adobe-defined-functions.md)
   - [스파크 SQL 함수](sql/spark-sql-functions.md)
   - [메타데이터 명령](sql/metadata.md)
   - [준비된 설명](sql/prepared-statements.md)
   - [데이터 집합 샘플](sql/dataset-samples.md)
- 클라이언트를 Query Service에 연결 {#clients}
   - [클라이언트 연결 개요](clients/overview.md)
   - [SSL 모드](./clients/ssl-modes.md)
   - [아쿠아 데이터 스튜디오](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupiter 노트북](clients//jupyter-notebook.md)
   - [조회](clients/looker.md)
   - [포스티코](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [타블로](clients/tableau.md)
- 데이터 거버넌스 {#data-governance}
   - [개요](data-governance/overview.md)
   - [감사 로그 안내서](data-governance/audit-log-guide.md)
   - [임시 스키마 데이터 세트의 ID](data-governance/ad-hoc-schema-identities.md)
   - [Ad Hoc 스키마에 대한 특성 기반 액세스 제어 지원](./data-governance/ad-hoc-schema-labels.md)
- [문제 해결 안내서](troubleshooting-guide.md)
- [API 참조](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [플랫폼 릴리스 노트](https://www.adobe.com/go/platform-release-notes-en)