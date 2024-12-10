---
title: 목표 스키마 필드 그룹
description: 목표 스키마 필드 그룹에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 87715274-cc9d-41da-9ca7-1634903b4e8f
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---

# [!UICONTROL 목표] 스키마 필드 그룹

[!UICONTROL 목표]은(는) [[!DNL XDM Individual Profile] 클래스](../../../classes/individual-profile.md) 및 [[!DNL Provider class]](../../../classes/provider.md)에 대한 표준 스키마 필드 그룹입니다. 환자, 그룹 또는 조직 관리에 대해 의도한 목표를 설명하는 단일 개체 유형 필드 `healthcareGoal`을(를) 제공합니다.

![필드 그룹 구조](../../../images/healthcare/field-groups/goal/goal.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 달성 상태] | `achievementStatus` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 목표에 대한 진행 상황 또는 부족을 설명합니다. |
| [!UICONTROL 주소] | `addresses` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 목표에 의해 해결되기 위한 조건 및 기타 상태 기록 요소. |
| [!UICONTROL 범주] | `category` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 식이 또는 행동 등 목표가 포함되는 범주를 나타냅니다. |
| [!UICONTROL 설명] | `description` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 목표를 설명하는 코드 또는 텍스트입니다. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) 배열 | 리소스가 업데이트되고 서버에서 서버로 전파될 때 일정하게 유지되는 수행자 또는 기타 시스템이 이 목표에 할당한 비즈니스 식별자입니다. |
| [!UICONTROL 메모] | `note` | [[!UICONTROL 주석]](../data-types/annotation.md) 배열 | 목표에 대한 주석입니다. |
| [!UICONTROL 결과] | `outcome` | [[!UICONTROL 코드 가능한 참조]](../data-types/codeable-reference.md) 배열 | 목표 상태를 평가할 때 변경(또는 변경 부족)을 식별합니다. |
| [!UICONTROL 우선 순위] | `priority` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 목표 도달 또는 지속과 관련하여 상호 합의된 중요도를 식별합니다. |
| [!UICONTROL Source] | `source` | [[!UICONTROL 참조]](../data-types/reference.md) | 환자나 의료인과 같은 목표의 출처를 나타냅니다. |
| [!UICONTROL 코드 가능한 개념 시작] | `startCodeableConcept` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 그 후에 목표가 설득되어야 하는 사건. |
| [!UICONTROL 제목 |]`subject` | [[!UICONTROL 참조]](../data-types/reference.md) | 목표를 설정하고 있는 환자, 그룹 또는 조직을 식별합니다. |
| [!UICONTROL Target] | `target` | 오브젝트 배열 | 목표의 특정 단계에 대한 타임라인을 나타냅니다. 자세한 내용은 아래 [섹션](#target)을 참조하세요. |
| [!UICONTROL 연속] | `continous` | 부울 | 목표 달성 후 목표 목표를 유지하기 위해 지속적인 활동이 필요한지 여부를 나타냅니다. |
| [!UICONTROL 라이프사이클 상태] | `lifecycleStatus` | 문자열 | 목표의 라이프사이클 상태입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL 시작 날짜] | `startDate` | 날짜 | 목표를 추진해야 하는 시작 날짜입니다. |
| [!UICONTROL 상태 날짜] | `statusDate` | 날짜 | 상태가 생성된 시기를 식별합니다. |
| [!UICONTROL 상태 이유] | `statusReason` | 문자열 | 현재 상태에 대한 이유를 캡처합니다. |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![대상 구조](../../../images/healthcare/field-groups/goal/target.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 세부 코드 가능 개념] | `detailCodeableConcept` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 목표 달성을 나타내기 위해 달성할 대상 코드. |
| [!UICONTROL 세부 수량] | `detailQuantity` | [[!UICONTROL 수량]](../data-types/quantity.md) | 목표 달성을 나타내기 위해 달성할 목표 수량. |
| [!UICONTROL 세부 범위] | `detailRange` | [[!UICONTROL Range]](../data-types/range.md) | 목표 달성을 나타내기 위해 달성할 목표 범위. |
| [!UICONTROL 세부 비율] | `detailRatio` | [[!UICONTROL 비율]](../data-types/ratio.md) | 목표 달성을 나타내기 위해 달성해야 할 목표 비율입니다. |
| [!UICONTROL 측정] | `measure` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 해당 값이 있는 매개 변수가 추적 중입니다. |
| [!UICONTROL 세부 정보 부울] | `detailBoolean` | 부울 | 목표의 달성을 나타냅니다. |
| [!UICONTROL 세부 정수] | `detailInteger` | 정수 | 목표 달성을 나타내기 위해 달성할 목표 번호입니다. |
| [!UICONTROL 세부 문자열] | `detailString` | 문자열 | 목표 달성을 나타내기 위해 달성할 목표 값. |
| [!UICONTROL 기한] | `dueDate` | 날짜 | 타겟이 충족되어야 하는 날짜. |
