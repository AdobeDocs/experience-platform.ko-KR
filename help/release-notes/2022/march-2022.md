---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
source-git-commit: 004835ab8af8f187c3e6af036429072e8de19024
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 7%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 3월 30일**

Adobe Experience Platform의 새로운 기능:

- [감사 로그](#audit-logs)

Adobe Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Query Service]](#query-service)
- [소스](#sources)
<!-- - [Experience Data Model (XDM)](#xdm) -->

## 감사 로그 {#audit-logs}

Experience Platform을 사용하면 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 감사 로그는 작업을 수행한 사람과 수행한 시기에 대한 정보를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 집합, 스키마, 클래스, 필드 그룹, 데이터 유형, 샌드박스, 대상, 세그먼트, 병합 정책, 계산된 속성, 제품 프로필 및 계정(Adobe)에 대한 감사 로그 | 감사 로그에 기록되는 리소스입니다. 이 기능이 활성화되어 있으면 활동이 발생하면 감사 로그가 자동으로 수집됩니다. 수동으로 로그 수집을 활성화할 필요는 없습니다. |
| 감사 로그 내보내기 | 감사 로그를 `CSV` 또는 `JSON` 파일. 생성된 파일은 컴퓨터에 직접 저장됩니다. |

{style=&quot;table-layout:auto&quot;}

Platform의 감사 로그에 대한 자세한 내용은 [감사 로그 개요](../../landing/governance-privacy-security/audit-logs/overview.md).

## 경고 {#alerts}

Experience Platform을 사용하면 다양한 플랫폼 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 을 통해 다른 경고 규칙에 가입할 수 있습니다 [!UICONTROL 경고] 플랫폼 사용자 인터페이스의 탭. 및 UI 자체 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 경고 규칙 | 이제 데이터 수집과 관련된 소스에 두 개의 새로운 경고 규칙을 사용할 수 있습니다. 다음 사항에 대한 개요를 참조하십시오. [경고 규칙](../../observability/alerts/rules.md) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

Platform의 경고에 대한 자세한 내용은 [경고 개요](../../observability/alerts/overview.md).

## 대시보드 {#dashboards}

Adobe Experience Platform은 여러 기능을 제공합니다 [!DNL dashboards] 을 통해 일일 스냅샷 동안 캡처된 조직 데이터에 대한 중요한 정보를 볼 수 있습니다.

### 프로필 대시보드

프로필 대시보드는 Experience Platform의 프로필 저장소 내에 조직에 있는 속성(레코드) 데이터의 스냅숏을 표시합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 세그먼트화되지 않은 프로필 위젯 | 위젯은 세그먼트에 첨부되지 않은 모든 프로필의 총 수를 제공합니다. 생성된 숫자는 마지막 스냅샷에서 정확하며 조직 전체에서 프로파일 활성화 기회를 나타냅니다. 자세한 내용은 [프로필 표준 위젯 설명서](../../dashboards/guides/profiles.md#standard-widgets) 추가 정보. |
| 세그먼트화되지 않은 프로필 트렌드 위젯 | 이 위젯은 주어진 기간 동안 어떤 세그먼트에도 첨부되지 않는 프로필 수에 대한 선 그래프 그림을 제공합니다. 이 트렌드는 30일, 90일 및 12개월 기간에 걸쳐 시각화할 수 있습니다. 자세한 내용은 [프로필 표준 위젯 설명서](../../dashboards/guides/profiles.md#standard-widgets) 추가 정보. |
| ID 위젯으로 세그먼트화되지 않은 프로필 | 이 위젯은 세그먼트화되지 않은 프로필의 총 수를 고유 식별자로 분류합니다. 데이터는 막대 차트에 시각화됩니다. 자세한 내용은 [프로필 표준 위젯 설명서](../../dashboards/guides/profiles.md#standard-widgets) 추가 정보. |
| 단일 ID 프로필 위젯 | 이 위젯은 이메일 또는 ECID와 같은 ID 유형을 만드는 유형만 포함하는 조직의 프로필 수를 제공합니다. 자세한 내용은 [프로필 표준 위젯 설명서](../../dashboards/guides/profiles.md#standard-widgets) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

프로필 대시보드에 대한 자세한 내용은 [프로필 대시보드 개요](../../dashboards/guides/profiles.md).

### 대상 대시보드

대상 대시보드는 Experience Platform 내에서 조직에서 활성화한 대상의 스냅숏을 표시합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상 수 위젯 | 위젯은 시스템 내에서 대상을 활성화 및 전달할 수 있는 사용 가능한 총 엔드포인트 수를 제공합니다. 이 번호에는 활성 대상과 비활성 대상이 모두 포함됩니다. 자세한 내용은 [대상 표준 위젯 설명서](../../dashboards/guides/destinations.md#standard-widgets) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

Platform의 대상 대시보드에 대한 자세한 내용은 [대상 대시보드 개요](../../dashboards/guides/destinations.md).

<!-- ## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

| Feature | Description |
| --- | --- |
| Add or remove individual standard fields for a schema | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br>You can now also define ad-hoc custom fields directly within the schema structure and assign them to a new or existing custom field group without needing to create or edit the field group beforehand.<br><br>See the guide on [creating and editing schemas in the UI](../../xdm/ui/resources/schemas.md) for more information on these new workflows. |

{style="table-layout:auto"}

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md). -->

## 쿼리 서비스 {#query-service}

[!DNL Query Service] 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]. 에서 모든 데이터 세트에 가입할 수 있습니다 [!DNL Data Lake] 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새로운 데이터 세트로 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| `table_exists` | 새 기능 명령은 현재 시스템에 테이블이 있는지 여부를 확인하는 데 사용됩니다. 이 명령은 부울 값을 반환합니다. `true` 만약 **does** 존재 및 `false` 테이블에서 **not** 존재 자세한 내용은 [SQL 구문 설명서](../../query-service/sql/syntax.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

사용 가능한 기능에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 전체 데이터 수집을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 이제 B2B 사용에 대한 소스를 사용할 수 있습니다 | 이제 B2B 사용 사례에 대해 플랫폼에서 사용 가능한 모든 소스를 사용할 수 있습니다. 자세한 내용은 [소스 카탈로그](../../sources/home.md) 를 참조하십시오. |
| 신규 제품의 일반 공급 [!DNL Oracle Eloqua] 소스 | 이제 를 사용할 수 있습니다 [!DNL Oracle Eloqua] 소스에서 데이터를 원활하게 수집할 수 있습니다. [!DNL Oracle Eloqua] Platform에 인스턴스(계정, 캠페인, 연락처)를 제공합니다. 다음 문서를 참조하십시오. [만들기 [!DNL Oracle Eloqua] 소스 연결](../../sources/connectors/marketing-automation/oracle-eloqua.md) 추가 정보. |
| 에 대한 API 개선 사항 [!DNL Data Landing Zone] | 다음 [!DNL Data Landing Zone] 이제 소스는 [!DNL Flow Service] API. 다음 문서를 참조하십시오. [만들기 [!DNL Data Landing Zone] 소스 연결](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
