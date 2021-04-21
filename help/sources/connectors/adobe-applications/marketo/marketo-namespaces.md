---
keywords: Experience Platform;홈;인기 항목;Marketo 소스 커넥터;네임스페이스;스키마
solution: Experience Platform
title: 'Marketo 네임스페이스 '
topic-legacy: overview
description: 이 문서에서는 Marketo Engage 소스 커넥터를 만들 때 필요한 사용자 정의 네임스페이스에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 6%

---


# (베타) [!DNL Marketo Engage] 네임스페이스 및 스키마

>[!IMPORTANT]
>
>[!DNL Marketo Engage] 소스는 현재 베타 상태입니다. 기능 및 설명서는 변경될 수 있습니다.

이 문서에서는 [!DNL Marketo Engage](이하 &quot;[!DNL Marketo]&quot;이라 함)에 사용되는 B2B 네임스페이스 및 스키마(이하 &quot;기본 설정&quot;이라 함)에 대한 정보를 제공합니다. 또한 이 문서에서는 [!DNL Marketo] B2B 네임스페이스 및 스키마를 생성하는 데 필요한 Postman 자동화 유틸리티 설정에 대한 세부 정보를 제공합니다.

## 전제 조건

B2B 네임스페이스 및 스키마를 생성하려면 먼저 플랫폼 개발자 콘솔 및 [!DNL Postman] 환경을 설정해야 합니다. 자세한 내용은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../../landing/postman.md)에 대한 자습서를 참조하십시오.

플랫폼 개발자 콘솔 및 [!DNL Postman]이(가) 설정되면 다음 변수를 [!DNL Marketo] 환경에 적용합니다.

| 환경 변수 | 값 예 | 참고 |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | 자세한 내용은 [인스턴스 [!DNL Marketo] 인스턴스](./marketo-auth.md)를 인증하는 자습서를 참조하십시오. |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | 조직 ID 취득에 대한 자세한 내용은 다음 [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)를 참조하십시오. |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | 조직 ID 취득에 대한 자세한 내용은 다음 [[!DNL Microsoft Dynamics] guide](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name)를 참조하십시오. |
| `has_abm` | `false` | 계정 기반 마케팅을 구독하는 경우 이 값은 `true`으로 설정됩니다. |
| `has_msi` | `false` | [!DNL Marketo Sales Insight]에 가입한 경우 이 값은 `true`으로 설정됩니다. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] 네임스페이스

ID 네임스페이스는 ID와 관련된 컨텍스트의 표시기 역할을 하는 [[!DNL Identity Service]](../../../../identity-service/home.md)의 구성 요소입니다.

정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다. 모든 새로운 [!DNL Marketo] 인스턴스와 데이터 집합 조합에 대해 새 사용자 지정 네임스페이스가 필요합니다. 예를 들어 `programs` 데이터 세트를 인제스트하는 소스 커넥터에는 고유한 사용자 정의 네임스페이스가 필요하며, 동일한 데이터 세트를 인제스트하는 다른 Marketo 소스 커넥터에도 고유한 사용자 정의 네임스페이스가 필요합니다. [!DNL Marketo] 자세한 내용은 [네임스페이스 개요](../../../../identity-service/namespaces.md)를 참조하십시오.

[!DNL Marketo] 네임스페이스는 엔티티의 기본 ID에 사용됩니다.

다음 표는 [!DNL Marketo] 네임스페이스에 대해 설정된 기본 설정에 대한 정보를 포함합니다.

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

| 디스플레이 이름 | ID 기호 | ID 유형 | 발급자 유형 | 발급자 엔티티 유형 | [!DNL Salesforce] 구독 조직 ID 예 |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | 자동 생성 | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] 네임스페이스

[!DNL Dynamics] 통합을 구독하는 경우 [!DNL Dynamics] 네임스페이스가 엔티티의 보조 ID로 사용됩니다.

다음 표는 [!DNL Dynamics] 네임스페이스에 대해 설정된 기본 설정에 대한 정보를 포함합니다.

