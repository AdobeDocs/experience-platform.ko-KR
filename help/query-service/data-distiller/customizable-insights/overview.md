---
title: 사용자 지정 가능한 인사이트
description: Data Distiller을 사용하여 사용자 정의 가능한 통찰력 대시보드를 개발하는 사용 사례, 필수 기능 및 필수 단계에 대해 알아봅니다. Data Distiller 내의 사용자 지정 가능한 인사이트 기능을 통해 프로필, 대상, 캠페인, 여정, 권한 및 동의와 같은 다양한 차원에 대한 투명성을 높이고 운영 인사이트를 얻는 방법에 대해 알아봅니다.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 사용자 지정 가능한 인사이트

맞춤형 보고 데이터 모델을 만들어 Data Distiller의 사용자 정의 가능한 인사이트를 통해 보다 심층적인 통찰력을 추출하고 전략을 최적화하며 특정 비즈니스 요구 사항을 충족하도록 분석을 조정할 수 있습니다. 사용자 지정 가능한 인사이트 기능을 사용하여 프로필, 대상, 캠페인, 여정, 권한 및 동의와 같은 차원 전반에서 Adobe Experience Platform 데이터의 투명성을 높이고 운영 통찰력을 얻을 수 있습니다. 이 기능은 조직의 보고 데이터 모델을 특정 비즈니스 요구에 맞게 조정할 수 있는 다목적 적응형 솔루션을 제공합니다.

종료 [사용자 정의 가능한 인사이트 시각화](../../../dashboards/data-distiller/overview.md) 다음을 사용할 수 있습니다. [query pro 모드](../../../dashboards/data-distiller/customizable-insights/query-pro-mode.md) 사용자 지정 SQL 쿼리를 사용하여 복잡한 분석을 수행하고 데이터를 쉽게 해석 가능한 차트로 변환합니다. Query pro 모드를 사용하면 대시보드에서 맞춤형 인사이트와 시각화를 만들고 인사이트를 CSV 파일로 다운로드하여 기술 대상과 기술 이외의 대상 모두에 맞출 수 있습니다.

이 문서에서는 Data Distiller을 사용하여 사용자 정의 가능한 통찰력 대시보드를 개발하는 사용 사례, 필수 기능 및 필수 단계를 다룹니다.

## 전제 조건

이 자습서에서는 사용자 정의 대시보드를 사용하여 Platform UI 내에서 사용자 정의 데이터 모델의 데이터를 시각화합니다. 다음을 참조하십시오. [사용자 정의 대시보드 설명서](../../../dashboards/user-defined-dashboards.md) 이 기능에 대해 자세히 알아보십시오.

## 시작하기

