---
title: 타이밍 데이터 유형
description: XDM(타이밍 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 0640d0c2daab67ad7a77d3265ccae45851ba45b8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 7%

---

# [!UICONTROL 타이밍] 데이터 형식

[!UICONTROL Timing]은(는) 여러 번 발생할 수 있는 이벤트에 대한 정보를 제공하는 시간 일정을 설명하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![타이밍 데이터 형식 구조](../../images/data-types/healthcare/timing.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 이벤트] | `event` | DateTime 배열 | 이벤트가 발생하는 시간. |
| [!UICONTROL 반복] | `repeat` | [[!UICONTROL 반복]](../healthcare/repeat.md) | 이벤트 발생 시기에 대한 정보입니다. |
| [!UICONTROL 코드] | `code` | [[!UICONTROL 코드 가능한 개념]](../healthcare/codeable-concept.md) | 이벤트와 관련된 코드입니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
