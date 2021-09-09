---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;예약;숙박형;
title: 숙박예약 스키마 필드 그룹
description: 이 문서에서는 Losage Reservation 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 5%

---


# [!UICONTROL Lacting ] Reservationschema 필드 그룹

[!UICONTROL 숙박예약] 은 숙박예약과 관련된 정보를  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 캡처하는 데 사용되는 클래스에 대한 표준 스키마 필드 그룹입니다.

필드 그룹은 [!UICONTROL 예약 세부 정보] 필드 그룹의 확장이며 단일 개체 유형 필드 `reservations` 아래에 동일한 모든 필드를 포함합니다. 이러한 일반 필드 외에 [!UICONTROL 숙박예약]에도 `lodgingReservations` 배열이 포함되어 있습니다. 이 일련의 물건들은 숙박하기에 독특한 속성을 가진 하나 이상의 예약을 설명하는데 사용됩니다.

>[!NOTE]
>
>이 문서에서는 `lodgingReservations` 배열의 세부 정보를 다룹니다. `reservations` 개체 아래에 제공된 다른 필드에 대한 자세한 내용은 [[!UICONTROL 예약 세부 정보] 필드 그룹 참조](./reservation-details.md)를 참조하십시오.

![숙박예약 구조](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` 숙박 예약 목록을 나타내는 일련의 개체입니다. 예약 이벤트가 이동 경로를 따라 여러 다른 호텔에서의 예약을 포함하는 경우, 이러한 예약은 단일 이벤트에 대해 `lodgingReservations` 아래에 개별 객체로 나열될 수 있습니다.

`lodgingReservations` 아래에 제공된 각 개체의 구조는 아래에 나와 있습니다.

![logingReservations 구조](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL 통화]](../../data-types/currency.md) | 호텔방의 일일 평균 가격입니다 |
| `lodgingCheckIn` | 개체 | 숙박 체크인 세부 정보를 설명하는 객체입니다. 다음 값을 포함합니다.<ul><li>`digitalKey`: (정수) 고객이 체크 인할 때 디지털 키 사용을 선택하는 시기를 나타냅니다.</li><li>`earlyCheckInRequested`: (정수) 게스트가 일반 체크인 시간보다 먼저 체크 인을 요청하는 시기를 나타냅니다.</li><li>`lateCheckInRequested`: (정수) 게스트가 일반 체크인 시간보다 늦게 체크 인을 요청하는 시기를 나타냅니다.</li><li>`noRoomCheckIn`: (정수) 이 값은 게스트가 해당 시간에 사용할 수 있는 공간이 없을 때 체크 인을 완료하면 캡처됩니다.</li><li>`oneRoomCheckIn`: (정수) 이 값은 게스트가 해당 시간에 사용할 수 있는 공간이 한 개만 있을 때 체크 인을 완료하면 캡처됩니다.</li><li>`roomKeys`: (정수) 체크인 시 제공되는 표준 회의실 키의 수입니다.</li><li>`userSelectedRoom`: (부울) 게스트가 체크 인에서 방을 선택했는지 여부를 나타냅니다.</li></ul> |
| `rackrate` | [[!UICONTROL 통화]](../../data-types/currency.md) | 사전 예약 없이 당일 예약에 드는 비용입니다. |
| `ID` | 문자열 | 예약 번호 또는 식별자입니다. |
| `agentID` | 문자열 | 호텔 예약과 연관된 에이전트 ID입니다. |
| `basePrice` | 문자열 | 할인이 추가되기 전의 기본 가격. |
| `bookingID` | 문자열 | 호텔 예약과 연관된 예약 ID입니다. |
| `cancellation` | 정수 | 이 값은 예약이 취소된 경우 캡처됩니다. |
| `checkInDate` | DateTime | 객실 예약의 체크인 날짜입니다. |
| `checkOutDate` | DateTime | 객실 예약의 체크아웃 날짜입니다. |
| `confirmationNumber` | 문자열 | 예약 확인 번호 또는 식별자입니다. |
| `couponCode` | 문자열 | 호텔 예약과 연관된 쿠폰 코드입니다. |
| `created` | 정수 | 이 값은 예약이 만들어지면 캡처됩니다. |
| `currencyCode` | 문자열 | 구매에 사용되는 ISO 4217 통화 코드입니다. |
| `discountPercent` | 이중 | 예약과 연관된 할인 백분율입니다. |
| `freeCancelation` | 부울 | 방에 무료 취소 정책이 있는지 여부를 나타냅니다. |
| `guestID` | 문자열 | 호텔 예약과 연관된 게스트 ID입니다. |
| `length` | 정수 | 예약의 총 일수입니다. |
| `loyaltyID` | 문자열 | 예약에 나열된 게스트에 대한 충성도 프로그램 ID입니다. |
| `modification` | 정수 | 이 값은 예약이 수정되었을 때 캡처됩니다. |
| `modificationDate` | DateTime | 예약을 마지막으로 수정한 시간입니다. |
| `numberOfAdults` | 정수 | 예약과 연관된 성인 수입니다. |
| `numberOfChildren` | 정수 | 예약과 연관된 하위 수입니다. |
| `numberOfRooms` | 정수 | 예약과 연결된 객실 수입니다. |
| `propertyID` | 문자열 | 예약 호텔이나 리조트의 식별자입니다. |
| `propertyName` | 문자열 | 예약하신 호텔 또는 리조트의 이름입니다. |
| `purpose` | 문자열 | 예약의 목적(일반적으로 업무 또는 개인). |
| `ratePlan` | 문자열 | 그 방이 팔렸던 요금 거래. |
| `refundable` | 부울 | 환불이 가능한지 여부를 나타냅니다. |
| `reservationStatus` | 문자열 | 예약 상태입니다. |
| `roomAccessibilityType` | 문자열 | 이동성, 청각 등과 같은 룸의 접근성 유형입니다. |
| `roomCapacity` | 정수 | 호텔방에 있는 사람들의 수입니다. |
| `roomType` | 문자열 | 예약중인 방의 유형입니다. |
| `smoking` | 부울 | 방이 흡연을 허용하는지 여부를 나타냅니다. |
| `tripType` | 문자열 | 일방향 여행, 왕복 또는 다중 도시 여행을 예약했는지 여부를 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
