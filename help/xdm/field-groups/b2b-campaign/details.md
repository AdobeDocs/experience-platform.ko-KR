---
title: XDM 비즈니스 캠페인 세부 정보 스키마 필드 그룹
description: XDM 비즈니스 캠페인 세부 사항 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# [!UICONTROL XDM 비즈니스 캠페인 세부 정보] 스키마 필드 그룹

[!UICONTROL XDM 비즈니스 캠페인 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!UICONTROL XDM 비즈니스 캠페인] 클래스](../../classes/b2b/business-campaign.md)비즈니스 캠페인에 대한 자세한 정보를 캡처합니다.

![UI에 표시되는 XDM 비즈니스 캠페인 세부 정보 필드 그룹의 구조](../../images/field-groups/b2b/business-campaign-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL 통화]](../../data-types/currency.md) | 비즈니스 캠페인의 실제 비용을 나타냅니다. |
| `budgetedCost` | [[!UICONTROL 통화]](../../data-types/currency.md) | 비즈니스 캠페인의 예산 비용을 나타냅니다. |
| `expectedRevenue` | [[!UICONTROL 통화]](../../data-types/currency.md) | 비즈니스 캠페인이 창출할 것으로 예상되는 매출을 나타냅니다. |
| `parentCampaignKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 상위 캠페인에 대한 합성 ID(해당하는 경우). |
| `campaignEndDate` | [!UICONTROL DateTime] | 캠페인이 종료되거나 종료될 시점의 ISO 8601 타임스탬프. |
| `campaignProgressionName` | [!UICONTROL 문자열] | 캠페인 진행률 이름. |
| `campaignStartDate` | [!UICONTROL DateTime] | 캠페인이 시작되거나 시작될 때의 ISO 8601 타임스탬프입니다. |
| `campaignStatus` | [!UICONTROL 문자열] | 캠페인의 현재 상태입니다. |
| `channelName` | [!UICONTROL 문자열] | 이 캠페인과 연계된 채널 이름. |
| `expectedResponse` | [!UICONTROL 문자열] | 캠페인에 대한 예상 응답입니다. |
| `integrationPartnerName` | [!UICONTROL 문자열] | 이 캠페인과 통합된 파트너의 이름입니다. |
| `isActive` | [!UICONTROL 부울] | 이 캠페인이 활성 상태인지 여부를 나타냅니다. |
| `isDeleted` | [!UICONTROL 부울] | Marketo Engage 시 이 캠페인이 삭제되었는지 여부를 나타냅니다.<br><br>사용 시 [Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md), Marketo에서 삭제된 모든 레코드는 실시간 고객 프로필에 자동으로 반영됩니다. 그러나 이러한 프로필과 관련된 레코드가 데이터 레이크에 계속 남아 있을 수 있습니다. 설정별 `isDeleted` 끝 `true`, 필드를 사용하여 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필터링할 수 있습니다. |
| `lastActivityDate` | [!UICONTROL DateTime] | 캠페인과 연계된 마지막 활동의 ISO 8601 타임스탬프. |
| `timeZone` | [!UICONTROL 문자열] | 캠페인이 작동하는 시간대입니다. |
| `timeZoneDelivery` | [!UICONTROL 문자열] | 캠페인이 작동하는 게재 시간대. |
| `timeZoneName` | [!UICONTROL 문자열] | 캠페인이 작동하는 시간대의 이름입니다. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | 이 캠페인에 대한 마지막 웨비나 내역 동기화의 ISO 8601 타임스탬프. |
| `webinarHistorySyncStatus` | [!UICONTROL 문자열] | 이 캠페인에 대한 웨비나 내역 동기화 상태입니다. |
| `webinarSessionDescription` | [!UICONTROL 문자열] | 이 캠페인과 연결된 웨비나 세션에 대한 설명입니다. |
| `webinarSessionName` | [!UICONTROL 문자열] | 이 캠페인과 연결된 웨비나 세션의 이름입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
