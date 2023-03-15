---
title: XDM 비즈니스 캠페인 멤버 세부 정보 스키마 필드 그룹
description: 이 문서에서는 XDM 비즈니스 캠페인 멤버 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# [!UICONTROL XDM 비즈니스 캠페인 멤버 세부 정보] 스키마 필드 그룹

[!UICONTROL XDM 비즈니스 캠페인 멤버 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!UICONTROL XDM 비즈니스 캠페인 멤버] 클래스](../../classes/b2b/business-campaign-members.md)비즈니스 캠페인에 대한 자세한 정보를 캡처합니다.

![UI에 표시되는 XDM 비즈니스 캠페인 멤버 세부 정보 필드 그룹의 구조](../../images/field-groups/b2b/business-campaign-member-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 해당 캠페인 구성원을 획득한 캠페인의 복합 ID. |
| `acquiredByCampaignID` | [!UICONTROL 문자열] | 해당 캠페인 구성원을 획득한 캠페인에 대한 문자열 식별자. |
| `firstRespondedDate` | [!UICONTROL DateTime] | 개인이 캠페인에 처음 응답한 시간의 ISO 8601 타임스탬프. |
| `hasReachedSuccess` | [!UICONTROL 부울] | 이 캠페인 멤버가 정상적으로 전환되었는지 여부를 나타냅니다. |
| `hasResponded` | [!UICONTROL 부울] | 이 캠페인 멤버가 캠페인에 응답했는지 여부를 나타냅니다. |
| `isDeleted` | [!UICONTROL 부울] | Marketo Engage 시 이 캠페인 멤버가 삭제되었는지 여부를 나타냅니다.<br><br>사용 시 [Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md), Marketo에서 삭제된 모든 레코드는 실시간 고객 프로필에 자동으로 반영됩니다. 그러나 이러한 프로필과 관련된 레코드가 데이터 레이크에 계속 남아 있을 수 있습니다. 설정별 `isDeleted` 끝 `true`, 필드를 사용하여 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필터링할 수 있습니다. |
| `isExhausted` | [!UICONTROL 부울] | 이 캠페인 멤버가 모든 캠페인 상호 작용을 소진했는지 여부를 나타냅니다. |
| `lastStatus` | [!UICONTROL 문자열] | 캠페인 멤버의 마지막 상태입니다. |
| `memberStatus` | [!UICONTROL 문자열] | 캠페인 멤버의 현재 상태. |
| `memberStatusReason` | [!UICONTROL 문자열] | 캠페인 멤버의 현재 상태에 대한 설명. |
| `membershipDate` | [!UICONTROL DateTime] | 캠페인 멤버의 현재 상태에 대한 설명. |
| `nurtureCadence` | [!UICONTROL 문자열] | 캠페인 멤버에게 표시될 캠페인 관련 정보의 시간 간격을 나타냅니다. |
| `nurtureTrackName` | [!UICONTROL 문자열] | 이 캠페인 멤버에게 적용되는 육성 프로그램의 이름. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | 캠페인 멤버가 성공적으로 전환된 시점의 ISO 8601 타임스탬프. |
| `webinarConfirmationUrl` | [!UICONTROL 문자열] | 캠페인 멤버에 대한 웨비나 확인 URL입니다. |
| `webinarRegistrationID` | [!UICONTROL 문자열] | 캠페인 멤버에 대한 웨비나 등록 ID. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
