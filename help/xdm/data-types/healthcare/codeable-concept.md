---
title: 코드 가능한 개념 데이터 유형
description: 코드 가능한 XDM(Concept Experience Data Model) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# [!UICONTROL 코드 가능한 개념] 데이터 형식

[!UICONTROL Codeable Concept]은(는) 리소스 간 참조를 설명하는 표준 XDM(경험 데이터 모델) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![코드 가능한 개념 데이터 형식 구조](../../images/data-types/healthcare/codeable-concept.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 코딩] | `coding` | [[!UICONTROL 코딩]](../healthcare/coding.md) 배열 | 용어 시스템에 의해 정의된 코드. |
| [!UICONTROL 텍스트] | `text` | 문자열 | 개념의 일반 텍스트 표현입니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
