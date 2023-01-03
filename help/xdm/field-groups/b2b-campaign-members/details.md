---
title: XDM 비즈니스 캠페인 구성원 세부 정보 스키마 필드 그룹
description: 이 문서에서는 XDM 비즈니스 캠페인 구성원 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 캠페인 구성원 세부 정보] 스키마 필드 그룹

[!UICONTROL XDM 비즈니스 캠페인 구성원 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!UICONTROL XDM 비즈니스 캠페인 구성원] 클래스](../../classes/b2b/business-campaign-members.md)- 비즈니스 캠페인에 대한 자세한 정보를 캡처합니다.

![XDM 비즈니스 캠페인 구성원 세부 정보 필드 그룹의 구조가 UI에 표시되는 것입니다](../../images/field-groups/b2b/business-campaign-member-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 이 캠페인 구성원을 획득한 캠페인의 복합 ID입니다. |
| `acquiredByCampaignID` | [!UICONTROL 문자열] | 이 캠페인 구성원을 획득한 캠페인의 문자열 식별자입니다. |
| `firstRespondedDate` | [!UICONTROL DateTime] | 개인이 캠페인에 처음 응답한 ISO 8601 타임스탬프입니다. |
| `hasReachedSuccess` | [!UICONTROL 부울] | 이 캠페인 구성원이 성공적으로 전환되었는지 여부를 나타냅니다. |
| `hasResponded` | [!UICONTROL 부울] | 이 캠페인 구성원이 캠페인에 응답했는지 여부를 나타냅니다. |
| `isDeleted` | [!UICONTROL 부울] | 이 캠페인 구성원이 Marketo Engage에서 삭제되었는지 여부를 나타냅니다.<br><br>를 사용할 때 [Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md)를 입력하면 Marketo에서 삭제된 모든 레코드가 실시간 고객 프로필에 자동으로 반영됩니다. 그러나 이러한 프로필과 관련된 레코드는 여전히 Data Lake에서 유지됩니다. 설정 `isDeleted` to `true`, 필드를 사용하여 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필터링할 수 있습니다. |
| `isExhausted` | [!UICONTROL 부울] | 이 캠페인 구성원이 모든 캠페인 상호 작용을 지쳤는지 여부를 나타냅니다. |
| `lastStatus` | [!UICONTROL 문자열] | 캠페인 구성원의 마지막 상태입니다. |
| `memberStatus` | [!UICONTROL 문자열] | 캠페인 구성원의 현재 상태입니다. |
| `memberStatusReason` | [!UICONTROL 문자열] | 캠페인 구성원의 현재 상태 이면에 대한 이유입니다. |
| `membershipDate` | [!UICONTROL DateTime] | 캠페인 구성원의 현재 상태 이면에 대한 이유입니다. |
| `nurtureCadence` | [!UICONTROL 문자열] | 캠페인 구성원에게 제공할 캠페인 관련 정보에 대한 시간 간격. |
| `nurtureTrackName` | [!UICONTROL 문자열] | 이 캠페인 구성원이 대상으로 하는 교육 프로그램의 이름입니다. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | 캠페인 멤버에 대해 성공적으로 변환이 수행된 시기에 대한 ISO 8601 타임스탬프입니다. |
| `webinarConfirmationUrl` | [!UICONTROL 문자열] | 캠페인 구성원의 웨비나 확인 URL입니다. |
| `webinarRegistrationID` | [!UICONTROL 문자열] | 캠페인 구성원의 웨비나 등록 ID입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
