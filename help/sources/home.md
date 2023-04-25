---
keywords: Experience Platform;홈;인기 항목;소스 커넥터;소스 커넥터;소스;데이터 소스;데이터 소스;데이터 소스 연결
solution: Experience Platform
title: 소스 커넥터 개요
description: Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 2%

---

# 소스 커넥터 개요

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 저장소, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Flow Service] 는 플랫폼 내에서 다양한 서로 다른 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다. 이러한 소스 연결을 통해 타사 시스템을 인증하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform을 사용하면 서로 다른 소스에서 수집한 데이터에 중앙 집중화를 수행하여 얻은 통찰력을 사용하여 더 많은 작업을 수행할 수 있습니다.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 소스 유형

Experience Platform 소스는 다음 카테고리로 그룹화됩니다.

### Adobe 애플리케이션 {#adobe-applications}

Experience Platform을 사용하면 Adobe Analytics 및 Adobe Audience Manager을 포함한 다른 Adobe 애플리케이션에서 데이터를 수집할 수 있습니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Adobe Audience Manager 소스 개요](connectors/adobe-applications/audience-manager.md)
   - [UI에서 Adobe Audience Manager 소스 연결 만들기](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics 분류 데이터 소스 개요](connectors/adobe-applications/classifications.md)
   - [UI에서 Adobe Analytics 분류 데이터 소스 연결 만들기](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics 보고서 세트 데이터 소스 개요](connectors/adobe-applications/analytics.md)
   - [UI에서 Adobe Analytics 소스 연결 만들기](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services 소스 개요](connectors/adobe-applications/campaign.md)
   - [UI에서 Adobe Campaign Managed Cloud Services 소스 연결 만들기](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe 데이터 수집 소스 개요](connectors/adobe-applications/data-collection.md)
   - [UI에서 고객 속성 소스 연결 만들기](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 소스 개요](connectors/adobe-applications/marketo/marketo.md)
   - [만들기 [!DNL Marketo Engage] UI의 소스 연결](./tutorials/ui/create/adobe-applications/marketo.md)
   - [만들기 [!DNL Marketo Engage] 사용자 지정 활동 데이터를 위한 소스 연결 및 데이터 흐름](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
- [Adobe Workfront 소스 개요](connectors/adobe-applications/workfront.md)
   - [UI에서 Workfront 소스 연결 만들기](./tutorials/ui/create/adobe-applications/workfront.md)

### Advertising {#advertising}

Experience Platform은 타사 광고 시스템에서 데이터 섭취를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Google 광고](connectors/advertising/ads.md)

### Analytics {#analytics}

Experience Platform은 타사 분석 플랫폼에서 데이터를 수집하는 데 대한 지원을 제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md)

### 클라우드 스토리지 {#cloud-storage}

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 고유한 데이터를 플랫폼으로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 사용자 인터페이스를 사용하여 소스 워크플로우에 통합됩니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### 동의 및 기본 설정 {#consent}

Experience Platform은 타사 동의 및 환경 설정 관리 플랫폼에서 데이터를 수집하는 데 대한 지원을 제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### CRM(고객 관계 관리) {#customer-relationship-management}

CRM 시스템은 고객 관계를 구축하는 데 도움이 되는 데이터를 제공하므로 충성도를 만들고 고객 유지 수준을 향상시킬 수 있습니다. Experience Platform에서 CRM 데이터 섭취를 지원합니다 [!DNL Microsoft Dynamics 365] 및 [!DNL Salesforce]. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### 고객 성공 {#customer-success}

Experience Platform은 타사 고객 성공 애플리케이션에서 데이터를 수집하기 위한 지원을 제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md)
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### 데이터베이스 {#database}

Experience Platform은 타사 데이터베이스에서 데이터를 수집하기 위한 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md)

### eCommerce {#ecommerce}

Experience Platform은 타사 eCommerce 시스템에서 데이터를 수집하기 위한 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)
- [[!DNL Shopify Streaming]](connectors/ecommerce/shopify-streaming.md)

### 로컬 시스템 {#local-system}

Experience Platform은 로컬 시스템에서 데이터를 수집하기 위한 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [로컬 파일 업로드](connectors/local-system/local-file-upload.md)

### 마케팅 자동화 {#marketing-automation}

Experience Platform은 타사 마케팅 자동화 시스템에서 데이터 섭취를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md)
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md)
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### 결제 {#payments}

Experience Platform은 타사 결제 시스템에서 데이터 섭취를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### 스트리밍 {#streaming}

Experience Platform은 스트리밍 소스에서 데이터를 수집하도록 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL HTTP API]](connectors/streaming/http.md)

### 프로토콜 {#protocols}

Experience Platform은 타사 프로토콜 시스템에서 데이터 섭취를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## 데이터 수집의 소스에 대한 액세스 제어

