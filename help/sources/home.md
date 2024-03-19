---
keywords: Experience Platform;홈;인기 항목;소스 커넥터;소스 커넥터;소스;데이터 소스;데이터 소스;데이터 소스 연결
solution: Experience Platform
title: 소스 커넥터 개요
description: Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: f8df3ddb96ad0810a7a46b0a55125336c427aebd
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 1%

---

# 소스 커넥터 개요

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 저장소, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Flow Service] 는 플랫폼 내의 다양한 개별 소스에서 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 소스 연결을 통해 서드파티 시스템을 인증하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform을 사용하면 다양한 소스에서 수집한 데이터를 중앙에서 관리하고 여기에서 얻은 통찰력을 사용하여 더 많은 작업을 수행할 수 있습니다.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Adobe이 빌드한 소스 및 파트너가 빌드한 소스 {#adobe-and-partner-built-sources}

Experience Platform 소스 카탈로그의 일부 커넥터는 Adobe에서 빌드하고 유지 관리하는 반면, 다른 커넥터는 를 사용하여 파트너 회사에서 빌드하고 유지 관리합니다 [소스 SDK](/help/sources/sources-sdk/overview.md). 파트너가 소스를 만들고 유지 관리하는 경우 파트너가 빌드한 각 커넥터에 대한 설명서 페이지 맨 위의 메모가 호출됩니다. 예를 들어 [Amazon S3 커넥터](/help/sources/connectors/cloud-storage/s3.md) 은 Adobe에 의해 만들어지지만 [RainFocus 커넥터](/help/sources/connectors/analytics/rainfocus.md) 는 RainFocus 팀에서 만들고 유지 관리합니다.

파트너가 작성 및 유지 관리하는 커넥터의 경우 파트너 팀이 커넥터 문제를 해결해야 할 수 있습니다(설명서 페이지의 메모에 제공된 연락 방법). Adobe 작성 및 유지 관리되는 커넥터와 관련된 문제는 Adobe 담당자 또는 고객 지원 센터에 문의하십시오.

## 소스 유형

Experience Platform의 소스는 다음 카테고리로 그룹화됩니다.

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
- [Adobe Commerce 소스 개요](connectors/adobe-applications/commerce.md)
- [Adobe 데이터 수집 소스 개요](connectors/adobe-applications/data-collection.md)
   - [UI에서 고객 속성 소스 연결 만들기](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 소스 개요](connectors/adobe-applications/marketo/marketo.md)
   - [만들기 [!DNL Marketo Engage] UI의 소스 연결](./tutorials/ui/create/adobe-applications/marketo.md)
   - [만들기 [!DNL Marketo Engage] 사용자 지정 활동 데이터에 대한 소스 연결 및 데이터 흐름](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

Experience Platform은 서드파티 광고 시스템에서 데이터를 수집하는 기능을 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Google 광고](connectors/advertising/ads.md) [!BADGE 일괄 처리]{type=Informative}

### Analytics {#analytics}

Experience Platform은 서드파티 분석 플랫폼에서 데이터를 수집하는 기능을 지원합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE 스트리밍]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE 스트리밍]{type=Positive}

### 클라우드 스토리지 {#cloud-storage}

클라우드 스토리지 소스는 다운로드, 포맷 또는 업로드 없이도 고유한 데이터를 플랫폼으로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 사용자 인터페이스를 사용하여 소스 워크플로우에 통합됩니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE 스트리밍]{type=Positive}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE 스트리밍]{type=Positive}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE 스트리밍]{type=Positive}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE 일괄 처리]{type=Informative}

### 동의 및 환경 설정 {#consent}

Experience Platform은 서드파티 동의 및 환경 설정 관리 플랫폼에서 데이터를 수집하는 기능을 지원합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE 일괄 처리]{type=Informative}

### CRM(고객 관계 관리) {#customer-relationship-management}

