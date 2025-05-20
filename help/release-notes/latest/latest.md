---
title: Adobe Experience Platform 릴리스 노트 2025년 5월
description: Adobe Experience Platform의 2025년 5월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 8f1538efc96c8dc47a505511ec7f064b07f124c8
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 48%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 노트는 다음 설명서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/latest)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2025년 5월 20일 수요일**

Adobe Experience Platform의 기존 기능 및 설명서 업데이트:

- [카탈로그 서비스](#catalog-service)
- [데이터 준비](#data-prep)
- [대상](#destinations)
- [ID 서비스](#identity)
- [쿼리 서비스](#query-service)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 카탈로그 서비스 {#catalog-service}

카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 데이터 레이크에 파일 및 디렉터리로 저장되지만 카탈로그는 조회 및 모니터링 목적으로 해당 파일 및 디렉터리에 대한 메타데이터와 설명을 제공합니다.

| 기능 | 설명 |
| --- | --- |
| 데이터 세트 수준 보존 규칙으로 데이터 스토리지 최적화 | 지정된 일정에 따라 오래된 데이터를 삭제하는 보존 정책을 통해 데이터 스토리지를 효율적으로 관리합니다. <ul><li>**데이터 집합 보존**: 데이터 레이크 및 프로필 저장소에서 오래된 데이터를 제거하려면 데이터 집합 규칙을 정의하십시오.</li><li>**저장소 인사이트**: 인라인 지표를 통해 사용량을 모니터링하고 라이선스 부여 조건을 준수하는지 확인합니다.</li><li>**향상된 가시성**: 향상된 모니터링을 통해 수집에서 삭제까지 데이터 세트 활동을 추적합니다.</li><li>**관리 간소화**:액세스 유지 설정, 모니터링, 감사 로그 및 통찰력을 하나의 통합 보기로 제공합니다.</li></ul> 자세한 내용은 [데이터 집합 보존 규칙](../../catalog/datasets/user-guide.md#data-retention-policy)의 안내서를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 참조하세요.

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 경험 데이터 모델(XDM)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics에 대한 가져오기 및 내보내기 매핑 지원 | 이제 Adobe Analytics 소스 커넥터를 사용할 때 Adobe Analytics 보고서 세트 데이터에 대한 가져오기 및 내보내기 매핑 기능을 사용할 수 있습니다. <br><br>매핑을 CSV 파일로 내보내고 스프레드시트에서 로컬로 구성합니다. 그런 다음 UI의 매핑 인터페이스를 사용하여 업데이트된 매핑을 Experience Platform으로 가져올 수 있습니다. 이 기능을 사용하면 UI에서 수동으로 빌드하지 않고도 대량의 매핑을 구성할 수 있습니다. 또한 새로운 데이터 흐름을 생성할 때 매핑 사본을 Experience Platform에 직접 업로드하여 워크플로를 가속화할 수 있습니다. <br><br>자세한 내용은 [Experience Platform에 Adobe Analytics 연결](../../sources/tutorials/ui/create/adobe-applications/analytics.md)에 대한 안내서를 참조하십시오.</br> |

{style="table-layout:auto"}

자세한 내용은 [데이터 준비 개요](../../data-prep/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| --- | --- |
| [Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md)에 대한 추가 식별자 지원 | 이제 Google 고객 일치 대상은 Google 플랫폼의 향상된 일치율을 위해 주소 관련 필드 매핑을 지원합니다. <br><br>Google이 주소와 일치하는지 확인하려면 네 개의 주소 필드(`address_info_first_name`, `address_info_last_name`, `address_info_country_code` 및 `address_info_postal_code`)를 모두 매핑하고 내보낸 프로필에 데이터가 없는지 확인해야 합니다. <br> 필드가 매핑되지 않았거나 누락된 데이터를 포함하는 경우 Google이 주소와 일치하지 않습니다. |
| [Facebook](../../destinations/catalog/social/facebook.md) 연결에 대한 계정 만료 열 | 이제 [찾아보기](../../destinations/ui/destinations-workspace.md#browse) 및 [계정](../../destinations/ui/destinations-workspace.md#accounts) 탭에서 Facebook 계정 토큰 만료 날짜를 확인할 수 있습니다. |
| API에서 생성한 데이터 세트 내보내기 | 이제 API에서 만든 데이터 세트를 내보낼 수 있습니다. UI에서 생성된 데이터 세트만 내보내기에 사용할 수 있었던 이전의 제한이 해제되었습니다. [데이터 세트 내보내기](../../destinations/ui/export-datasets.md)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하세요.

## ID 서비스 {#identity}

Adobe Experience Platform ID 서비스를 사용하여 여러 디바이스 및 시스템에 걸쳐 ID를 연결하여 고객과 고객의 행동을 종합적으로 파악할 수 있으므로, 실시간으로 효과적인 개인 디지털 환경을 제공할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Identity Graph Linking Rules] 소개 | [!DNL Identity Graph Linking Rules]은(는) 그래프 축소를 방지하여 개인화된 마케팅을 위해 정확한 고객 프로필을 유지할 수 있도록 설계되었습니다.<ul><li>[그래프 시뮬레이션 도구](../../identity-service/identity-graph-linking-rules/graph-simulation.md)를 사용하여 구성을 테스트하고 확인하십시오.</li><li>조직의 그래프 축소 인스턴스를 모니터링하려면 [ID 대시보드](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs)를 참조하세요.</li><li>시작하려면 [[!DNL Identity Graph Linking Rules] 구현 가이드](../../identity-service/identity-graph-linking-rules/implementation-guide.md)를 읽어 보세요.</li></ul> **참고**: ID 설정을 수동으로 구성할 때까지 데이터가 변경됩니다. |

{style="table-layout:auto"}

자세한 내용은 [ID 서비스 개요](../../identity-service/home.md)를 참조하세요.

## 쿼리 서비스 {#query-service}

쿼리 서비스가 포함된 표준 SQL을 사용하여 Adobe Experience Platform 데이터 레이크에서 데이터를 쿼리합니다. 데이터 세트를 원활하게 결합하고 쿼리 결과에서 새로운 데이터 세트를 생성하여 보고를 강화하고, 데이터 과학 워크플로를 활성화하거나, 실시간 고객 프로필로 수집할 수 있습니다. 예를 들어 고객 거래 데이터와 행동 데이터를 병합하여 타기팅된 마케팅 캠페인의 가치가 높은 대상자를 파악할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
|--------|-------------|
| JWT에서 OAuth 자격 증명으로 마이그레이션 | 서비스 중단을 방지하려면 만료되지 않는 JWT 자격 증명을 2025년 6월 30일까지 OAuth 서버 간 서버로 마이그레이션해야 합니다. 이 변경 사항은 보안 및 플랫폼 일관성을 향상시킵니다. 자세한 내용은 [JWT에서 OAuth 서버 간 자격 증명 안내서로 마이그레이션](../../query-service/ui/migrate-jwt-to-oauth.md)을 참조하십시오. |
| 기존 결과 테이블(제한된 가용성) | 드래그하여 선택 워크플로에 의존하는 사용자는 브라우저 기반 선택 및 복사 동작을 지원하는 기존 결과 표에 대한 액세스를 요청할 수 있습니다. 붙여넣은 출력은 탭으로 구분되므로 열이 Excel에서 정렬되고 읽을 수 있게 유지되므로 스프레드시트 검토 및 QA 프로세스가 더 쉬워집니다. 자세한 내용은 [쿼리 편집기 UI 안내서](../../query-service/ui/user-guide.md#legacy-results-table)를 참조하십시오. |

[!DNL Query Service]에 대한 자세한 내용은 [[!DNL Query Service] 개요](../../query-service/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다. 이러한 요구 사항을 처리하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분류해 주는 샌드박스를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 도구 플러그인 지원 확장 | 이제 채널 구성, 통합 의사 결정, 실험 설정/변형 등을 포함한 샌드박스 도구를 통해 추가 종속 오브젝트와 함께 캠페인을 마이그레이션할 수 있습니다. 지원되는 모든 Adobe Journey Optimizer 개체와 지원되는 캠페인 개체의 전체 목록을 보려면 [샌드박스 도구](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects) 안내서를 읽어 보십시오. |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상은 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계학적 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 세분화 기준 업데이트 | 2025년 5월 릴리스부터 스트리밍 세분화를 사용할 수 있는 대상 기준이 업데이트되었습니다. 이러한 변경 사항에 대한 자세한 내용은 [스트리밍 세분화 적격성 기준 업데이트](../../segmentation/eligibility-criteria-update.md)에서 확인할 수 있습니다. |

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 서드파티 데이터 소스에서 데이터를 수집합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL MySQL]에 대한 기본 인증 지원 | 이제 기본 인증을 사용하여 [!DNL MySQL] 데이터베이스를 Experience Platform에 연결할 수 있습니다. 자세한 내용은 [[!DNL MySQL] 소스 개요](../../sources/connectors/databases/mysql.md)를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.