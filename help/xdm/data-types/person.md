---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;개인;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 개인 데이터 유형
description: 이 문서에서는 XDM(Person Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 4%

---

# [!UICONTROL 개인] 데이터 유형

[!UICONTROL 개인] 는 개별 개인을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다. 이 데이터 유형은 고객, 연락처 또는 소유자와 같은 다양한 역할에 따라 활동하는 사람을 나타낼 수 있습니다.

<img src="../images/data-types/person.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `name` | [[!UICONTROL 개인 이름]](./person-name.md) | 개인의 전체 이름에 대한 세부 사항을 설명합니다. |
| `birthDate` | 날짜 | 한 사람이 태어난 그 전체 날짜. 날짜 형식(시간 없이)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `birthDayAndMonth` | 문자열 | MM-DD 형식으로 사람이 태어난 날과 달입니다. 이 필드는 출생일 또는 출생일이 알려지는 때에 사용해야 하지만, 연도에는 사용하지 않아야 합니다. 이 속성의 형식은 이 정규식을 준수해야 합니다 `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | 정수 | 세기를 포함한 개인이 태어난 연도(예: `1983`). 이 필드는 만 알고 있을 때 전체 생년월일이 아닌 경우에 사용해야 합니다. 이 값은 1에서 32767 사이여야 합니다. |
| `gender` | 문자열 | 사람의 성별 ID. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 이 값의 기본값은 입니다. `not_specified`. |
| `maritalStatus` | 문자열 | 중요한 다른 사람과의 관계에 대해 설명합니다. 이 속성의 값은 다음 열거형 값 중 하나와 같아야 합니다. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 이 값의 기본값은 입니다. `not_specified`. |
| `nationality` | 문자열 | ISO 3166-1 Alpha-2 코드를 사용하여 표시되는 개인 및 해당 상태 간의 법적 관계. 이 속성의 형식은 이 정규식을 준수해야 합니다 `^[A-Z]{2}$`. |
| `taxId` | 문자열 | 미국의 납세자 식별 번호(TIN) 또는 스페인의 CIF/NIF(Certificado de Identificación Fishance)와 같은 개인의 세금 또는 회계 ID입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
