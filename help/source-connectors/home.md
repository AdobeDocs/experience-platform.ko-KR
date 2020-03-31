---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 소스 커넥터 개요
topic: overview
translation-type: tm+mt
source-git-commit: 291d669cc0f5b009b23dc2771688ee54b53d08db

---


# 소스 커넥터 개요

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 제공업체에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 인터랙티브한 UI를 제공합니다. 이러한 소스 연결을 통해 타사 시스템을 인증하고, 통합 실행에 대한 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Adobe Experience Platform을 사용하면 서로 다른 소스로부터 수집한 데이터를 중앙에서 관리하고 이를 통해 얻은 인사이트를 활용하여 더 많은 작업을 수행할 수 있습니다.

## 소스 유형

경험 플랫폼의 소스는 다음 카테고리로 그룹화됩니다.

### Adobe 애플리케이션

Adobe Experience Platform을 사용하면 Adobe Analytics, Adobe Audience Manager, Experience Platform Launch 등 다른 Adobe 애플리케이션에서 데이터를 인제스트할 수 있습니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Adobe Audience Manager 커넥터 개요](./ui/adobe-applications/audience-manager.md)
- [UI에서 Adobe Audience Manager 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)
- [Adobe Analytics 데이터 커넥터 개요](./ui/adobe-applications/analytics.md)
- [UI에서 Adobe Analytics 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)

### 클라우드 스토리지

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드하지 않고도 고유한 데이터를 플랫폼에 가져올 수 있습니다. 프로세스의 모든 단계는 사용자 인터페이스를 사용하여 소스 워크플로우에 통합됩니다. 클라우드 저장소 공급자에 대한 지원에는 Amazon S3, Azure Blob, FTP 서버 및 SFTP 서버가 포함됩니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [UI 파섹](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/amazon-s3-ui-tutorial.md)
- [UI에서 Azure Data Lake Storage Gen2 원본 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/adls-gen2-ui-tutorial.md)
- [UI에서 FTP 또는 SFTP 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/ftp-sftp-ui-tutorial.md)
- [UI에서 Google 클라우드 스토리지 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/google-cloud-storage-ui-tutorial.md)

### 고객 관계 관리(CRM)

CRM 시스템은 고객과의 관계를 구축하는 데 도움이 되는 데이터를 제공하므로 충성도를 생성하고 고객 유지율을 높일 수 있습니다. Experience Platform은 Microsoft Dynamics 365 및 Salesforce에서 CRM 데이터를 인제스트할 수 있도록 지원합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [UI에서 Microsoft Dynamics 365 또는 Salesforce 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/dynamics-salesforce-ui-tutorial.md)
- [UI에서 PayPal 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/paypal-tutorial.md)

### 고객 성공(CS)

Adobe Experience Platform은 타사 고객 성공 애플리케이션의 데이터 인제스트 지원을 제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [UI에서 Salesforce Service Cloud 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/salesforce-service-cloud-tutorial.md)
- [UI에서 ServiceNow 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/servicenow-ui-tutorial.md)

### 데이터베이스

Experience Platform은 타사 데이터베이스의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [UI에서 AWS Redshift 소스 커넥터 생성](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/amazon-redshift-ui-tutorial.md)
- [UI 파섹](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/azure-synapse-analytics-ui-tutorial.md)
- [UI에서 Google BigQuery 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/google-big-query-ui-tutorial.md)
- [UI에서 MariaDB 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/database-nosql/mariadb-api-tutorial.md)
- [UI에서 Microsoft SQL Server 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/sql-server-ui-tutorial.md)
- [UI에서 MySQL 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/mysql-ui-tutorial.md)
- [UI에서 PostgreSQL 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/postgresql-tutorial.md)

### 마케팅 자동화

Adobe Experience Platform은 타사 마케팅 자동화 시스템의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [UI에서 HubSpot 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/marketing-automation/hubspot-tutorial.md)

## API 자습서

Flow Service API를 사용하여 소스 커넥터를 만들 수 있습니다. 자세한 내용은 [소스 API 자습서 문서를](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)참조하십시오.

## 데이터 수집의 소스에 대한 액세스 제어

데이터 수집의 소스에 대한 권한은 Adobe Admin Console에서 관리할 수 있습니다. 특정 제품 프로필의 권한 *탭을 통해* 권한을 액세스할 수 있습니다. [ **권한 편집** ] 패널에서 *데이터 통합 메뉴 항목을 통해 소스와 관련된 권한을* 액세스할 수 있습니다. 소스 **보기** 권한은 카탈로그 *탭의 사용 가능한 소스 및* 검색 *탭의 인증된 소스에 대한 읽기 전용 액세스 권한을* 부여하는 반면, 소스 관리 권한은 **소스를 만들고, 편집하고, 비활성화할 수 있는 모든 액세스 권한을** 부여합니다.

다음 표에서는 이러한 권한의 다양한 조합을 기반으로 UI가 어떻게 동작하는지에 대해 설명합니다.

| 권한 수준 | 설명 |
| ---- | ----|
| **소스** 보기 | [카탈로그] 탭에서 각 소스 유형의 소스에 대한 읽기 액세스 권한을 부여할 *수* 있고 *검색*, 계정 *및* DataFlow ** 탭도있습니다. |
| **소스** 관리 | [소스 보기]에 포함된 **기능**&#x200B;외에도 *카탈로그의* Connect 소스 *옵션* 및 [검색 *]의 [데이터 선택]* **&#x200B;및 [검색]의 [데이터 선택] 옵션에 대한 액세스 권한을 부여합니다. **또한 소스** 관리를 사용하면 DataFlow를 활성화하거나 비활성화하고 *일정을* 편집할 수 있습니다. |
| **소스 보기** 해제 **및 소스** 관리 해제 | 소스에 대한 모든 액세스 권한을 취소합니다. |

Admin Console을 통해 부여된 사용 가능한 권한(이러한 네 가지 소스 포함)에 대한 자세한 내용은 [액세스 제어 개요를](../access-control/home.md)참조하십시오.
