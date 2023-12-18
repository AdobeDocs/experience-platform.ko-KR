---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;개인;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 개인 데이터 유형
description: XDM(개인 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 3%

---

# [!UICONTROL 개인] 데이터 유형

[!UICONTROL 개인] 는 개인을 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 이 데이터 유형은 고객, 연락처 또는 소유자와 같은 다양한 역할을 수행하는 사람을 나타낼 수 있습니다.

<img src="../images/data-types/person.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `name` | [[!UICONTROL 개인 이름]](./person-name.md) | 개인의 전체 이름에 대한 세부 사항을 설명합니다. |
| `birthDate` | 날짜 | 개인의 출생월일. 날짜 형식(시간 없음)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `birthDayAndMonth` | 문자열 | MM-DD 형식으로 사람이 태어난 날짜와 시간. 이 필드는 출생월일이 알려진 경우 사용해야 하지만 연도가 아닌 경우 사용해야 합니다. 이 속성의 형식은 이 정규 표현식을 준수해야 합니다 `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | 정수 | 세기가 포함된 사람이 태어난 연도(예: `1983`). 이 필드는 전체 생년월일이 아니라 개인의 연령만 알 때 사용해야 합니다. 이 값은 1에서 32767 사이여야 합니다. |
| `gender` | 문자열 | 개인의 성 정체성. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 이 값의 기본값은 입니다. `not_specified`. |
| `maritalStatus` | 문자열 | 다른 중요 인물과의 관계를 설명합니다. 이 속성의 값은 다음 열거형 값 중 하나와 같아야 합니다. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 이 값의 기본값은 입니다. `not_specified`. |
| `nationality` | 문자열 | ISO 3166-1 Alpha-2 코드를 사용하여 표시된 사용자와 해당 주 간의 법적 관계. 이 속성의 형식은 이 정규 표현식을 준수해야 합니다 `^[A-Z]{2}$`. |
| `taxId` | 문자열 | 사용자의 세금 또는 회계 ID(예: 미국의 납세자 식별 번호(TIN) 또는 스페인의 Certificado de Identificación Fiscal (CIF/NIF)). |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
