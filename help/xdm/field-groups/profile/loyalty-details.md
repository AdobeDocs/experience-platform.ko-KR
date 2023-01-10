---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;충성도 세부 사항;스키마 디자인;필드 그룹;필드 그룹;
solution: Experience Platform
title: 충성도 세부 정보 스키마 필드 그룹
description: 이 문서에서는 충성도 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 3%

---

# [!UICONTROL 충성도 세부 사항] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 다음 문서를 참조하십시오. [필드 그룹 이름 업데이트](../name-updates.md) 추가 정보.

[!UICONTROL 충성도 세부 사항] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md). 필드 그룹은 단일 객체 유형 필드를 제공합니다. `loyalty`- 고객 충성도 프로그램에서 개인 멤버십과 관련된 정보를 캡처합니다.

![](../../images/field-groups/loyalty-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `pointsExpiration` | 개체 배열 | 만료될 충성도 포인트(또는 충성도 포인트 그룹)와 만료될 날짜를 나열합니다. 각 배열 항목은 다음 두 속성을 포함하는 객체여야 합니다. <ul><li>`pointsExpirationDate`: 포인트가 만료되는 ISO 8601 날짜/시간입니다.</li><li>`pointsExpiring`: 연결된 만료 날짜 현재 만료되는 포인트 잔액.</li></ul> |
| `joinDate` | DateTime | 개인이 충성도 프로그램에 가입한 ISO 8601 날짜/시간입니다. |
| `loyaltyID` | 문자열 배열 | 충성도 프로그램 멤버와 연결된 충성도 프로그램 ID를 나타냅니다. |
| `points` | 이중 | 충성도 멤버에 대한 현재 충성도 점수 또는 포상. |
| `pointsRedeemed` | 이중 | 충성도 멤버가 구매에 적용되었거나 다른 방법으로 상환된 포인트의 양입니다. |
| `program` | 문자열 | 개인이 등록된 충성도 프로그램의 이름입니다. |
| `status` | 문자열 | 다음과 같은 개인 충성도 멤버십의 현재 상태입니다. `active`, `disabled`, 또는 `suspended`. |
| `tier` | 문자열 | 개인이 등록된 충성도 프로그램 계층을 캡처합니다. |
| `upgradeDate` | 문자열 | 충성도 멤버가 가장 최근 계층 수준으로 업그레이드된 날짜입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
