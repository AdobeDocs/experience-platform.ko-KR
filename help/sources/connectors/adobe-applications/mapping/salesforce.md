---
keywords: Experience Platform;홈;인기 항목;Salesforce;salesforce;필드 매핑;필드 매핑;매핑;marketo;B2B;b2b
solution: Experience Platform
title: Salesforce 매핑 필드
topic-legacy: overview
description: 아래 표에는 Salesforce 소스 필드와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.
source-git-commit: 00207ae10979b48d190cbda63aecf55e0f6d0f9c
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 11%

---

# [!DNL Salesforce] 필드 매핑

아래 표에는 [!DNL Salesforce] 소스 필드와 해당 XDM(Experience Data Model) 필드 간의 매핑이 포함되어 있습니다.

## 연락처 {#contact}

| 소스 필드 | Target XDM 필드 경로 | 참고 |
| --- | --- | --- |
| `AccountId` | `b2b.accountID` |
| `AccountId` | `personComponents.sourceAccountID` |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `Birthdate` | `person.birthDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Department` | `extendedWorkDetails.departments` |
| `Email` | `workEmail.address` | 이것이 보조 ID입니다. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `HomePhone` | `homePhone.number` |
| `Id` | `personID` | 이것이 기본 ID입니다 |
| `Id` | `personComponents.sourcePersonID` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `MailingCity` | `workAddress.city` |
| `MailingCountry` | `workAddress.country` |
| `MailingLatitude` | `workAddress._schema.latitude` |
| `MailingLongitude` | `workAddress._schema.longitude` |
| `MailingPostalCode` | `workAddress.postalCode` |
| `MailingState` | `workAddress.state` |
| `MailingStreet` | `workAddress.street1` |
| `MobilePhone` | `mobilePhone.number` |
| `Name` | `person.name.fullName` |
| `OtherCity` | `otherAddress.city` |
| `OtherCountry` | `otherAddress.country` |
| `OtherLatitude` | `otherAddress._schema.latitude` |
| `OtherLongitude` | `otherAddress._schema.longitude` |
| `OtherPhone` | `otherPhone.number` |
| `OtherPostalCode` | `otherAddress.postalCode` |
| `OtherState` | `otherAddress.state` |
| `OtherStreet` | `otherAddress.street1` |
| `Phone` | `workPhone.number` |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |
| `Salutation` | `person.name.courtesyTitle` |
| `Title` | `extendedWorkDetails.jobTitle` |

{style=&quot;table-layout:auto&quot;}

## 리드 {#lead}

| 소스 필드 | Target XDM 필드 경로 | 참고 |
| --- | --- | --- |
| `City` | `workAddress.city` |
| `ConvertedContactId` | `b2b.convertedContactID` |
| `ConvertedContactId` | `personComponents.sourceConvertedContactID` |
| `ConvertedDate` | `b2b.convertedDate` |
| `Country` | `workAddress.country` |
| `Email` | `workEmail.address` | 이것이 보조 ID입니다 |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `IsConverted` | `b2b.isConverted` |
| `Id` | `personID` | 이것이 기본 ID입니다 |
| `Id` | `personComponents.sourcePersonID` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `Latitude` | `workAddress._schema.latitude` |
| `Longitude` | `workAddress._schema.longitude` |
| `MiddleName` | `person.name.middleName` |
| `Name` | `person.name.fullName` |
| `PostalCode` | `workAddress.postalCode` |
| `Salutation` | `person.name.courtesyTitle` |
| `State` | `workAddress.state` |
| `Status` | `b2b.personStatus` |
| `Status` | `personComponents.personStatus` |
| `Street` | `workAddress.street1` |
| `Title` | `extendedWorkDetails.jobTitle` |
| `Suffix` | `person.name.suffix` |

{style=&quot;table-layout:auto&quot;}

## 계정 {#account}

| 소스 필드 | Target XDM 필드 경로 | 참고 |
| --- | --- | --- |
| `AccountNumber` | `accountNumber` |
| `AccountSource` | `accountSourceType` |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |
| `BillingCity` | 주소 | `accountBillingAddress.city` |
| `BillingCountry` | `accountBillingAddress.country` |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |
| `BillingState` | `accountBillingAddress.state` |
| `BillingStreet` | `accountBillingAddress.street1` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `accountDescription` |
| `DunsNumber` | `accountOrganization.DUNSNumber` | data.com 기능 |
| `Fax` | `accountFax.number` |
| `Id` | `accountID` | 이것이 기본 ID입니다 |
| `Industry` | `accountOrganization.industry` |
| `Jigsaw` | `accountOrganization.jigsaw` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `NaicsCode` | `accountOrganization.NAICSCode` | data.com 기능 |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | data.com 기능 |
| `Name` | `accountName` |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `Ownership` | `accountOwnership` |
| `ParentId` | `accountParentID` |
| `Phone` | `accountPhone.number` |
| `Rating` | `accountOrganization.rating` |
| `ShippingCity` | `accountShippingAddress.city` |
| `ShippingCountry` | `accountShippingAddress.country` |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |
| `ShippingState` | `accountShippingAddress.state` |
| `ShippingStreet` | `accountShippingAddress.street1` |
| `Sic` | `accountOrganization.SICCode` |
| `SicDesc` | `accountOrganization.SICDescription` |
| `Site` | `accountSite` |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |
| `Tradestyle` | `accountTradeStyle` | data.com 기능 |
| `Type` | `accountType` |

