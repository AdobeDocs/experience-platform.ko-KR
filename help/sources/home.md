---
keywords: Experience Platform;홈;인기 항목;소스 커넥터;소스 커넥터;소스;데이터 소스;데이터 소스;데이터 소스 연결
solution: Experience Platform
title: Source 커넥터 개요
description: Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 952fc2fac819c545304aca4505208fe59841097f
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 8%

---

# Source 커넥터 개요

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 저장소, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Flow Service]은(는) Experience Platform 내의 다양한 개별 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 소스 연결을 통해 서드파티 시스템을 인증하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform을 사용하면 다양한 소스에서 수집한 데이터를 중앙에서 관리하고 여기에서 얻은 통찰력을 사용하여 더 많은 작업을 수행할 수 있습니다.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

>[!BEGINSHADEBOX]

## Adobe이 빌드하고 파트너가 빌드한 소스 {#adobe-and-partner-built-sources}

Experience Platform 소스 카탈로그의 일부 커넥터는 Adobe에서 빌드하고 유지 관리하는 반면, 다른 커넥터는 [소스 SDK](/help/sources/sources-sdk/overview.md)를 사용하여 파트너 회사에서 빌드하고 유지 관리합니다. 파트너가 소스를 만들고 유지 관리하는 경우 파트너가 빌드한 각 커넥터에 대한 설명서 페이지 맨 위의 메모가 호출됩니다. 예를 들어 [Amazon S3 커넥터](/help/sources/connectors/cloud-storage/s3.md)는 Adobe에서 만들고 [RainFocus 커넥터](/help/sources/connectors/analytics/rainfocus.md)는 RainFocus 팀에서 만들고 유지 관리합니다.

파트너가 작성 및 유지 관리하는 커넥터의 경우 파트너 팀이 커넥터 문제를 해결해야 할 수 있습니다(설명서 페이지의 메모에 제공된 연락 방법). Adobe 작성 및 유지 관리 커넥터와 관련된 문제는 Adobe 담당자 또는 고객 지원 센터에 문의하십시오.

>[!ENDSHADEBOX]

## 소스 카탈로그

소스 카탈로그에서 사용할 수 있는 모든 소스 목록은 다음 섹션을 참조하십시오.

### Adobe 애플리케이션 {#adobe-applications}

