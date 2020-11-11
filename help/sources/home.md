---
keywords: Experience Platform;home;popular topics;source connectors;source connector;sources;data sources;data source;data source connection
solution: Experience Platform
title: Adobe Experience Platform 소스 커넥터 개요
topic: overview
description: Adobe Experience Platform은 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있도록 허용합니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.
translation-type: tm+mt
source-git-commit: d26eaf699a67a1bc7111f5f97da277368fcc4629
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# 소스 커넥터 개요

Adobe Experience Platform은 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있도록 허용합니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 제공자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 타사 시스템을 인증하고, 통합 실행에 대한 시간을 설정하고, 데이터 처리 처리량을 관리할 수 있습니다.

이를 통해 서로 다른 소스에서 수집한 데이터를 중앙에서 관리하고, 얻은 인사이트를 활용하여 더 많은 작업을 수행할 수 있습니다. [!DNL Experience Platform]

## 소스 유형

소스 [!DNL Experience Platform] 는 다음 카테고리로 그룹화됩니다.

### Adobe 응용 프로그램

[!DNL Experience Platform] adobe analytics, Adobe Audience Manager 및 기타 Adobe 애플리케이션에서 데이터를 수집할 수 있습니다 [!DNL Experience Platform Launch]. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Adobe Audience Manager 커넥터 개요](connectors/adobe-applications/audience-manager.md)
- [UI에서 Adobe Audience Manager 소스 커넥터 만들기](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics 분류 데이터 커넥터 개요](connectors/adobe-applications/classifications.md)
- [UI에서 Adobe Analytics 분류 데이터 소스 커넥터 만들기](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics 데이터 커넥터 개요](connectors/adobe-applications/analytics.md)
- [UI에서 Adobe Analytics 소스 커넥터 만들기](./tutorials/ui/create/adobe-applications/analytics.md)
- [UI에서 고객 속성 소스 커넥터 만들기](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### 광고

[!DNL Experience Platform] 타사 광고 시스템에서 데이터 인제스트를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Google AdWords]](connectors/advertising/ads.md) 커넥터

### 클라우드 스토리지

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 [!DNL Platform] 없이 고유한 데이터를 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공식 또는 구분 기호로 형식을 지정할 수 있습니다. 프로세스의 모든 단계는 사용자 인터페이스를 사용하여 소스 워크플로우에 통합됩니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Azure Data Lake Storage Gen2] 커넥터](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] 커넥터](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] 커넥터](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] 커넥터](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] 커넥터](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] 커넥터](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] 커넥터](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP and SFTP] 커넥터](connectors/cloud-storage/ftp-sftp.md)
- [[!DNL Google Cloud Storage] 커넥터](connectors/cloud-storage/google-cloud-storage.md)

### 고객 관계 관리(CRM)

CRM 시스템은 고객과의 관계를 구축하는 데 도움이 되는 데이터를 제공하므로 충성도를 생성하고 고객 유지율을 높일 수 있습니다. [!DNL Experience Platform] 및 [!DNL Microsoft Dynamics 365] 에서 CRM 데이터 인제스트 지원을 [!DNL Salesforce]제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Microsoft Dynamics] 커넥터](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] 커넥터](connectors/crm/salesforce.md)

### 고객 성공 사례

[!DNL Experience Platform] 타사 고객 성공 애플리케이션에서 데이터 인제스트 지원을 제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Salesforce Service Cloud] 커넥터](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] 커넥터](connectors/customer-success/servicenow.md)

### 데이터베이스

[!DNL Experience Platform] 타사 데이터베이스의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Amazon Redshift] 커넥터](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] 커넥터](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] 커넥터](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] 커넥터](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] 커넥터](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] 커넥터](connectors/databases/ats.md)
- [[!DNL Couchbase] 커넥터](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] 커넥터](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] 커넥터](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] 커넥터](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] 커넥터](connectors/databases/ibm-db2.md)
- [[!DNL Microsoft SQL Server] 커넥터](connectors/databases/sql-server.md)
- [[!DNL MySQL] 커넥터](connectors/databases/mysql.md)
- [[!DNL Oracle] 커넥터](connectors/databases/oracle.md)
- [[!DNL Phoenix] 커넥터](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] 커넥터](connectors/databases/postgres.md)

