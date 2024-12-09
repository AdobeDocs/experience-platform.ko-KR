---
title: 수량 데이터 유형
description: XDM(Quantity Experience Data Model) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 10%

---

# [!UICONTROL 수량] 데이터 형식

[!UICONTROL 수량]은(는) 측정되거나 측정 가능한 양을 제공하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![수량 데이터 형식 구조](../../images/data-types/healthcare/quantity.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 코드] | `code` | 문자열 | 장치의 코드화된 형식입니다. |
| [!UICONTROL 비교 연산자] | `comparator` | 문자열 | 비교 연산자. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL 시스템] | `system` | 문자열 | URI로 표시되는 코딩된 단위 양식을 정의하는 시스템입니다. |
| [!UICONTROL 단위] | `unit` | 문자열 | 단위 표현입니다. |
| [!UICONTROL 값] | `value` | 더블 | 숫자 값입니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