| 디스플레이 이름 | ID 기호 | ID 유형 | 발급자 유형 | 발급자 엔티티 유형 | [!DNL Salesforce] 구독 조직 ID 예 |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | 자동 생성 | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | 자동 생성 | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | 자동 생성 | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | 자동 생성 | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | 자동 생성 | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | 자동 생성 | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

## [!DNL Marketo] 스키마

Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

데이터를 플랫폼에 인제스트하려면 데이터 구조를 설명하고 각 필드에 포함할 수 있는 데이터 유형에 제약 조건을 제공하도록 스키마를 구성해야 합니다. 스키마는 기본 클래스와 0개 이상의 혼합으로 구성됩니다.

디자인 원칙 및 우수 사례를 포함하여 스키마 구성 모델에 대한 자세한 내용은 스키마 컴포지션](../../../../xdm/schema/composition.md)의 [기본 사항을 참조하십시오.

다음 표는 [!DNL Marketo] 스키마의 기본 설정에 대한 정보를 포함합니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 스키마 이름 | 기본 클래스 | 혼합 | 기본 ID | 기본 ID 네임스페이스 | 보조 ID | 보조 ID 네임스페이스 | 관계 | 참고 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] 회사 {MUNCHKIN_ID} | XDM 비즈니스 계정 | XDM 비즈니스 계정 세부 정보 | `accountID` 기본 클래스에서 | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` XDM 비즈니스 계정 세부 정보 혼합에서</li><li>유형:1대1</li><li>참조 스키마:Marketo 회사 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] 사람 {MUNCHKIN_ID} | XDM 개별 프로필 | <ul><li>XDM 비즈니스 담당자 세부 정보</li><li>XDM 비즈니스 담당자 구성 요소</li></ul> | `personID` 기본 클래스에서 | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` XDM 비즈니스 담당자 세부 정보 혼합</li><li>`workEmail.address` XDM 비즈니스 담당자 세부 정보 혼합</li><li>`identityMap` ID 맵 혼합</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>이메일</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` XDM 비즈니스 담당자 구성 요소 믹싱</li><li>유형:다대다</li><li>참조 스키마:Marketo 회사 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_company_{MUNCHKIN_ID}`</li><li>대상 속성:`accountID`</li><li>현재 스키마의 관계 이름:계정</li><li>참조 스키마의 관계 이름:People</li></ul> |
| [!DNL Marketo] 기회 {MUNCHKIN_ID} | XDM 비즈니스 기회 | XDM 비즈니스 기회 세부 정보 | `opportunityID` 기본 클래스에서 | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:Marketo 회사 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_company_{MUNCHKIN_ID}`</li><li>대상 속성:`accountID`</li><li>현재 스키마의 관계 이름:계정</li><li>참조 스키마의 관계 이름:기회</li></ul> |
| [!DNL Marketo] 기회 연락처 역할 {MUNCHKIN_ID} | XDM 사업 기회 담당자 관계 | None | `opportunityPersonID` 기본 클래스에서 | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 첫 번째 관계<ul><li>`personID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:Marketo Person {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_person_{MUNCHKIN_ID}`</li><li>대상 속성:`personID`</li><li>현재 스키마의 관계 이름:Person</li><li>참조 스키마의 관계 이름:기회</li></ul>두 번째 관계<ul><li>`opportunityID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:Marketo 기회 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>대상 속성:`opportunityID`</li><li>현재 스키마의 관계 이름:기회</li><li>참조 스키마의 관계 이름:People</li></ul> |
| [!DNL Marketo] 프로그램 {MUNCHKIN_ID} | XDM 비즈니스 캠페인 | XDM 비즈니스 캠페인 세부 사항 | `campaignID` 기본 클래스에서 | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] 프로그램 구성원 {MUNCHKIN_ID} | XDM 비즈니스 캠페인 구성원 | XDM 비즈니스 캠페인 멤버 세부 사항 | `campaignMemberID` 기본 클래스에서 | `marketo_program_member_{MUNCHKIN_ID}` | 없음 | 없음 | 첫 번째 관계<ul><li>`personID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:Marketo Person {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_person_{MUNCHKIN_ID}`</li><li>대상 속성:`personID`</li><li>현재 스키마의 관계 이름:Person</li><li>참조 스키마의 관계 이름:프로그램</li></ul>두 번째 관계<ul><li>`campaignID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:Marketo 프로그램 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_program_{MUNCHKIN_ID}`</li><li>대상 속성:campaignID</li><li>현재 스키마의 관계 이름:프로그램</li><li>참조 스키마의 관계 이름:People</li></ul> |
| [!DNL Marketo] 정적 목록 {MUNCHKIN_ID} | XDM 비즈니스 마케팅 목록 | 없음 | `marketingListID` 기본 클래스에서 | `marketo_static_list_{MUNCHKIN_ID}` | 없음 | 없음 | 없음 | 정적 목록은 [!DNL Salesforce]에서 동기화되지 않으므로 보조 ID가 없습니다. |
| [!DNL Marketo] 정적 목록 멤버 {MUNCHKIN_ID} | XDM 비즈니스 마케팅 목록 구성원 | 없음 | `marketingListMemberID` 기본 클래스에서 | `marketo_static_list_member_{MUNCHKIN_ID}` | 없음 | 없음 | 첫 번째 관계<ul><li>`personID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:Marketo Person {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_person_{MUNCHKIN_ID}`</li><li>대상 속성:`personID`</li><li>현재 스키마의 관계 이름:Person</li><li>참조 스키마의 관계 이름:목록</li></ul>두 번째 관계<ul><li>`marketingListID` 기본 클래스에서</li><li>유형:다대다</li><li>참조 스키마:Marketo 정적 목록 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_static_list_{MUNCHKIN_ID}`</li><li>대상 속성:`marketingListID`</li><li>현재 스키마의 관계 이름:목록</li><li>참조 스키마의 관계 이름:People</li></ul> |
| [!DNL Marketo] 지정된 계정 {MUNCHKIN_ID} | XDM 비즈니스 계정 | XDM 비즈니스 계정 세부 정보 | `accountID` 기본 클래스에서 | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 기본 클래스에서 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` XDM 비즈니스 계정 세부 정보 혼합에서</li><li>유형:1대1</li><li>참조 스키마:Marketo 명명된 계정 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] 활동 {MUNCHKIN ID} | XDM 경험 이벤트 | <ul><li>웹 페이지 방문</li><li>새 리드</li><li>리드 변환</li><li>목록에 추가</li><li>목록에서 제거</li><li>기회에 추가</li><li>기회에서 제거</li><li>양식 작성됨</li><li>링크 클릭 수</li><li>배달된 이메일</li><li>연 이메일</li><li>클릭한 이메일</li><li>바운스된 이메일</li><li>바운스된 이메일 소프트</li><li>구독 취소된 이메일</li><li>점수 변경됨</li><li>기회 업데이트됨</li><li>캠페인 진행 상태의 상태가 변경됨</li><li>개인 식별자</li><li>Marketo 웹 URL | `personID` 사람 식별자 혼합 | marketing_person_{MUNCHKIN_ID} | 없음 | 없음 | 첫 번째 관계<ul><li>`listOperations.listID` 필드</li><li>유형:1대1</li><li>참조 스키마:Marketo 정적 목록 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>두 번째 관계<ul><li>`opportunityEvent.opportunityID` 필드</li><li>유형:1대1</li><li>참조 스키마:Marketo 기회 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>제3의 관계<ul><li>`leadOperation.campaignProgression.campaignID` 필드</li><li>유형:1대1</li><li>참조 스키마:Marketo 프로그램 {MUNCHKIN_ID}</li><li>네임스페이스: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>모든 스키마는 [!DNL Real-time Customer Profile]에 대해 사용할 수 있습니다.

## 다음 단계

[!DNL Marketo] 데이터를 플랫폼에 연결하는 방법을 알아보려면 UI](../../../tutorials/ui/create/adobe-applications/marketo.md)에서 Marketo 소스 커넥터 만들기에서 자습서를 참조하십시오.[