Experience Platform을 사용하면 Adobe Analytics 및 Adobe Audience Manager을 포함한 다른 Adobe 애플리케이션에서 데이터를 수집할 수 있습니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [UI에서 Adobe Audience Manager 소스 연결 만들기](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics 분류 데이터](connectors/adobe-applications/classifications.md)
   - [UI에서 Adobe Analytics 분류 데이터 소스 연결 만들기](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics 보고서 세트 데이터](connectors/adobe-applications/analytics.md)
   - [UI에서 Adobe Analytics 소스 연결 만들기](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [UI에서 Adobe Campaign Managed Cloud Services 소스 연결 만들기](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Adobe 데이터 수집](connectors/adobe-applications/data-collection.md)
   - [UI에서 고객 속성 소스 연결 만들기](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [UI에서  [!DNL Marketo Engage] 소스 연결 만들기](./tutorials/ui/create/adobe-applications/marketo.md)
   - [사용자 지정 활동 데이터에 대한  [!DNL Marketo Engage] 소스 연결 및 데이터 흐름 만들기](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### 고급 엔터프라이즈 소스 {#advanced-enterprise-sources}

다음 소스는 [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) 고객만 사용할 수 있습니다.

| 소스 | 카테고리 | 수집 유형 | 클라우드 |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | 클라우드 스토리지 | 스트리밍 | Azure, AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | 데이터베이스 | 배치 | Azure, AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | 데이터베이스 | 배치 | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | 클라우드 스토리지 | 스트리밍 | Azure, AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | 데이터베이스 | 배치 | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | 데이터베이스 | 배치 | Azure |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | 클라우드 스토리지 | 스트리밍 | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | 데이터베이스 | 스트리밍 | Azure, AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | 데이터베이스 | 배치 | Azure, AWS |

{style="table-layout:auto"}

### Advertising {#advertising}

다음 소스를 사용하여 광고 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [Google 광고](connectors/advertising/ads.md) | 배치 | Azure |

{style="table-layout:auto"}

### Analytics {#analytics}

다음 소스를 사용하여 분석 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | 배치 | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | 스트리밍 | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | 스트리밍 | Azure |

{style="table-layout:auto"}

### 클라우드 스토리지 {#cloud-storage}

클라우드 스토리지 소스는 다운로드, 포맷 또는 업로드 없이도 자신의 데이터를 Experience Platform으로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 사용자 인터페이스를 사용하여 소스 워크플로우에 통합됩니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

다음 소스를 사용하여 클라우드 스토리지 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | 배치 | Azure |
| [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) | 배치 | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | 배치 | Azure, AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | 배치 | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | 배치 | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | 배치 | Azure, AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | 배치 | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | 배치 | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | 배치 | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | 배치 | Azure |

{style="table-layout:auto"}

### 동의 및 환경 설정 {#consent}

다음 소스를 사용하여 Experience Platform에 동의 및 환경 설정 데이터를 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | 배치 | Azure |

{style="table-layout:auto"}

### CRM(고객 관계 관리) {#customer-relationship-management}

CRM 시스템은 고객 관계를 구축하고 충성도를 창출하며 고객 유지를 촉진하는 데 도움이 되는 데이터를 제공합니다. Experience Platform에서는 [!DNL Microsoft Dynamics 365] 및 [!DNL Salesforce]에서 CRM 데이터를 수집할 수 있습니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

다음 소스를 사용하여 CRM 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | 배치 | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | 배치 | Azure, AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | 배치 | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | 배치 | Azure |

{style="table-layout:auto"}

### 고객 성공 {#customer-success}

다음 소스를 사용하여 고객 성공 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | 배치 | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | 배치 | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | 배치 | Azure |

{style="table-layout:auto"}

### 데이터베이스 {#database}

Experience Platform은 타사 데이터베이스에서 데이터를 수집하는 기능을 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

다음 소스를 사용하여 데이터베이스의 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | 배치 | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | 배치 | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | 배치 | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | 배치 | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | 배치 | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | 배치 | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | 배치 | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | 배치 | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | 배치 | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | 배치 | Azure, AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | 배치 | Azure |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | 배치 | Azure, AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | 배치 | Azure |

{style="table-layout:auto"}

### 데이터 및 ID 파트너 {#data-partner}

다음 소스를 사용하여 데이터 및 ID 파트너 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | 배치 | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | 배치 | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | 배치 | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | 배치 | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | 배치 | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | 배치 | Azure |

{style="table-layout:auto"}

### 전자 상거래 {#ecommerce}

다음 소스를 사용하여 전자 상거래 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | 배치 | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | 배치 | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | 스트리밍 | Azure |

{style="table-layout:auto"}

### 로컬 시스템 {#local-system}

다음 소스를 사용하여 로컬 시스템에서 Experience Platform으로 데이터를 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [로컬 파일 업로드](connectors/local-system/local-file-upload.md) | 배치 | Azure |

{style="table-layout:auto"}

### 마케팅 자동화 {#marketing-automation}

다음 소스를 사용하여 마케팅 자동화 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | 스트리밍 | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | 스트리밍 | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | 스트리밍 | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | 배치 | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | 배치 | Azure |
| [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) | 배치 | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | 배치 | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | 배치 | Azure |
| [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) | 배치 | Azure, AWS |

{style="table-layout:auto"}

### 결제 {#payments}

다음 소스를 사용하여 결제 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | 배치 | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | 배치 | Azure |

{style="table-layout:auto"}

### 스트리밍 {#streaming}

다음 소스를 사용하여 데이터를 Experience Platform으로 스트리밍할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 지원 |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | 스트리밍 | Azure, AWS |

{style="table-layout:auto"}

### 프로토콜 {#protocols}

다음 소스를 사용하여 프로토콜 데이터를 Experience Platform으로 수집할 수 있습니다.

| 소스 | 수집 유형 | 클라우드 지원 |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | 배치 | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | 배치 | Azure |

{style="table-layout:auto"}

## 데이터 수집에서 소스에 대한 액세스 제어

데이터 수집의 소스에 대한 권한은 Adobe Admin Console 내에서 관리할 수 있습니다. 특정 제품 프로필의 **[!UICONTROL 권한]** 탭을 통해 권한에 액세스할 수 있습니다. **[!UICONTROL 권한 편집]** 패널에서 **[!UICONTROL 데이터 수집]** 메뉴 항목을 통해 소스와 관련된 권한에 액세스할 수 있습니다. **[!UICONTROL 소스 보기]** 권한은 **[!UICONTROL 카탈로그]** 탭의 사용 가능한 소스와 **[!UICONTROL 찾아보기]** 탭의 인증된 소스에 대한 읽기 전용 액세스 권한을 부여하고 **[!UICONTROL 소스 관리]** 권한은 소스를 읽기, 만들기, 편집 및 비활성화할 수 있는 전체 액세스 권한을 부여합니다.

다음 표에서는 이러한 권한의 다양한 조합을 기반으로 UI가 작동하는 방식을 설명합니다.

| 권한 수준 | 설명 |
| ---- | ----|
| 다음에서 **[!UICONTROL 소스 보기]**: | [카탈로그] 탭과 [찾아보기], [계정] 및 [데이터 흐름] 탭에서 각 소스 유형의 소스에 대한 읽기 전용 액세스 권한을 부여합니다. |
| 다음에서 **[!UICONTROL 소스 관리]**: | **[!UICONTROL 소스 보기]**&#x200B;에 포함된 함수 외에 **[!UICONTROL 카탈로그]**&#x200B;의 **[!UICONTROL Source 연결]** 옵션 및 **[!UICONTROL 찾아보기]**&#x200B;의 **[!UICONTROL 데이터 선택]** 옵션에 대한 액세스 권한을 부여합니다. **[!UICONTROL 소스 관리]**&#x200B;를 통해 **[!UICONTROL DataFlows]**&#x200B;을(를) 활성화 또는 비활성화하고 일정을 편집할 수도 있습니다. |
| **[!UICONTROL 소스 보기]** 해제 및 **[!UICONTROL 소스 관리]** 해제 | 소스에 대한 모든 액세스를 취소합니다. |

Adobe 권한을 통해 부여된 사용 가능한 권한에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하십시오.

### 속성 기반 액세스 제어

Adobe Experience Platform의 속성 기반 액세스 제어를 통해 관리자는 속성에 따라 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있습니다.

속성 기반 액세스 제어를 사용하면 권한이 있는 필드에 매핑 구성을 적용할 수 있습니다. 또한 데이터 세트의 모든 필드에 대한 액세스 권한이 없는 경우에는 데이터 세트에 데이터를 수집할 수 없습니다.

#### 소스에서의 속성 기반 액세스 제어 지원

>[!TIP]
>
>특성 기반 액세스 제어는 다음과 같이 작동합니다. **역할**&#x200B;은(는) Experience Platform 인스턴스와 상호 작용하는 사용자 유형을 분류하도록 만들어집니다. 지정된 역할에 대한 액세스를 지정하기 위해 **레이블**&#x200B;이(가) **역할**&#x200B;에 적용됩니다. **레이블**&#x200B;은(는) 스키마 필드 및 세그먼트와 같은 리소스에도 적용됩니다. 사용자가 특정 스키마 필드 및 세그먼트에 액세스하려면 *쿼리된 리소스에 할당된 레이블과 동일한 역할을 가진 역할*&#x200B;에 추가되어야 합니다. 자세한 내용은 [특성 기반 액세스 제어 전체 가이드](../access-control/abac/end-to-end-guide.md)를 참조하십시오.

- 조직의 특정 스키마 필드에 대한 액세스를 정의하기 위해 스키마 필드에 레이블을 적용합니다. 특정 스키마 필드에 대한 액세스가 설정되면 사용자는 액세스 권한이 있는 필드에 대한 매핑만 만들 수 있습니다.
- 적절한 역할이 없는 사용자는 액세스할 수 없는 스키마 필드가 포함된 매핑으로 데이터 흐름을 만들거나 업데이트할 수 없습니다. 또한 권한이 없는 사용자는 액세스할 수 없는 스키마 필드로 기존 데이터 흐름을 업데이트, 삭제, 활성화 또는 비활성화할 수 없습니다.
- 또한 데이터 흐름의 매핑, 대상 데이터 세트 및 대상 연결에서 스키마 ID와 버전이 정확히 동일해야 합니다.

특성 기반 액세스 제어에 대한 자세한 내용은 [특성 기반 액세스 제어 개요](../access-control/abac/overview.md)를 참조하십시오.

## 사용 약관 {#terms-and-conditions}

Beta(&quot;Beta&quot;)로 레이블이 지정된 소스를 사용함으로써 귀하는 Beta이 어떠한 종류의 보증도 없이 ***&quot;있는 그대로&quot; 제공된다는 것을 인정합니다***.

Adobe은 Beta을 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 이러한 Beta 및/또는 동봉된 자료의 올바른 기능이나 성능에 어떤 식으로든 의존하지 말고 정보 자료를 사용하는 것이 좋습니다. Beta은 Adobe의 기밀 정보로 간주됩니다.

귀하가 Adobe에 제공한 &quot;피드백&quot;(Beta 사용 중 발생하는 문제 또는 결함, 제안, 개선 사항 및 권장 사항을 포함하되 이에 제한되지 않는 Beta 관련 정보)은 해당 피드백에 대한 모든 권한, 제목 및 관심을 포함하여 Adobe에 할당됩니다.

진행 중 피드백을 제출하거나 지원 티켓을 만들어 제안을 공유하거나 버그를 보고하면 기능 개선 사항을 확인할 수 있습니다.
