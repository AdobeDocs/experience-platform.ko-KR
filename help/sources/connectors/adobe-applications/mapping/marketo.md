---
keywords: Experience Platform;홈;인기 항목;Marketo Engage;marketo engage;Marketo;매핑
solution: Experience Platform
title: Marketo Engage Source에 대한 필드 매핑
description: 아래 표에는 Marketo 데이터 세트의 필드와 해당 XDM 필드 간의 매핑이 포함되어 있습니다.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: 3b21d952da603b519c9919b08467cd5c6091f235
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 5%

---

# [!DNL Marketo Engage] 필드 매핑 {#marketo-engage-field-mappings}

아래 표에는 9개의 [!DNL Marketo] 데이터 세트의 필드와 해당 XDM(Experience Data Model) 필드 간의 매핑이 포함되어 있습니다.

>[!TIP]
>
>[!DNL Marketo]을(를) 제외한 모든 `Activities` 데이터 세트가 이제 `isDeleted`을(를) 지원합니다. 기존 데이터 흐름에는 `isDeleted`이(가) 자동으로 포함되지만 새로 수집된 데이터에 대한 플래그만 수집됩니다. 모든 이전 데이터에 플래그를 적용하려면 기존 데이터 흐름을 중지하고 새 매핑을 사용하여 다시 만들어야 합니다. `isDeleted`을(를) 제거하면 더 이상 기능에 액세스할 수 없습니다. 매핑은 자동으로 채워진 후에도 유지되어야 합니다.

## 활동 {#activities}

