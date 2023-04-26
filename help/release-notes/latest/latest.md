---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 2023년 3월 릴리스 노트입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 938b4ba7affadc7ad0eca086d7cc2c9ce1a54a83
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2023년 4월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 준비](#data-prep)
- [경험 데이터 모델](#xdm)
- [실시간 고객 프로필](#profile)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처된 대로 조직의 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 개의 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능** {#dashboards-new-updated-features}

| 기능 | 설명 |
| --- | --- |
| 사용자 정의 대시보드 | 이제 다음을 수행할 수 있습니다 **내역 데이터 필터링** 위젯 인사이트에서 최근 데이터 또는 사용자 지정 분석 기간을 사용합니다.<br>이제 다음을 수행할 수도 있습니다 **기존 위젯 복제**. 복제를 사용자 지정하고 해당 속성을 편집함으로써 고유한 새 위젯을 만들 때 처음부터 다시 시작하지 않도록 할 수 있습니다. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 지정 위젯을 만드는 방법 등 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md).

## 데이터 준비 {#data-prep}

데이터 준비를 통해 데이터 엔지니어가 XDM(Experience Data Model) 간 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 비프로덕션 샌드박스의 Adobe Analytics 채우기 기간 업데이트 | 비프로덕션 샌드박스의 Adobe Analytics 채우기 기간이 3개월로 줄었습니다. 프로덕션 샌드박스의 채우기 기능은 13개월에서 동일하게 유지됩니다. 이 변경 사항은 새 흐름에만 적용되며 기존 흐름에 영향을 주지 않습니다. 자세한 내용은 [Adobe Analytics 개요](../../sources/connectors/adobe-applications/analytics.md). |
| FPID 문자열을 ECID로 변환하는 새 매퍼 함수 | 를 사용하십시오 `fpid_to_ecid` Experience Platform 및 Experience Cloud 애플리케이션에서 사용할 FPID 문자열을 ECID로 변환하는 함수입니다. 자세한 내용은 [데이터 준비 함수 안내서](../../data-prep/functions.md). |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 이름 표시 전환 | 이제 스키마 편집기에서 원래 필드 이름과 더 사람이 읽을 수 있는 표시 이름 간에 전환할 수 있습니다. 이러한 유연성을 통해 필드 검색 및 스키마 편집을 향상시킬 수 있습니다. 표준 필드 그룹의 표시 이름은 시스템에서 생성되지만 필요한 경우 UI를 통해 사용자 지정할 수도 있습니다. |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 고객 데이터를 통합할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 익명의 프로필 데이터 만료 | 일반적으로 익명의 프로필 데이터 만료 기능을 사용할 수 있습니다. 이 릴리스는 활성화되면 Experience Platform 인스턴스에서 오래된 익명의 프로필을 계속 제거합니다. 이 기능 및 익명의 프로필에 대한 자세한 내용은 [익명의 프로필 데이터 만료 안내서](../../profile/pseudonymous-profiles.md). |

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Microsoft Dynamics, Salesforce CRM 및 Salesforce Marketing Cloud에 대한 행 수준 데이터 필터링을 위한 API 지원 | 논리 및 비교 연산자를 사용하여 Microsoft Dynamics, Salesforce CRM 및 Salesforce Marketing Cloud 소스에 대한 행 수준 데이터를 필터링합니다. 안내서 읽기 [API를 사용하여 소스에 대한 데이터 필터링](../../sources/tutorials/api/filter.md) 추가 정보. |
| Shopify 스트리밍 베타 가용성 | 다음 [Shopify 스트리밍 소스](../../sources/connectors/ecommerce/shopify-streaming.md) 이제 베타로 제공됩니다. Shopify 스트리밍 소스를 사용하여 Shopify 파트너 계정의 데이터를 Experience Platform으로 스트리밍합니다. |
| OneTrust 통합의 일반 공급 | 다음 [OneTrust 통합 소스](../../sources/connectors/consent-and-preferences/onetrust.md) 은 현재 GA입니다. OneTrust 통합 소스를 사용하여 OneTrust 통합 계정의 동의 및 환경 설정 데이터를 Experience Platform으로 가져옵니다. |
| oracle 서비스 클라우드의 일반 공급 | 다음 [Oracle 서비스 클라우드 소스](../../sources/connectors/customer-success/oracle-service-cloud.md) 은 현재 GA입니다. oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 데이터를 Experience Platform으로 가져옵니다. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).