CRM 시스템은 고객 관계를 구축하고 충성도를 창출하며 고객 유지를 촉진하는 데 도움이 되는 데이터를 제공합니다. Experience Platform은 CRM 데이터 수집을 지원합니다. [!DNL Microsoft Dynamics 365] 및 [!DNL Salesforce]. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE 일괄 처리]{type=Informative}

### 고객 성공 {#customer-success}

Experience Platform은 서드파티 고객 성공 애플리케이션에서 데이터를 수집하는 데 대한 지원을 제공합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE 일괄 처리]{type=Informative}

### 데이터베이스 {#database}

Experience Platform은 타사 데이터베이스에서 데이터를 수집하는 기능을 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE 스트리밍]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE 일괄 처리]{type=Informative}

### 데이터 및 ID 파트너 {#data-partner}

Experience Platform은 타사 데이터베이스에서 데이터를 수집하는 기능을 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE 일괄 처리]{type=Informative}

### eCommerce {#ecommerce}

Experience Platform은 서드파티 전자 상거래 시스템에서 데이터를 수집하는 기능을 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE 스트리밍]{type=Positive}

### 로컬 시스템 {#local-system}

Experience Platform은 로컬 시스템에서 데이터를 수집할 수 있도록 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [로컬 파일 업로드](connectors/local-system/local-file-upload.md)

### 마케팅 자동화 {#marketing-automation}

Experience Platform은 서드파티 마케팅 자동화 시스템에서 데이터를 수집하는 기능을 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Braze]](connectors/marketing-automation/braze.md) [!BADGE 스트리밍]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE 스트리밍]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE 스트리밍]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE 일괄 처리]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### 결제 {#payments}

Experience Platform은 서드파티 결제 시스템에서 데이터를 수집할 수 있도록 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Stripe]](connectors/payments/stripe.md) [!BADGE 일괄 처리]{type=Informative}

### 스트리밍 {#streaming}

Experience Platform은 스트리밍 소스에서 데이터 수집을 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE 스트리밍]{type=Positive}

### 프로토콜 {#protocols}

Experience Platform은 타사 프로토콜 시스템에서 데이터를 수집하는 기능을 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE 일괄 처리]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE 일괄 처리]{type=Informative}

## 데이터 수집에서 소스에 대한 액세스 제어

데이터 수집의 소스에 대한 권한은 Adobe Admin Console 내에서 관리할 수 있습니다. 다음을 통해 권한에 액세스할 수 있습니다. **[!UICONTROL 권한]** 특정 제품 프로필의 탭 다음에서 **[!UICONTROL 권한 편집]** 패널 을 통해 소스와 관련된 권한에 액세스할 수 있습니다. **[!UICONTROL 데이터 수집]** 메뉴 항목. 다음 **[!UICONTROL 소스 보기]** 권한은에서 사용 가능한 소스에 대한 읽기 전용 액세스 권한을 부여합니다. **[!UICONTROL 카탈로그]** 의 탭 및 인증된 소스 **[!UICONTROL 찾아보기]** 탭, **[!UICONTROL 소스 관리]** 권한은 소스를 읽기, 만들기, 편집 및 비활성화할 수 있는 전체 액세스 권한을 부여합니다.

다음 표에서는 이러한 권한의 다양한 조합을 기반으로 UI가 작동하는 방식을 설명합니다.

| 권한 수준 | 설명 |
| ---- | ----|
| **[!UICONTROL 소스 보기]** 날짜 | [카탈로그] 탭과 [찾아보기], [계정] 및 [데이터 흐름] 탭에서 각 소스 유형의 소스에 대한 읽기 전용 액세스 권한을 부여합니다. |
| **[!UICONTROL 소스 관리]** 날짜 | 에 포함된 함수 외에 **[!UICONTROL 소스 보기]**, 다음에 대한 액세스 권한 부여: **[!UICONTROL 소스 연결]** 의 옵션 **[!UICONTROL 카탈로그]** 및 종료 **[!UICONTROL 데이터 선택]** 의 옵션 **[!UICONTROL 찾아보기]**. **[!UICONTROL 소스 관리]** 또한 을(를) 활성화 또는 비활성화할 수 있습니다 **[!UICONTROL 데이터 흐름]** 일정을 편집할 수 있습니다. |
| **[!UICONTROL 소스 보기]** 끔 및 **[!UICONTROL 소스 관리]** 끔 | 소스에 대한 모든 액세스를 취소합니다. |

