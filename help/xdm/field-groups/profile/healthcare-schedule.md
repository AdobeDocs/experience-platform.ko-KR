---
title: 일정 스키마 필드 그룹
description: 예약 스키마 필드 그룹에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# [!UICONTROL 일정] 스키마 필드 그룹

[!UICONTROL 일정]은(는) [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md) 및 [[!DNL Provider class]](../../classes/provider.md)에 대한 표준 스키마 필드 그룹입니다. 예약 약속에 사용할 수 있는 일정 시간의 컨테이너인 단일 개체 유형 필드 `healthcareSchedule`을(를) 제공합니다.

![필드 그룹 구조](../../images/field-groups/schedule.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 작업자] | `actor` | [[!UICONTROL 참조]](../../data-types/healthcare/reference.md) 배열 | 이 일정을 참조하는 슬롯은 참조된 리소스에 대한 가용성 세부 사항을 제공합니다. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../../data-types/healthcare/identifier.md) 배열 | 예약에 대한 외부 식별자. |
| [!UICONTROL 계획 대상 기간] | `planningHorizon` | [[!UICONTROL 기간]](../../data-types/healthcare/period.md) | 이 일정을 참조하는 슬롯이 없는 경우에도 포함되는 기간입니다. |
| [!UICONTROL 서비스 범주] | `serviceCategory` | [[!UICONTROL 코드 가능한 개념 배열]](../../data-types/healthcare/codeable-concept.md) | 약속 중에 수행할 서비스에 대한 광범위한 분류. |
| [!UICONTROL 서비스 유형] | `serviceType` | [[!UICONTROL 코드 가능한 참조]](../../data-types/healthcare/codeable-reference.md) 배열 | 약속 중에 수행할 특정 서비스입니다. |
| [!UICONTROL 전문] | `specialty` | [[!UICONTROL 코드 가능한 개념 배열]](../../data-types/healthcare/codeable-concept.md) | 약속에서 요청된 서비스를 수행하는 데 필요한 개업의 전문성. |
| [!UICONTROL 활성] | `active` | 부울 | 일정 레코드가 활성 상태인지 여부를 나타냅니다. |
| [!UICONTROL 댓글] | `comment` | 문자열 | 슬롯에 대한 사용자 지정 제한 등 확장된 정보를 설명하는 데 사용할 수 있는 가용성에 대한 설명입니다. |
| [!UICONTROL 이름] | `name` | 문자열 | 검색하는 동안 소비자에게 표시되는 일정에 대한 설명입니다. |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
