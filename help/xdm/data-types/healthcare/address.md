---
title: 주소 데이터 유형
description: XDM(주소 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 9%

---

# [!UICONTROL 주소] 데이터 형식

[!UICONTROL Address]은(는) 우편 규칙(GPS 또는 다른 위치 정의 형식이 아닌)을 사용하여 표현된 주소를 설명하는 표준 XDM(Experience Data Model) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![주소 데이터 형식 구조](../../images/data-types/healthcare/address.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 기간] | `period` | [[!UICONTROL 기간]](../healthcare/period.md) | 주소가 사용 중이었던 기간. |
| [!UICONTROL 구/군/시] | `city` | 문자열 | 도시 이름. |
| [!UICONTROL 국가] | `country` | 문자열 | ISO 3166 국제 표준에 설명된 국가 코드. 코드는 alpha-2 또는 alpha-3 중 하나일 수 있습니다. |
| [!UICONTROL 구] | `district` | 문자열 | 지역 이름. |
| [!UICONTROL 줄] | `line` | 문자열 | 거리 이름, 번호, 방향, 사서함 또는 이와 유사한 |
| [!UICONTROL 우편 번호] | `postalCode` | 문자열 | 우편 번호. |
| [!UICONTROL 상태] | `state` | 문자열 | 국가의 하위 단위입니다. 약어는 사용할 수 있습니다. |
| [!UICONTROL 텍스트] | `text` | 문자열 | 주소의 텍스트 표현입니다. |
| [!UICONTROL 유형] | `type` | 문자열 | 주소 유형. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL 사용] | `use` | 문자열 | 주소의 목적입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)