데이터 수집 소스에 대한 권한은 Adobe Admin Console 내에서 관리할 수 있습니다. 를 통해 권한에 액세스할 수 있습니다 **[!UICONTROL 권한]** 특정 제품 프로필의 탭입니다. 에서 **[!UICONTROL 권한 편집]** 패널에서는 **[!UICONTROL 데이터 수집]** 메뉴 항목. 다음 **[!UICONTROL 소스 보기]** 권한 은 의 사용 가능한 소스에 대한 읽기 전용 액세스 권한을 부여합니다 **[!UICONTROL 카탈로그]** 의 탭 및 인증된 소스 **[!UICONTROL 찾아보기]** 탭, **[!UICONTROL 소스 관리]** 권한을 통해 소스를 읽고, 만들고, 편집하고, 비활성화할 수 있는 전체 액세스 권한을 부여합니다.

다음 표에서는 이러한 권한의 다양한 조합을 기반으로 UI가 어떻게 동작하는지에 대해 설명합니다.

| 권한 수준 | 설명 |
| ---- | ----|
| **[!UICONTROL 소스 보기]** 설정 | 카탈로그 탭의 각 소스 유형에 있는 소스와 찾아보기, 계정 및 데이터 흐름 탭의 소스에 대한 읽기 전용 액세스 권한을 부여합니다. |
| **[!UICONTROL 소스 관리]** 설정 | 에 포함된 함수 외에 **[!UICONTROL 소스 보기]**, 액세스 권한을 부여합니다 **[!UICONTROL 연결 소스]** 옵션 **[!UICONTROL 카탈로그]** 및 **[!UICONTROL 데이터 선택]** 옵션 **[!UICONTROL 찾아보기]**. **[!UICONTROL 소스 관리]** 을 활성화하거나 비활성화할 수도 있습니다 **[!UICONTROL 데이터 흐름]** 일정을 편집합니다. |
| **[!UICONTROL 소스 보기]** 해제 및 **[!UICONTROL 소스 관리]** 해제 | 소스에 대한 모든 액세스를 취소합니다. |

Adobe 권한을 통해 부여된 사용 가능한 권한에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md).

### 속성 기반 액세스 제어

관리자는 Adobe Experience Platform의 속성 기반 액세스 제어를 사용하여 속성을 기반으로 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있습니다.

속성 기반 액세스 제어를 사용하면 권한이 있는 필드에 매핑 구성을 적용할 수 있습니다. 또한 데이터 집합에 있는 모든 필드에 액세스할 수 없는 경우 데이터를 데이터 집합에 수집할 수 없습니다.

#### 소스에서 속성 기반 액세스 제어 지원

>[!TIP]
>
>속성 기반 액세스 제어는 다음과 같이 작동합니다. **역할** 는 Platform 인스턴스와 상호 작용하는 사용자 유형을 분류하기 위해 만들어집니다. **레이블** 에 적용됩니다. **역할** 지정된 역할의 액세스를 지정합니다. **레이블** 스키마 필드 및 세그먼트와 같은 리소스에도 적용됩니다. 사용자가 특정 스키마 필드 및 세그먼트에 액세스할 수 있으려면 다음을 추가해야 합니다 *쿼리된 리소스에 할당된 레이블이 동일한 역할*. 자세한 내용은 [특성 기반 액세스 제어 종단 안내서](../access-control/abac/end-to-end-guide.md).

- 스키마 필드에 레이블을 적용하여 조직의 특정 스키마 필드에 대한 액세스를 정의합니다. 특정 스키마 필드에 대한 액세스 권한이 설정되면 사용자는 액세스 권한이 있는 필드에 대한 매핑을 만들 수만 있습니다.
- 적절한 역할이 없는 사용자는 액세스할 수 없는 스키마 필드가 포함된 매핑으로 데이터 흐름을 만들거나 업데이트할 수 없습니다. 또한 권한이 없는 사용자는 액세스할 수 없는 스키마 필드를 사용하여 기존 데이터 흐름을 업데이트, 삭제, 활성화 또는 비활성화할 수 없습니다.
- 또한 데이터 흐름의 매핑, 대상 데이터 세트 및 타겟 연결에 동일한 스키마 ID와 버전이 있어야 합니다.

속성 기반 액세스 제어에 대한 자세한 내용은 [속성 기반 액세스 제어 개요](../access-control/abac/overview.md).

## 약관 {#terms-and-conditions}

베타(&quot;베타&quot;)로 레이블이 지정된 소스를 사용하면 귀하는 베타가 제공된다는 것을 확인합니다 ***&quot;있는 그대로&quot; 어떤 종류의 보증도 없이***.

Adobe은 베타를 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 따라서 이러한 베타 및/또는 추가 자료의 올바른 기능이나 성능에 의존하지 않도록 주의하십시오. 베타는 Adobe의 기밀 정보로 간주됩니다.

Adobe에 사용자가 제공하는 모든 &quot;피드백&quot;(베타, 제안, 개선 사항 및 권장 사항 중 발생하는 문제나 결함을 포함하되, 이에 제한되지 않음) Adobe은 해당 피드백과 관련된 모든 권한, 제목, 관심 사항을 포함하는에 할당됩니다.

Open Feedback을 제출하거나 Support Ticket을 만들어 제안을 공유하거나 버그를 보고하려면 기능 개선 사항을 찾으십시오.
