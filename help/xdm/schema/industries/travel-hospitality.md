---
solution: Experience Platform
title: 여행 및 숙박 업계 데이터 모델 ERD
description: Adobe Experience Platform에서 사용할 XDM(Experience Data Model)과 호환되는 여행 및 숙박 산업에 대한 표준화된 데이터 모델을 설명하는 ERD(엔티티 관계 다이어그램)를 봅니다.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# [!UICONTROL 여행 및 숙박] 업계 데이터 모델 ERD

다음 엔티티 관계 다이어그램(ERD)은 여행 및 숙박 산업에 대한 표준화된 데이터 모델을 나타냅니다. ERD는 Adobe Experience Platform에 데이터가 저장되는 방식을 고려하여 의도적으로 표준화된 방식으로 제공됩니다.

>[!NOTE]
>
>설명된 ERD는 이 업계 사용 사례에 대해 데이터를 모델링하는 방법에 대한 권장 사항입니다. Platform에서 이 데이터 모델을 사용하려면 권장 스키마와 관계를 직접 구성해야 합니다. 관리에 대한 안내서를 참조하십시오 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) ( UI에서)를 참조하십시오.

이 ERD를 해석하려면 다음 범례를 사용하십시오.

* 에 표시된 각 엔티티는 기본 [XDM(경험 데이터 모델) 클래스](../composition.md#class).
* 지정된 엔티티의 경우 각 행이 **굵게** 는 필드 그룹 또는 데이터 유형을 나타내며, 이 필드가 제공하는 관련 필드는 번역되지 않은 텍스트로 나열됩니다.
* 주어진 엔터티에 대해 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 다음 속성 중 하나가 &quot;기본 ID&quot;로 표시되어 있습니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 사람이나 개인을 결정할 수 없기 때문에 엔티티 관계는 비종속적으로 표시됩니다.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>경험 이벤트 엔티티에는 고유 식별자(`_id`) 속성 을 사용할 수 있습니다. 다음에서 참조 문서를 참조하십시오. [XDM ExperienceEvent](../../classes/experienceevent.md) 를 참조하십시오.

## [!UICONTROL 여행 및 숙박] 사용 사례

다음 표에서는 여행 및 숙박 산업을 위한 몇 가지 공통 사용 사례에 대해 권장되는 클래스 및 스키마 필드 그룹에 대해 설명합니다.

| 사용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 호텔 예약 시 시장 투숙객과 손님에게 크로스셀 식사 및 기타 지역 관광 명소를 제공합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예약 세부 정보](../../field-groups/event/reservation-details.md)</li><li>[숙박예약](../../field-groups/event/lodging-reservation.md)</li><li>[식사 예약](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 세부 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[작업 연락처 세부 정보](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 호텔 예약 시 시장 투숙객과 손님에게 업셀(Up-sell) 식사 및 기타 지역 관광 명소를 제공합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예약 세부 정보](../../field-groups/event/reservation-details.md)</li><li>[식사 예약](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 세부 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[작업 연락처 세부 정보](../../field-groups/profile/work-contact-details.md)</li><li>[충성도 세부 사항](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 호텔 예약 시 시장 투숙객과 손님에게 업셀 호텔 및 기타 지역 관광 명소를 제공합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예약 세부 정보](../../field-groups/event/reservation-details.md)</li><li>[숙박예약](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 세부 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[작업 연락처 세부 정보](../../field-groups/profile/work-contact-details.md)</li><li>[충성도 세부 사항](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 호텔 예약 시 시장 투숙객과 손님에게 상향 판매 항공권 및 기타 지역 관광 정보를 제공해 드립니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[예약 세부 정보](../../field-groups/event/reservation-details.md)</li><li>[비행 예약](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 세부 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[작업 연락처 세부 정보](../../field-groups/profile/work-contact-details.md)</li><li>[충성도 세부 사항](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
