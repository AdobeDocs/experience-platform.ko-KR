---
title: Data Governance in Query Service
description: This overview covers the major elements of data governance in Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: c98ae492b12fb5b9596f19a3d64785090439f7e1
workflow-type: tm+mt
source-wordcount: '3182'
ht-degree: 0%

---

# Data governance in Query Service

Adobe Experience Platform brings data from multiple enterprise systems together and allows you to clean, shape, manipulate and enrich the data through Query Service according to your needs. This allows marketers to identify, understand, and engage customers in a better way. Ensuring adequate data governance is a critical aspect of handling personal information as certain data may be subject to usage restrictions based on organizational policies and legal regulations. It is critical to ensure that your ingested data and its related operations are compliant with the defined data usage policies.

Data governance within Query Service allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. This plays a key role when ensuring the usage policies have been applied according to the regulations defined by your business.

Organizations that routinely conduct data processing are recommended to outline, practice, and enforce these guidelines to create a privacy-conscious environment for all users.

The following categories are instrumental in adhering to data compliance regulations when using Query Service:

1. 보안
1. 감사
1. Data usage
1. 개인 정보 보호
1. Data hygiene

This document examines each of the different areas of governance and demonstrates how to facilitate data compliance when using Query Service. See the [governance, privacy, and security overview](../../landing/governance-privacy-security/overview.md) for broader information on how Experience Platform allows you to manage customer data and ensure compliance.

## 보안 {#security}

Data security is the process of protecting data from unauthorized access and ensuring secure access throughout its lifecycle. Secure access is maintained in Experience Platform through the application of roles and permissions by capabilities such as role-based access control and attribute-based access control. Credentials, SSL, and data encryption are also used to ensure data protection across Experience Platform.

Security in regard to Query Service is divided into the following categories:

