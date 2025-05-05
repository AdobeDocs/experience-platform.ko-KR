---
title: Microsoft Dynamics 매핑 필드
description: 아래 표에는 Microsoft Dynamics 소스 필드와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.
exl-id: 32f51761-5de3-4192-8f23-c1412ca12c08
source-git-commit: ec42cf27c082611acb1a08500b7bbd23fc34d730
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 8%

---

# [!DNL Microsoft Dynamics] 필드 매핑

아래 표에는 [!DNL Microsoft Dynamics] 소스 필드와 해당 XDM(경험 데이터 모델) 필드 간의 매핑이 포함되어 있습니다.

## 연락처 {#contacts}

| 소스 필드 | 타겟 XDM 필드 | 참고 |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `assistantname` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `assistantphone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `birthdate` | `person.birthDate` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `contactid` | `b2b.personKey.sourceID` |
| `concat(contactid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | 기본 ID. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `iif(contactid != null && contactid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", contactid, "sourceKey", concat(contactid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `department` | `extendedWorkDetails.departments` |
| `fullname` | `person.name.fullName` |
| `suffix` | `person.name.suffix` |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey", concat(parentcustomerid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourceAccountKey` |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey",  concat(parentcustomerid, "@${CRM_ORG_ID}.Dynamics")), null)` | `b2b.accountKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | 보조 식별자. |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `lastname` | `person.name.lastName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |
| `telephone1` | `workPhone.number` |

{style="table-layout:auto"}

## 잠재 고객 {#leads}

| 소스 필드 | 타겟 XDM 필드 | 참고 |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `telephone1` | `workPhone.number` |
| `mobilephone` | `mobilePhone.number` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | 보조 식별자 |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `fax` | `faxPhone.number` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `lastname` | `person.name.lastName` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `leadid` | `b2b.personKey.sourceID` |
| `concat(leadid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | 기본 ID. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `iif(leadid != null && leadid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", leadid, "sourceKey", concat(leadid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |

{style="table-layout:auto"}

## 계정 {#accounts}

| 소스 필드 | 타겟 XDM 필드 | 참고 |
| --- | --- | --- |
| `"Dynamics"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `accountid` | `accountKey.sourceID` | 기본 ID. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `accountnumber` | `accountNumber` |
| `accountratingcode` | `accountOrganization.rating` |
| `address1_addressid` | `accountPhysicalAddress._id` |
| `address1_city` | `accountPhysicalAddress.city` |
| `address1_country` | `accountPhysicalAddress.country` |
| `address1_county` | `accountPhysicalAddress.region` |
| `address1_latitude` | `accountPhysicalAddress._schema.latitude` |
| `address1_line1` | `accountPhysicalAddress.street1` |
| `address1_line2` | `accountPhysicalAddress.street2` |
| `address1_line3` | `accountPhysicalAddress.street3` |
| `address1_longitude` | `accountPhysicalAddress._schema.longitude` |
| `address1_name` | `accountPhysicalAddress.label` |
| `address1_postalcode` | `accountPhysicalAddress.postalCode` |
| `address1_postofficebox` | `accountPhysicalAddress.postOfficeBox` |
| `address1_stateorprovince` | `accountPhysicalAddress.state` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `accountDescription` |
| `fax` | `accountFax.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `name` | `accountName` |
| `numberofemployees` | `accountOrganization.numberOfEmployees` |
| `revenue` | `accountOrganization.annualRevenue.amount` |
| `sic` | `accountOrganization.SICCode` |
| `telephone1` | `accountPhone.number` |
| `tickersymbol` | `accountOrganization.tickerSymbol` |
| `websiteurl` | `accountOrganization.website` |
| `concat(accountid,"@${CRM_ORG_ID}.Dynamics")` | `accountKey.sourceKey` |

{style="table-layout:auto"}

## 기회 {#opportunities}

| 소스 필드 | 타겟 XDM 필드 | 참고 |
| --- | --- | --- |
| `name` | `opportunityName` |
| `"Dynamics"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `iif(parentaccountid != null && parentaccountid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", parentaccountid, "sourceKey", concat(parentaccountid, "@${CRM_ORG_ID}.Dynamics")), null)` | `accountKey` |
| `actualclosedate` | `actualCloseDate` |
| `actualvalue` | `opportunityAmount.amount` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `campaignKey` |
| `closeprobability` | `probabilityPercentage` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `opportunityDescription` |
| `estimatedclosedate` | `expectedCloseDate` |
| `estimatedvalue` | `expectedRevenue.amount` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `opportunityid` | `opportunityKey.sourceID` |
| `concat(opportunityid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityKey.sourceKey` | 기본 ID. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `salesstage` | `opportunityStage` |
| `stepname` | `nextStep` |

{style="table-layout:auto"}

## 영업 기회 연락처 역할 {#opportunity-contact-roles}

| 소스 필드 | 타겟 XDM 필드 | 참고 |
| --- | --- | --- |
| `"Dynamics"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `connectionid` | `opportunityPersonKey.sourceID` |
| `concat(connectionid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityPersonKey.sourceKey` | 기본 ID. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `iif(record1id != null && record1id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record1id, "sourceKey", concat(record1id,"@${CRM_ORG_ID}.Dynamics")), null)` | `opportunityKey` |
| `iif(record2id != null && record2id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record2id, "sourceKey", concat(record2id,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `connectionrole1.name` | `personRole` |
| `record1objecttypecode` | *사용자 지정 필드 그룹을 대상 스키마로 정의해야 합니다.* 자세한 내용은 부록 섹션에서 [선택 목록 유형 소스 필드를 대상 XDM 스키마에 매핑하는 방법](#picklist-type-fields)을 참조하십시오. | `record1objecttypecode` 원본 필드에 대한 가능한 목록, 값 및 레이블은 이 [[!DNL Microsoft Dynamics] 연결 엔터티 참조 문서](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record1objecttypecode-options)를 참조하십시오. |
| `record2objecttypecode` | *사용자 지정 필드 그룹을 대상 스키마로 정의해야 합니다.* 자세한 내용은 부록 섹션에서 [선택 목록 유형 소스 필드를 대상 XDM 스키마에 매핑하는 방법](#picklist-type-fields)을 참조하십시오. | `record2objecttypecode` 원본 필드에 대한 가능한 목록, 값 및 레이블은 이 [[!DNL Microsoft Dynamics] 연결 엔터티 참조 문서](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record2objecttypecode-options)를 참조하십시오. |

{style="table-layout:auto"}

## 캠페인 {#campaigns}

| 소스 필드 | 타겟 XDM 필드 | 참고 |
| --- | --- | --- |
| `campaignid` | `campaignKey.sourceID` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `concat(campaignid,"@${CRM_ORG_ID}.Dynamics")` | `campaignKey.sourceKey` | 기본 ID. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `"Dynamics"` | `campaignKey.sourceType` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey`은(는) 보조 ID입니다. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedby` | `extSourceSystemAudit.lastUpdatedBy` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `description` | `campaignDescription` |
| `name` | `campaignName` |
| `totalactualcost` | `actualCost.amount` |
| `budgetedcost` | `budgetedCost.amount` |
| `expectedrevenue` | `expectedRevenue.amount` |
| `actualend` | `campaignEndDate` |
| `actualstart` | `campaignStartDate` |
| `expectedresponse` | `expectedResponse` |
| `utcconversiontimezonecode` | `timeZone` |
| `utcconversiontimezonecode` | `timezoneName` |

{style="table-layout:auto"}

## 마케팅 목록 {#marketing-list}

| 소스 필드 | 타겟 XDM 필드 | 참고 |
| --- | --- | --- |
| `"Dynamics"` | `marketingListKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListKey.sourceInstanceID` | `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `description` | `marketingListDescription` |
| `listname` | `marketingListName` |
| `listid` | `marketingListKey.sourceID` |
| `concat(listid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListKey.sourceKey` | 기본 ID. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## 마케팅 목록 멤버 {#marketing-list-members}

| 소스 필드 | 타겟 XDM 필드 | 참고 |
| --- | --- | --- |
| `"Dynamics"` | `marketingListMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListMemberKey.sourceInstanceID` | `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `iif(entityid != null && entityid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", entityid, "sourceKey", concat(entityid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `listmemberid` | `marketingListMemberKey.sourceID` |
| `concat(listmemberid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListMemberKey.sourceKey` | 기본 ID. `"${CRM_ORG_ID}"`의 값이 자동으로 대체됩니다. |
| `iif(listid != null && listid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", listid, "sourceKey", concat(listid,"@${CRM_ORG_ID}.Dynamics")), null)` | `marketingListKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## 부록

아래 섹션에서는 [!DNL Microsoft] Dynamics 소스에 대해 B2B 매핑을 구성할 때 사용할 수 있는 추가 정보를 제공합니다.

### 선택 목록 유형 필드 {#picklist-type-fields}

[계산된 필드](../../../../data-prep/ui/mapping.md#calculated-fields)을(를) 사용하여 [!DNL Microsoft Dynamics]의 선택 목록 유형 원본 필드를 대상 XDM 필드에 매핑할 수 있습니다.

예를 들어 `genderCode` 필드에는 다음 두 가지 옵션이 포함됩니다.

| 값 | 레이블 |
| --- | --- |
| 1 | `male` |
| 2 | `female` |

다음 옵션을 사용하여 `genderCode` 원본 필드를 `person.gender` 대상 필드에 매핑할 수 있습니다.

#### 논리 연산자 사용

| 소스 필드 | 타겟 XDM 필드 |
| --- | --- |
| `decode(genderCode, "1", "male", "2", "female", "default")` | `person.gender` |

이 시나리오에서 값은 키가 옵션에 있는 경우 키에 해당하고, `default`이(가) 있고 키를 찾을 수 없는 경우 `default`에 해당합니다. 옵션이 `null`이거나 `default`이(가) 없고 키를 찾을 수 없는 경우 값은 `null`에 해당합니다.

#### 계산된 필드 사용

| 소스 필드 | 타겟 XDM 필드 |
| --- | --- |
| `iif(gendercode.equals("1"),"male",iif(gendercode.equals("2"),"female",null))` | `person.gender` |

>[!TIP]
>
>위의 작업의 중첩 반복은 `iif(condition, iif(cond1, tv1, fv1), iif(cond2, tv2, fv2))`과(와) 비슷합니다.

자세한 내용은  [!DNL Data Prep][&#128279;](../../../../data-prep/functions.md##logical-operators)의 논리 연산자에 대한 문서를 참조하십시오
