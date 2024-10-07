---
title: SQL Insights
description: Data Distiller을 사용하여 SQL Insights 대시보드를 개발하는 사용 사례, 필수 기능 및 필수 단계에 대해 알아봅니다. Data Distiller 내의 SQL Insights 기능을 통해 투명성을 높이고 프로필, 대상, 캠페인, 여정, 권한 및 동의와 같은 다양한 차원에서 운영 통찰력을 얻는 방법에 대해 알아봅니다.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: 4e78a7983fba492ded866a8f1fc6f98e20510b2b
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# SQL Insights

맞춤형 보고 데이터 모델을 만들어 Data Distiller의 SQL Insights를 통해 보다 심층적인 통찰력을 추출하고 전략을 최적화하며 특정 비즈니스 요구 사항을 충족하도록 분석을 조정할 수 있습니다. SQL Insights 기능을 사용하면 프로필, 대상, 캠페인, 여정, 권한 및 동의와 같은 차원 전반에서 Adobe Experience Platform 데이터의 투명성을 높이고 운영 통찰력을 얻을 수 있습니다. 이 기능은 조직의 보고 데이터 모델을 특정 비즈니스 요구에 맞게 조정할 수 있는 다목적 적응형 솔루션을 제공합니다.

[SQL Insights 시각화](../../../dashboards/data-distiller/sql-insights/overview.md)를 위해 [쿼리 프로 모드](../../../dashboards/data-distiller/query-pro-mode/overview.md)를 사용하여 사용자 지정 SQL 쿼리를 사용하여 복잡한 분석을 수행하고 데이터를 쉽게 해석 가능한 차트로 변환할 수 있습니다. Query pro 모드를 사용하면 대시보드에서 맞춤형 인사이트와 시각화를 만들고 인사이트를 CSV 파일로 다운로드하여 기술 대상과 기술 이외의 대상 모두에 맞출 수 있습니다.

이 문서에서는 Data Distiller을 사용하여 SQL 인사이트 대시보드를 개발하는 데 필요한 사용 사례, 필수 기능 및 단계를 다룹니다.

## 전제 조건

이 자습서에서는 사용자 정의 대시보드를 사용하여 Platform UI 내에서 사용자 정의 데이터 모델의 데이터를 시각화합니다. 이 기능에 대한 자세한 내용은 [사용자 정의 대시보드 설명서](../../../dashboards/user-defined-dashboards.md)를 참조하세요.

## 시작하기

