---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트(2020년 4월 8일)
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: b3ee2839412c9949d67c2ae976e3df32fea7731e

---


# Adobe Experience Platform 릴리스 노트

## 릴리스 날짜: 2020년 4월 8일

## 개인 정보 서비스

새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform 개인 정보 보호 서비스는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 개인 정보 보호 서비스를 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터를 액세스하고 삭제할 수 있는 요청을 제출하여 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | 이제 태국에 있는 개인 정보 보호 법(PDPA)에 따라 개인 정보 요청을 작성하고 추적할 수 있습니다. API에서 개인 정보 요청을 할 때 `regulation` 배열은 &quot;pdpa_tha&quot; 값을 수락합니다. |
| UI의 네임스페이스 유형 | 이제 개인 정보 서비스 UI의 요청 빌더에서 다른 네임스페이스 유형을 지정할 수 있습니다. 자세한 내용은 [사용 안내서를](../../privacy-service/ui/user-guide.md) 참조하십시오. |
| 이전 끝점 사용 중단 | 이전 API 끝점(`data/privacy/gdpr`)은 더 이상 사용되지 않습니다. |

알려진 문제

* 없음

개인정보 보호 서비스에 대한 자세한 내용은 먼저 개인정보 보호 서비스 [개요를](../../privacy-service/home.md)읽으십시오.

## 소스

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 인터랙티브한 UI와 RESTful API를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

### 새로운 기능

| 기능 | 설명 |
| ------- | ----------- |
| 데이터베이스에 대한 API 및 UI 지원 | Apache Spark(HDInsights에서), Azure Synapse Analytics, Azure Table Storage, Hive(HDInsights에서) 및 Phoenix에 대한 새 원본 커넥터입니다. |
| 결제 기반의 애플리케이션에 대한 API 및 UI 지원 | PayPal의 새로운 소스 커넥터 |
| 프로토콜 기반 애플리케이션에 대한 API 및 UI 지원 | 범용 OData의 새 소스 커넥터. |

### 알려진 문제

* 없음

소스에 대한 자세한 내용은 [소스 개요를](../../source-connectors/home.md)참조하십시오.

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->