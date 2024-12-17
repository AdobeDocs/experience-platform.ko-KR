---
title: 약속 스키마 필드 그룹
description: 약속 스키마 필드 그룹에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 2a58f6f1663e95c1c7576cd4909fa937b41ae099
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 5%

---

# [!UICONTROL 약속] 스키마 필드 그룹

[!UICONTROL 약속]은(는) [[!DNL XDM Individual Profile] 클래스](../../../classes/individual-profile.md) 및 [[!DNL Provider class]](../../../classes/provider.md)에 대한 표준 스키마 필드 그룹입니다. 특정 날짜 및 시간의 환자, 실무자, 관련 사용자 및/또는 장치 간의 의료 이벤트 예약에 대한 정보를 포함하는 단일 개체 유형 필드 `healthcareAppointment`을(를) 제공합니다.

![약속 필드 그룹 구조의 스키마 다이어그램입니다.](../../../images/healthcare/field-groups/appointment/appointment.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 계정] | `account` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 청구에 사용될 것으로 예상되는 계정 세트입니다. |
| [!UICONTROL 약속 유형] | `appointmentType` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 슬롯에 예약된 약속 스타일 또는 환자(서비스 유형이 아님). |
| [!UICONTROL 기준] | `basedOn` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 선임 요청은 절차 요청과 같이 평가를 위해 할당됩니다. |
| [!UICONTROL 취소 이유] | `cancellationReason` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 약속이 취소되는 코딩된 이유입니다. 이는 추가 작업이 필요한지 또는 특정 비용이 적용되는지 여부를 확인하기 위해 보고, 청구 또는 처리에 자주 사용됩니다. |
| [!UICONTROL 클래스] | `class` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 외래 환자, 입원 환자 또는 응급 환자 등 환자 만남의 분류를 나타내는 개념입니다. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) 배열 | 약속에 연결된 고유 식별자 목록. 이러한 식별자는 비즈니스 규칙을 기반으로 하거나 약속에 대한 직접 URL 링크가 적합하지 않을 때 할당됩니다. |
| [!UICONTROL 메모] | `note` | [[!UICONTROL 주석]](../data-types/annotation.md) 배열 | 약속에 대한 추가 참고 사항 또는 댓글. |
| [!UICONTROL 원래 약속] | `originatingAppointment` | [[!UICONTROL 참조]](../data-types/reference.md) | 되풀이되는 관련 약속 세트의 원래 약속. |
| [!UICONTROL 참가자] | `participant` | 오브젝트 배열 | 약속과 관련된 참가자 목록입니다. 자세한 내용은 아래 [섹션](#participant)을 참조하세요. |
| [!UICONTROL 환자 지침] | `patientInstruction` | [[!UICONTROL 코드 가능한 참조]](../data-types/reference.md) 배열 | 약속과 관련된 진단. |
| [!UICONTROL 이전 약속] | `previousAppointment` | [[!UICONTROL 참조]](../data-types/reference.md) | 일련의 관련 약속에서 이전 약속. |
| [!UICONTROL 우선 순위] | `priority` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 선임의 우선 순위. 선임의 우선 순위를 다시 지정해야 하는 경우 정보에 입각한 결정을 내리는 데 사용할 수 있습니다. iCal Standard에서는 `0`을(를) 정의되지 않은 것으로 지정하고, `1`을(를) 가장 높은 우선 순위로 지정하고, `9`을(를) 가장 낮은 우선 순위로 지정합니다. |
| [!UICONTROL 이유] | `reason` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 일반적으로 조건 또는 절차인 약속이 예약되는 이유입니다. |
| [!UICONTROL 반복 템플릿] | `recurrenceTemplate` | 오브젝트 배열 | 되풀이 약속을 만드는 데 사용되는 되풀이 패턴 또는 템플릿에 대한 세부 정보를 포함합니다.  자세한 내용은 아래 [섹션](#recurrence)을 참조하세요. |
| [!UICONTROL 바꾸기] | `replaces` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 약속이 이 약속으로 대체됩니다. 취소가 있는 경우 참조된 리소스의 `cancellationReason` 속성에서 취소에 대한 세부 정보를 찾을 수 있습니다. |
| [!UICONTROL 요청한 기간] | `requestedPeriod` | [[!UICONTROL 기간]](../data-types/period.md) 배열 | 약속을 예약하는 데 선호되는 날짜 범위 집합(시간 포함 가능)입니다. |
| [!UICONTROL 서비스 범주] | `serviceCategory` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 약속 중에 수행할 서비스에 대한 광범위한 분류. |
| [!UICONTROL 서비스 유형] | `serviceType` | [[!UICONTROL 코드 가능한 참조]](../data-types/codeable-reference.md) 배열 | 약속 중에 수행할 특정 서비스입니다. |
| [!UICONTROL 슬롯] | `slot` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 참석자의 일정에서 시간이 정해져 있어 약속에 의해 채워집니다. |
| [!UICONTROL 전문] | `speciality` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 이 약속에서 요청된 서비스를 수행하는 데 필요한 전문가의 전문성. |
| [!UICONTROL 제목] | `subject` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 약속과 연계된 환자 또는 그룹. |
| [!UICONTROL 지원 정보] | `supportingInformation` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 지원 약속을 정할 때 추가 정보 제공. |
| [!UICONTROL 가상 서비스] | `virtualService` | [[!UICONTROL 가상 서비스 세부 정보]](../data-types/virtual-service-detail.md) 배열 | 전화 회의와 같은 가상 서비스의 연결 세부 정보. |
| [!UICONTROL 취소 날짜] | `cancellationDate` | 날짜/시간 | 약속이 취소된 날짜와 시간. |
| [!UICONTROL 생성일] | `created` | 날짜/시간 | 약속을 만든 날짜 및 시간입니다. |
| [!UICONTROL 설명] | `description` | 문자열 | 약속에 대한 간략한 설명. 자세한 정보 또는 확장된 정보는 `note` 필드에 입력해야 합니다. |
| [!UICONTROL 종료] | `end` | 날짜/시간 | 약속 종료 날짜 및 시간입니다. |
| [!UICONTROL 분 기간] | `minutesDuration` | 정수 | 약속이 소요되는 시간(분)입니다. 시작 시간과 종료 시간 사이의 기간보다 작을 수 있습니다. 허용되는 최소 값은 `0`입니다. |
| [!UICONTROL 항목이 변경됨] | `occurenceChanged` | 부울 | 이 약속이 반복 패턴과 다른지 여부를 나타내는 플래그. |
| [!UICONTROL RecurrenceId] | `RecurrenceId` | 정수 | 반복 패턴의 특정 약속을 식별하는 시퀀스 번호입니다. 최소값은 `0`입니다. |
| [!UICONTROL 시작] | `start` | 날짜/시간 | 약속을 수행할 날짜 및 시간입니다. |
| [!UICONTROL 상태] | `status` | 문자열 | 약속 상태. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `proposed` </li> <li> `pending` </li> <li> `booked` </li> <li> `arrived` </li> <li> `fulfilled` </li> <li> `cancelled` </li> <li> `noshow` </li> <li> `entered-in-error` </li> <li> `checked-in` </li> <li> `waitlist` </li> |


필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.schema.json)

## `participant` {#participant}

`participant`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![참가자 개체 구조의 스키마 다이어그램입니다.](../../../images/healthcare/field-groups/appointment/participant.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 작업자] | `actor` | [[!UICONTROL 참조]](../data-types/reference.md) | 약속에 참여하는 개인, 장치, 위치 또는 서비스. |
| [!UICONTROL 기간] | `period` | [[!UICONTROL 기간]](../data-types/period.md) | 참여자(행위자)가 약속에 참여하는 기간. |
| [!UICONTROL 유형] | `type` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 약속에서 참가자(행위자)의 역할. |
| [!UICONTROL 필수] | `required` | 부울 | 이 참가자의 참석 필요 여부. |
| [!UICONTROL 상태] | `status` | 문자열 | 참가자의 수락 상태입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `accepted` </li> <li> `declined` </li> <li> `tentative` </li> <li> `needs-action` </li> |

## `recurrenceTemplate` {#recurrence}

`recurrenceTemplate`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![다시 실행 템플릿 개체 구조의 스키마 다이어그램입니다.](../../../images/healthcare/field-groups/appointment/recurrence-template.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 월별 템플릿] | `monthlyTemplate` | 오브젝트 배열 | 월별 반복 약속에 대한 정보입니다. 자세한 내용은 아래 [섹션](#monthly-template)을 참조하세요. |
| [!UICONTROL 반복 유형] | `recurrenceType` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 주별, 월별 또는 연도별 등 약속 시리즈가 반복되어야 하는 빈도. |
| [!UICONTROL 표준 시간대] | `timezone` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 되풀이 약속의 시간대. |
| [!UICONTROL 주별 템플릿] | `weeklyTemplate` | 오브젝트 배열 | 주별 반복 약속에 대한 정보입니다. 자세한 내용은 아래 [섹션](#weekly-template)을 참조하세요. |
| [!UICONTROL 연간 템플릿] | `yearlyTemplate` | 오브젝트 | 연간 되풀이 약속에 대한 정보입니다. `yearInterval` 속성을 포함합니다. 이 속성은 약속이 다시 시작되는 n번째 연도를 나타내는 정수 값을 포함합니다. |
| [!UICONTROL 날짜 제외] | `excludingDate` | 날짜 배열 | 휴일과 같이 되풀이에서 제외해야 하는 모든 날짜. |
| [!UICONTROL 반복 Id 제외] | `excludingRecurrenceId` | 정수 배열 | 반복에서 제외해야 하는 모든 반복 ID. 이는 제외할 약속의 `reccurenceID`을(를) 나타내는 `excludingDate`의 대안입니다. |
| [!UICONTROL 마지막 발생 날짜] | `lastOccurenceDate` | 날짜 | 이후 예정된 더 이상의 반복 약속이 없는 날짜입니다. |
| [!UICONTROL 발생 횟수] | `occurenceCount` | 정수 | 반복에 계획된 약속 수입니다. 최소값은 `0`입니다. |
| [!UICONTROL 발생 날짜] | `occurenceDate` | 날짜 배열 | 약속이 예정된 특정 날짜 목록. |

## `weeklyTemplate` {#weekly-template}

`weeklyTemplate`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![주별 템플릿 개체 구조의 스키마 다이어그램입니다.](../../../images/healthcare/field-groups/appointment/weekly-template.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 금요일] | `friday` | 부울 | 반복되는 약속이 금요일에 발생함을 나타냅니다. |
| [!UICONTROL 월요일] | `monday` | 부울 | 자동연장 약속이 월요일에 발생해야 함을 나타냅니다. |
| [!UICONTROL 토요일] | `saturday` | 부울 | 자동연장 약속이 토요일에 발생함을 나타냅니다. |
| [!UICONTROL 일요일] | `sunday` | 부울 | 반복적인 약속이 일요일에 발생해야 함을 나타냅니다. |
| [!UICONTROL 목요일] | `thursday` | 부울 | 반복 약속이 목요일에 발생함을 나타냅니다. |
| [!UICONTROL 화요일] | `tuesday` | 부울 | 반복 약속이 화요일에 발생함을 나타냅니다. |
| [!UICONTROL 수요일] | `wednesday` | 부울 | 반복 약속이 수요일에 발생함을 나타냅니다. |
| [!UICONTROL 주 간격] | `weekInterval` | 정수 | 매주 n번째 주를 기준으로 약속이 다시 발생하는 빈도를 지정합니다. 기본값은 매주 이므로 일반적인 값은 2 이상입니다. |

## `monthlyTemplate` {#monthly-template}

`monthlyTemplate`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![월별 템플릿 개체 구조의 스키마 다이어그램입니다.](../../../images/healthcare/field-groups/appointment/monthly-template.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 요일] | `dayOfWeek` | [[!UICONTROL 코딩]] | 약속이 특정 요일에 발생해야 함을 나타냅니다. |
| [!UICONTROL n번째 주] | `nthWeekOfMonth` | [[!UICONTROL 코딩]](../data-types/coding.md) | 약속이 재개되어야 하는 월의 n번째 주를 나타냅니다. |
| [!UICONTROL 날짜] | `dayOfMonth` | 정수 | 약속이 해당 월의 특정 날짜에 발생해야 함을 나타냅니다. |
| [!UICONTROL 월 간격] | `monthInterval` | 정수 | 되풀이 약속이 n개월마다 발생함을 나타냅니다. |
