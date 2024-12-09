---
title: 식별자 데이터 유형
description: XDM(식별자 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# [!UICONTROL 식별자] 데이터 형식

[!UICONTROL 식별자]은(는) 계산용 식별자를 제공하는 표준 XDM(경험 데이터 모델) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![식별자 데이터 형식 구조](../../images/data-types/healthcare/identifier.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 기간] | `period` | [[!UICONTROL 기간]](../healthcare/period.md) | ID가 사용되거나 사용되기 유효한 기간. |
| [!UICONTROL 유형] | `type` | [[!UICONTROL 코드 가능한 개념]](../healthcare/codeable-concept.md) | 식별자에 대한 설명. |
| [!UICONTROL 할당자] | `assigner` | 문자열 | ID를 발행한 조직입니다. |
| [!UICONTROL 시스템] | `system` | 문자열 | URI로 표시되는 식별자 값의 네임스페이스입니다. |
| [!UICONTROL 사용] | `use` | 문자열 | 식별자의 사용입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나 이상과 같아야 합니다. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL 값] | `value` | 문자열 | ID의 고유 값. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)
