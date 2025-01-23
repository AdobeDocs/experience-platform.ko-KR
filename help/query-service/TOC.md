---
audience: user
user-guide-title: Adobe Experience Platform 쿼리 서비스 도움말
breadcrumb-title: 쿼리 서비스 안내서
user-guide-description: 표준 SQL을 사용하여 Experience Platform의 데이터 레이크 내에서 데이터를 쿼리합니다.
feature: Queries
role: User,Developer
source-git-commit: c3065710e5f50541b074fc493df07130221d8078
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 21%

---


# Adobe Experience Platform 쿼리 서비스 {#query}

- [쿼리 서비스 개요](home.md)
- [쿼리 서비스 패키징](packaging.md)
- [쿼리 서비스 보호 기능](guardrails.md)
- 시작 {#get-started}
   - [전제 조건](get-started/prerequisites.md)
- 데이터 Distiller {#data-distiller}
   - [개요](data-distiller/overview.md)
   - [라이선스 사용](data-distiller/license-usage.md)
   - 파생 데이터 세트 {#derived-datasets}
      - [개요](data-distiller/derived-datasets/overview.md)
      - [SQL을 사용하여 파생 데이터 세트 만들기](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [십분위수 기반 파생 데이터 세트 만들기](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - 확장 앱 보고 {#sql-insights}에 대한 SQL Insights
      - [개요](data-distiller/sql-insights/overview.md)
      - [쿼리 프로 모드](data-distiller/sql-insights/query-pro-mode.md)
      - [가속화된 쿼리 보내기](data-distiller/sql-insights/send-accelerated-queries.md)
      - [Reporting insights 데이터 모델 안내서](data-distiller/sql-insights/reporting-insights-data-model.md)
   - AI/ML 기능 파이프라인 {#ml-feature-pipelines}
      - [개요](data-distiller/ml-feature-pipelines/overview.md)
      - [Jupyter Notebooks 연결](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [탐색적 데이터 분석](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [ML용 엔지니어 기능](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [ML 환경으로 데이터 내보내기](data-distiller/ml-feature-pipelines/export-data.md)
      - [AI/ML 데이터 파이프라인 강화 통합 워크플로](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- 데이터 Distiller 통계 및 머신 러닝 {#advanced-statistics}
   - [개요](advanced-statistics/overview.md)
   - [기능 엔지니어링](advanced-statistics/feature-engineering.md)
   - [모델](advanced-statistics/models.md)
   - [기능 변환](advanced-statistics/feature-transformation.md)
모델 {#implement-models} 구현
      - [모델 구현](advanced-statistics/implement-models/implement-models.md)
      - [회귀](advanced-statistics/implement-models/regression.md)
      - [분류](advanced-statistics/implement-models/classification.md)
      - [클러스터링](advanced-statistics/implement-models/clustering.md)
예제 {#examples}
      - [SQL 기반 로지스틱 회귀 분석을 사용하여 고객 이탈 예측](advanced-statistics/examples/predict-customer-churn.md)
- 데이터 Distiller 대상 {#data-distiller-audiences}
   - [SQL을 사용하여 외부 대상 작성](data-distiller-audiences/overview.md)
- 예 {#use-cases}
   - [개요](use-cases/overview.md)
   - [찾아보기 중단됨](use-cases/abandoned-browse.md)
   - [속성 분석](use-cases/attribution-analysis.md)
   - [보트 필터링](use-cases/bot-filtering.md)
   - [이벤트의 트렌드 보고서 만들기](use-cases/trended-report-of-events.md)
   - [동의 분석](use-cases/consent-analysis.md)
   - [고객 생애 가치](use-cases/customer-lifetime-value.md)
   - [데이터 탐색](./use-cases/data-exploration.md)
   - [십분위 기반 파생 데이터 세트](use-cases/deciles-use-case.md)
   - [퍼지 매치](use-cases/fuzzy-match.md)
   - [사용자의 페이지 보기 나열](use-cases/list-visitor-sessions.md)
   - [페이지 보기별로 방문자 나열](use-cases/visitors-by-number-of-page-views.md)
   - [SQL을 사용하여 고객 이탈 예측](use-cases/predict-customer-churn-stub.md)
   - [성향 점수](use-cases/propensity-score.md)
   - [고차 함수로 유사한 레코드 검색](use-cases/retrieve-similar-records.md)
   - [분석 데이터에서 머천다이징 변수 반환 및 사용](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [방문자에 대한 롤업 보고서 보기](use-cases/roll-up-report-of-a-visitor.md)
   - [웹 및 모바일 분석 인사이트](use-cases/analytics-insights.md)
- 주요 개념 {#key-concepts}
   - [중첩 데이터 구조 작업](key-concepts/nested-data-structures.md)
   - [중첩된 데이터 구조 평면화](key-concepts/flatten-nested-data.md)
   - [익명 블록](key-concepts/anonymous-block.md)
   - [인라인 템플릿](key-concepts/inline-templates.md)
   - [증분 로드](key-concepts/incremental-load.md)
   - [데이터 중복 제거](key-concepts/deduplication.md)
   - [데이터 세트 샘플](key-concepts/dataset-samples.md)
   - [데이터 세트 통계 계산](key-concepts/dataset-statistics.md)
- 데이터 Distiller Hypercubes {#hypercubes}
   - [하이퍼큐브를 통한 효율적인 빅 데이터 분석](hypercubes/overview.md)
- 클라이언트를 쿼리 서비스 {#clients}에 연결
   - [클라이언트 연결 개요](clients/overview.md)
   - [SSL 모드](./clients/ssl-modes.md)
   - [아쿠아 데이터 스튜디오](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [GitHub Copilot](./clients/github-copilot.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [보는 사람](clients/looker.md)
   - [포스티코](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [스튜디오](clients/rstudio.md)
   - [타블로](clients/tableau.md)
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
- 쿼리 서비스 API {#api}
   - [시작하기](api/getting-started.md)
   - [쿼리](api/queries.md)
   - [연결 매개변수](api/connection-parameters.md)
   - [예약](api/scheduled-queries.md)
   - [예약된 쿼리에 대해 실행](api/runs-scheduled-queries.md)
   - [쿼리 템플릿](api/query-templates.md)
   - [가속화된 쿼리](api/accelerated-queries.md)
   - [경고 구독](api/alert-subscriptions.md)
- Data Distiller 인증 API {#auth-api}
   - [개요](auth-api/overview.md)
   - [시작하기](auth-api/getting-started.md)
   - [액세스](auth-api/ip-access.md)
   - [유효성 검사](auth-api/validate.md)
- 데이터 거버넌스 {#data-governance}
   - [개요](data-governance/overview.md)
   - [감사 로그 안내서](data-governance/audit-log-guide.md)
   - [애드혹 스키마 데이터 세트의 ID](data-governance/ad-hoc-schema-identities.md)
   - [Ad Hoc 스키마에 대한 속성 기반 액세스 제어 지원](./data-governance/ad-hoc-schema-labels.md)
- 권장사항 {#best-practices}
   - [쿼리 실행](best-practices/writing-queries.md)
   - [데이터 자산 조직](./best-practices/organize-data-assets.md)
- SQL 참조 {#sql}
   - [SQL 개요](sql/overview.md)
   - [SQL 구문](sql/syntax.md)
   - [Adobe 정의 함수](sql/adobe-defined-functions.md)
   - [고차 함수](sql/higher-order-functions.md)
   - [Spark SQL 함수](sql/spark-sql-functions.md)
   - [메타데이터 명령](sql/metadata.md)
   - [준비된 문](sql/prepared-statements.md)
- [자주 묻는 질문](troubleshooting-guide.md)
- [허용 목록에 추가하다 IP 주소](ip-address-allowlist.md)
- [API 참조](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [플랫폼 릴리스 정보](https://experienceleague.adobe.com/ko/docs/experience-platform/release-notes/latest)
