---
title: Adobe Experience Platform 릴리스 정보 2022년 3월
description: Adobe Experience Platform의 2022년 3월 릴리스 정보입니다.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 18%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2022년 3월 30일**

Adobe Experience Platform의 새로운 기능:

- [감사 로그](#audit-logs)
- [Real-Time CDP B2B 에디션의 관련 계정](#related-accounts)

Adobe Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [데이터 수집](#data-collection)
- [[!DNL Query Service]](#query-service)
- [소스](#sources)

## 감사 로그 {#audit-logs}

Experience Platform을 사용하면 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 감사 로그는 누가 무엇을 언제 수행했는지에 대한 정보를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 세트, 스키마, 클래스, 필드 그룹, 데이터 유형, 샌드박스, 대상, 세그먼트, 병합 정책, 계산된 속성, 제품 프로필 및 계정(Adobe)에 대한 감사 로그 | 이러한 리소스는 감사 로그에서 기록됩니다. 이 기능이 활성화되어 있으면 활동이 발생할 때 감사 로그가 자동으로 수집됩니다. 로그 수집을 수동으로 활성화할 필요가 없습니다. |
| 감사 로그 내보내기 | 감사 로그는 다음으로 다운로드할 수 있습니다. `CSV` 또는 `JSON` 파일. 생성된 파일은 컴퓨터에 직접 저장됩니다. |

{style="table-layout:auto"}

플랫폼의 감사 로그에 대한 자세한 내용은 [감사 로그 개요](../../landing/governance-privacy-security/audit-logs/overview.md).

## Real-Time CDP B2B 에디션의 관련 계정 {#related-accounts}

>[!NOTE]
>
>관련 계정 기능은 Real-Time CDP B2B 에디션 고객만 사용할 수 있습니다.

B2B 기업은 고객 정보가 여러 시스템에 저장되어 있는 경우가 많으며, 각 시스템에는 동일한 실제 사업체에 대한 부분적인 데이터만 포함되어 있거나 심지어 충돌하는 데이터도 포함되어 있습니다. 따라서 B2B 마케팅 및 판매 노력의 효율성과 효과를 줄이기 위해 고객을 정확하게 파악해야 하는 과제가 커집니다. 관련 계정의 출시와 함께 [!DNL Real-Time CDP B2B] 이제 탐색 중인 계정과 유사한 계정 목록이 표시됩니다. 세그먼트 정의에 관련 계정을 포함시켜 범위를 넓히거나 세그먼트에 더 넓은 기준을 적용할 수 있습니다.

다음 설명서 페이지에서 기능에 대해 자세히 알아보십시오.

- [Real-Time CDP B2B 에디션의 관련 계정 개요](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [계정 프로필 UI 안내서의 관련 계정 탭](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [세그먼트 정의에서 관련 계정을 사용하는 방법](../../rtcdp/segmentation/b2b.md#related-accounts)

Real-Time CDP B2B 에디션에 대한 자세한 내용은 [개요](../../rtcdp/overview.md).

## 경고 {#alerts}

Experience Platform을 사용하면 다양한 플랫폼 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 다음을 통해 다양한 경고 규칙에 가입할 수 있습니다. [!UICONTROL 경고] Platform 사용자 인터페이스의 탭으로, UI 자체 내에서 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 경고 규칙 | 이제 데이터 수집과 관련된 소스에 대해 두 가지 새로운 경고 규칙을 사용할 수 있습니다. 의 개요 보기 [경고 규칙](../../observability/alerts/rules.md) 경고 유형 업데이트 목록. |

{style="table-layout:auto"}

플랫폼의 경고에 대한 자세한 내용은 [경고 개요](../../observability/alerts/overview.md).

## 대시보드 {#dashboards}

Adobe Experience Platform에서 여러 기능 제공 [!DNL dashboards] 이를 통해 일별 스냅샷 중에 캡처한 대로 조직 데이터에 대한 중요한 정보를 볼 수 있습니다.

### 프로필 대시보드

Experience Platform 대시보드에는 조직이 Profile Store in Profile에 가지고 있는 속성(레코드) 데이터의 스냅샷이 표시됩니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 세분화되지 않은 프로필 위젯 | 위젯은 세그먼트에 첨부되지 않은 모든 프로필의 총 수를 제공합니다. 생성된 숫자는 마지막 스냅샷을 기준으로 정확하며 조직 전체에서 프로필 활성화 기회를 나타냅니다. 다음을 참조하십시오. [프로필 표준 위젯 설명서](../../dashboards/guides/profiles.md#standard-widgets) 추가 정보. |
| 세분화되지 않은 프로필 트렌드 위젯 | 이 위젯은 지정된 기간 동안 세그먼트에 연결되지 않은 프로필 개수에 대한 선 그래프 그림을 제공합니다. 30일, 90일, 12개월 기간에 걸쳐 트렌드를 시각화할 수 있습니다. 다음을 참조하십시오. [프로필 표준 위젯 설명서](../../dashboards/guides/profiles.md#standard-widgets) 추가 정보. |
| ID 위젯별 세분화되지 않은 프로필 | 이 위젯은 고유 식별자별로 분할되지 않은 총 프로필 개수를 분류합니다. 데이터는 막대 차트로 시각화됩니다. 다음을 참조하십시오. [프로필 표준 위젯 설명서](../../dashboards/guides/profiles.md#standard-widgets) 추가 정보. |
| 단일 ID 프로필 위젯 | 이 위젯에서는 ID를 만드는 한 가지 유형의 ID(이메일 또는 ECID)만 있는 조직 프로필 수를 제공합니다. 다음을 참조하십시오. [프로필 표준 위젯 설명서](../../dashboards/guides/profiles.md#standard-widgets) 추가 정보. |

{style="table-layout:auto"}

프로필 대시보드에 대한 자세한 내용은 [프로필 대시보드 개요](../../dashboards/guides/profiles.md).

### 대상 대시보드

대상 대시보드에는 조직이 Experience Platform 내에서 활성화한 대상의 스냅샷이 표시됩니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상 수 위젯 | 위젯은 대상을 활성화하고 시스템 내에서 전달할 수 있는 사용 가능한 총 끝점 수를 제공합니다. 이 개수에는 활성 대상과 비활성 대상이 모두 포함됩니다. 다음을 참조하십시오. [대상 표준 위젯 설명서](../../dashboards/guides/destinations.md#standard-widgets) 추가 정보. |

{style="table-layout:auto"}

플랫폼의 대상 대시보드에 대한 자세한 내용은 [대상 대시보드 개요](../../dashboards/guides/destinations.md).

## 데이터 수집 {#data-collection}

Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 전역 데이터 스트림 설정 | 이제 데이터스트림을 구성할 때 지리적 위치, 자사 ID 쿠키 및 타사 ID 동기화와 같은 몇 가지 새로운 전역 설정을 구성할 수 있습니다. 의 섹션을 참조하십시오. [데이터스트림 구성](../../datastreams/overview.md#create) 자세한 내용은 데이터스트림 UI 안내서를 참조하십시오. |
| [Edge Network Server API](../../server-api/overview.md) | Server API를 사용하면 고객이 새로운 인증된 엔드포인트를 사용하여 Experience Platform 에지 네트워크와 상호 작용하여 다양한 데이터 수집, 개인화, 광고 및 마케팅 사용 사례를 강화할 수 있습니다. |

Platform에서의 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md).

## 쿼리 서비스 {#query-service}

[!DNL Query Service] 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]. 에서 모든 데이터 세트를 결합할 수 있습니다. [!DNL Data Lake] 보고, Data Science Workspace에 사용하거나 실시간 고객 프로필로 수집하기 위한 새 데이터 세트로 쿼리 결과를 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| `table_exists` | 새 기능 명령은 시스템에 현재 테이블이 있는지 확인하는 데 사용됩니다. 이 명령은 부울 값을 반환합니다. `true` 테이블인 경우 **다음과 같음** 존재함, 및 `false` 테이블이 다음과 같은 경우 **아님** 존재합니다. 다음을 참조하십시오. [SQL 구문 설명서](../../query-service/sql/syntax.md) 추가 정보. |

{style="table-layout:auto"}

사용 가능한 기능에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집을 전체적으로 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 이제 B2B 사용에 사용할 수 있는 소스 | 이제 B2B 사용 사례용 플랫폼에서 사용 가능한 모든 소스를 사용할 수 있습니다. 다음을 참조하십시오. [소스 카탈로그](../../sources/home.md) 사용 가능한 소스의 전체 목록. |
| 새로운 기능의 일반 출시 [!DNL Oracle Eloqua] 소스 | 이제 다음을 사용할 수 있습니다. [!DNL Oracle Eloqua] 소스에서 데이터를 원활하게 수집 [!DNL Oracle Eloqua] 인스턴스(계정, 캠페인, 연락처)를 플랫폼에 추가합니다. 다음에서 설명서를 참조하십시오. [만들기 [!DNL Oracle Eloqua] 소스 연결](../../sources/connectors/marketing-automation/oracle-eloqua.md) 추가 정보. |
| 의 API 개선 사항 [!DNL Data Landing Zone] | 다음 [!DNL Data Landing Zone] 이제 소스는 를 사용할 때 파일 속성의 자동 검색을 지원합니다. [!DNL Flow Service] API. 다음에서 설명서를 참조하십시오. [만들기 [!DNL Data Landing Zone] 소스 연결](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 추가 정보. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
