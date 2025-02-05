---
title: 확장 연락처 세부 정보 데이터 유형
description: 확장 연락처 세부 정보 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4ac9b3d7-acc8-4a82-b34f-ec63a8bf12e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 6%

---

# [!UICONTROL 확장 연락처 세부 정보] 데이터 형식

[!UICONTROL 확장 연락처 세부 정보]은(는) 확장 연락처의 정보를 설명하는 표준 XDM(Experience Data Model) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![확장된 연락처 세부 정보 데이터 형식 구조](../../../images/healthcare/data-types/extended-contact-detail.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 주소] | `address` | [[!UICONTROL 주소]](../data-types/address.md) | 연락처의 주소입니다. |
| [!UICONTROL 이름] | `name` | [[!UICONTROL 사람 이름]](../data-types/human-name.md) 배열 | 연락할 개인의 이름입니다. |
| [!UICONTROL 조직] | `organization` | [[!UICONTROL 참조]](../data-types/reference.md) | 연락처 세부 정보를 처리/모니터링하는 조직입니다. |
| [!UICONTROL 기간] | `period` | [[!UICONTROL 기간]](../data-types/period.md) | 연락처가 유효하거나 사용에 대해 유효했던 기간. |
| [!UICONTROL 용도] | `purpose` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 연락처의 유형입니다. |
| [!UICONTROL 통신] | `telecom` | [[!UICONTROL 연락처]](../data-types/contact-point.md) 배열 | 연락처 세부 정보. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
