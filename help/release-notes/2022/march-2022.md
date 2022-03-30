---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
source-git-commit: 9117fffc58786f05e8741d9695ddb551344b6cc7
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 7%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 3월 30일**

Adobe Experience Platform의 새로운 기능:

- [감사 로그](#audit-logs)

Adobe Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [XDM(경험 데이터 모델)](#xdm)
- [소스](#sources)

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

## XDM(경험 데이터 모델) {#xdm}

XDM(Experience Data Model)은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마에 대한 개별 표준 필드 추가 또는 제거 | 이제 스키마 편집기 UI를 사용하여 스키마에 표준 필드 그룹 부분을 추가할 수 있으므로, 사용자 지정 리소스를 처음부터 빌드하지 않아도 포함하도록 선택한 필드에 더 유연하게 대처할 수 있습니다.<br><br>이제 스키마 구조 내에서 직접 임시 사용자 지정 필드를 정의하고 필드 그룹을 미리 만들거나 편집할 필요 없이 새 사용자 지정 필드 그룹에 할당할 수도 있습니다.<br><br>다음 안내서를 참조하십시오. [UI에서 스키마 만들기 및 편집](../../xdm/ui/resources/schemas.md) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 이제 B2B 사용에 대한 소스를 사용할 수 있습니다 | 이제 B2B 사용 사례에 대해 플랫폼에서 사용 가능한 모든 소스를 사용할 수 있습니다. 자세한 내용은 [소스 카탈로그](../../sources/home.md) 를 참조하십시오. |
| 신규 제품의 일반 공급 [!DNL Oracle Eloqua] 소스 | 이제 를 사용할 수 있습니다 [!DNL Oracle Eloqua] 소스에서 데이터를 원활하게 수집할 수 있습니다. [!DNL Oracle Eloqua] Platform에 인스턴스(계정, 캠페인, 연락처)를 제공합니다. 다음 문서를 참조하십시오. [만들기 [!DNL Oracle Eloqua] 소스 연결](../../sources/connectors/oracle-eloqua.md) 추가 정보. |
| 에 대한 API 개선 사항 [!DNL Data Landing Zone] | 다음 [!DNL Data Landing Zone] 이제 소스는 [!DNL Flow Service] API. 다음 문서를 참조하십시오. [만들기 [!DNL Data Landing Zone] 소스 연결](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
