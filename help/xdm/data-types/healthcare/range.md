---
title: 범위 데이터 유형
description: XDM(범위 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 8%

---

# [!UICONTROL 범위] 데이터 형식

[!UICONTROL 범위]은(는) 낮은 값과 높은 값으로 바인딩된 값 집합을 제공하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![범위 데이터 형식 구조](../../images/data-types/healthcare/range.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 높음] | `high` | [[!UICONTROL 단순 수량]](../healthcare/simple-quantity.md) | 최대 한도입니다. |
| [!UICONTROL 낮음] | `low` | [[!UICONTROL 단순 수량]](../healthcare/simple-quantity.md) | 가장 낮은 한도입니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)