Adobe 권한을 통해 부여된 사용 가능한 권한에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md).

### 속성 기반 액세스 제어

Adobe Experience Platform의 속성 기반 액세스 제어를 통해 관리자는 속성에 따라 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있습니다.

속성 기반 액세스 제어를 사용하면 권한이 있는 필드에 매핑 구성을 적용할 수 있습니다. 또한 데이터 세트의 모든 필드에 대한 액세스 권한이 없는 경우에는 데이터 세트에 데이터를 수집할 수 없습니다.

#### 소스에서 속성 기반 액세스 제어 지원

>[!TIP]
>
>속성 기반 액세스 제어는 다음과 같이 작동합니다. **역할** 는 Platform 인스턴스와 상호 작용하는 사용자 유형을 분류하기 위해 만들어집니다. **레이블** 적용 대상 **역할** 해당 역할의 액세스 권한을 지정합니다. **레이블** 스키마 필드 및 세그먼트와 같은 리소스에도 적용됩니다. 사용자가 특정 스키마 필드 및 세그먼트에 액세스하려면 를 추가해야 합니다. *쿼리된 리소스에 할당된 레이블과 동일한 역할*. 자세한 내용은 [속성 기반 액세스 제어 엔드투엔드 안내서](../access-control/abac/end-to-end-guide.md).

- 조직의 특정 스키마 필드에 대한 액세스를 정의하기 위해 스키마 필드에 레이블을 적용합니다. 특정 스키마 필드에 대한 액세스가 설정되면 사용자는 액세스 권한이 있는 필드에 대한 매핑만 만들 수 있습니다.
- 적절한 역할이 없는 사용자는 액세스할 수 없는 스키마 필드가 포함된 매핑으로 데이터 흐름을 만들거나 업데이트할 수 없습니다. 또한 권한이 없는 사용자는 액세스할 수 없는 스키마 필드로 기존 데이터 흐름을 업데이트, 삭제, 활성화 또는 비활성화할 수 없습니다.
- 또한 데이터 흐름의 매핑, 대상 데이터 세트 및 대상 연결에서 스키마 ID와 버전이 정확히 동일해야 합니다.

속성 기반 액세스 제어에 대한 자세한 내용은 [속성 기반 액세스 제어 개요](../access-control/abac/overview.md).

## 사용 약관 {#terms-and-conditions}

베타(&quot;베타&quot;)로 레이블이 지정된 소스를 사용함으로써 귀하는 베타가 제공되었음을 인정합니다 ***어떠한 종류의 보증도 없이 &quot;있는 그대로&quot;***.

Adobe은 Beta 를 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 귀하는 Informatic을 사용하고 이러한 베타 및/또는 동봉된 자료의 올바른 기능이나 성능에 어떠한 의존도 하지 않는 것이 좋습니다. 베타 버전은 Adobe의 기밀 정보로 간주됩니다.

귀하가 Adobe에 제공한 &quot;피드백&quot;(베타 사용 중 발생하는 문제나 결함, 제안, 개선 사항 및 권장 사항을 포함하지만 이에 국한되지 않는 베타 관련 정보)은 이에 따라 해당 피드백에 대한 모든 권한, 제목 및 관심을 포함하는 Adobe에 할당됩니다.

진행 중 피드백을 제출하거나 지원 티켓을 만들어 제안을 공유하거나 버그를 보고하면 기능 개선 사항을 확인할 수 있습니다.