Data Distiller SKU는 보고 통찰력에 대한 사용자 지정 데이터 모델을 구축하고 풍부한 플랫폼 데이터를 포함하는 Real-Time CDP 데이터 모델을 확장하는 데 필요합니다. Data Distiller SKU와 관련된 [패키징](../../packaging.md), [보호 기능](../../guardrails.md#query-accelerated-store) 및 [라이선스](../../data-distiller/license-usage.md) 설명서를 참조하십시오. Data Distiller SKU가 없는 경우 Adobe 고객 서비스 담당자에게 자세한 내용을 문의하십시오.

## SQL Insights 활용 사례 {#use-cases}

다음은 Data Distiller의 SQL Insights를 통해 효과적으로 해결할 수 있는 일반적인 사용 사례입니다.

### 프로필 및 대상자 사용 투명도 {#usage-transparency}

**과제:** 비즈니스 단위, 충성도 상태 또는 CLTV(고객 생애 가치)와 같은 특정 기준에 따라 주요 성과 지표(KPI)를 분류하는 방법.

**SQL Insights 솔루션:** Data Distiller을 사용하면 Adobe Experience Platform에서 보고 데이터 모델을 확장하여 [CLTV](../../use-cases/customer-lifetime-value.md) 또는 충성도 상태와 같은 사용자 지정 프로필 특성을 추가할 수 있습니다.

### 동의 예외 항목 추적 {#consent-anomaly-tracking}

**과제:** 전자 메일, SMS, 전화와 같은 채널에 대해 사용자 지정된 동의 특성에 대상 겹침 및 크기 추세선 보고서를 적용하는 방법

**SQL Insights 솔루션:** 보고 데이터 모델을 확장하여 시간 경과에 따른 동의 환경 설정 변경을 추적할 수 있습니다. 여기에는 동의 환경 설정의 트렌드를 확인할 수 있는 추가 팩트 및 차원 테이블을 작성하고 [증분 데이터 새로 고침](../../key-concepts/incremental-load.md)을 예약하는 작업이 포함됩니다.

### 대상자 세분화 전략 최적화 {#optimize-audience-segmentation-strategy}

**과제:** 머신 러닝(ML) 모델에서 생성한 성향 점수를 대상 KPI 보고서에 통합하는 방법.

**SQL Insights 솔루션:** Data Distiller을 사용하면 사용자 지정 ML 모델의 [성향 점수](../../use-cases/propensity-score.md)를 포함하여 대상 수준에서 집계 점수를 쉽게 계산할 수 있습니다. 그런 다음 표준 KPI와 함께 이 데이터를 보고할 수 있습니다.

### 대상 확장 {#audience-expansion}

**과제:** 대상 중복 보고서에서 프로필 카운트 이상을 획득하고 대상 확장 전략을 안내하기 위해 추가적인 인구 통계학적 데이터 또는 환경 설정을 달성하는 방법.

**SQL Insights 솔루션:** 보고 데이터 모델을 확장하면 사용자가 추가 프로필 특성을 통합할 수 있으므로 대상 중복 보고서를 관련 인구 통계학적 데이터 및 환경 설정으로 보강할 수 있습니다.

## SQL Insights 생성을 위한 주요 기능 {#key-capabilities}

아래 그림에서는 SQL Insights 생성을 위한 몇 가지 필수 기능을 강조하고 있습니다. 이러한 기능에는 다음이 포함됩니다.

1. **데이터 시각화:** 데이터 트렌드를 포괄적으로 볼 수 있도록 트렌드 및 막대 차트와 같은 시각적 요소를 통합합니다.
1. **대시보드 작성:** 특정 사용 사례에 맞게 맞춤화된 사용자 지정 대시보드를 만들 수 있도록 함으로써 보다 개인화되고 타깃팅된 분석 환경을 제공합니다.
1. **유연한 SQL 데이터 모델링:** 사용자가 다양한 데이터 세트를 매끄럽게 결합하고 조작할 수 있는 다양한 SQL 데이터 모델링 방법을 사용하여 적응성 및 분석 깊이를 향상시킵니다.
1. **가속화된 저장소:** SQL을 통해 집계된 통찰력을 효율적으로 제공하는 가속화된 저장소 메커니즘을 구현하여 중요한 정보에 대한 효율적이고 신속한 액세스를 보장합니다.
1. **BI 연결:** Power BI, Tableau, Looker 및 Apache Superset을 포함하여 인기 있는 Business Intelligence(BI) 도구와의 원활한 통합을 지원합니다. 이러한 연결을 통해 다양한 BI 환경과의 호환성을 보장하므로 사용자가 원하는 도구를 사용하여 심층적인 분석 및 보고를 수행할 수 있습니다.

![Data Distiller의 SQL Insights의 주요 기능을 시각적으로 표시합니다.](../../images/data-distiller/sql-insights/key-capabilities-of-customizable-insights.png)

## SQL Insights를 만드는 단계 {#steps-to-create}

Data Distiller 내에서 SQL Insights 대시보드를 개발하려면 아래 단계별 지침을 따르십시오.

1. **Ad Hoc 쿼리 탐색:** Ad Hoc `SELECT` 쿼리를 실행하여 데이터 레이크에서 원시 데이터를 탐색합니다. 이를 통해 즉석으로 탐색적인 데이터 분석을 수행하여 쿼리 결과가 데이터 레이크에 저장되지 않은 데이터를 검증할 수 있습니다.
1. **일괄 쿼리 사용률:** 일괄 쿼리를 사용하여 인사이트 집계 테이블을 생성하기 위해 [예약된 작업을 생성](../../api/scheduled-queries.md#create-a-new-scheduled-query)하여 데이터 처리에 대한 체계적이고 자동화된 접근 방식을 보장합니다. 일괄 처리 쿼리는 `INSERT TABLE AS SELECT` 및 `CREATE TABLE AS SELECT` 쿼리를 실행하여 데이터를 정리하고, 모양을 만들고, 조작하고, 보강합니다. 이러한 쿼리의 결과는 데이터 레이크에 저장됩니다.
1. **집계된 인사이트 로드:** 생성된 집계된 인사이트를 가속화된 저장소에 로드하고 SQL을 사용하여 쿼리를 테스트하고 데이터 검색의 정확성과 효율성을 확인합니다. [상태 비저장 쿼리를 가속화된 저장소에 만드는](../../api/accelerated-queries.md) 방법에 대해 알아보려면 설명서를 참조하세요.
1. **액세스 및 통합:** Adobe Experience Platform [사용자 정의 대시보드](../../../dashboards/user-defined-dashboards.md) 또는 기타 기본 Business Intelligence(BI) 도구와 통합하여 가속화된 저장소에 저장된 인사이트에 원활하게 액세스합니다. 서드파티 클라이언트와의 이러한 통합은 사용자가 통합적이고 직관적인 경험을 사용할 수 있도록 합니다.

![Data Distiller에서 SQL Insights의 네 가지 단계를 설명하는 인포그래픽입니다.](../../images/data-distiller/sql-insights/steps-to-customizable-insights.png)

## 다음 단계

이제 이 문서를 읽고 사용 사례, 필수 기능 및 Data Distiller을 사용하여 SQL 인사이트 대시보드를 개발하는 데 필요한 단계에 대해 더 잘 이해할 수 있습니다. 맞춤형 보고 데이터 모델을 만드는 방법을 계속 알아보려면 [보고 인사이트 데이터 모델 안내서](./reporting-insights-data-model.md)를 참조하세요.
