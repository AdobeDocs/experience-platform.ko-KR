---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: 인구 통계 세부 정보 혼합
topic: overview
description: 이 문서에서는 인구 통계 세부 사항 혼합에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 3%

---


# [!UICONTROL 인구 통계 세부] 정보 혼합

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트에](../name-updates.md) 대한 문서를 참조하십시오.

[!UICONTROL 인구 통계 세부 사항] 은 [[!DNL XDM Individual Profile] 학급](../../classes/individual-profile.md)표준이다. 이 혼합물은 루트 수준 개체를 제공하며, 이 하위 필드는 개별 사용자에 대한 정보를 설명합니다. `person`

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `person.name` | [사람 이름](../../data-types/person-name.md) | 사람 이름의 다양한 요소를 설명하는 하위 필드가 있는 개체. |
| `person.birthDate` | 날짜 | ISO 8601 타임스탬프 형식으로 태어난 사람의 전체 날짜입니다. |
| `person.birthDayAndMonth` | 문자열 | MM-DD 형식으로 사람이 태어난 날과 월 이 필드는 출생일의 요일과 달이 알려지는 때에 사용해야 하지만, 연도에는 사용하지 말아야 합니다. |
| `person.birthYear` | 정수 | 세기(예: 1989년)를 포함하여 사람이 태어난 연도. 이 필드는 생년월일이 아닌 연령만 알고 있을 때 사용해야 합니다. |
| `person.gender` | 문자열 | 사람의 성 ID. |
| `person.martialStatus` | 문자열 | 중요한 다른 사람과의 관계에 대해 설명합니다. |
| `person.nationality` | 문자열 | ISO 3166-1 Alpha-2 코드를 사용하여 나타나는 사람과 상태 간의 법적 관계. |
| `person.taxId` | 문자열 | 미국의 TIN 또는 스페인의 CIF/NIF와 같은 개인의 세금/재정 ID. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)오