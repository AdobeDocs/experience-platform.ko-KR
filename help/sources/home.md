---
keywords: Experience Platform;홈;인기 항목;소스 커넥터;소스 커넥터;소스;데이터 소스;데이터 소스;데이터 소스 연결
solution: Experience Platform
title: 소스 커넥터 개요
topic-legacy: overview
description: Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 8236fb3a5786a6990fe85482c2fee0eda48bcf1f
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# 소스 커넥터 개요

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Flow Service] 는 플랫폼 내에서 다양한 서로 다른 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다. 이러한 소스 연결을 통해 타사 시스템을 인증하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform을 사용하면 서로 다른 소스에서 수집한 데이터에 중앙 집중화를 수행하여 얻은 통찰력을 사용하여 더 많은 작업을 수행할 수 있습니다.

## 소스 유형

Experience Platform 소스는 다음 카테고리로 그룹화됩니다.

### Adobe 애플리케이션

Experience Platform을 사용하면 Adobe Analytics, Adobe Audience Manager 및 [!DNL Experience Platform Launch] 등 다른 Adobe 애플리케이션에서 데이터를 수집할 수 있습니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Adobe Audience Manager 커넥터 개요](connectors/adobe-applications/audience-manager.md)
- [UI에서 Adobe Audience Manager 소스 연결 만들기](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics 분류 데이터 소스 연결 개요](connectors/adobe-applications/classifications.md)
- [UI에서 Adobe Analytics 분류 데이터 소스 연결 만들기](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics 보고서 세트 데이터 소스 연결 개요](connectors/adobe-applications/analytics.md)
- [UI에서 Adobe Analytics 소스 연결 만들기](./tutorials/ui/create/adobe-applications/analytics.md)
- [UI에서 고객 속성 소스 연결 만들기](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 커넥터 개요](connectors/adobe-applications/marketo/marketo.md)
- [UI에서 [!DNL Marketo Engage] 소스 연결 만들기](./tutorials/ui/create/adobe-applications/marketo.md)

### 광고

Experience Platform은 타사 광고 시스템에서 데이터 섭취를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Google AdWords]](connectors/advertising/ads.md) 커넥터

### 클라우드 스토리지

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 고유한 데이터를 플랫폼으로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 사용자 인터페이스를 사용하여 소스 워크플로우에 통합됩니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Azure Data Lake Storage Gen2] 커넥터](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] 커넥터](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] 커넥터](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] 커넥터](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] 커넥터](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] 커넥터](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] 커넥터](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] 커넥터](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] 커넥터](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] 커넥터](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] 커넥터](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] 커넥터](connectors/cloud-storage/sftp.md)

### CRM(고객 관계 관리)

CRM 시스템은 고객 관계를 구축하는 데 도움이 되는 데이터를 제공하므로 충성도를 만들고 고객 유지 수준을 향상시킬 수 있습니다. Experience Platform은 [!DNL Microsoft Dynamics 365] 및 [!DNL Salesforce]에서 CRM 데이터 섭취를 지원합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Microsoft Dynamics] 커넥터](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] 커넥터](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)

### 고객 성공

Experience Platform은 타사 고객 성공 애플리케이션에서 데이터를 수집하기 위한 지원을 제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Salesforce Service Cloud] 커넥터](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] 커넥터](connectors/customer-success/servicenow.md)

### 데이터베이스

Experience Platform은 타사 데이터베이스에서 데이터를 수집하기 위한 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

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
- [[!DNL MariaDB] 커넥터](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server] 커넥터](connectors/databases/sql-server.md)
- [[!DNL MySQL] 커넥터](connectors/databases/mysql.md)
- [[!DNL Oracle] 커넥터](connectors/databases/oracle.md)
- [[!DNL Phoenix] 커넥터](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] 커넥터](connectors/databases/postgres.md)

### eCommerce

Experience Platform은 타사 eCommerce 시스템에서 데이터를 수집하기 위한 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 마케팅 자동화

