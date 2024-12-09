---
title: 데이터 유형 반복
description: XDM(반복 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---

# [!UICONTROL 반복] 데이터 형식

[!UICONTROL Repeat]은(는) 이벤트가 예약되는 시기를 설명하는 규칙 집합을 제공하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![데이터 형식 구조 반복](../../images/data-types/healthcare/reference.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 바인딩된 기간] | `boundsPeriod` | [[!UICONTROL 기간]](../healthcare/period.md) | 시작 및 종료 시간. |
| [!UICONTROL 바운드 범위] | `boundsRange` | [[!UICONTROL Range]](../healthcare/range.md) | 범위 제한. |
| [!UICONTROL 바인딩된 기간] | `boundsDuration` | [[!UICONTROL 기간]](../healthcare/duration.md) | 기간 제한. |
| [!UICONTROL Count] | `count` | 정수 | 반복 횟수입니다. 최소값은 `0`입니다. |
| [!UICONTROL 최대 개수] | `countMax` | 정수 | 반복할 최대 횟수이며 최소값은 `0`입니다. |
| [!UICONTROL 요일] | `dayOfWeek` | 문자열 배열 | 사용 가능한 날짜를 자세히 설명하는 문자열 배열입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나 이상과 같아야 합니다. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL 기간] | `duration` | 더블 | 시간 길이입니다. |
| [!UICONTROL 최대 기간] | `durationMax` | 더블 | 최대 시간 길이입니다. |
| [!UICONTROL 기간 단위] | `durationUnit` | 문자열 | 기간 단위. 이 속성의 값은 다음 알려진 열거형 값 중 하나 이상과 같아야 합니다. <li> `s`(초) </li> <li> `min`(분) </li> <li> `h`(시간별) </li> <li> `d`(일별) </li>  <li> `wk`(주별) </li> <li> `mo`(월별) </li> <li> `a`(연간)</li> |
| [!UICONTROL 빈도] | `frequency` | 더블 | 최소값이 `0`인 기간 내에 발생해야 하는 반복 횟수입니다. |
| [!UICONTROL 최대 빈도] | `frequencyMax` | 더블 | 마침표로 발생해야 하는 최대 반복 횟수이며 최소값은 `0`입니다. |
| [!UICONTROL 오프셋] | `offset` | 정수 | 이벤트까지(이전 또는 이후)의 분. |
| [!UICONTROL 기간] | `period` | 더블 | 빈도가 적용되는 기간. |
| [!UICONTROL 최대 기간] | `periodMax` | 더블 | 기간의 상한. |
| [!UICONTROL 기간 단위] | `periodUnit` | 문자열 | 시간 단위입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나 이상과 같아야 합니다. <li> `s`(초) </li> <li> `min`(분) </li> <li> `h`(시간별) </li> <li> `d`(일별) </li>  <li> `wk`(주별) </li> <li> `mo`(월별) </li> <li> `a`(연간)</li> |
| [!UICONTROL 시간] | `timeOfDay` | 문자열 배열 | 작업을 수행할 시간입니다. |
| [!UICONTROL When] | `when` | 문자열 배열 | 작업 기간에 대한 코드입니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
