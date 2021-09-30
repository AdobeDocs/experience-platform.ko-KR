---
keywords: Experience Platform;홈;인기 항목;crm 스키마;crm;CRM;salesforce;Salesforce
solution: Experience Platform
title: Salesforce 소스 커넥터 개요
topic-legacy: overview
description: API 또는 사용자 인터페이스를 사용하여 Salesforce를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 759f38bac9b59fe32594dff771617ba8eaabae41
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# [!DNL Salesforce] 커넥터

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 CRM 시스템에서 데이터 섭취를 지원합니다. CRM 공급자에 대한 지원에는 [!DNL Salesforce]이 포함됩니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

<!--
## Field mapping from [!DNL Salesforce] to XDM

To establish a source connection between [!DNL Salesforce] and Platform, the [!DNL Salesforce] source data fields must be mapped to their appropriate target XDM fields prior to being ingested into Platform.

See the following for detailed information on the field mapping rules between [!DNL Salesforce] datasets and Platform:

- [Contacts](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Accounts](../adobe-applications/mapping/salesforce.md#account)
- [Opportunities](../adobe-applications/mapping/salesforce.md#opportunity)
- [Opportunity contact roles](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campaigns](../adobe-applications/mapping/salesforce.md#campaign)
- [Campaign members](../adobe-applications/mapping/salesforce.md#campaign-member)

## Set up the [!DNL Salesforce] namespace and schema auto-generation utility

To use the [!DNL Salesforce] source as part of [!DNL B2B-CDP], you must first set up a [!DNL Postman] utility to auto-generate your [!DNL Salesforce] namespaces and schemas. The following documentation provides additonal information on setting up the [!DNL Postman] utility:

- You can download the namespace and schema auto-generation utility collection and environment from this [GitHub repository](https://git.corp.adobe.com/marketo-engineering/namespace_schema_utility).
- For information on using Platform APIs including details on how to gather values for required headers and read sample API calls, see the guide on [getting started with Platform APIs](../../../landing/api-guide.md).
- For information on how to generate your credentials for Platform APIs, see the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md).
- For information on how to set up [!DNL Postman] for Platform APIs, see the tutorial on [setting up developer console and [!DNL Postman]](../../../landing/postman.md).

With a Platform developer console and [!DNL Postman] set up, you can now start applying the appropriate environment values to your [!DNL Postman] environment.

The following table contains example values as well as additional information on populating your [!DNL Postman] environment:

| Variable | Description | Example |
| --- | --- | --- |
| `CLIENT_SECRET` | A unique identifier used to generate your `{ACCESS_TOKEN}`. See the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md) for information on how to retrieve your `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | The JSON Web Token (JWT) is an authentication credential used to generate your {ACCESS_TOKEN}. See the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md) for information on how to generate your `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | A unique identifier used to authenticate calls to Experience Platform APIs. See the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md) for information on how to retrieve your `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | The authorization token required to complete calls to Experience Platform APIs. See the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md) for information on how to retrieve your `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | With regards to [!DNL Marketo], this value is fixed and is alway set to: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | The `global` container holds all standard Adobe and Experience Platform partner provided classes, schema field groups, data types, and schemas. With regards to [!DNL Marketo], this value is fixed and is always set to `global`. | `global` |
| `PRIVATE_KEY` | A credential used to authenticate your [!DNL Postman] instance to Experience Platform APIs. See the tutorial on setting up developer console and [setting up developer console and [!DNL Postman]](../../../landing/postman.md) for instructions on how to retrieve your {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | A credential used to integrate to Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | The Identity Management System (IMS) provides the framework for authentication to Adobe services. With regards to [!DNL Marketo], this value is fixed and is always set to: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | A corporate entity that can own or license products and services and allow access to its members. See the tutorial on [setting up developer console and [!DNL Postman]](../../../landing/postman.md) for instructions on how to retrieve your `{IMS_ORG}` information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | The name of the virtual sandbox partition that you are using. | `prod` |
| `TENANT_ID` | An ID used to ensure that the resources you create are namespaced properly and are contained within your IMS Organization. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | The URL endpoint that you are making API calls to. This value is fixed and is always set to: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | The unique ID for your [!DNL Marketo] account. See the tutorial on [authenticating your [!DNL Marketo] instance](../adobe-applications/marketo/marketo-auth.md) for information on how to retrieve your `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | The organization ID for your [!DNL Salesforce] account. See the following [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&type=1&mode=1) for more information on acquiring your [!DNL Salesforce] organization ID. | `00D4W000000FgYJUA0` |
`f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | A boolean value that indicates if you are subscribed to [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | A boolean value that indicates if you are subcscribed to [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Running the scripts

With your [!DNL Postman] collection and environment set up, you can now run the script through the [!DNL Postman] interface.

In the [!DNL Postman] interface, select the root folder of the auto-generator utility and then select **[!DNL Run]** from the top header.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

The [!DNL Runner] interface appears. From here, ensure that all the checkboxes are selected and then select **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

A successful request creates the B2B namespaces and schemas according to beta specifications.

-->

## API를 사용하여 [!DNL Salesforce] 을 플랫폼에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Salesforce]을 Platform에 연결하는 방법에 대한 정보를 제공합니다.

- [Flow Service API를 사용하여 Salesforce 기본 연결 만들기](../../tutorials/api/create/crm/salesforce.md)
- [Flow Service API를 사용하여 CRM 소스의 데이터 구조 및 컨텐츠를 탐색합니다](../../tutorials/api/explore/crm.md)
- [Flow Service API를 사용하여 CRM 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/crm.md)

## UI를 사용하여 [!DNL Salesforce] 을 플랫폼에 연결

- [UI에서 Salesforce 소스 연결 만들기](../../tutorials/ui/create/crm/salesforce.md)
- [UI에서 CRM 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
