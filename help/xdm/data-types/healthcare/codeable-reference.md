---
title: 코드 가능한 참조 데이터 유형
description: 코드 가능한 XDM(참조 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# [!UICONTROL 코드 가능한 참조] 데이터 형식

[!UICONTROL 코드 가능한 참조]은(는) 리소스 또는 개념에 대한 참조를 설명하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![코드 가능한 참조 데이터 형식 구조](../../images/data-types/healthcare/codeable-reference.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 개념] | `concept` | [[!UICONTROL 코드 가능한 개념]](../healthcare/codeable-concept.md) | 개념에 대한 참조(클래스별)입니다. |
| [!UICONTROL 참조] | `reference` | [[!UICONTROL 참조]](../healthcare/reference.md) | 리소스에 대한 참조입니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
