---
keywords: Experience Platform;홈;인기 항목;Marketo 소스 커넥터;네임스페이스;스키마
solution: Experience Platform
title: Marketo 네임스페이스
topic-legacy: overview
description: 이 문서에서는 Marketo Engage 소스 커넥터를 만들 때 필요한 사용자 정의 네임스페이스에 대한 개요를 제공합니다.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: af728fb508c514db3d5871114f9a406c1ed428f2
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 5%

---

# (베타) [!DNL Marketo Engage] 네임스페이스 및 스키마

>[!IMPORTANT]
>
>[!DNL Marketo Engage] 소스는 현재 베타 상태입니다. 기능 및 설명서는 변경될 수 있습니다.

이 문서에서는 [!DNL Marketo Engage](이하 &quot;[!DNL Marketo]&quot;이라 함)에 사용되는 B2B 네임스페이스 및 스키마(이하 &quot;기본 설정&quot;이라 함)에 대한 정보를 제공합니다. 또한 이 문서에서는 [!DNL Marketo] B2B 네임스페이스 및 스키마를 생성하는 데 필요한 Postman 자동화 유틸리티 설정에 대한 세부 정보를 제공합니다.

## [!DNL Marketo] 네임스페이스 및 스키마 자동 생성 유틸리티를 설정합니다.

[!DNL Marketo] 네임스페이스 및 스키마 자동 생성 유틸리티 사용의 첫 번째 단계는 플랫폼 개발자 콘솔 및 [!DNL Postman] 환경을 설정하는 것입니다.

