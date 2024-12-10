---
title: 주석 데이터 유형
description: XDM(Annotation Experience Data Model) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# [!UICONTROL 주석] 데이터 형식

[!UICONTROL 주석]은(는) 작성자에 대한 속성이 있는 텍스트 노드가 포함된 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![주석 데이터 형식 구조](../../../images/healthcare/data-types/annotation.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 작성자 참조] | `authorReference` | [[!UICONTROL 참조]](../data-types/reference.md) | 작성자에 대한 참조. |
| [!UICONTROL 작성자] | `authorString` | 문자열 | 주석을 담당하는 개인입니다. |
| [!UICONTROL 텍스트] | `text` | 문자열 | 주석의 콘텐츠입니다. |
| [!UICONTROL 시간] | `time` | 날짜/시간 | 주석을 작성한 시간. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
