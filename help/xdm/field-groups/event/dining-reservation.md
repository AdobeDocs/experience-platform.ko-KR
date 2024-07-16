---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;예약;식사;
title: 식사 예약 스키마 필드 그룹
description: 식사 예약 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 13%

---

# [!UICONTROL 식사 예약] 스키마 필드 그룹

[!UICONTROL 식사 예약]은(는) 식사 예약 관련 정보를 캡처하는 데 사용되는 [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)의 표준 스키마 필드 그룹입니다.

필드 그룹은 [!UICONTROL 예약 세부 정보] 필드 그룹의 확장이며 단일 개체 유형 필드 `reservations`에 있는 동일한 필드를 모두 포함합니다. 이러한 일반 필드 외에 [!UICONTROL 식사 예약]에는 `diningReservations` 배열도 포함됩니다. 이 객체 배열은 레스토랑별 속성을 가진 하나 이상의 예약을 설명하는 데 사용됩니다.

>[!NOTE]
>
>이 문서에서는 `diningReservations` 배열에 대한 세부 정보를 다룹니다. `reservations` 개체 아래에 제공된 다른 필드에 대한 자세한 내용은 [[!UICONTROL 예약 세부 정보] 필드 그룹 참조](./reservation-details.md)를 참조하십시오.

![식사 예약 구조](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations`은(는) 식사 예약 목록을 나타내는 개체 배열입니다. 예를 들어 예약 이벤트에 하루 중 서로 다른 시간에 여러 개의 다른 레스토랑에서 예약하는 경우 이러한 예약은 단일 이벤트에 대해 `diningReservations` 아래에 개별 객체로 나열될 수 있습니다.

`diningReservations` 아래에 제공된 각 개체의 구조는 아래에 나와 있습니다.

![diningReservations 구조](../../images/field-groups/dining-reservation/diningReservations.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `ID` | 문자열 | 예약 번호 또는 식별자. |
| `cancellation` | 정수 | 이 값은 예약이 취소되면 캡처됩니다. |
| `confirmationNumber` | 문자열 | 예약 확인 번호 또는 식별자. |
| `created` | 정수 | 이 값은 예약이 생성되면 캡처됩니다. |
| `cuisine` | 정수 | 레스토랑 요리 종류. |
| `currencyCode` | 문자열 | 구매 시 사용되는 ISO 4217 통화 코드. |
| `deliveryPartners` | 문자열 | 레스토랑에서 사용 가능한 배달 파트너. |
| `diningOptions` | 문자열 | 레스토랑에서 사용 가능한 배달 및 식사 옵션. |
| `groupReservation` | 부울 | 그룹에 대한 예약 여부를 나타냅니다. |
| `length` | 정수 | 총 예약 일수. |
| `loyaltyID` | 문자열 | 예약에 나열된 게스트에 대한 고객 충성도 프로그램 ID입니다. |
| `modification` | 정수 | 이 값은 예약이 수정되면 캡처됩니다. |
| `modificationDate` | 날짜/시간 | 예약을 마지막으로 수정한 시간입니다. |
| `numberOfAdults` | 정수 | 예약한 성인 수입니다. |
| `numberOfChildren` | 정수 | 예약과 연계된 하위 항목 수. |
| `numberOfRooms` | 정수 | 예약과 연계된 룸 수. |
| `partySize` | 정수 | 식사 파티에 참석한 개인 수. |
| `priceCategory` | 문자열 | 진행 중인 예약 요금 범주. |
| `purpose` | 문자열 | 예약 목적(일반적으로 비즈니스 또는 개인). |
| `reservationTime` | 날짜/시간 | 식사가 예약된 시간. |
| `restaurantID` | 문자열 | 레스토랑 또는 식사 위치에 대한 식별자. |
| `reservationStatus` | 문자열 | 예약 상태. |
| `specialOccasion` | 부울 | 특별 행사를 위한 예약인지 여부를 나타냅니다. |
| `status` | 정수 | 식사 예약 상태. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