### eCommerce

[!DNL Experience Platform] 타사 e커머스 시스템에서 데이터 인제스트를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 마케팅 자동화

[!DNL Experience Platform] 타사 마케팅 자동화 시스템에서 데이터 인제스트를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL HubSpot] 커넥터](connectors/marketing-automation/hubspot.md)

### 결제

[!DNL Experience Platform] 타사 결제 시스템에서 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL PayPal] 커넥터](connectors/payments/paypal.md)

### 프로토콜

[!DNL Experience Platform] 타사 프로토콜 시스템에서 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Generic OData] 커넥터](connectors/protocols/odata.md)

## 데이터 수집의 소스에 대한 액세스 제어

데이터 수집의 소스에 대한 권한은 Adobe Admin Console 내에서 관리할 수 있습니다. 특정 제품 프로필의 **[!UICONTROL 권한]** 탭을 통해 권한을 액세스할 수 있습니다. [ **[!UICONTROL 권한]** 편집] 패널에서 **[!UICONTROL 데이터 수집]** 메뉴 항목을 통해 소스와 관련된 권한에 액세스할 수 있습니다. 소스 **[!UICONTROL 보기]** 권한은 **[!UICONTROL 카탈로그]** 탭 및 검색 **[!UICONTROL 탭의 인증된 소스]** 에 대한 읽기 전용 액세스 권한을 허용하지만, 소스 관리 권한은 소스를 만들고, 편집하고, 비활성화하는 데 대한 전체 액세스 권한을 **** 부여합니다.

다음 표에서는 이러한 권한의 다양한 조합을 기반으로 UI가 어떻게 동작하는지를 설명합니다.

| 권한 수준 | 설명 |
| ---- | ----|
| **[!UICONTROL 소스]** 보기 켜기 | [카탈로그] 탭에서 각 소스 유형의 소스에 대한 읽기 전용 액세스 권한뿐만 아니라 [찾아보기], [계정] 및 [데이터 흐름] 탭을 부여할 수 있습니다. |
| **[!UICONTROL 소스]** 관리 켜기 | 소스 **[!UICONTROL 보기에 포함된 기능 외에,]**&#x200B;카탈로그 **[!UICONTROL 의]** Connect 소스 **[!UICONTROL 옵션]** 에 대한 액세스 권한을 **[!UICONTROL 허용하며, Browse에서 Select Data]** 및 Select **** DataOption에 대한 액세스 권한을 부여합니다. **[!UICONTROL 또한 소스]** 관리를 사용하면 DataFlow를 활성화하거나 비활성화하고 **[!UICONTROL 해당 일정을]** 편집할 수 있습니다. |
| **[!UICONTROL 소스 보기]** 해제 및 **[!UICONTROL 소스]** 관리 해제 | 소스에 대한 모든 액세스 권한을 취소합니다. |

Admin Console을 통해 부여된 사용 가능한 권한(이러한 네 가지 소스 포함)에 대한 자세한 내용은 [액세스 제어 개요를 참조하십시오](../access-control/home.md).

## 약관 {#terms-and-conditions}

베타(&quot;베타&quot;)로 레이블이 지정된 소스를 사용함으로써, 귀하는 베타가 어떠한 형태의 보증도 없이 &quot;있는 그대로&quot; 제공된다는 ***점을 동의합니다***.

Adobe은 베타를 유지, 수정, 업데이트, 변경, 수정, 또는 기타 지원을 할 의무가 없습니다. 귀하는 이러한 베타 및/또는 관련 자료의 올바른 기능이나 성능에 어떠한 방법으로든 의존하지 않도록 주의하십시오. 베타는 Adobe의 기밀 정보로 간주됩니다.

귀하가 Adobe에 제공한 모든 &quot;피드백&quot;(베타 버전 사용 시 발생하는 문제나 결함을 포함하며 이에 국한되지 않는 베타 관련 정보, 제안, 개선 사항 및 권장 사항)은 이러한 피드백에 대한 모든 권한, 권한 및 관심을 포함하여 Adobe에 할당됩니다.

진행 중인 피드백을 제출하거나 지원 티켓을 만들어 제안을 공유하거나 버그를 보고하려면 기능을 개선하십시오.
