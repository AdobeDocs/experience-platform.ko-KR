---
audience: user
user-guide-title: Adobe Experience Platform 쿼리 서비스 도움말
breadcrumb-title: 쿼리 서비스 안내서
user-guide-description: 표준 SQL을 사용하여 Experience Platform의 데이터 레이크 내에서 데이터를 쿼리합니다.
feature: Queries
source-git-commit: a78f7499b55dcedbe379e917b94946948c66e6e5
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 20%

---


# Adobe Experience Platform 쿼리 서비스 {#query}

- [쿼리 서비스 개요](home.md)
- [쿼리 서비스 패키징](packages.md)
- [쿼리 서비스 보호 기능](guardrails.md)
- 시작 {#get-started}
   - [전제 조건](get-started/prerequisites.md)
- 데이터 Distiller {#data-distiller}
   - [개요](data-distiller/overview.md)
   - [라이선스 사용](data-distiller/license-usage.md)
   - 쿼리 가속 저장소 {#query-accelerated-store}
      - [가속화된 쿼리 보내기](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Reporting insights 데이터 모델 안내서](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - 파생 속성 {#derived-attributes}
      - [개요](data-distiller/derived-attributes/overview.md)
      - [원활한 SQL 흐름](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [십분위수 기반 파생 속성 만들기](data-distiller/derived-attributes/decile-based-derived-attributes.md)
   - AI/ML 기능 파이프라인 {#ml-feature-pipelines}
      - [개요](data-distiller/ml-feature-pipelines/overview.md)
      - [Jupyter Notebooks 연결](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [탐색적 데이터 분석](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [ML용 엔지니어 기능](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [ML 환경으로 데이터 내보내기](data-distiller/ml-feature-pipelines/export-data.md)
      - [AI/ML 데이터 파이프라인 강화 통합 워크플로](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- 사용 사례 {#use-cases}
   - [찾아보기 중단됨](use-cases/abandoned-browse.md)
   - [속성 분석](use-cases/attribution-analysis.md)
   - [봇 필터링](use-cases/bot-filtering.md)
   - [이벤트의 트렌드 보고서 만들기](use-cases/trended-report-of-events.md)
   - [동의 분석](use-cases/consent-analysis.md)
   - [고객 생애 가치](use-cases/customer-lifetime-value.md)
   - [십분위수 기반 파생 속성](use-cases/deciles-use-case.md)
   - [유사 항목 일치](use-cases/fuzzy-match.md)
   - [사용자의 페이지 보기 나열](use-cases/list-visitor-sessions.md)
   - [페이지 보기별로 방문자 나열](use-cases/visitors-by-number-of-page-views.md)
   - [성향 점수](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [분석 데이터에서 머천다이징 변수 반환 및 사용](use-cases/merchandising-variables.md)
   - [방문자에 대한 롤업 보고서 보기](use-cases/roll-up-report-of-a-visitor.md)
   - [웹 및 모바일 분석 인사이트](use-cases/analytics-insights.md)
- 클라이언트를 쿼리 서비스에 연결 {#clients}
   - [클라이언트 연결 개요](clients/overview.md)
   - [SSL 모드](./clients/ssl-modes.md)
   - [아쿠아 데이터 스튜디오](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [보는 사람](clients/looker.md)
   - [포스티코](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [스튜디오](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- 쿼리 서비스 UI {#ui}
   - [UI 개요](ui/overview.md)
   - [쿼리 편집기 사용 안내서](ui/user-guide.md)
   - [쿼리 템플릿](ui/query-templates.md)
   - [매개변수화된 쿼리](ui/parameterized-queries.md)
   - [쿼리 일정](ui/query-schedules.md)
   - [쿼리 로그](ui/query-logs.md)
   - [예약된 쿼리 모니터링](ui/monitor-queries.md)
   - [자격 증명 안내서](ui/credentials.md)
   - [쿼리 결과에서 출력 데이터 세트 생성](ui/create-datasets.md)
- 쿼리 서비스 API 끝점 {#api}
   - [시작하기](api/getting-started.md)
   - [쿼리](api/queries.md)
   - [연결 매개변수](api/connection-parameters.md)
   - [일정](api/scheduled-queries.md)
   - [예약된 쿼리에 대해 실행](api/runs-scheduled-queries.md)
   - [쿼리 템플릿](api/query-templates.md)
   - [가속화된 쿼리](api/accelerated-queries.md)
   - [경고 구독](api/alert-subscriptions.md)
- 데이터 거버넌스 {#data-governance}
   - [개요](data-governance/overview.md)
   - [감사 로그 안내서](data-governance/audit-log-guide.md)
   - [애드혹 스키마 데이터 세트의 ID](data-governance/ad-hoc-schema-identities.md)
   - [Ad Hoc 스키마에 대한 속성 기반 액세스 제어 지원](./data-governance/ad-hoc-schema-labels.md)
- 모범 사례 {#best-practices}
   - [쿼리 실행](best-practices/writing-queries.md)
   - [데이터 자산 조직](./best-practices/organize-data-assets.md)
- 기본 개념 {#essential-concepts}
   - [중첩 데이터 구조 작업](essential-concepts/nested-data-structures.md)
   - [중첩된 데이터 구조 평면화](essential-concepts/flatten-nested-data.md)
   - [익명 블록](essential-concepts/anonymous-block.md)
   - [인라인 템플릿](essential-concepts/inline-templates.md)
   - [증분 로드](essential-concepts/incremental-load.md)
   - [데이터 중복 제거](essential-concepts/deduplication.md)
   - [데이터 세트 샘플](essential-concepts/dataset-samples.md)
   - [데이터 세트 통계 계산](essential-concepts/dataset-statistics.md)
- SQL 참조 {#sql}
   - [SQL 개요](sql/overview.md)
   - [SQL 구문](sql/syntax.md)
   - [Adobe 정의 함수](sql/adobe-defined-functions.md)
   - [Spark SQL 함수](sql/spark-sql-functions.md)
   - [메타데이터 명령](sql/metadata.md)
   - [준비된 문](sql/prepared-statements.md)
- [자주 묻는 질문](troubleshooting-guide.md)
- [허용 목록에 추가하다 IP 주소](ip-address-allowlist.md)
- [API 참조](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Platform 릴리스 정보](https://www.adobe.com/go/platform-release-notes-kr)