이제 [!DNL Marketo] 원본에서 추가 표준 활동을 지원합니다. 스키마를 업데이트하지 않고 새 [&#x200B; 데이터 흐름을 만들면 새 대상 필드가 스키마에 없으므로 표준 활동을 사용하려면 &#x200B;](../marketo/marketo-namespaces.md)스키마 자동 생성 유틸리티`activities`를 사용하여 스키마를 업데이트해야 합니다. 스키마를 업데이트하지 않도록 선택하는 경우에도 새 데이터 흐름을 만들고 오류를 무시할 수 있습니다. 그러나 새 필드나 업데이트된 필드는 Experience Platform에 수집되지 않습니다.

XDM 클래스 및 XDM 필드 그룹에 대한 자세한 내용은 [XDM 경험 이벤트 클래스](../../../../xdm/classes/experienceevent.md)에 대한 설명서를 참조하십시오.

>[!NOTE]
>
>`iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` 원본 필드는 Experience Platform UI의 **[!UICONTROL 계산된 필드 추가]** 옵션을 사용하여 추가해야 하는 계산된 필드입니다. 자세한 내용은 [계산된 필드 추가](../../../../data-prep/ui/mapping.md#calculated-fields)에 대한 자습서를 참조하십시오.

| Marketo 소스 필드 | 활동 유형 ID | Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------------- | ---------------- | -------------- | ---------------- | ----- |
| `_id` |  | `_id` | `_id` |  |
|  |  | `"Marketo"` | `personKey.sourceType` |  |
|  |  | `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `leadId` |  | `personID` | `personKey.sourceID` |  |
|  |  | `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `activityTypeId` |  | `eventType` | `eventType` |  |
| <ul><li><code>activityTypeId가</code> is 1, 2, 3, 9, 10 또는 11 → 표시 <code>producedBy</code> <strong>self</strong>(으)로.</li><li><code>activityTypeId가</code> is 6, 7, 8, 12, 21, 22, 24, 25, 27, 32, 34, 35, 36, 46, 101, 104, 110, 113, 114 또는 115 → 표시 <code>producedBy</code> <strong>system</strong>.</li><li>다른 모든 값→ <code>producedBy로 표시합니다.</code> <strong>self</strong>(으)로.</li></ul> |  | `producedBy` | `producedBy` |  |
| `activityDate` |  | `timestamp` | `timestamp` |  |
| `attributes.Webpage URL` |  | `web.webPageDetails.URL` | `web.webPageDetails.URL` |  |
| `attributes.User Agent` |  | `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |  |
| `attributes.Client IP Address` |  | `environment.ipV4` | `environment.ipV4` |  |
| `attributes.Search Query` |  | `search.keywords` | `search.keywords` |  |
| `attributes.Search Engine` |  | `search.searchEngine` | `search.searchEngine` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.name` | `web.webPageDetails.name` |  |
| `attributes.Personalized URL` | 1 | `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |  |
| `attributes.Query Parameters` | 1 | `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |  |
| `attributes.Referrer URL` |  | `web.webReferrer.URL` | `web.webReferrer.URL` |  |
| `primaryAttributeValueId when activityTypeId in (24, 25)` | 24,25 | `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |  |
| `attributes.Is Primary` | 34,35,36 | `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |  |
| (34, 35, 36)에서 activityTypeId일 때 primaryAttributeValueId | 34,35,36 | `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |  |
| `attributes.Role` | 34,35,36 | `opportunityEvent.role` | `opportunityEvent.role` |  |
| `attributes.Created Date` |  | `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |  |
| `attributes.Form Name` |  | `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |  |
| `attributes.Lead Source` |  | `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |  |
| `attributes.List Name` |  | `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |  |
| `attributes.SFDC Type` |  | `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |  |
| `attributes.Source Type` |  | `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |  |
| activityTypeId = 21인 경우 primaryAttributeValue | 21 | `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |  |
| `attributes.Converted Status` | 21 | `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |  |
| `attributes.Send Notification Email` | 21 | `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |  |
| (7, 8, 9, 10, 11, 27)에서 activityTypeId일 때 primaryAttributeValueId | 7, 8, 9, 10, 11, 27 | `iif(${directMarketing\\.mailingID} != null && ${directMarketing\\.mailingID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${directMarketing\\.mailingID}, \"sourceKey\", concat(${directMarketing\\.mailingID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `directMarketing.mailingKey` |  |
| (7, 8, 9, 10, 11, 27)에서 activityTypeId일 때 primaryAttributeValueId | 7, 8, 9, 10, 11, 27 | `directMarketing.mailingName` | `directMarketing.mailingName` |  |
|  |  | `directMarketing.testVariantName` | `directMarketing.testVariantName` |  |
| `attributes.Test Variant` |  | `directMarketing.testVariantID` | `directMarketing.testVariantID` |  |
| `attributes.Subcategory` <ul><li><strong>activityTypeId = 8</strong><ul><li>1099 → 메시지 차단됨</li><li>Source에서 1003 → 스팸 차단됨</li><li>메시지에서 1004 → 스팸 차단됨</li><li>2003 → 이메일 주소가 잘못됨</li><li>2001 → 주소 오류</li><li>* → 바운스에 대한 알 수 없는 이유</li></ul></li><li><strong>activityTypeId = 27</strong><ul><li>3999 → 메시지가 수락되지 않음</li><li>3001 → 가득 참</li><li>3004 → 시간 초과 발생</li><li>4003 → 실패</li><li>4002 → 메시지가 너무 큼</li><li>→ 정책 위반</li><li>4999 → 일시적 실패</li><li>9999 → 잘못된 응답 수신</li><li>* → 소프트 바운스에 대한 알 수 없는 이유</li></ul></li></ul> | 8, 27 | `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |  |
| `attributes.Details` |  | `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |  |
| `attributes.Email` |  | `directMarketing.email` | `directMarketing.email` |  |
| `attributes.Is Mobile Device` |  | `device.isMobileDevice` | `device.isMobileDevice` |  |
| `attributes.device` |  | `device.model` | `device.model` |  |
| `attributes.Platform` |  | `environment.operatingSystem` | `environment.operatingSystem` |  |
| `attributes.Link` |  | `directMarketing.linkURL` | `directMarketing.linkURL` |  |
| activityTypeId = 3 else attributes.Link ID인 경우 primaryAttributeValueId | 3 | `iif(${web\\.webInteraction\\.linkID} != null && ${web\\.webInteraction\\.linkID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.webInteraction\\.linkID}, \"sourceKey\", concat(${web\\.webInteraction\\.linkID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.webInteraction.webInteractionKey` |  |
| activityTypeId = 2 else attributes.Webform ID인 경우 primaryAttributeValueId | 2 | `iif(${web\\.fillOutForm\\.webFormID} != null && ${web\\.fillOutForm\\.webFormID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.fillOutForm\\.webFormID}, \"sourceKey\", concat(${web\\.fillOutForm\\.webFormID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.fillOutForm.webFormKey` |  |
| activityTypeId = 2 또는 null인 경우 primaryAttributeValueId | 2 | `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |  |
| activityTypeId = 3 else attributes.Link인 경우 primaryAttributeValueId | 3 | `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |  |
| `attributes.Change Value` | 22 | `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |  |
| `attributes.New Value` | 22 | `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |  |
| `attributes.Old Value` | 22 | `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |  |
| `attributes.Priority` | 22 | `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |  |
| `attributes.Reason` | 22 | `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |  |
| `attributes.Relative Score` | 22 | `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |  |
| `attributes.Relative Urgency` | 22 | `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |  |
| activityTypeId = 22일 때 primaryAttributeValueId | 22 | `iif(${leadOperation\.changeScore\.scoreAttributeID} != null && ${leadOperation\.changeScore\.scoreAttributeID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeScore\.scoreAttributeID}, "sourceKey", concat(${leadOperation\.changeScore\.scoreAttributeID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeScore.scoreAttributeKey` |  |
| activityTypeId = 22일 때 primaryAttributeValueId | 22 | `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |  |
| `attributes.Urgency` | 22 | `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |  |
| `attributes.Data Value Changes` |  | `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |  |
| activityTypeId = 104일 때 primaryAttributeValueId | 104 | `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |  |
| `attributes.Acquired By` | 104 | `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |  |
| `attributes.Success` | 104 | `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |  |
| `attributes.New Status ID` | 104 | `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |  |
| `attributes.New Status` | 104 | `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |  |
| `attributes.Old Status ID` | 104 | `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |  |
| `attributes.Old Status` | 104 | `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |  |
| `attributes.Reason` | 104 | `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |  |
| `attributes.Date` | 46 | `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |  |
| `attributes.Description` | 46 | `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |  |
| `attributes.Source` | 46 | `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |  |
| activityTypeId = 46인 경우 primaryAttributeValue | 46 | `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |  |
| activityTypeId = 110인 경우 primaryAttributeValueId | 110 | `iif(${leadOperation\\.callWebhook\\.webhookID} != null && ${leadOperation\\.callWebhook\\.webhookID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.callWebhook\\.webhookID}, \"sourceKey\", concat(${leadOperation\\.callWebhook\\.webhookID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.callWebhook.webhookKey` |  |
| activityTypeId = 110인 경우 primaryAttributeValueId | 110 | `leadOperation.callWebhook.webhookName` | `leadOperation.callWebhook.webhookName` |  |
| `attributes.Error Type` | 110 | `leadOperation.callWebhook.responseCode` | `leadOperation.callWebhook.responseCode` |  |
| activityTypeId = 115인 경우 primaryAttributeValueId | 115 | `iif(${leadOperation\\.changeCampaignCadence\\.campaignID} != null && ${leadOperation\\.changeCampaignCadence\\.campaignID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.changeCampaignCadence\\.campaignID}, \"sourceKey\", concat(${leadOperation\\.changeCampaignCadence\\.campaignID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeCampaignCadence.campaignKey` |  |
| `attributes.New Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.newCadence` | `leadOperation.changeCampaignCadence.newCadence` |  |
| `attributes.Previous Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.previousCadence` | `leadOperation.changeCampaignCadence.previousCadence` |  |
| activityTypeId = 114일 때 primaryAttributeValueId | 113 | `iif(${leadOperation\.addToCampaign\.campaignID} != null && ${leadOperation\.addToCampaign\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.campaignID}, "sourceKey", concat(${leadOperation\.addToCampaign\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.campaignKey` |  |
| `attributes.Track ID` | 113 | `iif(${leadOperation\.addToCampaign\.streamID} != null && ${leadOperation\.addToCampaign\.streamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.streamID}, "sourceKey", concat(${leadOperation\.addToCampaign\.streamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.streamKey` |  |
| `attributes.Stream Name` | 113 | `leadOperation.addToCampaign.streamName` | `leadOperation.addToCampaign.streamName` |  |
| activityTypeId = 115인 경우 primaryAttributeValueId | 115 | `iif(${leadOperation\.changeCampaignStream\.campaignID} != null && ${leadOperation\.changeCampaignStream\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.campaignID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.campaignKey` |  |
| `attributes.New Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.newStreamID} != null && ${leadOperation\.changeCampaignStream\.newStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.newStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.newStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.newStreamKey` |  |
| `attributes.New Track Name` | 115 | `leadOperation.changeCampaignStream.newStreamName` | `leadOperation.changeCampaignStream.newStreamName` |  |
| `attributes.Previous Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.previousStreamID} != null && ${leadOperation\.changeCampaignStream\.previousStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.previousStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.previousStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.previousStreamKey` |  |
| `attributes.Previous Stream Name` | 115 | `leadOperation.changeCampaignStream.previousStreamName` | `leadOperation.changeCampaignStream.previousStreamName` |  |
| activityTypeId = 101인 경우 primaryAttributeValueId | 101 | `iif(${leadOperation\.changeRevenueStage\.modelID} != null && ${leadOperation\.changeRevenueStage\.modelID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.modelID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.modelID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.modelKey` |  |
| activityTypeId = 101인 경우 primaryAttributeValueId | 101 | `leadOperation.changeRevenueStage.modelName` | `leadOperation.changeRevenueStage.modelName` |  |
| `attributes.New Stage ID` | 101 | `iif(${leadOperation\.changeRevenueStage\.newStageID} != null && ${leadOperation\.changeRevenueStage\.newStageID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.newStageID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.newStageID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.newStageKey` |  |
| `attributes.New Stage` | 101 | `leadOperation.changeRevenueStage.newStageName` | `leadOperation.changeRevenueStage.newStageName` |  |
| `attributes.Old Stage ID` | 101 | `iif(${leadOperation\\.changeRevenueStage\\.previousStageID} != null && ${leadOperation\\.changeRevenueStage\\.previousStageID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${leadOperation\\.changeRevenueStage\\.previousStageID}, \"sourceKey\", concat(${leadOperation\\.changeRevenueStage\\.previousStageID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeRevenueStage.previousStageKey` |  |
| `attributes.Old Stage` | 101 | `leadOperation.changeRevenueStage.previousStageName` | `leadOperation.changeRevenueStage.previousStageName` |  |
| `attributes.Reason` | 101 | `leadOperation.changeRevenueStage.reason` | `leadOperation.changeRevenueStage.reason` |  |
| activityTypeId = 32인 경우 `attributes.Merge IDs` | 32 | `json_to_object(${leadOperation\.mergeLeads\.mergeIDs})` | `leadOperation.mergeLeads.sourceKeys` |  |
| `attributes.Master Updated` | 32 | `leadOperation.mergeLeads.targetUpdated` | `leadOperation.mergeLeads.targetUpdated` |  |
| `attributes.Merged in Sales` | 32 | `leadOperation.mergeLeads.mergedInCRM` | `leadOperation.mergeLeads.mergedInCRM` |  |
| `attributes.Merge Source` | 32 | `leadOperation.mergeLeads.mergeSource` | `leadOperation.mergeLeads.mergeSource` |  |
| activityTypeId = 6일 때 primaryAttributeValueId | 6 | `iif(${directMarketing\.emailSent\.mailingID} != null && ${directMarketing\.emailSent\.mailingID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${directMarketing\.emailSent\.mailingID}, "sourceKey", concat(${directMarketing\.emailSent\.mailingID},"@${MUNCHKIN_ID}.Marketo")), null)` | `directMarketing.emailSent.mailingKey` |  |
| activityTypeId = 6일 때 primaryAttributeValueId | 6 | `directMarketing.emailSent.mailingName` | `directMarketing.emailSent.mailingName` |  |
| `attributes.Test Variant` | 6 | `directMarketing.emailSent.testVariantID` | `directMarketing.emailSent.testVariantID` |  |
| 참고 - 보조 에셋 값에서 파생 |  | `directMarketing.emailSent.testVariantName` | `directMarketing.emailSent.testVariantName` |  |
| `attributes.Campaign Run ID` | 6 | `directMarketing.emailSent.automationRunID` | `directMarketing.emailSent.automationRunID` |  |
|  |  | `directMarketing.automationRunID` | `directMarketing.automationRunID` |  |

{style="table-layout:auto"}

## 프로그램 {#programs}

XDM 클래스에 대한 자세한 내용은 [XDM 비즈니스 캠페인 개요](../../../../xdm/classes/b2b/business-campaign.md)를 참조하십시오. XDM 필드 그룹에 대한 자세한 내용은 [비즈니스 캠페인 세부 정보 스키마 필드 그룹](../../../../xdm/field-groups/b2b-campaign/details.md) 안내서를 참조하십시오.

>[!NOTE]
>
>사용자 지정 태그 유형의 경우 스키마로 이동하여 새 필드 그룹을 만듭니다. 그런 다음 소스 필드를 대상 XDM 필드와 매핑하는 데 필요한 모든 추가 필드 이름을 추가합니다.

| Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `"Marketo"` | `campaignKey.sourceType` |  |
| `channel` | `channelName` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `cost` | `actualCost.amount` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `description` | `campaignDescription` |  |
| `endDate` | `campaignEndDate` |  |
| `id` | `campaignKey.sourceID` |  |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |  |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`은(는) 보조 ID입니다. CRM_TYPE 및 CRM_ORG_ID가 탐색 API의 일부로 대체됩니다. |
| `integrationPartner` | `integrationPartnerName` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `name` | `campaignName` |  |
| `startDate` | `campaignStartDate` |  |
| `status` | `campaignStatus` |  |
| `type` | `campaignType` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |  |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |  |
| `webinarSessionDescription` | `webinarSessionDescription` |  |
| `webinarSessionName` | `webinarSessionName` |  |

{style="table-layout:auto"}

## 프로그램 멤버십 {#program-memberships}

XDM 클래스에 대한 자세한 내용은 [XDM 비즈니스 캠페인 멤버 개요](../../../../xdm/classes/b2b/business-campaign-members.md)를 참조하십시오. XDM 필드 그룹에 대한 자세한 내용은 [XDM 비즈니스 캠페인 멤버 세부 정보 스키마 필드 그룹](../../../../xdm/field-groups/b2b-campaign-members/details.md) 안내서를 참조하십시오.

| Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `id` | `campaignMemberKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | 관계 |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 관계 |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |  |
| `reachedSuccess` | `hasReachedSuccess` |  |
| `isExhausted` | `isExhausted` |  |
| `statusName` | `memberStatus` |  |
| `statusReason` | `memberStatusReason` |  |
| `membershipDate` | `membershipDate` |  |
| `nurtureCadence` | `nurtureCadence` |  |
| `trackName` | `nurtureTrackName` |  |
| `webinarUrl` | `webinarConfirmationUrl` |  |
| `registrationCode` | `webinarRegistrationID` |  |
| `reachedSuccessDate` | `reachedSuccessDate` |  |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`은(는) 보조 ID입니다. CRM_TYPE 및 CRM_ORG_ID가 탐색 API의 일부로 대체됩니다. |
| `sfdc.lastStatus` | `lastStatus` |  |
| `sfdc.hasResponded` | `hasResponded` |  |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 회사 {#companies}

XDM 클래스에 대한 자세한 내용은 [XDM 비즈니스 계정 개요](../../../../xdm/classes/b2b/business-account.md)를 참조하십시오.

| Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` | |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` | |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| <ul><li><code>iif(mktoCdpExternalId != null &amp;&amp; mktoCdpExternalId != &quot;&quot;, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, mktoCdpExternalId, &quot;sourceKey&quot;, concat(mktoCdpExternalId,&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(msftCdpExternalId != null &amp;&amp; msftCdpExternalId != &quot;&quot;, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, msftCdpExternalId, &quot;sourceKey&quot;, concat(msftCdpExternalId,&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`은(는) 보조 ID입니다. CRM_ORG_ID 및 CRM_TYPE이 탐색 API의 일부로 대체됩니다. |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |
| `billingCity` | `accountBillingAddress.city` | |
| `billingCountry` | `accountBillingAddress.country` | |
| `billingPostalCode` | `accountBillingAddress.postalCode` | |
| `billingState` | `accountBillingAddress.state` | |
| `billingStreet` | `accountBillingAddress.street1` | |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` | |
| `sicCode` | `accountOrganization.SICCode` | |
| `industry` | `accountOrganization.industry` | |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` | |
| `website` | `accountOrganization.website` | |
| `mainPhone` | `accountPhone.number` | |
| `company` | `accountName` | |
| `companyNotes` | `accountDescription` | |
| `site` | `accountSite` | |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` | |
| `marketoIsDeleted` | `isDeleted` | |

{style="table-layout:auto"}

## 정적 목록 {#static-lists}

XDM 클래스에 대한 자세한 내용은 [XDM 비즈니스 마케팅 목록 개요](../../../../xdm/classes/b2b/business-marketing-list.md)를 참조하십시오.

| Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `id` | `marketingListKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `name` | `marketingListName` |  |
| `description` | `marketingListDescription` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 정적 목록 멤버십 {#static-list-memberships}

XDM 클래스에 대한 자세한 내용은 [XDM 비즈니스 마케팅 목록 멤버 개요](../../../../xdm/classes/b2b/business-marketing-list-members.md)를 참조하십시오.

| Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |  |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | 관계 |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 관계 |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 명명된 계정 {#named-accounts}

>[!IMPORTANT]
>
>명명된 계정 데이터 세트는 Marketo의 계정 기반 마케팅(ABM) 기능에만 필요합니다. ABM을 사용하지 않는 경우에는 명명된 계정에 대한 매핑을 설정할 필요가 없습니다.

XDM 클래스에 대한 자세한 내용은 [XDM 비즈니스 계정 개요](../../../../xdm/classes/b2b/business-account.md)를 참조하십시오.

| Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |  |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`은(는) 보조 ID입니다. CRM_TYPE 및 CRM_ORG_ID가 탐색 API의 일부로 대체됩니다. |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `city` | `accountBillingAddress.city` |  |
| `country` | `accountBillingAddress.country` |  |
| `state` | `accountBillingAddress.state` |  |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |  |
| `sicCode` | `accountOrganization.SICCode` |  |
| `industry` | `accountOrganization.industry` |  |
| `logoUrl` | `accountOrganization.logoUrl` |  |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |  |
| `name` | `accountName` |  |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |  |
| `sourceType` | `accountSourceType` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 기회 {#opportunities}

XDM 클래스에 대한 자세한 내용은 [XDM 비즈니스 영업 기회 개요](../../../../xdm/classes/b2b/business-opportunity.md)를 참조하십시오.

| Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `id` | `opportunityKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`은(는) 보조 ID입니다. CRM_TYPE 및 CRM_ORG_ID가 탐색 API의 일부로 대체됩니다. |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | 관계 |
| `description` | `opportunityDescription` |  |
| `name` | `opportunityName` |  |
| `stage` | `opportunityStage` |  |
| `type` | `opportunityType` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `expectedRevenue` | `expectedRevenue.amount` |  |
| `amount` | `opportunityAmount.amount` |  |
| `closeDate` | `expectedCloseDate` |  |
| `fiscalQuarter` | `fiscalQuarter` |  |
| `fiscalYear` | `fiscalYear` |  |
| `forecastCategory` | `forecastCategory` |  |
| `forecastCategoryName` | `forecastCategoryName` |  |
| `isClosed` | `isClosed` |  |
| `isWon` | `isWon` |  |
| `quantity` | `opportunityQuantity` |  |
| `probability` | `probabilityPercentage` |  |
| `iif(mktoCdpSourceCampaignId != null && mktoCdpSourceCampaignId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpSourceCampaignId, "sourceKey", concat(mktoCdpSourceCampaignId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Salesforce 통합 사용 고객 전용 |
| `lastActivityDate` | `lastActivityDate` |  |
| `leadSource` | `leadSource` |  |
| `nextStep` | `nextStep` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 영업 기회 연락처 역할 {#opportunity-contact-roles}

XDM 클래스에 대한 자세한 내용은 [XDM 비즈니스 영업 기회 사용자 관계 개요](../../../../xdm/classes/b2b/business-account-person-relation.md)를 참조하십시오.

| Source 데이터 세트 | XDM 타겟 필드 | 참고 |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `"Marketo"` | `opportunityPersonKey.sourceType` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityPersonKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `id` | `opportunityPersonKey.sourceID` |  |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 관계 |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | 관계 |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`은(는) 보조 ID입니다. CRM_TYPE 및 CRM_ORG_ID가 탐색 API의 일부로 대체됩니다. |
| `isPrimary` | `isPrimary` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `role` | `personRole` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |

{style="table-layout:auto"}

## 개인 {#persons}

XDM 클래스에 대한 자세한 내용은 [XDM 개별 프로필 개요](../../../../xdm/classes/individual-profile.md)를 참조하십시오. XDM 필드 그룹에 대한 자세한 내용은 [XDM 비즈니스 사용자 세부 정보 스키마 필드 그룹](../../../../xdm/field-groups/profile/business-person-details.md) 안내서 및 [XDM 비즈니스 사용자 구성 요소 스키마 필드 그룹](../../../../xdm/field-groups/profile/business-person-components.md) 안내서를 참조하십시오.

| 소스 필드 | 타겟 XDM 필드 | 참고 |
|---|---|---|
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `"Marketo"` | `b2b.personKey.sourceType` | |
| `address` | `workAddress.street1` | |
| `city` | `workAddress.city` | |
| `company` | `organizations` | |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | 기본 ID. MUNCHKIN_ID는 explore API의 일부로 대체됩니다. |
| `country` | `workAddress.country` | |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `dateOfBirth` | `person.birthDate` | |
| `email` | `personComponents.workEmail.address` | |
| `email` | `workEmail.address` | |
| `fax` | `faxPhone.number` | |
| `firstName` | `person.name.firstName` | |
| `id` | `b2b.personKey.sourceID` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` | |
| <ul><li><code>iif(decode(sfdcType, &quot;연락처&quot;, sfdcContactId, &quot;리드&quot;, sfdcLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;,&quot;sourceID&quot;, decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null), &quot;sourceKey&quot;, concat(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;,&quot;sourceID&quot;, decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null), &quot;sourceKey&quot;, concat(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `personComponents.sourceExternalKey` | |
| <ul><li><code>iif(decode(sfdcType, &quot;연락처&quot;, sfdcContactId, &quot;리드&quot;, sfdcLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;,&quot;sourceID&quot;, decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null), &quot;sourceKey&quot;, concat(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;,&quot;sourceID&quot;, decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null), &quot;sourceKey&quot;, concat(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`은(는) 보조 ID입니다. |
| `iif(ecids != null, to_object('ECID',arrays_to_objects('id',explode(ecids))), null)` | `identityMap` | 계산된 필드입니다. |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` | |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.convertedContactKey` | 계산된 필드입니다. |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceConvertedContactKey` | 계산된 필드입니다. |
| `iif(unsubscribed == 'true', 'n', 'y' )` | `consents.marketing.email.val` | 구독 취소가 true(즉, 값 = 1)인 경우 consents.marketing.email.val을 &quot;n&quot;으로 설정합니다. 구독 취소가 false인 경우(즉, 값 = 0) consents.marketing.email.val을 null로 설정합니다. |
| `iif(unsubscribedReason != null && unsubscribedReason != "", substr(unsubscribedReason, 0, 100), null)` | `consents.marketing.email.reason` | |
| `lastName` | `person.name.lastName` | |
| `leadPartitionId` | `b2b.personGroupID` | |
| `leadPartitionId` | `personComponents.personGroupID` | |
| `leadScore` | `b2b.personScore` | |
| `leadScore` | `personComponents.personScore` | |
| `leadSource` | `b2b.personSource` | |
| `leadSource` | `personComponents.personSource` | |
| `leadStatus` | `b2b.personStatus` | |
| `leadStatus` | `personComponents.personStatus` | |
| `marketingSuspended` | `b2b.isMarketingSuspended` | |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` | |
| `marketoIsDeleted` | `isDeleted` | |
| `middleName` | `person.name.middleName` | |
| `mktoCdpConvertedDate` | `b2b.convertedDate` | |
| `mktoCdpIsConverted` | `b2b.isConverted` | |
| `mobilePhone` | `mobilePhone.number` | |
| `personType` | `b2b.personType` | |
| `personType` | `personComponents.personType` | |
| `phone` | `workPhone.number` | |
| `postalCode` | `workAddress.postalCode` | |
| `salutation` | `person.name.courtesyTitle` | |
| `state` | `workAddress.state` | |
| `title` | `extendedWorkDetails.jobTitle` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |

{style="table-layout:auto"}

## 다음 단계

이 문서를 읽고 [!DNL Marketo] 데이터 세트와 해당 XDM 필드 간의 매핑 관계에 대한 insight을 얻었습니다. [&#x200B; 데이터 흐름을 완료하려면  [!DNL Marketo] 원본 연결 만들기](../../../tutorials/ui/create/adobe-applications/marketo.md)2&rbrace;에 대한 자습서를 참조하십시오.[!DNL Marketo]