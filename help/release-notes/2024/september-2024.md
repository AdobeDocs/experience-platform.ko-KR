---
title: Adobe Experience Platform 릴리스 정보 2024년 9월
description: Adobe Experience Platform의 2024년 9월 릴리스 정보입니다.
source-git-commit: eac613434f631cab567ab3fa6e30d33acac79d2f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 9월 24일**

Adobe Experience Platform의 기존 기능 및 설명서 업데이트:

- [경고](#alerts)
- [대시보드](#dashboards)
- [데이터 준비](#data-prep)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [ID 서비스](#identity-service)
- [쿼리 서비스](#query-service)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 사용하면 다양한 플랫폼 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 플랫폼 사용자 인터페이스의 [!UICONTROL 경고] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며, UI 자체 또는 이메일 알림을 통해 알림 메시지를 받도록 선택할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 개발 샌드박스 지원 | 이제 프로덕션과 개발 샌드박스 모두에서 [경고를 구독](../../observability/alerts/ui.md)하여 모든 환경에서 원활한 모니터링을 수행할 수 있습니다. |
| 이메일 템플릿 | [이제 이메일 경고에](../../observability/alerts/ui.md) 상세한 자산 정보가 포함되어 모든 주요 세부 정보를 손쉽게 확인할 수 있게 됩니다. |
| 맞춤화 기능 개선 | 이제 다음 경고 유형에 대해 특정 요구 사항에 맞게 경고를 맞춤 설정할 수 있는 더 큰 유연성을 제공하도록 [경고 임계값](../../observability/alerts/ui.md#alert-threshold)을 구성할 수 있습니다.<br><ul><li>세그먼트 작업 지연</li><li>세그먼트 내보내기 지연</li><li>대상 흐름 실행 지연</li><li>ID 서비스 흐름 실행 지연</li><li>프로필 흐름 실행 지연</li><li>소스 흐름 실행 지연</li><li>쿼리 실행 지연</li><li>활성화 건너뛰기 비율 초과됨</li><li>소스 수집 오류율 초과됨</ul> |
| 경고 확장됨 | 이제 다음 [경고 규칙](../../observability/alerts/rules.md)에 대해 감사 이벤트 정보 경고 구독이 가능합니다.<br><ul><li>대상자 만들기</li><li>대상자 업데이트</li><li>대상자 삭제</li><li>데이터 세트 만들기</li><li>데이터 세트 업데이트</li><li>데이터 세트 삭제</li><li>스키마 만들기</li><li>스키마 업데이트</li><li>스키마 삭제. |

{style="table-layout:auto"}

경고에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../../observability/home.md)를 참조하십시오.

## 대시보드 {#dashboards}

Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 라이선스 사용 추가 기능 테이블 | 핵심 제품 및 추가 기능에 대한 전용 테이블을 통해 라이선스 사용에 대한 세부적인 가시성을 확보하고 플랫폼 리소스를 관리할 수 있습니다. 샌드박스 수준의 드릴 스루 보기를 통해 각 핵심 제품에 대한 주요 지표를 추적하고 분석합니다. 추가 기능 지표는 핵심 제품 지표와 완벽하게 통합되어 사용 현황에 대한 포괄적인 보기를 제공합니다. 가시성이 향상되면 라이선스 관리를 최적화하고 조직의 요구 사항에 맞게 리소스를 조정할 수 있습니다. 자세한 내용은 [[!UICONTROL 라이선스 사용] 대시보드 안내서](../../dashboards/guides/license-usage.md#overview-tab)를 참조하십시오. |
| 쿼리 프로 모드 - 전역 필터 업그레이드 | 쿼리 프로 모드의 새로운 날짜 필터로 분석을 개선하십시오. SQL 쿼리에서 동적 날짜 매개변수를 사용하여 인사이트를 구체화하고 특정 시간대별로 데이터를 필터링하십시오. 직관적인 UI로 사전 설정이나 사용자 정의 날짜 범위를 선택하여 대시보드가 모든 사용자에게 높은 관련성을 유지할 수 있도록 하십시오. 워크플로를 단순화하고, 정확성을 유지하며, 시의적절한 결정을 내려보십시오. 자세한 내용은 [날짜 필터 생성 안내서](../../dashboards/sql-insights-query-pro-mode/filters/global-filter.md)를 참조하십시오. |
| 쿼리 프로 모드 - 드릴 스루 | 쿼리 프로 모드의 드릴 스루 기능으로 더욱 깊은 인사이트를 얻고 높은 수준의 차트에서 상세한 대시보드까지 원활하게 탐색해 보십시오. 이 기능을 사용해 요약에서 심층 분석으로 간편하게 이동하고 추세, 고객 행동, KPI를 살펴볼 수 있습니다. 자동 필터 패스 스루 및 여러 수준의 드릴 스루를 통해 데이터의 일관성이 유지되므로 원활한 탐색이 가능합니다. 업무 흐름을 단순화하고, 맥락을 유지하고, 의사 결정을 가속화해 보십시오. 자세한 내용은 [드릴 스루 생성에 대한 단계별 안내서](../../dashboards/sql-insights-query-pro-mode/drill-through.md)를 읽어 보십시오. |
| 쿼리 프로 모드 - 고급 테이블 속성 | 쿼리 프로 모드의 고급 테이블 속성을 사용하면 데이터 시각화 간소화, 워크플로 효율성 강화, 데이터 명확성 개선이 가능합니다. 사용자 정의 대시보드에서 바로 표에 자동 정렬, 크기 조정 및 페이지 매김을 추가해 보십시오. 주요 데이터의 우선순위를 정해 열을 정렬하고, 최적의 가독성을 위해 크기를 조정하고, SQL 쿼리를 수정하지 않고도 대용량 데이터 세트를 원활하게 탐색할 수 있습니다. 이러한 기능들을 통합하고 데이터 인사이트를 강화하는 방법에 대해서는 “[더 보기](../../dashboards/sql-insights-query-pro-mode/view-more.md)” 안내서를 읽어 보십시오. |
| 총 데이터 양 | “평균 프로필 풍부도” 지표가 “총 데이터 양” 지표로 대체되었습니다. 총 데이터 양은 참여 및 개인화 워크플로에 실시간 고객 프로필을 사용하여 사용할 수 있는 데이터의 총량을 나타냅니다. 이 변경 사항에 대한 자세한 내용은 [총 데이터 양 안내서](../../landing/license-usage-and-guardrails/total-data-volume.md)에서 확인할 수 있습니다. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 경험 데이터 모델(XDM)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 대상에서 사용할 수 있는 새로운 데이터 준비 기능 | 이제 대상 사용 사례에 대해 다음과 같은 배열 함수를 사용할 수 있습니다.<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> 자세한 내용은 [데이터 준비 기능 안내서](../../data-prep/functions.md#arrays)를 참조하십시오. |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md)를 참조하십시오.

## 대상 {#destinations}

**업데이트 일자: 2024년 9월 30일**

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 설명 |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | 2024년 9월 릴리스에서는 `countryCode` 매개변수를 Amazon Ads로 내보내는 매핑 옵션을 추가했습니다. [매핑 단계](/help/destinations/catalog/advertising/amazon-ads.md#map)에서 `countryCode`를 사용하여 Amazon의 신원 일치율을 개선해 보십시오. |
| [[!BADGE B2B]{type=Informative} Demandbase](/help/destinations/catalog/advertising/demandbase.md) | 이 대상을 사용하여 Account-Based Marketing(ABM) 사용 사례에 대한 계정 대상자를 활성화할 수 있습니다. DemandBase의 B2B Demand Side Platform(DSP)을 통해 대상 계정의 관련 페르소나와 역할에 광고를 게재하십시오. 대상 계정은 마케팅과 판매의 다른 다운스트림 사용 사례를 위해 Demandbase 서드파티 데이터로 강화할 수도 있습니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| --- | --- |
| [데이터 세트 내보내기](/help/destinations/ui/export-datasets.md) 개선 사항 | Experience Platform의 2024년 9월 릴리스에는 다양한 데이터 이그레스 사용 사례를 보다 효과적으로 지원할 수 있도록 데이터 세트 내보내기 기능 성능이 다방면으로 개선되었습니다. 해당 기능 향상 사항에는 다음과 같은 내용이 포함됩니다. <ul><li>하위 폴더 추가 및 제거 옵션을 포함한 새로운 데이터 폴더 구성 옵션이 추가되었습니다.</li><li>전체 파일 내보내기(한 번) 및 종료 날짜를 지정할 수 있는 기능 등 새로운 내보내기 옵션</li><li>참고: Adobe는 9월 릴리스 이전에 생성된 모든 데이터 세트 내보내기 데이터 흐름에 대해 2025년 5월 1일이라는 기본 종료일을 적용합니다. 이러한 모든 데이터 흐름에 대해 고객은 종료일이 되기 전에 데이터 흐름 종료일을 수동으로 업데이트해야 합니다. 그렇지 않은 경우 해당 날짜에 내보내기가 중지됩니다.</li></ul> <br> ![예약 단계에서 예약 및 폴더 편집 옵션이 강조 표시된 Experience Platform 사용자 인터페이스 이미지.](../2024/assets/september/edit-schedule-folders.png "예약 단계에서 예약 및 폴더 옵션을 편집합니다."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마 편집기 개선 사항 | 스키마 편집기에서 업데이트된 관계 워크플로를 통해 스키마 관계를 제어해 보십시오. Experience Platform UI에서 직접 기존 관계를 쉽게 업데이트하거나 제거할 수 있으므로 스키마 관리를 보다 원활하고 직관적으로 만들 수 있게 되었습니다. 세분화 및 기타 주요 프로세스 전반에 걸쳐 빈틈 없는 데이터 무결성을 보장하면서도 참조 스키마를 조정하고 관계 이름을 확실하게 변경할 수 있습니다. 스키마 관계를 효율적으로 관리하는 방법에 대한 자세한 내용은 [UI에서 관계 필드 정의하기](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group)와 [B2B 관계](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship)에 대한 안내서에서 확인할 수 있습니다. |

{style="table-layout:auto"}

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## ID 서비스 {#identity-service}

Adobe Experience Platform ID 서비스를 사용하여 여러 디바이스 및 시스템에 걸쳐 ID를 연결하여 고객과 고객의 행동을 종합적으로 파악할 수 있으므로, 실시간으로 효과적인 개인 디지털 환경을 제공할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 아이덴티티 그래프 연결 규칙 제한 공개 | ID 그래프 연결 규칙은 사용자에게 정확한 개인화를 보장하는 데 사용할 수 있는 ID 서비스의 도구 모음입니다. <ul><li>이제 [ID 최적화 알고리즘](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md)을 사용하여 ID 그래프가 단일 사용자를 나타내는지 확인하고, 실시간 고객 프로필에서 원치 않는 ID 병합을 방지할 수 있습니다.</li><li>[네임스페이스 우선 순위](../../identity-service/identity-graph-linking-rules/namespace-priority.md)를 구성하여 각 네임스페이스의 중요성을 정의하고 프로필이 형성되고 세분화되는 방식에 영향을 줍니다.</li><li>[UI의 그래프 시뮬레이션 도구](../../identity-service/identity-graph-linking-rules/graph-simulation.md)를 사용하여 다양한 구성으로 ID 그래프를 시뮬레이션합니다.</li><li>[ID 설정 인터페이스](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md)를 사용하여 고유한 네임스페이스를 지정하고 조직의 모든 네임스페이스에 대한 우선 순위를 설정합니다.</li><li>그래프 데이터와 관련된 지표와 추세에 대한 자세한 내용은 [ID 대시보드](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs)를 참조하십시오.</li></ul> 아이덴티티 그래프 연결 규칙을 시도해 보려면 Adobe 계정 팀에 문의하여 개발 샌드박스에 대한 액세스를 요청하십시오. |

**업데이트된 설명서**

| 기능 | 설명 |
| --- | --- |
| 아이덴티티 그래프 연결 규칙에 대한 문제 해결 안내서 | 아이덴티티 그래프 연결 규칙에 대한 새로운 [문제 해결 안내서](../../identity-service/identity-graph-linking-rules/troubleshooting.md)를 읽고 아이덴티티 그래프 연결 규칙 사용에서 발생 가능한 일반적 문제 해결에 활용할 수 있는 접근 방식과 디버깅 솔루션에 대해 알아보십시오. |
| 아이덴티티 그래프 연결 규칙에 대한 FAQ | 네임스페이스 우선순위, ID 최적화 알고리즘 및 아이덴티티 그래프 연결 규칙의 다른 패싯, 관련 자주 묻는 질문에 대한 답변 목록을 보려면 새로운 [아이덴티티 그래프 연결 규칙 FAQ](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions)를 읽어 보십시오. |

{style="table-layout:auto"}

ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL로 Adobe Experience Platform [!DNL data lake]에서 데이터를 쿼리할 수 있습니다. 데이터 레이크의 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Data Distiller 대상자 | Experience Platform의 Data Distiller에서 SQL 대상자 확장 기능을 활용해 손쉽게 대상자를 만들고, 관리하고, 활성화할 수 있습니다. 데이터 레이크에서 바로 SQL 명령을 사용해 대상자 세그먼트를 정의하므로 프로필에서 원시 데이터를 사용할 필요가 없습니다. 이와 같은 유연한 데이터 기반 접근 방식으로 타겟팅 전략을 강화하고 자동으로 대상자를 파일 기반 대상에 동기화하십시오. 워크플로를 간소화하고, 대상자 관리를 최적화하고, 데이터 잠재력을 최대로 활용하십시오. [SQL 대상자 확장 기능을 사용하는 방법에 대한 안내서](../../query-service/data-distiller-audiences/overview.md)를 읽고 대상자 전략을 한층 업그레이드하십시오. |
| Data Distiller 통계 - 하이퍼큐브 | 하이퍼큐브를 사용해 빅데이터 분석을 최적화하십시오. 내역 데이터를 다시 처리하지 않으면서도 고유 개수 및 다차원 분석 등의 같은 복잡한 계산을 처리할 수 있습니다. 정확성과 효율성을 유지하는 동시에 점진적으로 데이터를 업데이트하고, 워크플로를 간소화하고, 처리 시간을 단축하십시오. 더 빠르면서도 확장 가능하며 비용 효율적인 인사이트를 얻어 의사 결정 과정을 혁신해 보십시오. [하이퍼큐브 사용 안내서](../../query-service/hypercubes/overview.md)를 살펴보고 고급 분석 기능을 활용해 보십시오. |
| 쿼리 편집기 오브젝트 브라우저 | 쿼리 편집기에서 새로운 오브젝트 브라우저를 사용해 쿼리 효율성을 높여 보십시오. 빠르게 데이터 세트를 검색하고, 필터링하고, 데이터 세트에 액세스하여 쿼리를 더 빠르게 작성하고 구체화할 수 있습니다. 실시간 스키마 업데이트와 즉각적인 테이블 메타데이터를 활용하면 워크플로를 간소화하고, 탐색 시간을 줄이고, 쿼리 경험을 개선할 수 있습니다. 데이터 잠재력을 최대로 활용하고 분석을 최적화하십시오. 자세한 내용은 [오브젝트 브라우저 사용 안내서](../../query-service/ui/user-guide.md#object-browser)를 읽어 보십시오. |
| 컴퓨팅 시간 | 예약된 쿼리에 대해 컴퓨팅 시간 지표를 볼 수 있게 되었으므로 리소스 사용 제어가 용이해졌습니다. 쿼리 실행 수준에서 컴퓨팅 시간을 확인하여 CTAS/ITAS 배치 쿼리에 대한 리소스 사용을 모니터링하고 최적화하십시오. 각 쿼리 실행에 대한 추적 시작 시간, 완료 상태, 컴퓨팅 시간을 추적할 수 있습니다. 성능을 세부 조정하고 손쉽게 비용을 절감해 보십시오. [컴퓨팅 시간에 대한 안내서](../../query-service/ui/query-schedules.md#compute-hours-at-job-level)를 읽고 쿼리 효율성 극대화 방법에 대한 정보를 확인해 보십시오. |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md)를 살펴보십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 세분화 기준 업데이트 | 2024년 9월 릴리스를 시작으로 스트리밍 세분화의 대상자 기준이 업데이트되었습니다. 이러한 변경 사항에 대한 자세한 내용은 [스트리밍 세분화 적격성 기준 업데이트](../../segmentation/eligibility-criteria-update.md)에서 확인할 수 있습니다. |
| 통합 검색 구현 | 이제 세그먼트 빌더 내의 검색 행동이 통합 검색을 사용합니다. 이를 통해 세그먼트 멤버십에 대해 재사용될 대상자를 검색 및 관리할 때 보다 강력한 경험을 제공할 수 있게 됩니다. 이 변경 사항에 대한 자세한 내용은 [세그먼트 빌더 안내서](../../segmentation/ui/segment-builder.md#rule-builder-canvas)를 참조하십시오. |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 서드파티 데이터 소스에서 데이터를 수집합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative} UI에서 암호화된 데이터 수집 기능 지원 | 이제 Experience Platform 사용자 인터페이스의 소스 작업 영역을 사용해 클라우드 스토리지 배치 소스에서 암호화된 데이터를 수집할 수 있습니다. 자세한 내용은 [UI에서 암호화된 데이터 수집](../../sources/tutorials/ui/encryped-ingestion.md)을 읽어 보십시오. |
| [!DNL Snowflake Streaming] 소스의 일반 가용성 | 이제 [!DNL Snowflake Streaming] 소스는 GA 상태입니다. 이 소스를 사용하여 사용자의 [!DNL Snowflake] 계정을 Experience Platform으로 스트리밍할 수 있습니다. 자세한 내용은 [[!DNL Snowflake Streaming] 개요](../../sources/connectors/databases/snowflake-streaming.md)를 참조하십시오. |
| [!DNL Google BigQuery]에서 서비스 계정 인증 지원 | 이제 서비스 계정 인증을 사용하여 Experience Platform에 [!DNL Google BigQuery] 계정을 추가할 수 있습니다. 자세한 내용은 [[!DNL Google BigQuery] 개요](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)를 읽어 보십시오. <br> ![예약 단계에서 예약 및 폴더 편집 옵션이 강조 표시된 Experience Platform 사용자 인터페이스 이미지.](../2024/assets/september/service_auth.png "Google BigQuery에 대한 서비스 인증."){width="250" align="center" zoomable="yes"} |
| 샘플 데이터 미리보기 건너뛰기 지원 | 이제 다음과 같은 소스로 소스 연결을 만들 때 데이터 미리보기를 건너뛰도록 선택할 수 있습니다. <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> 데이터 미리보기를 건너뛰어 대량의 배치 데이터 수집 시 발생할 수 있는 시간 초과를 피할 수 있습니다. 이 경우 계산된 필드 및 필수 필드의 자동 유효성 검사가 수행되지 않을 수 있습니다. 데이터 미리보기 건너뛰기를 선택하면 매핑하는 동안 계산된 필드 및 필수 필드의 유효성을 수동 검사해야 할 수 있습니다. |
| [!DNL SFTP]에서의 청크화 비활성화 지원 | 이제 [!DNL SFTP] 소스에서 청크화를 비활성화할 수 있는 설정 구성이 가능합니다. 자세한 내용은 [[!DNL SFTP] 개요](../../sources/connectors/cloud-storage/sftp.md)를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