* [Access control](#access-control): Access is controlled through roles and permissions including dataset and column-level permissions.
* Securing data through [connectivity](#connectivity): Data is secured through Experience Platform and external clients by achieving a limited connection with expiring credentials, or non-expiring credentials.
* Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest.

### 액세스 제어 {#access-control}

Access control in Adobe Experience Platform is managed by role-based permissions that determine which users can use Query Service features. Similarly, you can control access to specific data attributes through label management on schemas and data fields.

This section outlines the required access control permissions that a user must have in order to fully utilize Query Service features. See the documents on [managing permissions](../../access-control/ui/permissions.md) and [managing users](../../access-control/ui/users.md) for detailed instructions on assigning access to a product profile.

#### Relevant permissions

The relevant access control permissions are defined in the tables below according to their level of scope.

**Query execution permissions**

To run queries within Query Service, a user must be assigned a role with the following permission:

| 사용 권한 | 설명 |
|---|---|
| [!UICONTROL Manage Queries] | This permission allows users to execute data exploration and batch queries, which can either read an existing dataset or write data on datasets. This includes both `CREATE TABLE AS SELECT` (`CTAS`) and `INSERT INTO AS SELECT` (`ITAS`) queries. |

**Dataset permissions**

This section serves as a guide for the resource-based access required to access datasets while querying data through Query Service.

Through the Permissions interface you can define resource-based access control for a dataset and schema with the following permissions:

| 사용 권한 | 설명 |
|---|---|
| [!UICONTROL Manage Datasets] | This permission provides read-only access for schemas and allows access to read, create, edit, and delete datasets for use with Query Service. |
| [!UICONTROL View Datasets] | This permission allows read-only access for datasets and schemas for use with Query Service. |

#### Access control for columns/fields

The attribute-based access control feature enables Query Service users to restrict access to critical user data. Access can be granted or restricted based on the permissions assigned to a role. User access to individual columns is controlled by the relevant data usage labels and the permission sets applied to the roles assigned to users.

Tagging schema field groups and classes with data usage labels applies data usage restrictions to all schemas with the same field groups and classes. See the overview on [attribute-based access control](../../access-control/abac/overview.md) for comprehensive information on this feature.

This feature enables you to grant access rights on confidential columns to the user groups of your choice. Access control on a column can restrict both the read and write capabilities for a particular type of user.

Access control for columns can be applied at the schema level for both standard and ad hoc schemas. Apply data usage labels to XDM schemas to restrict access to one or more columns. Data labeling is consistently applied, even for datasets created via Query Service using either a predefined schema or an ad hoc schema generated as part of CTAS operation.

Once the appropriate level of access has been applied using labels and roles, the following system behavior occurs when a user tries to access the non-accessible data:

1. If a user has been denied access to one of the columns within a schema, the user is also denied permission to read or write on the restricted column. This applies to the following common scenarios:

   * **Case 1**: When a user tries to execute a query affecting only a restricted column, the system throws an error that the column doesn&#39;t exist.
   * **Case 2**: When a user tries to execute a query with multiple columns including a restricted column, the system returns output for all non-restricted columns only.

1. If a user tries to access a calculated field, the user is required to have access to all the fields used in the composition or the system denies access to the calculated field as well.

#### Access controls for views

Query Service provides the ability to use standard ANSI SQL for [`CREATE VIEW`](../sql/syntax.md#create-view) statements. For highly sensitive data workflows, you must enforce appropriate controls when creating views.

The `CREATE VIEW` keyword defines a view of a query but the view is not physically materialized. Instead, the query is run every time the view is referenced in a query. When a user creates a view from a dataset, the role- and attribute-based access control rules for the parent dataset are **not** hierarchically applied. As a result, you must explicitly set permissions on each of the columns when a view is created.

#### Create field-based access restrictions on accelerated datasets {#create-field-based-access-restrictions-on-accelerated-datasets}

With the [attribute-based access control capability](../../access-control/abac/overview.md) you can define organizational or data usage scopes on fact and dimension datasets in the [accelerated store](../data-distiller/sql-insights/send-accelerated-queries.md). This allows administrators to manage access to specific segments and better manage the access given to users or groups of users.

To create field-based access restrictions on accelerated datasets, you can use Query Service CTAS queries to create accelerated datasets and structure these datasets based on existing XDM schemas or ad hoc schemas. Administrators can then [add and edit data usage labels for the schema](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) or [ad hoc schema](./ad-hoc-schema-labels.md#edit-governance-labels). You can apply, create, and edit labels to your schemas from the [!UICONTROL Labels] workspace in the [!UICONTROL Schemas] UI.

Data usage labels can also be [applied or edited directly onto the dataset](../../data-governance/labels/user-guide.md#add-labels) through the Datasets UI, or created from the Access Control [!UICONTROL Labels] workspace. See the guide on how to [create a new label](../../access-control/abac/ui/labels.md) for more information.

User access to individual columns can then be controlled by the attached data usage labels and the permission sets applied to the roles that are assigned to users.

### Connectivity {#connectivity}

Query Service is accessible through the Experience Platform UI or by forming a connection with external compatible clients. Access to all available fronts is controlled by a set of credentials.

#### Connectivity through external clients

서드파티 클라이언트를 사용하여 쿼리 서비스에 액세스하려면 인증을 위한 자격 증명이 필요합니다. 이러한 자격 증명은 호환되는 외부 클라이언트에서 Query Service에 액세스하는 데 필요합니다. [만료되는 자격 증명](#expiring-credentials) 또는 [만료되지 않는 자격 증명](#non-expiring-credentials)을 사용하여 외부 클라이언트에 연결할 수 있습니다.

#### 만료 자격 증명을 통한 제한된 연결 시간 {#expiring-credentials}

[자격 증명 만료](../ui/credentials.md)을(를) 통해 사용자는 외부 클라이언트와 임시 연결을 구성할 수 있습니다. 이 자격 증명 집합은 24시간 동안만 유효합니다. 이러한 유형의 자격 증명 만료는 쿼리 서비스 대시보드의 자격 증명 탭과 함께 볼 수 있습니다.

![만료 자격 증명이 강조 표시된 쿼리 서비스 작업 영역의 자격 증명 탭입니다.](../images/data-governance/overview/expiring-credentials.png)

#### 만료되지 않는 자격 증명 {#non-expiring-credentials}

[만료되지 않는 자격 증명](../ui/credentials.md#non-expiring-credentials)을 사용하면 외부 클라이언트와 영구적으로 연결할 수 있으므로 수동 암호를 사용하지 않고도 Query Service에 쉽게 연결할 수 있습니다.

만료되지 않는 자격 증명을 생성하는 옵션을 활성화하려면 요약된 [필수 워크플로](../ui/credentials.md#prerequisites)를 따라야 합니다. 이 프로세스의 일부로, 조직 관리자가 제품 프로필에 대한 권한을 구성해야 하며, 관리자가 만료되지 않는 자격 증명을 사용할 수 있는 액세스 권한을 보유할 수 있습니다.

만료되지 않는 자격 증명으로 허용된 기술 사용자 계정에는 역할로 할당하여 책임 및 요구 사항에 따라 읽기 및 쓰기 액세스 범위를 정의하여 적절한 데이터 거버넌스를 보장할 수 있습니다. 쿼리 서비스에 대한 액세스를 관리하려면 [액세스 제어를 통해 역할 기반 권한 사용](#access-control)에 대한 이전 섹션을 참조하십시오.

필수 구성 요소 워크플로가 완료되면 이제 권한이 있는 사용자가 [필요한 연결 자격 증명을 생성](../ui/credentials.md#generate-credentials)할 수 있습니다.

#### SSL 데이터 암호화

보안 강화를 위해 Query Service는 클라이언트/서버 통신을 암호화하기 위한 SSL 연결을 기본적으로 지원합니다. Experience Platform은 데이터 보안 요구 사항에 맞게 다양한 SSL 옵션을 지원하고 암호화 및 키 교환의 처리 오버헤드를 조정합니다.

`verify-full` SSL 매개 변수 값을 사용하여 연결하는 방법 등 자세한 내용은 쿼리 서비스에 대한 타사 클라이언트 연결에 사용할 수 있는 [SSL 옵션에 대한 가이드](../clients/ssl-modes.md)를 참조하십시오.

### 암호화 및 CMK(고객 관리 키) {#encryption-and-customer-managed-keys}

암호화는 데이터를 암호화하고 읽을 수 없는 텍스트로 변환하는 알고리즘 프로세스를 사용하여 암호 해독 키 없이 정보를 보호하고 액세스할 수 없도록 합니다.

Query Service 데이터 규정 준수는 데이터가 항상 암호화되도록 합니다. 전송 중인 데이터는 항상 HTTPS를 준수하며, 사용하지 않는 데이터는 시스템 수준 키를 사용하여 Azure Data Lake 저장소에서 암호화됩니다. 자세한 내용은 [Adobe Experience Platform에서 데이터를 암호화하는 방법](../../landing/governance-privacy-security/encryption.md)에 대한 설명서를 참조하십시오. 사용하지 않는 데이터를 Azure Data Lake Storage에서 암호화하는 방법에 대한 자세한 내용은 [공식 Azure 설명서](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)를 참조하십시오.

전송 중인 데이터는 항상 HTTPS를 준수하며 데이터가 데이터 레이크에 있는 경우에도 마찬가지로 암호화는 데이터 레이크 관리에서 이미 지원하는 CMK(고객 관리 키)로 수행됩니다. The currently supported version is TLS1.2. See the [customer-managed keys (CMK) documentation](../../landing/governance-privacy-security/customer-managed-keys/overview.md) to learn how to set up your own encryption keys for data stored in Adobe Experience Platform.


## 감사 {#audit}

Query Service records user activity and categorizes that activity in different log types. Logs supply information on **who** performed **what** action, and **when**. Each action recorded in a log contains metadata that indicates the action type, date and time, the email ID of the user who performed the action, and additional attributes relevant to the action type.

Any of the log categories can be requested as desired by an Experience Platform user. This section provides details on the type of information captured for Query Service and where this information can be accessed.

### Query logs {#query-logs}

The query logs UI allows you to monitor and review execution details for all queries that have been run either via the Query Editor or the Query Service API. This brings transparency to Query Service activities, allowing you to check the metadata for **all** the queries that have been executed across Query Service. It includes all types of queries whether it is an exploratory, batch, or scheduled query.

Query logs can be accessed either through the Experience Platform UI in the [!UICONTROL Logs] tab of the [!UICONTROL Queries] workspace.

![The Queries log tab with the details panel highlighted.](../images/data-governance/overview/queries-log.png)

### 감사 로그 {#audit-logs}

Audit logs contain more detailed information than query logs and enable you to filter logs based on attributes such as user, date, type of query, and so on. Beyond the details available in query log UI, Audit Logs stores details on individual users along with their session data or connectivity to a third-party client.

By providing an exact record of user actions, an audit trail can help with troubleshooting issues and help your business effectively comply with corporate data stewardship policies and regulatory requirements. Audit logs provide a record of all Experience Platform activities. Using audit logs you can audit user actions relating to query execution, templates, and scheduled queries to increase the transparency and visibility of actions performed by users in Query Service.

The following table indicates the query categories captured by audit logs and the action types they record:

| 카테고리 | 액션 유형 |
|---|---|
| 쿼리 | 실행 |
| 쿼리 템플릿 | Create, Delete, Update |
| 예약된 쿼리 | Create, Delete, Update |

Below is a list of three extended server logs that hold more details than those found within the query logs. The extended logs are found within the audit logs query categories:

1. **Meta query logs**: When a query is executed, various associated backend sub-queries (such as parsing) are executed. These types of queries are known as &quot;metadata&quot; queries. 감사 로그에서 관련 세부 정보를 확인할 수 있습니다.
1. **세션 로그**: 사용자가 쿼리를 실행하는지 여부에 관계없이 Query Service에 로그인할 때 시스템에 사용자의 세션 항목 로그가 만들어집니다.
1. **타사 클라이언트 연결 로그**: 사용자가 쿼리 서비스를 타사 클라이언트에 연결하면 연결 감사 로그가 생성됩니다.

감사 로그를 통해 조직의 데이터 규정 준수에 어떻게 도움이 되는지에 대한 자세한 내용은 [감사 로그 개요](../../landing/governance-privacy-security/audit-logs/overview.md)를 참조하십시오.

## 데이터 사용 {#data-usage}

Experience Platform의 데이터 거버넌스 프레임워크는 모든 Adobe 솔루션, 서비스 및 플랫폼에서 데이터를 책임감 있게 사용할 수 있는 균일한 방법을 제공합니다. Adobe Experience Cloud 전체에서 메타데이터를 캡처, 통신 및 사용하는 시스템 접근 방식을 조정합니다. 이렇게 하면 데이터 제어자가 필요한 마케팅 작업과 이러한 의도된 마케팅 작업에서 해당 데이터에 지정된 제한 사항에 따라 데이터에 레이블을 지정하는 데 도움이 됩니다. 데이터 거버넌스에서 데이터 세트 및 필드에 데이터 사용 레이블을 적용하는 방법에 대한 자세한 내용은 [데이터 사용 레이블](../../data-governance/labels/overview.md)에 대한 개요를 참조하십시오.

데이터 여정의 모든 단계에서 데이터 규정 준수를 위해 작업하는 것이 가장 좋습니다. 이를 위해 임시 스키마를 사용하는 파생된 데이터 세트는 데이터 거버넌스 프레임워크의 일부로 적절하게 레이블이 지정되어야 합니다. Query Service에서 형성되는 파생 데이터 세트에는 표준 스키마를 사용하는 데이터 세트와 애드혹 스키마를 사용하는 데이터 세트, 이렇게 두 가지 유형이 있습니다.

>[!NOTE]
>
>쿼리 서비스를 사용하여 만든 데이터 세트를 &quot;파생 데이터 세트&quot;라고 합니다.

애드혹 스키마는 특정 목적을 위해 개별 사용자에 의해 생성되므로 XDM 스키마 필드는 해당 특정 데이터 세트에 대해 네임스페이스가 지정되며 다른 데이터 세트에서 사용하기 위한 것이 아닙니다. 따라서 임시 스키마는 기본적으로 Experience Platform UI에 표시되지 않습니다. 표준 스키마와 애드혹 스키마 간에 데이터 사용 레이블 적용에 차이가 없지만 레이블 지정을 위해 쿼리 서비스에서 만든 애드혹 스키마는 먼저 Experience Platform UI에 표시되어야 합니다. 자세한 내용은 [Experience Platform UI 내에서 임시 스키마 찾기](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas)에 대한 안내서를 참조하십시오.

스키마에 액세스한 후에는 [개별 필드에 레이블을 적용](../../xdm/tutorials/labels.md)할 수 있습니다. 스키마에 레이블이 지정되면 해당 스키마에서 파생된 모든 데이터 세트는 해당 레이블을 상속합니다. 여기에서 특정 레이블이 있는 데이터의 활성화를 특정 대상으로 제한할 수 있는 데이터 사용 정책을 설정할 수 있습니다. 자세한 내용은 [데이터 사용 정책](../../data-governance/policies/overview.md)에 대한 개요를 참조하십시오.

## 개인 정보 보호 {#privacy}

[Privacy Service](../../privacy-service/home.md)을(를) 사용하면 법적 개인 정보 보호 규정에 따라 고객의 데이터 액세스 및 삭제 요청을 관리할 수 있습니다. 이렇게 하려면 데이터에 기존 식별자를 검색하고 요청된 개인 정보 작업에 따라 해당 데이터에 액세스하거나 삭제합니다. 서비스에서 개인 정보 보호 작업 중에 액세스하거나 삭제할 필드를 결정하려면 데이터에 올바른 레이블을 지정해야 합니다. 개인 정보 보호 요청의 대상이 되는 데이터는 다양한 데이터를 개인 정보 보호 요청이 적용되는 개별 사용자와 연결하기 위해 고객 ID 정보를 포함해야 합니다. Query Service는 개인 정보 보호 작업을 충족하기 위해 고유 식별자로 사용하는 데이터를 보강할 수 있습니다.

개인 정보 보호 요청은 데이터 레이크 또는 프로필 데이터 저장소로 전송될 수 있습니다. 데이터 레이크에서 삭제된 레코드는 해당 레코드에서 만든 프로필을 삭제하지 않습니다. 또한 데이터 레이크에서 개인 정보를 삭제하는 개인 정보 작업은 프로필을 삭제하지 않으므로 개인 정보 작업 완료 후 수집된 정보(해당 프로필 ID가 포함)는 해당 프로필을 정상적으로 업데이트합니다. 이렇게 하면 임시 스키마에 사용되는 데이터를 제대로 식별해야 하는 필요성이 재확인됩니다.

[개인 정보 보호 요청에 대한 ID 데이터](../../privacy-service/identity-data.md)에 대한 자세한 내용 및 데이터 작업을 구성하고 Adobe 기술을 활용하여 고객 개인 정보 보호 요청에 대한 적절한 ID 정보를 효과적으로 검색하는 방법에 대한 자세한 내용은 Privacy Service 설명서를 참조하십시오.

데이터 거버넌스를 위한 쿼리 서비스 기능은 데이터 분류 프로세스 및 데이터 사용 규정 준수를 간소화하고 간소화합니다. 데이터가 식별되면 쿼리 서비스를 사용하여 모든 출력 데이터 세트에 기본 ID를 할당할 수 있습니다. 데이터 개인 정보 보호 요청을 용이하게 하고 데이터 규정 준수 작업을 위해 **데이터 집합에 ID를**&#x200B;추가해야 합니다.

Experience Platform UI를 통해 스키마 데이터 필드를 ID 필드로 설정할 수 있으며 쿼리 서비스를 통해 SQL 명령 &#39;ALTER TABLE&#39;[&#128279;](../sql/syntax.md#alter-table)을(를) 사용하여 기본 ID를 표시할 수도 있습니다. `ALTER TABLE` 명령을 사용하여 ID를 설정하는 것은 Experience Platform UI를 통해 스키마에서 직접 가져오는 대신 SQL을 사용하여 데이터 세트를 만들 때 특히 유용합니다. 표준 스키마를 사용할 때 [UI에서 ID 필드를 정의](../../xdm/ui/fields/identity.md)하는 방법에 대한 지침은 설명서를 참조하세요.

## 데이터 위생 {#data-hygiene}

&quot;데이터 위생&quot;이란 오래된 데이터, 부정확한 데이터, 잘못된 포맷, 중복 데이터 또는 불완전한 데이터를 복구하거나 제거하는 프로세스를 말합니다. 이러한 프로세스를 통해 모든 시스템에서 데이터 세트가 정확하고 일관되도록 할 수 있습니다. 데이터 여정의 모든 단계와 심지어 초기 데이터 저장소 위치에서 적절한 데이터 위생을 보장하는 것이 중요합니다. Experience Platform 쿼리 서비스에서 이는 데이터 레이크 또는 가속 스토어입니다.

Experience Platform의 중앙 집중식 데이터 위생 서비스에 따라 데이터 관리를 허용하도록 파생된 데이터 세트에 ID를 할당할 수 있습니다.

반대로 가속화된 스토어에서 집계된 데이터 세트를 만들면 집계된 데이터를 원본 데이터를 파생시키는 데 사용할 수 없습니다. 이러한 데이터 집계로 인해 데이터 위생 요청을 제기할 필요성이 없어졌습니다.

이 시나리오의 예외는 삭제의 경우입니다. 데이터 세트에서 데이터 위생 삭제가 요청되고 삭제가 완료되기 전에 다른 파생된 데이터 세트 쿼리가 실행되는 경우 파생된 데이터 세트는 원래 데이터 세트의 정보를 캡처합니다. 이 경우 데이터 세트 삭제 요청이 전송된 경우 동일한 데이터 세트 소스를 사용하여 새로 파생된 데이터 세트 쿼리를 실행해서는 안 된다는 점을 염두에 두어야 합니다.

Adobe Experience Platform의 데이터 위생에 대한 자세한 내용은 [데이터 위생 개요](../../hygiene/home.md)를 참조하세요.
