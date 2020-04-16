---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 소스 커넥터 개요
topic: overview
translation-type: tm+mt
source-git-commit: 92ba230d71e419e33567833ad562e6ffef996d0a

---


# 소스 커넥터 개요

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 제공업체에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 인터랙티브한 UI를 제공합니다. 이러한 소스 연결을 통해 타사 시스템을 인증하고, 통합 실행에 대한 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Adobe Experience Platform을 사용하면 서로 다른 소스로부터 수집한 데이터를 중앙에서 관리하고 이를 통해 얻은 인사이트를 활용하여 더 많은 작업을 수행할 수 있습니다.

## 소스 유형

경험 플랫폼의 소스는 다음 카테고리로 그룹화됩니다.

### Adobe 애플리케이션

Adobe Experience Platform을 사용하면 Adobe Analytics, Adobe Audience Manager, Experience Platform Launch 등 다른 Adobe 애플리케이션에서 데이터를 인제스트할 수 있습니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Adobe Audience Manager 커넥터 개요](connectors/adobe-applications/audience-manager.md)
- [UI에서 Adobe Audience Manager 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)
- [Adobe Analytics 데이터 커넥터 개요](connectors/adobe-applications/analytics.md)
- [UI에서 Adobe Analytics 소스 커넥터 만들기](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)

### 광고

Adobe Experience Platform은 타사 광고 시스템의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Google 광고 커넥터](connectors/advertising/ads.md)

### 클라우드 스토리지

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드하지 않고도 고유한 데이터를 플랫폼에 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공 마루 또는 구분된 형태로 포맷될 수 있습니다. 프로세스의 모든 단계는 사용자 인터페이스를 사용하여 소스 워크플로우에 통합됩니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Azure Data Lake Storage Gen2 커넥터](connectors/cloud-storage/adls-gen2.md)
- [Azure Blob 및 Amazon S3 커넥터](connectors/cloud-storage/blob-s3.md)
- [FTP 및 SFTP 커넥터](connectors/cloud-storage/ftp-sftp.md)
- [Google 클라우드 스토리지 커넥터](connectors/cloud-storage/google-cloud-storage.md)

### 고객 관계 관리(CRM)

CRM 시스템은 고객과의 관계를 구축하는 데 도움이 되는 데이터를 제공하므로 충성도를 생성하고 고객 유지율을 높일 수 있습니다. Experience Platform은 Microsoft Dynamics 365 및 Salesforce에서 CRM 데이터를 인제스트할 수 있도록 지원합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Microsoft Dynamics 커넥터](connectors/crm/ms-dynamics.md)
- [Salesforce 커넥터](connectors/crm/salesforce.md)

### 고객 성공 사례

Adobe Experience Platform은 타사 고객 성공 애플리케이션의 데이터 인제스트 지원을 제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Salesforce Service Cloud 커넥터](connectors/customer-success/salesforce-service-cloud.md)
- [ServiceNow 커넥터](connectors/customer-success/servicenow.md)

### 데이터베이스

Experience Platform은 타사 데이터베이스의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Amazon Redshift 커넥터](connectors/databases/redshift.md)
- [Azure HDInsights 커넥터의 Apache Hive](connectors/databases/hive.md)
- [Azure HDInsights 커넥터의 Apache Spark](connectors/databases/spark.md)
- [Azure Synapse Analytics 커넥터](connectors/databases/synapse-analytics.md)
- [Azure 테이블 저장소 커넥터](connectors/databases/ats.md)
- [Google BigQuery 커넥터](connectors/databases/bigquery.md)
- [MariaDB 커넥터](connectors/databases/mariadb.md)
- [Microsoft SQL Server 커넥터](connectors/databases/sql-server.md)
- [MySQL 커넥터](connectors/databases/mysql.md)
- [피닉스 커넥터](connectors/databases/phoenix.md)
- [PostgreSQL 커넥터](connectors/databases/postgres.md)

### 마케팅 자동화

Adobe Experience Platform은 타사 마케팅 자동화 시스템의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [HubSpot 커넥터](connectors/marketing-automation/hubspot.md)

### 결제

Adobe Experience Platform은 타사 결제 시스템에서 데이터를 인제스트할 수 있도록 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [PayPal 커넥터](connectors/payments/paypal.md)

### 프로토콜

Experience Platform은 타사 프로토콜 시스템에서 데이터를 인제스트할 수 있도록 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [일반 OData 커넥터](connectors/protocols/odata.md)

## 데이터 수집의 소스에 대한 액세스 제어

데이터 수집의 소스에 대한 권한은 Adobe Admin Console에서 관리할 수 있습니다. 특정 제품 프로필의 권한 *탭을 통해* 권한을 액세스할 수 있습니다. [ **권한 편집** ] 패널에서 *데이터 통합 메뉴 항목을 통해 소스와 관련된 권한을* 액세스할 수 있습니다. 소스 **보기** 권한은 카탈로그 *탭의 사용 가능한 소스 및* 검색 *탭의 인증된 소스에 대한 읽기 전용 액세스 권한을* 부여하는 반면, 소스 관리 권한은 **소스를 만들고, 편집하고, 비활성화할 수 있는 모든 액세스 권한을** 부여합니다.

다음 표에서는 이러한 권한의 다양한 조합을 기반으로 UI가 어떻게 동작하는지에 대해 설명합니다.

| 권한 수준 | 설명 |
| ---- | ----|
| **소스** 보기 | [카탈로그] 탭에서 각 소스 유형의 소스에 대한 읽기 액세스 권한을 부여할 *수* 있고 *검색*, 계정 *및* DataFlow ** 탭도있습니다. |
| **소스** 관리 | [소스 보기]에 포함된 **기능**&#x200B;외에도 *카탈로그의* Connect 소스 *옵션* 및 [검색 *]의 [데이터 선택]* **&#x200B;및 [검색]의 [데이터 선택] 옵션에 대한 액세스 권한을 부여합니다. **또한 소스** 관리를 사용하면 DataFlow를 활성화하거나 비활성화하고 *일정을* 편집할 수 있습니다. |
| **소스 보기** 해제 **및 소스** 관리 해제 | 소스에 대한 모든 액세스 권한을 취소합니다. |

Admin Console을 통해 부여된 사용 가능한 권한(이러한 네 가지 소스 포함)에 대한 자세한 내용은 [액세스 제어 개요를](../access-control/home.md)참조하십시오.
