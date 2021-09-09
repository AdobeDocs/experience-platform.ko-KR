---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;예약;식사;
title: 식사 예약 스키마 필드 그룹
description: 이 문서에서는 Dining Reservation 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---


# [!UICONTROL 식사 ] 예약 스키마 필드 그룹

[!UICONTROL Dining ] Reservations는 식사 예약에 대한 정보를  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 캡처하는 데 사용되는 클래스에 대한 표준 스키마 필드 그룹입니다.

필드 그룹은 [!UICONTROL 예약 세부 정보] 필드 그룹의 확장이며 단일 개체 유형 필드 `reservations` 아래에 동일한 모든 필드를 포함합니다. 이러한 일반 필드 외에 [!UICONTROL Dining Reservation]에도 `diningReservations` 배열이 포함되어 있습니다. 이 개체 집합은 하나 이상의 레스토랑 특정 속성의 예약을 설명하는 데 사용됩니다.

>[!NOTE]
>
>이 문서에서는 `diningReservations` 배열의 세부 정보를 다룹니다. `reservations` 개체 아래에 제공된 다른 필드에 대한 자세한 내용은 [[!UICONTROL 예약 세부 정보] 필드 그룹 참조](./reservation-details.md)를 참조하십시오.

![식사 예약 구조](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` 는 식사 예약 목록을 나타내는 일련의 개체입니다. 예약 이벤트가 다른 시간에 여러 다른 레스토랑에서 예약하는 경우, 예를 들어, 이러한 예약은 단일 이벤트에 대해 `diningReservations` 아래에 개별 객체로 나열될 수 있습니다.

`diningReservations` 아래에 제공된 각 개체의 구조는 아래에 나와 있습니다.

![diningReservations 구조](../../images/field-groups/dining-reservation/diningReservations.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `ID` | 문자열 | 예약 번호 또는 식별자입니다. |
| `cancellation` | 정수 | 이 값은 예약이 취소된 경우 캡처됩니다. |
| `confirmationNumber` | 문자열 | 예약 확인 번호 또는 식별자입니다. |
| `created` | 정수 | 이 값은 예약이 만들어지면 캡처됩니다. |
| `cuisine` | 정수 | 레스토랑 요리 종류입니다. |
| `currencyCode` | 문자열 | 구매에 사용되는 ISO 4217 통화 코드입니다. |
| `deliveryPartners` | 문자열 | 레스토랑에서 제공하는 배달 파트너 |
| `diningOptions` | 문자열 | 레스토랑에서 배달 및 식사를 즐기실 수 있습니다. |
| `groupReservation` | 부울 | 그룹에 대한 예약 여부를 나타냅니다. |
| `length` | 정수 | 예약의 총 일수입니다. |
| `loyaltyID` | 문자열 | 예약에 나열된 게스트에 대한 충성도 프로그램 ID입니다. |
| `modification` | 정수 | 이 값은 예약이 수정되었을 때 캡처됩니다. |
| `modificationDate` | DateTime | 예약을 마지막으로 수정한 시간입니다. |
| `numberOfAdults` | 정수 | 예약과 연관된 성인 수입니다. |
| `numberOfChildren` | 정수 | 예약과 연관된 하위 수입니다. |
| `numberOfRooms` | 정수 | 예약과 연결된 객실 수입니다. |
| `partySize` | 정수 | 식사 파티에 있는 개인 수입니다. |
| `priceCategory` | 문자열 | 예약의 가격 범주입니다. |
| `purpose` | 문자열 | 예약의 목적(일반적으로 업무 또는 개인). |
| `reservationTime` | DateTime | 식사 예약 시간이 예약되어 있습니다 |
| `restaurantID` | 문자열 | 레스토랑 또는 식사 위치의 식별자입니다. |
| `reservationStatus` | 문자열 | 예약 상태입니다. |
| `specialOccasion` | 부울 | 특별한 경우에 예약되는지 여부를 나타냅니다. |
| `status` | 정수 | 식사 예약 상태입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
