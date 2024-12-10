---
title: 의료 서비스 플랜 스키마 필드 그룹
description: Care Plan 스키마 필드 그룹에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e6cbf44f-6c39-42bd-b083-a975860a64db
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# [!UICONTROL 관리 계획] 스키마 필드 그룹

[!UICONTROL 관리 계획]은(는) [[!DNL XDM Individual Profile] 클래스](../../../classes/individual-profile.md)의 표준 스키마 필드 그룹입니다. 환자나 그룹에 대한 의료 서비스 플랜을 캡처하는 단일 개체 유형 필드 `healthcareCarePlan`을(를) 제공합니다.

![필드 그룹 구조](../../../images/healthcare/field-groups/care-plan/care-plan.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 활동] | `activity` | 오브젝트 배열 | 계획의 일부로 발생했거나 발생할 예정인 작업을 식별합니다. 자세한 내용은 아래 [섹션](#activity)을 참조하세요. |
| [!UICONTROL 주소] | `addresses` | [[!UICONTROL 코드 가능한 참조]](../data-types/codeable-reference.md) 배열 | 돌봄 플랜이 처리하는 조건 또는 관련 사항을 식별합니다. |
| [!UICONTROL 기준] | `basedOn` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 이 지원 플랜에 의해 전체 또는 부분적으로 이행되는 상위 레벨 요청 리소스. |
| [!UICONTROL 관리 팀] | `careTeam` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 이 플랜이 구상하는 돌봄에 참여할 것으로 예상되는 모든 사람 및 조직을 식별합니다. |
| [!UICONTROL 범주] | `category` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 공존하는 여러 계획 간의 차별화를 지원하기 위한 계획의 종류를 식별합니다. |
| [!UICONTROL 참가자] | `contributor` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 돌봄 플랜 콘텐츠를 제공한 개인, 조직 또는 장치를 식별합니다. |
| [!UICONTROL 관리자] | `custodian` | [[!UICONTROL 참조]](../data-types/reference.md) | 채워진 경우, 관리인은 관리 계획에 대한 책임이 있고 이에 귀속됩니다. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL 참조]](../data-types/reference.md) | 돌봄 플랜이 생성된 동안의 만남. |
| [!UICONTROL 목표] | `goal` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 계획 수행에 대한 의도한 목표. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) 배열 | 자원이 업데이트되고 서버에서 서버로 전파될 때 일정하게 유지되는 수행자 또는 기타 시스템이 이 관리 계획에 할당한 비즈니스 식별자. |
| [!UICONTROL 메모] | `note` | [[!UICONTROL 주석]](../data-types/annotation.md) 배열 | 다른 속성에서는 다루지 않는 돌봄 계획에 대한 일반적인 참고 사항. |
| [!UICONTROL 일부] | `partOf` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 이 특정 진료 계획이 구성 요소 또는 단계인 더 큰 진료 계획. |
| [!UICONTROL 기간] | `period` | [[!UICONTROL 기간]](../data-types/period.md) | 플랜이 언제 발효되었는지(또는 계획된 것인지) 및 언제 종료되는지를 나타냅니다. |
| [!UICONTROL 바꾸기] | `replaces` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 본 진료 계획으로 기능을 인계받는 완료 또는 종료된 진료 계획. |
| [!UICONTROL 제목] | `subject` | [[!UICONTROL 참조]](../data-types/reference.md) | 플랜에서 의도한 진료를 설명하는 환자나 그룹을 식별합니다. |
| [!UICONTROL 지원 정보] | `supportingInfo` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 계획 형성에 영향을 준 환자 기록 부분을 식별합니다. 여기에는 동반자, 최근 절차, 제한 사항 또는 최근 평가가 포함될 수 있습니다. |
| [!UICONTROL 생성일] | `created` | 날짜/시간 | 시스템에서 이 관리 플랜이 생성된 시점을 나타냅니다. 이 날짜는 시스템에서 생성된 경우가 많습니다. |
| [!UICONTROL 설명] | `description` | 문자열 | 플랜의 범위와 특성에 대한 설명입니다. |
| [!UICONTROL 표준 인스턴스화] | `instantiatesCanonical` | 문자열 배열 | FHIR 정의 프로토콜, 지침, 설문지 또는 이 플랜에 의해 전체 또는 부분적으로 준수되는 기타 정의를 가리키는 URL입니다. |
| [!UICONTROL Uri 인스턴스화] | `instantiatesUri` | 문자열 배열 | URI로 표현되는, 이 플랜에 의해 전부 또는 부분적으로 첨부되는, 외부에서 유지되는 프로토콜, 지침, 설문지 또는 기타 정의를 가리키는 URL. |
| [!UICONTROL 의도] | `intent` | 문자열 | 치료 계획의 의도. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL 상태] | `status` | 문자열 | 돌봄 플랜 상태. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL Title] | `title` | 문자열 | 돌봄 플랜의 이름. |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![활동 구조](../../../images/healthcare/field-groups/care-plan/activity.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 수행된 활동] | `performedActivity` | [[!UICONTROL 코드 가능한 참조]](../data-types/codeable-reference.md) 배열 | 활동 결과(예: 약속 또는 절차). |
| [!UICONTROL 계획된 활동 참조] | `plannedActivityReference` | [[!UICONTROL 참조]](../data-types/reference.md) | 제안된 활동의 세부 정보. |
| [!UICONTROL 진행] | `progress` | [[!UICONTROL 주석]](../data-types/annotation.md) 배열 | 활동의 준수, 상태 또는 진행 상황에 대한 참고 사항. |
