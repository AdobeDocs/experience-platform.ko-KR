---
keywords: Experience Platform;홈;인기 항목;소스 커넥터;소스 커넥터;소스;데이터 소스;데이터 소스;데이터 소스;데이터 소스 연결
solution: Experience Platform
title: 소스 커넥터 개요
topic-legacy: overview
description: Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
translation-type: tm+mt
source-git-commit: 8edcb3697337edd0043f26553b92c31e52d3c87c
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# 소스 커넥터 개요

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반의 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Flow Service] 는 Platform(플랫폼) 내의 다양한 소스에서 나온 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 소스 연결을 통해 타사 시스템을 인증하고, 통합 실행에 대한 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform을 사용하면 서로 다른 소스에서 수집한 데이터를 중앙에서 관리하고, 얻은 인사이트를 활용하여 더 많은 작업을 수행할 수 있습니다.

## 소스 유형

Experience Platform의 소스는 다음 카테고리로 그룹화됩니다.

### Adobe 애플리케이션

Experience Platform을 사용하면 Adobe Analytics, Adobe Audience Manager 및 [!DNL Experience Platform Launch] 등 다른 Adobe 애플리케이션에서 데이터를 수집할 수 있습니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [Adobe Audience Manager 커넥터 개요](connectors/adobe-applications/audience-manager.md)
- [UI에서 Adobe Audience Manager 소스 연결 만들기](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics 분류 데이터 커넥터 개요](connectors/adobe-applications/classifications.md)
- [UI에서 Adobe Analytics 분류 데이터 소스 연결 만들기](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics 데이터 커넥터 개요](connectors/adobe-applications/analytics.md)
- [UI에서 Adobe Analytics 소스 연결 만들기](./tutorials/ui/create/adobe-applications/analytics.md)
- [UI에서 고객 속성 소스 연결 만들기](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 커넥터 개요](connectors/adobe-applications/marketo/marketo.md)
- [UI [!DNL Marketo Engage] 에서 리소스 연결 만들기](./tutorials/ui/create/adobe-applications/marketo.md)

### 광고

Experience Platform은 제3자 광고 시스템의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Google AdWords]](connectors/advertising/ads.md) 커넥터

### 클라우드 스토리지

클라우드 스토리지 소스는 다운로드, 포맷 또는 업로드 없이도 직접 데이터를 플랫폼에 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공 마루 또는 구분된 형태로 포맷될 수 있습니다. 프로세스의 모든 단계는 사용자 인터페이스를 사용하여 소스 워크플로우에 통합됩니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

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

### 고객 관계 관리(CRM)

CRM 시스템은 고객 관계를 구축하는 데 도움이 되는 데이터를 제공하므로, 이를 통해 충성도를 생성하고 고객 유지율을 향상시킬 수 있습니다. Experience Platform은 [!DNL Microsoft Dynamics 365] 및 [!DNL Salesforce]의 CRM 데이터 인제스트를 지원합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Microsoft Dynamics] 커넥터](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] 커넥터](connectors/crm/salesforce.md)

### 고객 성공 사례

Experience Platform은 제3자 고객 성공 애플리케이션에서 데이터를 인제스트할 수 있도록 지원합니다. 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Salesforce Service Cloud] 커넥터](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] 커넥터](connectors/customer-success/servicenow.md)

### 데이터베이스

Experience Platform은 제3자 데이터베이스의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

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

Experience Platform은 제3자 eCommerce 시스템의 데이터 인제스트를 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 마케팅 자동화

Experience Platform은 제3자 마케팅 자동화 시스템에서 데이터를 인제스트할 수 있도록 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL HubSpot] 커넥터](connectors/marketing-automation/hubspot.md)

### 결제

Experience Platform은 제3자 결제 시스템에서 데이터를 인제스트할 수 있도록 지원합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL PayPal] 커넥터](connectors/payments/paypal.md)

