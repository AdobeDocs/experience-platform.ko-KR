---
title: 개인 데이터 유형
description: XDM(개인 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 7%

---

# [!UICONTROL 사용자] 데이터 형식

[!UICONTROL Person]은(는) 일반 사용자 레코드에 대한 정보를 제공하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 이 데이터 유형은 HL7 FHIR 릴리스 5 사양에 따라 생성됩니다.

![개인 데이터 형식 구조](../../images/data-types/healthcare/person/person.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 주소] | `address` | [[!UICONTROL 주소]](../healthcare/address.md) 배열 | 개인용 하나 이상의 주소. |
| [!UICONTROL 통신] | `communication` | 오브젝트 배열 | 대상자와 자신의 건강에 대해 소통하는 데 사용할 수 있는 언어입니다. 자세한 내용은 아래 [섹션](#communication)을 참조하세요. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../healthcare/identifier.md) 배열 | 해당 사용자에 대한 사람 식별자. |
| [!UICONTROL 사용자 링크 세부 정보] | `link` | 오브젝트 배열 | 동일한 실제 사용자와 관련된 리소스에 대한 링크. 자세한 내용은 아래 [섹션](#link)을 참조하세요. |
| [!UICONTROL 조직 관리] | `managingOrganization` | [[!UICONTROL 참조]](../healthcare/reference.md) | 환자 기록의 관리자인 조직입니다. |
| [!UICONTROL 결혼 상태] | `maritalStatus` | [[!UICONTROL 코드 가능한 개념]](../healthcare/codeable-concept.md) | 개인의 혼인(또는 민사) 상태 |
| [!UICONTROL 이름] | `name` | [[!UICONTROL 사람 이름]](../healthcare/human-name.md) 배열 | 개인과 연관된 이름. |
| [!UICONTROL 연락처 정보] | `telecom` | [[!UICONTROL 연락처]] 배열 | 연락 가능한 연락처 세부 정보. |
| [!UICONTROL 활성 상태임] | `active` | 부울 | 개인의 레코드가 활성 상태인지 여부를 나타냅니다. |
| [!UICONTROL 생년월일] | `birthDate` | 날짜 | 개인의 생년월일. |
| [!UICONTROL 삭제된 표시기] | `deceasedBoolean` | 부울 | 개인의 사망 여부를 나타냅니다. |
| [!UICONTROL 중단된 날짜 시간] | `deceasedDateTime` | 날짜/시간 | 사망한 경우 사망한 날짜와 시간. |
| [!UICONTROL 성별] | `gender` | 문자열 | 개인의 성 정체성. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

## `communication` {#communication}

`communication`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![통신 구조](../../images/data-types/healthcare/person/communication.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 언어] | `language` | [[!UICONTROL 코드 가능한 개념]](../../data-types/healthcare/codeable-concept.md) | 대상자와 자신의 건강에 대해 소통하는 데 사용할 수 있는 언어입니다. |
| [!UICONTROL 기본 언어임] | `preferred` | 부울 | 언어가 기본 언어인지 여부를 나타냅니다. |

## `link` {#link}

`link`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![링크 구조](../../images/data-types/healthcare/person/link.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL Target] | `target` | [[!UICONTROL 참조]](../../data-types/healthcare/reference.md) | 이 실제 사용자와 연관된 리소스입니다. |
| [!UICONTROL 보증] | `assurance` | 문자열 | 링크에 연결된 보증 수준입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나 이상과 같아야 합니다. <li> `level1` </li> <li> `level2` </li> <li> `level3` </li> <li> `level4` </li> |
