---
title: 의약품 요청 스키마 필드 그룹
description: 약물 요청 스키마 필드 그룹에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8502380f-9557-4ca6-84bc-65010dfc6066
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# [!UICONTROL 약물 요청] 스키마 필드 그룹

[!UICONTROL 약물 요청]은(는) [[!DNL Medication] 클래스](../../../classes/medication.md), [[!DNL XDM Individual Profile] 클래스](../../../classes/individual-profile.md) 및 [[!DNL Provider class]](../../../classes/provider.md)에 대한 표준 스키마 필드 그룹입니다. 이 메서드는 약품 공급과 환자에게 약품을 투여하기 위한 지침 모두에 대한 주문 또는 요청을 캡처하는 단일 개체 유형 필드 `healthcareMedicationDispense`을(를) 제공합니다.

![필드 그룹 구조](../../../images/healthcare/field-groups/medication-request/medication-request.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 기준] | `basedOn` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 이 투약 요청에 의해 이행된 플랜 또는 요청. |
| [!UICONTROL 범주] | `category` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 투약 요청의 범주화 또는 그룹화입니다. |
| [!UICONTROL 치료 유형 과정] | `courseOfTherapyType` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 환자에게 투약하기 위한 전체적인 패턴에 대한 설명. |
| [!UICONTROL 장치] | `device` | [[!UICONTROL 코드 가능한 참조]](../data-types/codeable-reference.md) 배열 | 약물 관리에 사용할 장치 유형입니다. |
| [!UICONTROL 분배 요청] | `dispenseRequest` | 오브젝트 | 의약품 주문이라고도 하는 분배 요청의 특정 세부 정보를 나타냅니다. 자세한 내용은 아래 [섹션](#dispense-request)을 참조하세요. |
| [!UICONTROL 복용량 지침] | `dosageInstructions` | [[!UICONTROL 투약]](../data-types/dosage.md) 배열 | 환자가 약을 어떻게 사용할지에 대한 구체적인 지침. |
| [!UICONTROL 유효 선량 기간] | `effectiveDosePeriod` | [[!UICONTROL 기간]](../data-types/period.md) | 약물을 복용해야 하는 기간. 여러 `dosageInstruction`줄이 있는 경우(예: 용량을 줄인 경우), 이는 복용 설명서의 가장 빠른 날짜와 가장 늦은 날짜입니다. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL 참조]](../data-types/reference.md) | 요청을 생성하는 도중 발생한 발생 횟수. |
| [!UICONTROL 이벤트 기록] | `eventHistory` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 요청 이행, 주요 상태 전환 순간 또는 관련 업데이트 등 약물 요청과 관련된 이벤트 레코드에 대한 링크입니다. |
| [!UICONTROL 그룹 식별자] | `groupIdentifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) | 단일 작성자가 활성화한 여러 독립 요청 인스턴스에 대한 공유 식별자입니다. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) 배열 | 비즈니스 프로세스에 의해 정의되거나 리소스 자체에 대한 직접 URL 참조가 적절하지 않을 때 복약 요청과 연관된 식별자 및/또는 이를 참조하는 데 사용되는 식별자. |
| [!UICONTROL 정보 Source] | `informationSource` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 소스가 `requester` 이외의 다른 사용자인 경우 요청에 대한 정보를 제공한 개인 또는 조직 |
| [!UICONTROL 보험] | `insurance` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 요청된 서비스를 제공하는 데 필요할 수 있는 보험 플랜, 보장 범위 확장, 사전 승인 및/또는 사전 결정. |
| [!UICONTROL 약물] | `medication` | [[!UICONTROL 코드 사용 가능한 참조]](../data-types/codeable-reference.md) | 요청 중인 의약품을 식별합니다. 이는 약물의 세부 사항을 나타내는 리소스에 대한 링크이거나 약물을 식별하는 코드여야 합니다. |
| [!UICONTROL 메모] | `note` | [[!UICONTROL 주석]](../data-types/annotation.md) 배열 | 다른 속성으로 전달할 수 없었던 처방에 대한 추가 정보. |
| [!UICONTROL 수행자] | `performer` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 지정된 약물 치료/투여 수행자. 장치의 경우, 이것은 약물의 투여를 수행하도록 의도된 장치이다. |
| [!UICONTROL 수행자 유형] | `performerType` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 약물 관리에 사용할 수행자 유형을 나타냅니다. |
| [!UICONTROL 이전 처방] | `priorPrescription` | [[!UICONTROL 참조]](../data-types/reference.md) | 이 요청으로 대체되는 주문 또는 처방에 대한 참조. |
| [!UICONTROL 이유] | `reason` | [[!UICONTROL 코드 가능한 참조]](../data-types/reference.md) 배열 | 약제를 주문하거나 주문하지 않는 이유 또는 표시. |
| [!UICONTROL 레코더] | `recorder` | [[!UICONTROL 참조]](../data-types/reference.md) | 다른 개인을 대신하여 주문에 들어간 개인. |
| [!UICONTROL 요청자] | `requester` | [[!UICONTROL 참조]](../data-types/reference.md) | 요청을 시작했으며 활성화를 담당하는 개인, 조직 또는 장치입니다. |
| [!UICONTROL 상태 이유] | `statusReason` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 요청의 현재 상태에 대한 설명입니다. |
| [!UICONTROL 제목] | `subject` | [[!UICONTROL 참조]](../data-types/reference.md) | 약물치료를 요청한 개인 또는 그룹입니다. |
| [!UICONTROL 대체] | `substitution` | 오브젝트 | 대체가 분배의 일부일 수 있는지 또는 포함되어야 하는지 여부를 나타냅니다. 다음 세 가지 속성을 포함합니다. <li>`allowedBoolean`: 처방자가 대체를 허용하는 경우 true인 부울 값입니다.</li> <li>`allowedCodeableConcept`: 처방자가 대체를 허용하는 경우 코드를 제공하는 [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) 값입니다.</li> <li>`reason`: 대체 이유를 나타내는 [[!UICONTROL 코드 가능한 Concept]](../data-types/codeable-concept.md) 값입니다.</li> |
| [!UICONTROL 지원 정보] | `supportingInformation` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 환자의 키, 체중 등 약물 이행을 지원하는 정보입니다. |
| [!UICONTROL 작성일] | `authoredOn` | 날짜/시간 | 처방전이 작성된 날짜(및 선택적 시간). |
| [!UICONTROL 수행하지 않음] | `doNotPerform` | 부울 | true인 부울 지표는 환자가 약물 복용을 중단(또는 시작하지 않음)해야 한다는 것입니다. |
| [!UICONTROL 의도] | `intent` | 문자열 | 요청의 의도. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL 우선 순위] | `priority` | 문자열 | 요청의 우선 순위입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL 렌더링된 투약 지침] | `renderedDosageInstruction` | 문자열 | 모든 복용 지침에 포함된 복용 용량의 전체 표시. 용량 증가 또는 테이퍼링과 같은 복합 투여를 나타내기 위해 다중 투여량 지시사항이 포함될 때 사용됩니다. |
| [!UICONTROL 보고됨] | `reported` | 부울 | 이 레코드가 원래 기본 원본-팩트 레코드가 아닌 보조 보고 레코드로 캡처되었는지 여부를 나타냅니다. |
| [!UICONTROL 상태] | `status` | 문자열 | 분배 상태. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL 상태 변경됨] | `statusChanged` | 날짜/시간 | 상태가 변경된 날짜(및 선택 사항 시간)입니다. |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![분배 요청 구조](../../../images/healthcare/field-groups/medication-request/dispense-request.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 분배 간격] | `dispenseInterval` | [[!UICONTROL 기간]](../data-types/duration.md) | 약제의 조제 사이에 발생해야 하는 최소 기간. |
| [!UICONTROL 디스펜서] | `dispenser` | [[!UICONTROL 참조]](../data-types/reference.md) | 처방자가 명시한 대로 의약품을 조제할 의도한 조직. |
| [!UICONTROL 디스펜서 명령] | `dispenserInstruction` | [[!UICONTROL 주석]](../data-types/annotation.md) 배열 | 환자에게 제공될 상담과 같은 디스펜서에 대한 추가 정보 |
| [!UICONTROL 용량 투여 보조] | `doseAdministrationAid` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 의약품 분배에 제공될 부착 포장 유형에 대한 정보. |
| [!UICONTROL 예상 공급 기간] | `expectedSupplyDuration` | [[!UICONTROL 기간]](../data-types/duration.md) | 공급된 제품이 사용될 것으로 예상되는 기간 시간 또는 분배가 지속될 것으로 예상되는 시간 길이입니다. |
| [!UICONTROL 초기 채우기] | `initialFill` | 오브젝트 | 초기 채우기에 대한 정보입니다. 다음 두 가지 속성을 포함합니다. <li>`quantity`: 첫 번째 분배 시 제공할 양을 제공하는 [[!UICONTROL 단순 수량]](../data-types/simple-quantity.md) 값입니다.</li> <li>`duration`: 첫 번째 분배가 지속될 것으로 예상되는 시간을 제공하는 [[!UICONTROL Duration]](../data-types/duration.md) 값입니다.</li> |
| [!UICONTROL 수량] | `quantity` | [[!UICONTROL 단순 수량]](../data-types/simple-quantity.md) | 채우기를 위해 분배할 금액입니다. |
| [!UICONTROL 유효 기간] | `validityPeriod` | [[!UICONTROL 기간]](../data-types/period.md) | 시효의 유효 기간. |
| [!UICONTROL 허용된 반복 횟수] | `numberOfRepeatsAllowed` | 정수 | 승인된 리필 수입니다. 최소값은 0입니다. |