- 이 [GitHub 리포지토리](https://git.corp.adobe.com/marketo-engineering/namespace_schema_utility)에서 네임스페이스 및 스키마 자동 생성 유틸리티 컬렉션 및 환경을 다운로드할 수 있습니다.
- 필수 헤더에 대한 값을 모으고 샘플 API 호출을 읽는 방법에 대한 자세한 내용을 포함한 플랫폼 API 사용에 대한 자세한 내용은 [플랫폼 API 시작](../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.
- 플랫폼 API에 대한 자격 증명을 생성하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오.
- 플랫폼 API에 대해 [!DNL Postman]을 설정하는 방법에 대한 자세한 내용은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../../landing/postman.md)에 있는 자습서를 참조하십시오.

이제 플랫폼 개발자 콘솔과 [!DNL Postman] 설정을 통해 [!DNL Postman] 환경에 적절한 환경 값을 적용할 수 있습니다.

다음 표에는 [!DNL Postman] 환경 채우기에 대한 추가 정보와 예제 값이 포함되어 있습니다.

| 변수 | 설명 | 예 |
| --- | --- | --- |
| `CLIENT_SECRET` | `{ACCESS_TOKEN}`을(를) 생성하는 데 사용되는 고유 식별자입니다. `{CLIENT_SECRET}`의 검색 방법에 대한 자세한 내용은 [Experience Platform API](../../../../landing/api-authentication.md)를 인증하고 액세스하는 방법에 대한 자습서를 참조하십시오. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JWT(JSON 웹 토큰)는 {ACCESS_TOKEN}을 생성하는 데 사용되는 인증 자격 증명입니다. `{JWT_TOKEN}`을(를) 생성하는 방법에 대한 자세한 내용은 [Experience Platform API](../../../../landing/api-authentication.md)를 인증하고 액세스하는 방법에 대한 자습서를 참조하십시오. | `{JWT_TOKEN}` |
| `API_KEY` | Experience Platform API에 대한 호출을 인증하는 데 사용되는 고유 식별자입니다. `{API_KEY}`의 검색 방법에 대한 자세한 내용은 [Experience Platform API](../../../../landing/api-authentication.md)를 인증하고 액세스하는 방법에 대한 자습서를 참조하십시오. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Experience Platform API 호출을 완료하는 데 필요한 인증 토큰입니다. `{ACCESS_TOKEN}`의 검색 방법에 대한 자세한 내용은 [Experience Platform API](../../../../landing/api-authentication.md)를 인증하고 액세스하는 방법에 대한 자습서를 참조하십시오. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | [!DNL Marketo]과 관련하여 이 값은 고정되고 항상 다음으로 설정됩니다.`ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | `global` 컨테이너는 제공된 클래스, 스키마 필드 그룹, 데이터 유형 및 스키마를 모두 포함한 모든 표준 Adobe 및 Experience Platform 파트너를 보유합니다. [!DNL Marketo]과 관련하여 이 값은 고정되고 항상 `global`로 설정됩니다. | `global` |
| `PRIVATE_KEY` | Experience Platform API에 대해 [!DNL Postman] 인스턴스를 인증하는 데 사용되는 자격 증명입니다. {PRIVATE_KEY}를 검색하는 방법에 대한 자세한 내용은 개발자 콘솔 설정에 대한 자습서 및 [개발자 콘솔 설정 및 [!DNL Postman]](../../../../landing/postman.md)을 참조하십시오. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Adobe I/O에 통합하는 데 사용되는 자격 증명입니다. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | IMS(Identity Management System)는 Adobe 서비스에 대한 인증을 위한 프레임워크를 제공합니다. [!DNL Marketo]과 관련하여 이 값은 고정되고 항상 다음 값으로 설정됩니다.`ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 제품 및 서비스를 소유 또는 라이센스하고 해당 구성원에 대한 액세스를 허용할 수 있는 법인. `{IMS_ORG}` 정보를 검색하는 방법에 대한 지침은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../../landing/postman.md)에 대한 자습서를 참조하십시오. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 사용 중인 가상 샌드박스 파티션의 이름입니다. | `prod` |
| `TENANT_ID` | 만든 리소스가 적절하게 지정되어 IMS 조직 내에 들어 있는지 확인하는 데 사용되는 ID입니다. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | API 호출을 수행하는 URL 끝점입니다. 이 값은 고정되고 항상 다음과 같이 설정됩니다.`http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | [!DNL Marketo] 계정에 대한 고유 ID. `munchkinId`을(를) 검색하는 방법에 대한 자세한 내용은 [인스턴스 [!DNL Marketo] 인스턴스](./marketo-auth.md)를 인증하는 방법에 대한 자습서를 참조하십시오. | `123-ABC-456` |
| `sfdc_org_id` | [!DNL Salesforce] 계정의 조직 ID. [!DNL Salesforce] 조직 ID를 취득하는 방법에 대한 자세한 내용은 다음 [[!DNL Salesforce] 안내서](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)를 참조하십시오. | `00D4W000000FgYJUA0` |
| `msd_org_id` | [!DNL Dynamics] 계정의 조직 ID. [!DNL Dynamics] 조직 ID를 취득하는 방법에 대한 자세한 내용은 다음 [[!DNL Microsoft Dynamics] 안내서](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name)를 참조하십시오. | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | [!DNL Marketo Account-Based Marketing]에 가입했는지 여부를 나타내는 부울 값입니다. | `false` |
| `has_msi` | [!DNL Marketo Sales Insight]에 속하는지 여부를 나타내는 부울 값입니다. | `false` |

{style=&quot;table-layout:auto&quot;}

### 스크립트 실행

[!DNL Postman] 컬렉션 및 환경이 설정되면 이제 [!DNL Postman] 인터페이스를 통해 스크립트를 실행할 수 있습니다.

[!DNL Postman] 인터페이스에서 자동 생성기 유틸리티의 루트 폴더를 선택한 다음 상단 헤더에서 **[!DNL Run]**&#x200B;을 선택합니다.

![루트 폴더](../images/marketo/root-folder.png)

[!DNL Runner] 인터페이스가 나타납니다. 여기서 모든 확인란을 선택한 다음 **[!DNL Run Adobe I/O Access Token Generation + Automate Namespace creation]**&#x200B;을 선택합니다.

![run-generator](../images/marketo/run-generator.png)

요청이 성공하면 베타 사양에 따라 B2B 네임스페이스 및 스키마가 만들어집니다.

## [!DNL Marketo] 네임스페이스

ID 네임스페이스는 ID와 관련된 컨텍스트의 표시기 역할을 하는 [[!DNL Identity Service]](../../../../identity-service/home.md)의 구성 요소입니다.

정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다. 모든 새로운 [!DNL Marketo] 인스턴스와 데이터 집합 조합에 대해 새 사용자 지정 네임스페이스가 필요합니다. 예를 들어 `programs` 데이터 세트를 인제스트하는 소스 커넥터에는 고유한 사용자 정의 네임스페이스가 필요하며, 동일한 데이터 세트를 인제스트하는 다른 Marketo 소스 커넥터에도 고유한 사용자 정의 네임스페이스가 필요합니다. [!DNL Marketo] 자세한 내용은 [네임스페이스 개요](../../../../identity-service/namespaces.md)를 참조하십시오.

[!DNL Marketo] 네임스페이스는 엔티티의 기본 ID에 사용됩니다.

다음 표는 [!DNL Marketo] 네임스페이스에 대해 설정된 기본 설정에 대한 정보를 포함합니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 디스플레이 이름 | ID 기호 | ID 유형 | 발급자 유형 | 발급자 엔티티 유형 | Munchkin ID 예 |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | 자동 생성 | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | 자동 생성 | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | 자동 생성 | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | 자동 생성 | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | 자동 생성 | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | 자동 생성 | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | 자동 생성 | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | 자동 생성 | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | 자동 생성 | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] 네임스페이스

[!DNL Salesforce] 통합을 구독하는 경우 엔티티의 보조 ID에 [!DNL Salesforce] 네임스페이스가 사용됩니다.

다음 표는 [!DNL Salesforce] 네임스페이스에 대해 설정된 기본 설정에 대한 정보를 포함합니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 디스플레이 이름 | ID 기호 | ID 유형 | 발급자 유형 | 발급자 엔티티 유형 | [!DNL Salesforce] 구독 조직 ID 예 |
| --- | --- | --- | --- | --- | --- |
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] 네임스페이스

[!DNL Dynamics] 통합을 구독하는 경우 [!DNL Dynamics] 네임스페이스가 엔티티의 보조 ID로 사용됩니다.

다음 표는 [!DNL Dynamics] 네임스페이스에 대해 설정된 기본 설정에 대한 정보를 포함합니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 디스플레이 이름 | ID 기호 | ID 유형 | 발급자 유형 | 발급자 엔티티 유형 | [!DNL Dynamics] 구독 조직 ID 예 |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | 자동 생성 | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | 자동 생성 | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | 자동 생성 | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | 자동 생성 | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | 자동 생성 | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | 자동 생성 | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] 스키마

Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

데이터를 플랫폼에 인제스트하려면 데이터 구조를 설명하고 각 필드에 포함할 수 있는 데이터 유형에 제약 조건을 제공하도록 스키마를 구성해야 합니다. 스키마는 기본 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다.

디자인 원칙 및 우수 사례를 포함하여 스키마 구성 모델에 대한 자세한 내용은 스키마 컴포지션](../../../../xdm/schema/composition.md)의 [기본 사항을 참조하십시오.

다음 표는 [!DNL Marketo] 스키마의 기본 설정에 대한 정보를 포함합니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 스키마 이름 | 기본 클래스 | 필드 그룹 | [!DNL Profile] 스키마에서 | 기본 ID | 기본 ID 네임스페이스 | 보조 ID | 보조 ID 네임스페이스 | 관계 | 참고 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | XDM 비즈니스 계정 | XDM 비즈니스 계정 세부 정보 | 활성화됨 | `accountID` 기본 클래스에서 | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` XDM 비즈니스 계정 세부 정보 필드 그룹에서</li><li>유형:1대1</li><li>참조 스키마:`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | XDM 개별 프로필 | <ul><li>XDM 비즈니스 담당자 세부 정보</li><li>XDM 비즈니스 담당자 구성 요소</li><li>IdentityMap</li></ul> | 활성화됨 | `personID` 기본 클래스에서 | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` XDM Business Person Details 필드 그룹</li><li>`workEmail.address` XDM Business Person Details 필드 그룹</li><li>`identityMap` ID 맵 필드 그룹</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>이메일</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` XDM Business Person Components 필드 그룹</li><li>유형:다대다</li><li>참조 스키마:`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_company_{MUNCHKIN_ID}`</li><li>대상 속성:`accountID`</li><li>현재 스키마의 관계 이름:계정</li><li>참조 스키마의 관계 이름:People</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | XDM 비즈니스 기회 | XDM 비즈니스 기회 세부 정보 | 활성화됨 | `opportunityID` 기본 클래스에서 | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_company_{MUNCHKIN_ID}`</li><li>대상 속성:`accountID`</li><li>현재 스키마의 관계 이름:계정</li><li>참조 스키마의 관계 이름:기회</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | XDM 사업 기회 담당자 관계 | None | 활성화됨 | `opportunityPersonID` 기본 클래스에서 | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 첫 번째 관계<ul><li>`personID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:`[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_person_{MUNCHKIN_ID}`</li><li>대상 속성:`personID`</li><li>현재 스키마의 관계 이름:Person</li><li>참조 스키마의 관계 이름:기회</li></ul>두 번째 관계<ul><li>`opportunityID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:`[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>대상 속성:`opportunityID`</li><li>현재 스키마의 관계 이름:기회</li><li>참조 스키마의 관계 이름:People</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | XDM 비즈니스 캠페인 | XDM 비즈니스 캠페인 세부 사항 | 활성화됨 | `campaignID` 기본 클래스에서 | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | XDM 비즈니스 캠페인 구성원 | XDM 비즈니스 캠페인 멤버 세부 사항 | 활성화됨 | `campaignMemberID` 기본 클래스에서 | `marketo_program_member_{MUNCHKIN_ID}` | 없음 | 없음 | 첫 번째 관계<ul><li>`personID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:Marketo Person {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_person_{MUNCHKIN_ID}`</li><li>대상 속성:`personID`</li><li>현재 스키마의 관계 이름:Person</li><li>참조 스키마의 관계 이름:프로그램</li></ul>두 번째 관계<ul><li>`campaignID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:`[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_program_{MUNCHKIN_ID}`</li><li>대상 속성:`campaignID`</li><li>현재 스키마의 관계 이름:프로그램</li><li>참조 스키마의 관계 이름:People</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | XDM 비즈니스 마케팅 목록 | 없음 | 활성화됨 | `marketingListID` 기본 클래스에서 | `marketo_static_list_{MUNCHKIN_ID}` | 없음 | 없음 | 없음 | 정적 목록은 [!DNL Salesforce]에서 동기화되지 않으므로 보조 ID가 없습니다. |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | XDM 비즈니스 마케팅 목록 구성원 | 없음 | 활성화됨 | `marketingListMemberID` 기본 클래스에서 | `marketo_static_list_member_{MUNCHKIN_ID}` | 없음 | 없음 | 첫 번째 관계<ul><li>`personID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:`[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_person_{MUNCHKIN_ID}`</li><li>대상 속성:`personID`</li><li>현재 스키마의 관계 이름:Person</li><li>참조 스키마의 관계 이름:목록</li></ul>두 번째 관계<ul><li>`marketingListID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:`[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_static_list_{MUNCHKIN_ID}`</li><li>대상 속성:`marketingListID`</li><li>현재 스키마의 관계 이름:목록</li><li>참조 스키마의 관계 이름:People</li></ul> | 정적 목록 멤버는 [!DNL Salesforce]에서 동기화되지 않으므로 보조 ID가 없습니다. |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | XDM 비즈니스 계정 | XDM 비즈니스 계정 세부 정보 | 활성화됨 | `accountID` 기본 클래스에서 | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` XDM 비즈니스 계정 세부 정보 필드 그룹에서</li><li>유형:1대1</li><li>참조 스키마:`[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] 활동 `{MUNCHKIN ID}` | XDM ExperienceEvent | <ul><li>웹 페이지 방문</li><li>새 리드</li><li>리드 변환</li><li>목록에 추가</li><li>목록에서 제거</li><li>기회에 추가</li><li>기회에서 제거</li><li>양식 작성됨</li><li>링크 클릭 수</li><li>배달된 이메일</li><li>연 이메일</li><li>클릭한 이메일</li><li>바운스된 이메일</li><li>바운스된 이메일 소프트</li><li>구독 취소된 이메일</li><li>점수 변경됨</li><li>기회 업데이트됨</li><li>캠페인 진행 상태의 상태가 변경됨</li><li>개인 식별자</li><li>Marketo 웹 URL | 활성화됨 | `personID` 의 사람 식별자 필드 그룹 | `marketo_person_{MUNCHKIN_ID}` | 없음 | 없음 | 첫 번째 관계<ul><li>`listOperations.listID` 필드</li><li>유형:1대1</li><li>참조 스키마:`[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>두 번째 관계<ul><li>`opportunityEvent.opportunityID` 필드</li><li>유형:1대1</li><li>참조 스키마:`[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>제3의 관계<ul><li>`leadOperation.campaignProgression.campaignID` 필드</li><li>유형:1대1</li><li>참조 스키마:`[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>네임스페이스: `marketo_program_{MUNCHKIN_ID}`</li></ul> | `[!DNL Marketo] Activity {MUNCHKIN_ID}` 스키마의 기본 ID는 `personID`이며 `[!DNL Marketo] Person {MUNCHKIN_ID}` 스키마의 기본 ID와 같습니다. |

{style=&quot;table-layout:auto&quot;}

## 다음 단계

[!DNL Marketo] 데이터를 플랫폼에 연결하는 방법을 알아보려면 UI](../../../tutorials/ui/create/adobe-applications/marketo.md)에서 Marketo 소스 커넥터 만들기에서 자습서를 참조하십시오.[
