---
keywords: Experience Platform;홈;인기 항목;Marketo Engage;마케팅;참여;Marketo;매핑
solution: Experience Platform
title: Marketo Engage 소스의 매핑 필드
topic-legacy: overview
description: 아래 표에는 Marketo 데이터 집합의 필드와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
translation-type: tm+mt
source-git-commit: e4823a2b787667fc181f8a4d474c7d2eb73c8eec
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# (베타) [!DNL Marketo Engage] 필드 매핑

>[!IMPORTANT]
>
>[!DNL Marketo Engage] 소스는 현재 베타 상태입니다. 기능 및 설명서는 변경될 수 있습니다.

아래 표에는 9개의 [!DNL Marketo] 데이터 집합에 있는 필드와 해당 XDM(Experience Data Model) 필드 간의 매핑이 포함되어 있습니다.

## 활동 {#activities}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `personID` | `personID` | 기본 ID |
| `eventType` | `eventType` |
| `timestamp` | `timestamp` |
| `web.webPageDetails._marketo.URL` | `web.webPageDetails._marketo.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `listOperations.listID` | `listOperations.listID` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `opportunityEvent.dataValueChanges.attributeName` | `opportunityEvent.dataValueChanges.attributeName` |
| `opportunityEvent.dataValueChanges.newValue` | `opportunityEvent.dataValueChanges.newValue` |
| `opportunityEvent.dataValueChanges.oldValue` | `opportunityEvent.dataValueChanges.oldValue` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |

{style=&quot;table-layout:auto&quot;}

## 프로그램 {#programs}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `id` | `campaignID` | 기본 ID |
| `sfdcId` | `extSourceSystemAudit.externalID` | 보조 ID |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `parentProgramId` | `parentCampaignID` |
| `integrationPartner` | `integrationPartnerName` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |

{style=&quot;table-layout:auto&quot;}

## 프로그램 멤버십 {#program-memberships}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `id` | `campaignMemberID` | 기본 ID |
| `programId` | `campaignID` | 관계 |
| `leadId` | `personID` | 관계 |
| `acquiredByCampaignID` | `acquiredByCampaignID` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## 회사 {#companies}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | 기본 ID |
| `mktoCdpExternalId` | `extSourceSystemAudit.externalID` | 보조 ID |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |
| `mktoCdpParentOrgId` | `accountParentID` |

{style=&quot;table-layout:auto&quot;}

## 정적 목록 {#static-lists}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `id` | `marketingListID` | 기본 ID |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## 정적 목록 구성원 자격 {#static-list-memnberships}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `staticListMemberID` | `marketingListMemberID` | 기본 ID |
| `staticListID` | `marketingListID` | 관계 |
| `personID` | `personID` | 관계 |
| `createdAt` | `extSourceSystemAudit.createdDate` |

{style=&quot;table-layout:auto&quot;}

## 명명된 계정 {#named-accounts}

>[!IMPORTANT]
>
>명명된 계정 데이터 세트는 Marketo의 ABM(계정 기반 마케팅) 기능에만 필요합니다. ABM을 사용하지 않는 경우 지정된 계정에 대한 매핑을 설정할 필요가 없습니다.

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | 기본 ID |
| `crmGuid` | `extSourceSystemAudit.externalID` | 보조 ID |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `parentAccountId` | `accountParentID` |
| `sourceType` | `accountSourceType` |

{style=&quot;table-layout:auto&quot;}

## 기회 {#opportunities}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `id` | `opportunityID` | 기본 ID |
| `externalOpportunityId` | `extSourceSystemAudit.externalID` | 보조 ID |
| `mktoCdpAccountOrgId` | `accountID` | 관계 |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `mktoCdpSourceCampaignId` | `campaignID` | Salesforce 통합을 사용하는 경우에만 권장됩니다. |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |

{style=&quot;table-layout:auto&quot;}

## 기회 연락처 역할 {#opportunity-contact-roles}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `id` | `opportunityPersonID` | 기본 ID |
| `mktoCdpSfdcId` | `extSourceSystemAudit.externalID` | 보조 ID |
| `mktoCdpOpptyId` | `opportunityID` | 관계 |
| `leadId` | `personID` | 관계 |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## 사용자 {#persons}

| 소스 데이터 세트 | XDM 대상 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `id` | `personID` | 기본 ID |
| `emailSuspended` | `b2b.personOptInOut._channels.email` |
| `emailSuspendedAt` | `b2b.personOptInOut.optOutDetails.email.optOutDate` |
| `emailSuspendedCause` | `b2b.personOptInOut.optOutDetails.email.optOutReason` |
| `contactCompany` | `b2b.accountID` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpCnvContactPersonId` | `b2b.convertedContactID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| `sfdcLeadId` | `extSourceSystemAudit.externalID` | 보조 ID |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `organizations` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `mktoCdpCnvContactPersonId` | `personComponents.sourceConvertedContactID` |
| `contactCompany` | `personComponents.sourceAccountID` |
| `sfdcContactId` | `personComponents.sourceExternalID` | Salesforce 통합을 사용하는 경우에만 권장됩니다. |
| `id` | `personComponents.sourcePersonID` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |
| `to_object('ECID',arrays_to_objects('id',explode(ecids)))` | `identityMap` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>`to_object('ECID',arrays_to_objects('id',explode(ecids)))` 소스 필드는 플랫폼 UI에서 [!UICONTROL Add calculated field] 옵션을 사용하여 추가해야 하는 계산된 필드입니다. 자세한 내용은 [계산된 필드 추가](../../../../ingestion/tutorials/map-a-csv-file.md)에 대한 자습서를 참조하십시오.

## 다음 단계

이 문서를 읽으면 [!DNL Marketo] 데이터 세트와 해당 XDM 필드 간의 매핑 관계에 대한 통찰력을 얻을 수 있습니다. [!DNL Marketo] 데이터 흐름을 완료하려면 [소스 연결](../../../tutorials/ui/create/adobe-applications/marketo.md)을 만드는 방법에 대한 자습서를 참조하십시오. [!DNL Marketo] 
