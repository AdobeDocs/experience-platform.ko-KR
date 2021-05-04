---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마 디자인;mixin;person details;profile person details;person
solution: Experience Platform
title: 인구 통계 세부 정보 혼합
topic-legacy: overview
description: 이 문서에서는 인구 통계 세부 사항 혼합에 대한 개요를 제공합니다.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: 87b638df8a3b27fb6df5dee60b57d817d5e34a80
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---

# [!UICONTROL Demographic Details] 믹싱

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL Demographic Details] 는 클래스의 표준  [[!DNL XDM Individual Profile] 혼합입니다](../../classes/individual-profile.md). 혼합은 루트 레벨 `person` 객체를 제공하며 하위 필드에는 개별 사용자에 대한 정보가 설명되어 있습니다.

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `person.name` | [사람 이름](../../data-types/person-name.md) | 하위 필드에서 사람 이름의 다양한 요소를 설명하는 객체입니다. |
| `person.birthDate` | 날짜 | ISO 8601 타임스탬프 형식의 개인 출생일 |
| `person.birthDayAndMonth` | 문자열 | MM-DD 형식으로 사람이 태어난 날과 달. 이 필드는 출생일 및 월을 알고 있을 때는 사용해야 하지만, 해는 그렇지 않다. |
| `person.birthYear` | 정수 | 세기(예: 1989년)를 포함하여 사람이 태어난 연도. 이 필드는 전체 생년월일이 아닌 사용자의 연령만을 알 때 사용해야 합니다. |
| `person.gender` | 문자열 | 사람의 성 ID. |
| `person.martialStatus` | 문자열 | 중요한 다른 사람과의 관계에 대해 설명합니다. |
| `person.nationality` | 문자열 | ISO 3166-1 Alpha-2 코드를 사용하여 나타나는 사람과 상태 간의 법적 관계. |
| `person.taxId` | 문자열 | 미국의 TIN 또는 스페인의 CIF/NIF와 같은 개인의 세금/재정 ID. |

혼합에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)