### 스트리밍

Experience Platform은 스트리밍 소스의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL HTTP API]](connectors/streaming/http.md)


### 프로토콜

Experience Platform은 제3자 프로토콜 시스템의 데이터 인제스트 지원을 제공합니다. 특정 소스 커넥터에 대한 자세한 내용은 다음 관련 문서를 참조하십시오.

- [[!DNL Generic OData] 커넥터](connectors/protocols/odata.md)

## 데이터 수집에서 소스에 대한 액세스 제어

데이터 수집의 소스에 대한 권한은 Adobe Admin Console 내에서 관리할 수 있습니다. 특정 제품 프로필의 **[!UICONTROL Permissions]** 탭을 통해 권한을 액세스할 수 있습니다. **[!UICONTROL Edit Permissions]** 패널에서 **[!UICONTROL data ingestion]** 메뉴 항목을 통해 소스와 관련된 권한에 액세스할 수 있습니다. **[!UICONTROL View Sources]** 권한은 **[!UICONTROL Catalog]** 탭의 사용 가능한 소스와 **[!UICONTROL Browse]** 탭의 인증된 소스에 대한 읽기 전용 액세스 권한을 부여하는 반면 **[!UICONTROL Manage Sources]** 권한은 소스를 읽고, 만들고, 편집하고, 비활성화하기 위한 모든 액세스 권한을 부여합니다.

다음 표에서는 이러한 권한의 다양한 조합을 기반으로 UI가 어떻게 동작하는지를 설명합니다.

| 권한 수준 | 설명 |
| ---- | ----|
| **[!UICONTROL View Sources]** 설정 | [카탈로그] 탭에서 각 소스 유형의 소스에 대한 읽기 전용 액세스 권한과 [탐색], [계정] 및 [데이터 흐름] 탭을 부여할 수 있습니다. |
| **[!UICONTROL Manage Sources]** 설정 | **[!UICONTROL View Sources]**&#x200B;에 포함된 함수 외에도 **[!UICONTROL Catalog]**&#x200B;의 **[!UICONTROL Connect Source]** 옵션과 **[!UICONTROL Browse]**&#x200B;의 **[!UICONTROL Select Data]** 옵션에 대한 액세스 권한을 부여합니다. **[!UICONTROL Manage Sources]** 일정을 활성화 또는 비활성화하고  **[!UICONTROL DataFlows]** 편집할 수도 있습니다. |
| **[!UICONTROL View Sources]** 해제 및  **[!UICONTROL Manage Sources]** 해제 | 소스에 대한 모든 액세스 권한을 취소합니다. |

이러한 4개의 소스를 포함하여 Admin Console을 통해 부여된 사용 가능한 권한에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하십시오.

## 약관 {#terms-and-conditions}

베타(&quot;베타&quot;)로 레이블이 지정된 소스를 사용함으로써, 귀하는 베타가 어떠한 종류의&#x200B;***보증도 없이***&quot;as&quot;로 제공됨을 인정합니다.

Adobe은 베타를 유지, 수정, 업데이트, 변경, 수정 또는 기타 지원할 의무가 없습니다. 귀하는 이러한 베타 및/또는 관련 자료의 올바른 기능 또는 성능에 어떠한 방법으로든 의존하지 않도록 주의해서 주의해야 합니다. 베타는 Adobe의 기밀 정보로 간주됩니다.

귀하가 Adobe에 제공한 모든 &quot;피드백&quot;(베타 버전 사용 시 발생하는 문제나 결함을 포함하나 이에 한정되지 않는 베타 관련 정보), 제안, 개선 사항 및 권장 사항은 해당 피드백에 대한 모든 권리, 권한 및 이해관계를 포함하는 Adobe에 지정됩니다.

진행 중인 피드백을 제출하거나 지원 티켓을 만들어 제안을 공유하거나 버그를 보고하려면 기능 개선을 요청하십시오.
