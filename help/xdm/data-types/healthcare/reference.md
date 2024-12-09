---
title: 참조 데이터 유형
description: 참조 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---

# [!UICONTROL 참조] 데이터 형식

[!UICONTROL 참조]은(는) 표준 XDM(Experience Data Model) 데이터 형식으로서 한 리소스에서 다른 리소스로의 참조를 제공합니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![참조 데이터 형식 구조](../../images/data-types/healthcare/reference.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../healthcare/identifier.md) | 리터럴 참조를 알 수 없는 경우의 논리적 참조입니다. |
| [!UICONTROL 디스플레이] | `display` | 문자열 | 참조에 대한 텍스트 대체 요소입니다. |
| [!UICONTROL 참조] | `reference` | 문자열 | 리터럴 참조, 상대, 내부 또는 절대 URL입니다. |
| [!UICONTROL 유형] | `type` | 문자열 | 참조가 참조하는 유형으로, URI로 다시 표시됩니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
