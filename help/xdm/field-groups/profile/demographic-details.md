---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;개인;개인 세부 정보;프로필 개인 세부 정보;개인;
solution: Experience Platform
title: 인구 통계 세부 정보 스키마 필드 그룹
description: 이 문서에서는 인구 통계 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 4%

---


# [!UICONTROL 인구 통계 세부 정보] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 다음 문서를 참조하십시오. [필드 그룹 이름 업데이트](../name-updates.md) 추가 정보.

[!UICONTROL 인구 통계 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md). 필드 그룹은 루트 수준을 제공합니다 `person` 개체입니다. 하위 필드에서 개별 개인에 대한 정보를 설명합니다.

![](../../images/field-groups/demographic-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `person.name` | [개인 이름](../../data-types/person-name.md) | 하위 필드에서 개인 이름의 여러 요소를 설명하는 개체입니다. |
| `person.birthDate` | 날짜 | ISO 8601 타임스탬프 형식의 개인이 태어난 전체 날짜입니다. |
| `person.birthDayAndMonth` | 문자열 | MM-DD 형식으로 사람이 태어난 날과 달입니다. 이 필드는 출생일 또는 출생일이 알려지는 때에 사용해야 하지만, 연도에는 사용하지 않아야 합니다. |
| `person.birthYear` | 정수 | 세기를 포함한 사람이 태어난 해(예: 1989년)입니다. 이 필드는 전체 생년월일이 아닌 연령 만 알려진 경우에 사용해야 합니다. |
| `person.gender` | 문자열 | 사람의 성별 ID. |
| `person.martialStatus` | 문자열 | 중요한 다른 사람과의 관계에 대해 설명합니다. |
| `person.nationality` | 문자열 | ISO 3166-1 Alpha-2 코드를 사용하여 표시되는 개인 및 해당 상태 간의 법적 관계. |
| `person.taxId` | 문자열 | 미국의 TIN 또는 스페인의 CIF/NIF와 같은 개인의 세금/회계 ID입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)