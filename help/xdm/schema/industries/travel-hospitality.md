---
solution: Experience Platform
title: 여행 및 접대 산업 데이터 모델 ERD
description: Adobe Experience Platform에서 사용할 XDM(경험 데이터 모델)과 호환되는 여행 및 숙박 업계에 대한 표준화된 데이터 모델을 설명하는 ERD(엔티티 관계 다이어그램)를 봅니다.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!UICONTROL 여행 및 접대] 업계 데이터 모델 ERD

다음 엔티티 관계 다이어그램(ERD)은 여행 및 숙박 산업에 대한 표준화된 데이터 모델을 나타냅니다. ERD는 Adobe Experience Platform에서 데이터가 저장되는 방식을 고려하여 비표준화된 방식으로 의도적으로 제공됩니다.

>[!NOTE]
>
>설명된 대로 ERD는 이 업계 사용 사례에 맞게 데이터를 모델링하는 방법에 대한 권장 사항입니다. Experience Platform에서 이 데이터 모델을 사용하려면 권장 스키마와 해당 관계를 직접 구성해야 합니다. 자세한 내용은 UI에서 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) 관리에 대한 안내서를 참조하십시오.

다음 범례를 사용하여 이 ERD를 해석하십시오.

* 에 표시된 각 엔터티는 기본 [XDM(경험 데이터 모델) 클래스](../composition.md#class)를 기반으로 합니다.
* 상위 필드 아래에 들여쓴 필드는 상위 필드 그룹에 속하는 하위 필드 또는 하위 필드를 나타냅니다.
* 지정된 엔티티에 대한 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 &quot;ID&quot;로 표시되며, 이러한 속성 중 하나는 &quot;기본 ID&quot;로 표시됩니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 개인이나 개인을 결정할 수 없는 경우가 많기 때문에 엔티티 관계는 종속되지 않는 것으로 표시됩니다.

![여행 접대 데이터 모델에 대한 ERD 예](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>Experience Event 엔티티는 XDM ExperienceEvent 클래스에서 제공하는 고유 식별자(`_id`) 특성을 나타내는 &quot;_ID&quot; 필드를 포함합니다. 이 값에 필요한 사항에 대한 자세한 내용은 [XDM ExperienceEvent](../../classes/experienceevent.md)에 대한 참조 문서를 참조하십시오.

## [!UICONTROL 여행 및 접대] 사용 사례

다음 표에서는 여행 및 숙박 산업의 몇 가지 일반적인 사용 사례에 대한 권장 클래스 및 스키마 필드 그룹을 간략하게 설명합니다.

| 활용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 시장 내 고객과 호텔 예약 고객에게 식사 및 기타 상주 명소를 교차 판매합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예약 세부 정보](../../field-groups/event/reservation-details.md)</li><li>[숙박 예약](../../field-groups/event/lodging-reservation.md)</li><li>[식사 예약](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[회사 연락처 정보](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 마켓 내 고객과 향후 호텔 예약 고객에게 식사 및 기타 상주 명소를 업셀합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예약 세부 정보](../../field-groups/event/reservation-details.md)</li><li>[식사 예약](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[회사 연락처 정보](../../field-groups/profile/work-contact-details.md)</li><li>[충성도 세부 정보](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 마켓 내 투숙객 및 예정된 호텔 예약 고객에게 상향 판매 호텔 및 기타 상주 명소를 제공합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예약 세부 정보](../../field-groups/event/reservation-details.md)</li><li>[숙박 예약](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[회사 연락처 정보](../../field-groups/profile/work-contact-details.md)</li><li>[충성도 세부 정보](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 마켓 내 투숙객 및 예정된 호텔 예약 고객에게 상향 판매 항공편 및 기타 상주 명소. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예약 세부 정보](../../field-groups/event/reservation-details.md)</li><li>[비행 예약](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[회사 연락처 정보](../../field-groups/profile/work-contact-details.md)</li><li>[충성도 세부 정보](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
