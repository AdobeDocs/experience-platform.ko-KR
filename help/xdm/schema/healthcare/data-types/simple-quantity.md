---
title: 단순 수량 데이터 유형
description: XDM(Simple Quantity Experience Data Model) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 92d3d6a8-1d0f-43a4-a93f-8df79605c4e6
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 11%

---

# [!UICONTROL 단순 수량] 데이터 형식

[!UICONTROL 단순 양]은(는) 측정되거나 측정 가능한 양을 제공하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![단순 수량 데이터 형식 구조](../../../images/healthcare/data-types/simple-quantity.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 코드] | `code` | 문자열 | 장치의 코드화된 형식입니다. |
| [!UICONTROL 시스템] | `system` | 문자열 | URI로 표시되는 코딩된 단위 양식을 정의하는 시스템입니다. |
| [!UICONTROL 단위] | `unit` | 문자열 | 단위 표시. |
| [!UICONTROL 값] | `value` | 더블 | 숫자 값입니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