Data Distiller SKU는 보고 통찰력에 대한 사용자 지정 데이터 모델을 구축하고 풍부한 플랫폼 데이터를 포함하는 Real-Time CDP 데이터 모델을 확장하는 데 필요합니다. 다음을 참조하십시오. [포장](../../packaging.md), [보호 기능](../../guardrails.md#query-accelerated-store), 및  [라이선스](../../data-distiller/license-usage.md) Data Distiller SKU와 관련된 설명서입니다. Data Distiller SKU가 없는 경우 Adobe 고객 서비스 담당자에게 자세한 내용을 문의하십시오.

## 사용자 정의 가능한 통찰력 사용 사례 {#use-cases}

다음은 Data Distiller의 사용자 지정 가능한 인사이트를 통해 효과적으로 해결할 수 있는 일반적인 사용 사례입니다.

### 프로필 및 대상자 사용 투명도 {#usage-transparency}

**과제:** 비즈니스 단위, 충성도 상태 또는 CLTV(고객 생애 가치)와 같은 특정 기준으로 주요 성과 지표(KPI)를 분류하는 방법입니다.

**사용자 정의 가능한 통찰력 솔루션:** Data Distiller을 사용하면 Adobe Experience Platform에서 보고 데이터 모델을 확장하여 [cltv와 같은 사용자 지정 프로필 속성 추가](../../use-cases/customer-lifetime-value.md) 또는 충성도 상태

### 동의 예외 항목 추적 {#consent-anomaly-tracking}

**과제:** 이메일, SMS 및 전화와 같은 채널에 대한 사용자 지정된 동의 속성에 대상 겹침 및 크기 트렌드 라인 보고서를 적용하는 방법입니다.

**사용자 정의 가능한 통찰력 솔루션:** 보고 데이터 모델을 확장하여 시간 경과에 따른 동의 환경 설정 변경을 추적할 수 있습니다. 여기에는 동의 환경 설정 및 일정 추세를 위한 추가 팩트 및 차원 테이블 구축이 포함됩니다 [증분 데이터 새로 고침](../../key-concepts/incremental-load.md).

### 대상자 세분화 전략 최적화 {#optimize-audience-segmentation-strategy}

**과제:** 머신 러닝(ML) 모델에서 생성한 성향 점수를 대상 KPI 보고서에 통합하는 방법.

**사용자 정의 가능한 통찰력 솔루션:** Data Distiller을 사용하면 다음을 포함할 수 있습니다. [사용자 지정 ML 모델의 성향 점수](../../use-cases/propensity-score.md), 대상자 수준에서 집계 점수 계산을 용이하게 합니다. 그런 다음 표준 KPI와 함께 이 데이터를 보고할 수 있습니다.

### 대상 확장 {#audience-expansion}

**과제:** 대상 중복 보고서의 프로필 카운트 이상을 획득하고 대상 확장 전략을 안내하는 추가 인구 통계학적 데이터 또는 환경 설정을 달성하는 방법입니다.

**사용자 정의 가능한 통찰력 솔루션:** 보고 데이터 모델을 확장하면 사용자가 추가 프로필 속성을 통합할 수 있으므로 대상 중복 보고서를 관련 인구 통계 데이터 및 환경 설정으로 보강합니다.

## 사용자 정의 가능한 인사이트 생성을 위한 주요 기능 {#key-capabilities}

아래 그림에서는 사용자 지정 가능한 인사이트를 생성하기 위한 몇 가지 필수 기능을 강조합니다. 이러한 기능에는 다음이 포함됩니다.

1. **데이터 시각화:** 데이터 트렌드를 포괄적으로 볼 수 있도록 트렌드 및 막대 차트와 같은 시각적 요소를 통합합니다.
1. **대시보드 작성:** 특정 사용 사례에 맞게 맞춤화된 사용자 정의 대시보드를 만들 수 있으므로 보다 개인화되고 타겟팅된 분석 경험을 제공할 수 있습니다.
1. **유연한 SQL 데이터 모델링:** 사용자가 다양한 데이터 세트를 원활하게 결합하고 조작할 수 있는 다양한 SQL 데이터 모델링 방법을 사용하여 적응력과 분석 깊이를 향상시킵니다.
1. **가속화된 저장소:** SQL을 통해 집계된 통찰력을 효율적으로 제공하는 가속화된 스토어 메커니즘을 구현하여 중요한 정보에 대한 효율적이고 신속한 액세스를 보장합니다.
1. **BI 연결:** Power BI, 타블로, Looker 및 Apache Superset을 비롯한 인기 있는 Business Intelligence(BI) 도구와의 원활한 통합을 지원합니다. 이러한 연결을 통해 다양한 BI 환경과의 호환성을 보장하므로 사용자가 원하는 도구를 사용하여 심층적인 분석 및 보고를 수행할 수 있습니다.

![Data Distiller의 사용자 지정 가능한 통찰력의 주요 기능을 시각적으로 표시합니다.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## 사용자 정의 가능한 인사이트를 만드는 단계 {#steps-to-create}

Data Distiller 내에서 사용자 지정 가능한 Insights 대시보드를 개발하려면 아래의 단계별 지침을 따르십시오.

1. **임시 쿼리 탐색:** Ad Hoc 실행으로 시작 `SELECT` 데이터 레이크에서 원시 데이터를 탐색하는 쿼리입니다. 이를 통해 즉석으로 탐색적인 데이터 분석을 수행하여 쿼리 결과가 데이터 레이크에 저장되지 않은 데이터를 검증할 수 있습니다.
1. **배치 쿼리 사용률:** 일괄 처리 쿼리를 사용하여 [예약된 작업 만들기](../../api/scheduled-queries.md#create-a-new-scheduled-query) 통찰력 집계 테이블을 생성하여 데이터 처리에 대한 체계적이고 자동화된 접근 방식을 보장합니다. 일괄 처리 쿼리 실행 `INSERT TABLE AS SELECT` 및 `CREATE TABLE AS SELECT` 데이터를 정리, 셰이프, 조작 및 보강하는 쿼리입니다. 이러한 쿼리의 결과는 데이터 레이크에 저장됩니다.
1. **집계된 인사이트 로드:** 생성된 집계된 인사이트를 가속화된 저장소에 로드하고 SQL을 사용하여 쿼리를 테스트하고, 데이터 검색의 정확성과 효율성을 보장합니다. 방법 알아보기 [상태 비저장 쿼리를 가속 저장소에 만듭니다.](../../api/accelerated-queries.md)설명서를 참조하십시오.
1. **액세스 및 통합:** Adobe Experience Platform과 통합하여 가속화된 저장소에 저장된 인사이트에 원활하게 액세스합니다 [사용자 정의 대시보드](../../../dashboards/user-defined-dashboards.md) 또는 기타 기본 Business Intelligence(BI) 도구입니다. 서드파티 클라이언트와의 이러한 통합은 사용자가 통합적이고 직관적인 경험을 사용할 수 있도록 합니다.

![Data Distiller에서 사용자 정의 가능한 인사이트에 대한 네 가지 단계를 설명하는 인포그래픽입니다.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## 다음 단계

이제 이 문서를 읽고 사용 사례, 필수 기능 및 Data Distiller을 사용하여 사용자 정의 가능한 통찰력 대시보드를 개발하는 데 필요한 단계에 대해 더 잘 이해할 수 있습니다. 맞춤형 보고 데이터 모델 만들기에 대한 학습을 계속하려면 다음을 참조하십시오. [reporting insights 데이터 모델 안내서](./reporting-insights-data-model.md).
