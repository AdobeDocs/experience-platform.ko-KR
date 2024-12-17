---
title: 의료 데이터 모델 V2
description: 몇 가지 일반적인 의료 서비스 사용 사례와 최상의 클래스, 관련 필드 그룹 및 사용할 데이터 유형에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 8520be2a000edfd2d92bfbc6ebed41b1536fffc1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 3%

---

# [!UICONTROL 의료] 데이터 모델 V2

## 필드 그룹 및 클래스 {#field-groups}

다음 표에서는 몇 가지 일반적인 의료 서비스 사용 사례에 대한 권장 클래스 및 스키마 필드 그룹을 간략하게 설명합니다.

| 활용 사례 | 필드 그룹 및 호환 클래스 |
| --- | --- |
| **환자 만들기/업데이트**: 환자가 병원 프런트 데스크에 도착하면 식별자(선택 사항), 환자 이름, 생년월일, 성별 및 주소 등 인구 통계학적 세부 정보를 포함한 환자 기록이 설정됩니다. 이는 의료 IT의 핵심 구성 요소 역할을 합니다. | <ul><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[환자](./field-groups/patient.md)</li></ul></li></ul> |
| **예방접종**: 예방접종 프로세스 촉진, 환자 예방접종 기록 관리 및 EMR과 백신 관리 시스템 통합. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예방 접종](./field-groups/immunization.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[의약품 분배](./field-groups/medication-dispense.md)</li><li>[약물 요청](./field-groups/medication-request.md)</li><li>[환자](./field-groups/patient.md)</li></ul></li><li>**[위치](./classes/location.md)**:<ul><li>[위치](./field-groups/location.md)</li></ul><li>**[약물](../../classes/medication.md)**:<ul><li>[약물](./field-groups/medication.md)</li><li>[의약품 분배](./field-groups/medication-dispense.md)</li><li>[약물 요청](./field-groups/medication-request.md)</li></ul></li><li>**[공급자](../../classes/provider.md)**:<ul><li>[의약품 분배](./field-groups/medication-dispense.md)</li><li>[약물 요청](./field-groups/medication-request.md)</li></ul></li></ul> |
| **사후 관리 준수**: 환자와 간병인이 치료 계획을 완료하고 송금 비율을 줄일 수 있도록 동기를 부여합니다. | <ul><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[의료 서비스 플랜](./field-groups/care-plan.md)</li><li>[목표](./field-groups/goal.md)</li><li>[환자](./field-groups/patient.md)</li></ul></li><li>**[위치](./classes/location.md)**:<ul><li>[위치](./field-groups/location.md)</li></ul><li>**[공급자](../../classes/provider.md)**:<ul><li>[목표](./field-groups/goal.md)</li></ul></li></ul> |
| **보험에 대한 소비자 경험**: 보험에 가입하는 소비자 간의 디지털 획득 및 경험을 개선합니다. 해당 예는 다음과 같습니다. <li> 일반 정보(플랜, 플랜 이름/계층, 메디케이드 또는 웰빙 프로그램 등)가 포함된 페이지에 액세스하는 사람들에게 홍보 이메일 또는 타깃팅된 서드파티 광고를 보내기 위한 소비자 행동 이해</li><li> 심장 건강 및 백신 정보를 찾는 사람들에게 브랜드 경각심을 조성하기 위해 심장 건강에 대한 백신 관련 정보를 보내거나 백신 예약 요청을 보냅니다. </li> | <ul><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[계정](./field-groups/account.md)</li><li>[의약품 분배](./field-groups/medication-dispense.md)</li><li>[약물 요청](./field-groups/medication-request.md)</li><li>[환자](./field-groups/patient.md)</li></ul></li><li>**[위치](./classes/location.md)**:<ul><li>[위치](./field-groups/location.md)</li></ul><li>**[약물](../../classes/medication.md)**:<ul><li>[약물](./field-groups/medication.md)</li><li>[의약품 분배](./field-groups/medication-dispense.md)</li><li>[약물 요청](./field-groups/medication-request.md)</li></ul></li><li>**[공급자](../../classes/provider.md)**:<ul><li>[계정](./field-groups/account.md)</li><li>[의약품 분배](./field-groups/medication-dispense.md)</li><li>[약물 요청](./field-groups/medication-request.md)</li></ul><li>**[계획](../../classes/plan.md)**:<ul><li>[목표](./field-groups/coverage.md)</li></ul></li></ul> |
| **공급자 환경 개선**: EMR 시스템의 공급자 데이터를 사용하여 약속 가용성, 위치 및 특수성에 따라 대체 공급자를 제안합니다. <br> <br>공급자 검색을 개선하여 원하는 가용성의 결과를 표시하고, 선택한 공급자가 지불 네트워크에 포함되어 있는지 확인하고, 예상 비용을 제공합니다. | <ul><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[약속](./field-groups/appointment.md)</li><li>[조직](./field-groups/organization.md)</li><li>[환자](./field-groups/patient.md)</li><li>[실무자](./field-groups/practioner.md)</li><li>[일정](./field-groups/schedule.md)</li></ul></li><li>**[위치](./classes/location.md)**:<ul><li>[위치](./field-groups/location.md)</li></ul><li>**[공급자](../../classes/provider.md)**:<ul><li>[약속](./field-groups/appointment.md)</li><li>[조직](./field-groups/organization.md)</li><li>[실무자](./field-groups/practioner.md)</li><li>[일정](./field-groups/schedule.md)</li></ul></li></ul> |

{style="table-layout:auto"}

## 데이터 유형 {#data-types}

다음 표에서는 [!DNL HL7 FHIR Release 5] 사양에 따라 만들어진 데이터 형식을 설명합니다.

| 이름 | 설명 |
| --- | --- |
| [[!UICONTROL 주소]](./data-types/address.md) | GPS 또는 기타 위치 정의 형식이 아니라 우편 규칙을 사용하여 표현된 주소를 설명합니다. |
| [[!UICONTROL 주석]](./data-types/annotation.md) | 작성자에 대한 속성이 있는 텍스트 노드입니다. |
| [[!UICONTROL 가용성]](./data-types/availability.md) | 항목에 대한 가용성 데이터입니다. |
| [[!UICONTROL 코드 가능한 개념]](./data-types/codeable-concept.md) | 한 리소스에서 다른 리소스로의 참조. |
| [[!UICONTROL 코드 사용 가능한 참조]](./data-types/codeable-reference.md) | 리소스 또는 개념에 대한 참조입니다. |
| [[!UICONTROL 코딩]](./data-types/coding.md) | 용어 시스템에 의해 정의된 코드에 대한 참조. |
| [[!UICONTROL 연락처]](./data-types/contact-point.md) | 개인용 연락처 세부 정보. |
| [[!UICONTROL 용량]](./data-types/dosage.md) | 약물 복용 방법/복용 또는 복용해야 하는 방법. |
| [[!UICONTROL 기간]](./data-types/duration.md) | 오랜 시간. |
| [[!UICONTROL 확장 연락처 세부 정보]](./data-types/extended-contact-detail.md) | 확장 연락처의 정보입니다. |
| [[!UICONTROL 사람 이름]](./data-types/human-name.md) | 사람 또는 기타 살아있는 개체의 이름에 대한 정보입니다. |
| [[!UICONTROL 식별자]](./data-types/identifier.md) | 계산용 식별자입니다. |
| [[!UICONTROL 돈]](./data-types/money.md) | 일부 인정된 통화로 표시된 경제적 효용. |
| [[!UICONTROL 기간]](./data-types/period.md) | 시작 및 종료 날짜/시간으로 정의된 기간. |
| [[!UICONTROL 사용자]](./data-types/person.md) | 일반 개인 레코드에 대한 정보. |
| [[!UICONTROL 수량]](./data-types/quantity.md) | 측정 또는 측정 가능한 양. |
| [[!UICONTROL Range]](./data-types/range.md) | 낮은 값과 높은 값으로 바인딩된 값 세트입니다. |
| [[!UICONTROL 비율]](./data-types/ratio.md) | 분자 및 분모를 통한 두 [[!UICONTROL 수량]](./data-types/quantity.md) 값의 비율입니다. |
| [[!UICONTROL 참조]](./data-types/reference.md) | 한 리소스에서 다른 리소스로의 참조. |
| [[!UICONTROL 반복]](./data-types/repeat.md) | 이벤트가 예약되는 시기를 설명하는 규칙 세트입니다. |
| [[!UICONTROL 단순 수량]](./data-types/simple-quantity.md) | 측정 또는 측정 가능한 양. |
| [[!UICONTROL 시간]](./data-types/timing.md) | 여러 번 발생할 수 있는 이벤트에 대한 정보입니다. |
| [[!UICONTROL 가상 서비스 세부 정보]](./data-types/virtual-service-detail.md) | 가상 서비스 연락처 세부 정보. |
