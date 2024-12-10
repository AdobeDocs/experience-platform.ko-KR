---
title: 실무자 스키마 필드 그룹
description: Practor 스키마 필드 그룹에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 71210303-a3dd-458c-9c8a-ac8b546c2b1d
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 7%

---

# [!UICONTROL 연습자] 스키마 필드 그룹

[!UICONTROL 연습자]은(는) [[!DNL XDM Individual Profile] 클래스](../../../classes/individual-profile.md) 및 [[!DNL Provider class]](../../../classes/provider.md)에 대한 표준 스키마 필드 그룹입니다. 의료 서비스 또는 관련 서비스 프로비저닝에 직접 또는 간접적으로 관여하는 사용자에 대한 정보가 포함된 단일 개체 유형 필드 `healthcarePractioner`을(를) 제공합니다.

![필드 그룹 구조](../../../images/healthcare/field-groups/practitioner/practitioner.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 주소] | `address` | [[!UICONTROL 주소]](../data-types/address.md) 배열 | 집 주소 등 근무지 밖에 있는 실무자의 주소. |
| [!UICONTROL 통신] | `communication` | 개체 배열 | 의료인과 의사소통하는 데 사용할 수 있는 언어입니다. 자세한 내용은 아래 [섹션](#communication)을 참조하세요. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) 배열 | 이 역할의 해당 사용자에게 적용되는 식별자. |
| [!UICONTROL 이름] | `name` | [[!UICONTROL 사람 이름]](../data-types/human-name.md) 배열 | 의사와 연결된 이름입니다. |
| [!UICONTROL 자격] | `qualification` | 개체 배열 | 공인 자격, 인증, 자격, 교육, 면허 또는 이와 유사한 것은 의료인의 간호 제공에 관한 것입니다. 자세한 내용은 아래 [섹션](#qualification)을 참조하세요. |
| [!UICONTROL 연락처 정보] | `telecom` | [[!UICONTROL 연락처]](../data-types/contact-point.md) 배열 | 개업의 연락처 세부 정보. |
| [!UICONTROL 활성] | `active` | 부울 | 실무자 레코드가 활성 사용 중인지 여부를 나타냅니다. |
| [!UICONTROL 생년월일] | `birthDate` | 날짜 | 시술자의 생년월일. |
| [!UICONTROL 삭제된 표시기] | `deceasedBoolean` | 부울 | 시술자가 사망했는지 보여 줍니다. |
| [!UICONTROL 중단된 날짜 시간] | `deceasedDateTime` | 날짜/시간 | 시술자의 사망 날짜와 시간. |
| [!UICONTROL 성별] | `gender` | 문자열 | 개인의 성 정체성. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.schema.json)

## `communication` {#communication}

`communication`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![통신 구조](../../../images/healthcare/field-groups/practitioner/communication.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 언어] | `language` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 건강과 관련된 사람들과 의사소통하는 데 사용할 수 있는 언어입니다. |
| [!UICONTROL 기본 언어임] | `preferred` | 부울 | 언어가 기본 언어인지 여부를 나타냅니다. |

## `qualification` {#qualification}

`qualification`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![자격 구조](../../../images/healthcare/field-groups/practitioner/qualification.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 코드] | `code` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 자격의 코드화된 표현. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) 배열 | 자격에 대한 식별자. |
| [!UICONTROL 발급자] | `issuer` | [[!UICONTROL 참조]](../data-types/reference.md) | 자격을 규제하고 발급하는 조직. |
| [!UICONTROL 기간] | `period` | [[!UICONTROL 기간]](../data-types/period.md) | 자격이 유효한 기간입니다. |
