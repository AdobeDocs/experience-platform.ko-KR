---
title: 데이터 Distiller 개요
description: 라이선스 권한과 관련된 Query Service 데이터에 대한 Data Distiller 사용 제한 요약입니다.
source-git-commit: e4337dcebaf313365ed9e403a5891f49decb29e9
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---

# Data Distiller 개요

Data Distiller 는 Adobe Experience Platform의 기능 하위 집합을 포함하는 패키지 서비스입니다. Data Cloud를 사용하면 Query Service에서 배치 쿼리를 실행하여 실시간 고객 프로필 또는 분석 사용 사례에 대한 사후 수집 데이터 준비(예: 청소, 쉐이핑 및 조작)를 수행할 수 있습니다. 데이터 Distiller의 사용은 플랫폼 기반 애플리케이션에 대한 사용 권한에 따라 다릅니다.

## 라이선스 사용 {#license-usage}

<!-- Commented out references to licence usage dashboard. It is temporarily hidden:
The [Data Distiller license usage dashboard](./license-usage.md) is available once you have purchased Data Distiller compute hours. The license usage dashboard helps you to monitor the consumption of entitled compute hours. See the [Data Distiller license usage document](./license-usage.md) to view important information about your organization's Query Service license usage. 
-->

Data Distiller 계산 시간을 구입한 후에는 Data Analytics 라이선스 사용 대시보드를 사용할 수 있습니다. 라이선스 사용 대시보드는 권한이 있는 컴퓨팅 시간의 소비를 모니터링하는 데 도움이 됩니다.

<!-- Update these descriptions post 23.3 release
## Scoping parameters {#scoping-parameters}

Scoping parameters are usage limits that relate to the scoping of your required set up, and are defined by your license capacity. Without add-ons, Data Distiller's scoping parameters are as follows: 

* **Compute Hours**: You can use PSQL or the Query Service API to run batch queries executed in any sandbox (scheduled or otherwise) to scan and write data. This uses your allotted Compute Hours per year as determined in the scoping process of your license agreement. Total Compute Hours is accumulated across all Sandboxes.
* **Data Ingested**: The data ingested into Adobe Experience Platform which can be queried using Data Distiller is subject to the limitations described in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer.
* **Data Lake Storage**: The data lake storage provided in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Data Lake Storage is a shared feature.
* **Query Service Users**: The number of Query Service users detailed in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Query Service Users is a shared feature. 
-->

## 가드레일

자세한 내용은 [쿼리 서비스 보호 기능](../guardrails.md) 라이선스 권한과 관련하여 Query Service 데이터의 기본 사용 제한에 대한 문서가 제공됩니다.

<!-- Update these descriptions post 23.3 release
## Static limits

A static limit is the usage limit that relates to the functional boundaries of Adobe Experience Platform Activation. [More information on Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) can be found in the Adobe help documents. A summary of Data Distiller static limits are listed below, for more complete information please refer to the Query Service guardrail document.  

* **Batch Queries**: Scheduled batch queries time out after 24 hours.
* **Query Service**: You can use Query Service for the following purposes: 
    * To run SQL queries for data analysis and post ingestion data preparation (cleaning, shaping, and manipulation).
    * To run SQL queries to create roll-up metrics to surface directly into a BI tool.
    * To quickly inspect data within Adobe Experience Platform.
    * To generate meaningful insights from your data.
* **Reporting API Call**: To ensure queries run on aggregated data using the reporting API have enough resources to execute efficiently. This includes queries that enhance existing data models such as those provided by Real-Time Customer Data Platform. The reporting API tracks resource utilization by assigning concurrency slots to each query. A maximum of four reporting API calls are available concurrently. If you access the reporting API through a BI tool and require more concurrency slots, a BI server is required.
-->