Experience Platform은 타사 마케팅 자동화 시스템에서 데이터 섭취를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL HubSpot] 커넥터](connectors/marketing-automation/hubspot.md)

### 결제

Experience Platform은 타사 결제 시스템에서 데이터 섭취를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL PayPal] 커넥터](connectors/payments/paypal.md)

### 스트리밍

Experience Platform은 스트리밍 소스에서 데이터를 수집하도록 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL HTTP API]](connectors/streaming/http.md)


### 프로토콜

Experience Platform은 타사 프로토콜 시스템에서 데이터 섭취를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Generic OData] 커넥터](connectors/protocols/odata.md)

## 데이터 수집의 소스에 대한 액세스 제어

데이터 수집 소스에 대한 권한은 Adobe Admin Console 내에서 관리할 수 있습니다. 특정 제품 프로필의 **[!UICONTROL 권한]** 탭을 통해 권한에 액세스할 수 있습니다. **[!UICONTROL 권한 편집]** 패널에서 **[!UICONTROL 데이터 수집]** 메뉴 항목을 통해 소스와 관련된 권한에 액세스할 수 있습니다. **[!UICONTROL 소스 보기]** 권한은 **[!UICONTROL 카탈로그]** 탭과 **[!UICONTROL 찾아보기]** 탭의 인증된 소스에 대한 읽기 전용 액세스 권한을 부여하는 반면, **[!UICONTROL 소스 관리]** 권한은 소스를 읽고, 만들고, 편집하고, 비활성화할 수 있는 전체 액세스 권한을 부여합니다.

다음 표에서는 이러한 권한의 다양한 조합을 기반으로 UI가 어떻게 동작하는지에 대해 설명합니다.

| 권한 수준 | 설명 |
| ---- | ----|
| **[!UICONTROL 소스]** 보기 | 카탈로그 탭의 각 소스 유형에 있는 소스와 찾아보기, 계정 및 데이터 흐름 탭의 소스에 대한 읽기 전용 액세스 권한을 부여합니다. |
| **[!UICONTROL 소스]** 관리 | **[!UICONTROL 소스 보기]**&#x200B;에 포함된 함수 외에, **[!UICONTROL 카탈로그]**&#x200B;의 **[!UICONTROL 소스 연결]** 옵션과 **[!UICONTROL 찾아보기]**&#x200B;에서 **[!UICONTROL 데이터 선택]** 옵션에 대한 액세스 권한을 부여합니다. **[!UICONTROL 소스]** 관리를 사용하면 DataFlow를 활성화하거나 비활성화하고 해당 일정 **** 을 편집할 수도 있습니다. |
| **[!UICONTROL 소스]** 보기 및  **[!UICONTROL 소스]** 관리 해제 | 소스에 대한 모든 액세스를 취소합니다. |

이러한 네 개의 소스를 포함하여 Admin Console을 통해 부여된 사용 가능한 권한에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하십시오.

## 약관 {#terms-and-conditions}

베타(&quot;베타&quot;)로 레이블이 지정된 소스를 사용하면, 귀하는 베타가 어떠한 종류의&#x200B;***보증도 없이***&quot;as&quot;(있는 그대로) 제공된다는 것을 인정합니다.

Adobe은 베타를 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 따라서 이러한 베타 및/또는 추가 자료의 올바른 기능이나 성능에 의존하지 않도록 주의하십시오. 베타는 Adobe의 기밀 정보로 간주됩니다.

Adobe에 사용자가 제공하는 모든 &quot;피드백&quot;(베타, 제안, 개선 사항 및 권장 사항 중 발생하는 문제나 결함을 포함하되, 이에 제한되지 않음) Adobe은 해당 피드백과 관련된 모든 권한, 제목, 관심 사항을 포함하는에 할당됩니다.

Open Feedback을 제출하거나 Support Ticket을 만들어 제안을 공유하거나 버그를 보고하려면 기능 개선 사항을 찾으십시오.
