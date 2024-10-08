---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;충성도 세부 정보;스키마 디자인;필드 그룹;필드 그룹;
solution: Experience Platform
title: 충성도 세부 정보 스키마 필드 그룹
description: 충성도 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# [!UICONTROL 충성도 세부 정보] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 대한 문서를 참조하십시오.

[!UICONTROL 충성도 세부 정보]은(는) [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md)의 표준 스키마 필드 그룹입니다. 필드 그룹은 고객 충성도 프로그램에서 개인 멤버십과 관련된 정보를 캡처하는 단일 개체 유형 필드 `loyalty`을(를) 제공합니다.

![](../../images/field-groups/loyalty-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `pointsExpiration` | 오브젝트 배열 | 만료될 모든 충성도 포인트(또는 충성도 포인트 그룹)와 만료될 날짜를 나열합니다. 각 배열 항목은 다음 두 가지 속성을 포함하는 객체여야 합니다. <ul><li>`pointsExpirationDate`: 포인트가 만료되는 ISO 8601 날짜/시간입니다.</li><li>`pointsExpiring`: 연결된 만료일 현재 만료되는 포인트 잔액입니다.</li></ul> |
| `joinDate` | 날짜/시간 | 사용자가 고객 충성도 프로그램에 가입한 ISO 8601 날짜/시간입니다. |
| `loyaltyID` | 문자열 배열 | 충성도 프로그램 멤버와 연결된 충성도 프로그램 ID를 나타냅니다. |
| `points` | 더블 | 충성도 멤버의 현재 충성도 포인트 또는 포상 잔고. |
| `pointsRedeemed` | 더블 | 충성도 멤버가 구매에 지원하거나 다른 방식으로 상환한 포인트 금액. |
| `program` | 문자열 | 개인이 등록된 고객 충성도 프로그램의 이름. |
| `status` | 문자열 | 사용자의 충성도 멤버십의 현재 상태(예: `active`, `disabled` 또는 `suspended`). |
| `tier` | 문자열 | 개인이 등록된 고객 충성도 프로그램 계층을 캡처합니다. |
| `upgradeDate` | 문자열 | 충성도 멤버가 가장 최근 계층 수준으로 업그레이드된 날짜입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
