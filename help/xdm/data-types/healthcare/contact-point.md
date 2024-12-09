---
title: 연락처 데이터 유형
description: 연락처 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# [!UICONTROL 연락처] 데이터 형식

[!UICONTROL 연락처]은(는) 개인용 연락처 정보를 설명하는 표준 XDM(경험 데이터 모델) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![연락처 데이터 형식 구조](../../images/data-types/healthcare/contact-point.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 기간] | `period` | [[!UICONTROL 기간]](../healthcare/period.md) | 연락처가 사용 중이었던 기간. |
| [!UICONTROL 순위] | `rank` | 정수 | 연락처의 기본 사용을 나타내는 등급입니다. 최소값은 `1`이고 최대값은 `2147483647`입니다. 여기서 `1`은(는) 가장 높은 특이성입니다. |
| [!UICONTROL 시스템] | `system` | 문자열 | 연락 가능한 시스템입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL 사용] | `use` | 문자열 | 연락처의 목적입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL 값] | `value` | 문자열 | 연락처의 세부 정보. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)