{style=&quot;table-layout:auto&quot;}

## 기회 {#opportunity}

| 소스 필드 | Target XDM 필드 경로 | 참고 |
| --- | --- | --- |
| `AccountId` | `accountID` | 관계 |
| `Amount` | `opportunityAmount.amount` |
| `CampaignId` | `campaignID` |
| `CloseDate` | `actualCloseDate` / `expectedCloseDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `opportunityDescription` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `FiscalQuarter` | `fiscalQuarter` |
| `FiscalYear` | `fiscalYear` |
| `ForecastCategory` | `forecastCategory` |
| `ForecastCategoryName` | `forecastCategoryName` |
| `Id` | `opportunityID` | 이것이 기본 ID입니다 |
| `IsClosed` | `isClosed` |
| `IsWon` | `isWon` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `leadSource` |
| `Name` | `opportunityName` |
| `NextStep` | `nextStep` |
| `Probability` | `probabilityPercentage` |
| `StageName` | `opportunityStage` |
| `TotalOpportunityQuantity` | `opportunityQuantity` |
| `Type` | `opportunityType` |

{style=&quot;table-layout:auto&quot;}

## 기회 연락처 역할 {#opportunity-contact-role}

| 소스 필드 | Target XDM 필드 경로 | 참고 |
| --- | --- | --- |
| `ContactId` | `personID` | 관계 |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Id` | `opportunityPersonID` | 이것이 기본 ID입니다 |
| `IsPrimary` | `isPrimary` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `OpportunityId` | `opportunityID` | 관계 |
| `Role` | `personRole` |

{style=&quot;table-layout:auto&quot;}

## Campaign {#campaign}

| 소스 필드 | Target XDM 필드 경로 | 참고 |
| --- | --- | --- |
| `Id` | `xdm: campaignID` | 이것이 기본 ID입니다 |
| `Name` | `xdm: campaignName` |
| `ParentId` | `xdm: parentCampaignID` |
| `Type` | `xdm: campaignType` |
| `Status` | `xdm: campaignStatus` |
| `StartDate` | `xdm: campaignStartDate` |
| `EndDate` | `xdm: campaignEndDate` |
| `ExpectedRevenue` | `xdm: expectedRevenue.amount` |
| `BudgetedCost` | `xdm: budgetedCost.amount` |
| `ActualCost` | `xdm: actualCost.amount` |
| `ExpectedResponse` | `xdm: expectedResponse` |
| `IsActive` | `xdm: isActive` |
| `Description` | `xdm: campaignDescription` |
| `CreatedDate` | `xdm: extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `xdm: extSourceSystemAudit.lastUpdatedDate` |
| `LastActivityDate` | `xdm: extSourceSystemAudit.lastActivityDate` |
| `LastViewedDate` | `xdm: extSourceSystemAudit.lastViewedDate` |
| `LastReferencedDate` | `xdm: extSourceSystemAudit.lastReferencedDate` |

## 캠페인 구성원 {#campaign-member}

| 소스 필드 | Target XDM 필드 경로 | 참고 |
| --- | --- | --- |
| `Id` | `campaignMemberID` | 이것이 기본 ID입니다 |
| `CampaignId` | `campaignID` | 관계 |
| `LeadOrContactId` | `personID` | 관계 |
| `Status` | `memberStatus` |
| `HasResponded` | `hasResponded` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `FirstRespondedDate` | `firstRespondedDate` |

## 다음 단계

이 문서를 읽은 후에는 [!DNL Salesforce] 소스 필드와 해당 XDM 필드 간의 매핑 관계에 대한 통찰력을 얻을 수 있었습니다. [!DNL Salesforce] 데이터 흐름을 시작하려면 [소스 연결](../../../tutorials/ui/create/crm/salesforce.md)을 만드는 자습서를 참조하십시오. [!DNL Salesforce] 
