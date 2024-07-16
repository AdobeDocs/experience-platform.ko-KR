---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;예약;숙박;
title: 숙박 예약 스키마 필드 그룹
description: 숙박 예약 스키마 필드 그룹에 대해 알아봅니다.
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 7%

---

# [!UICONTROL 숙박 예약] 스키마 필드 그룹

[!UICONTROL 숙박 예약]은(는) 숙박 예약 관련 정보를 캡처하는 데 사용되는 [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다.

필드 그룹은 [!UICONTROL 예약 세부 정보] 필드 그룹의 확장이며 단일 개체 유형 필드 `reservations`에 있는 동일한 필드를 모두 포함합니다. 이러한 일반 필드 외에도 [!UICONTROL 숙박 예약]에는 `lodgingReservations` 배열도 포함됩니다. 이 객체 배열은 숙박 고유 속성을 가진 하나 이상의 예약을 설명하는 데 사용됩니다.

>[!NOTE]
>
>이 문서에서는 `lodgingReservations` 배열에 대한 세부 정보를 다룹니다. `reservations` 개체 아래에 제공된 다른 필드에 대한 자세한 내용은 [[!UICONTROL 예약 세부 정보] 필드 그룹 참조](./reservation-details.md)를 참조하십시오.

![숙박 예약 구조](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations`은(는) 숙박 예약 목록을 나타내는 개체 배열입니다. 예를 들어, 여행 경로에 따라 여러 다른 호텔에서 예약하는 예약 이벤트가 포함된 경우 이러한 예약은 단일 이벤트에 대해 `lodgingReservations` 아래에 개별 객체로 나열될 수 있습니다.

`lodgingReservations` 아래에 제공된 각 개체의 구조는 아래에 나와 있습니다.

![lodgingReservations 구조](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL 통화]](../../data-types/currency.md) | 호텔 룸의 평균 일일 가격. |
| `lodgingCheckIn` | 오브젝트 | 숙박 체크인 세부 사항을 설명하는 개체입니다. 다음 값을 포함합니다.<ul><li>`digitalKey`: (정수) 게스트가 체크인 시 디지털 키 사용을 선택하는 경우를 나타냅니다.</li><li>`earlyCheckInRequested`: (정수) 게스트가 일반 체크인 시간보다 일찍 체크인을 요청하는 경우를 나타냅니다.</li><li>`lateCheckInRequested`: (정수) 게스트가 일반 체크인 시간보다 늦게 체크인을 요청하는 경우를 나타냅니다.</li><li>`noRoomCheckIn`: (정수) 해당 시간에 사용할 수 있는 룸이 없을 때 게스트가 체크인을 마치면 이 값이 캡처됩니다.</li><li>`oneRoomCheckIn`: (정수) 해당 시간에 사용할 수 있는 방이 하나만 있을 때 게스트가 체크 인을 마치면 이 값이 캡처됩니다.</li><li>`roomKeys`: (정수) 체크 인 시 제공되는 표준 룸 키 수입니다.</li><li>`userSelectedRoom`: (부울) 체크인 시 게스트가 룸을 선택했는지 여부를 나타냅니다.</li></ul> |
| `rackrate` | [[!UICONTROL 통화]](../../data-types/currency.md) | 사전 예약 준비 없이 당일 예약하는 경우 요금. |
| `ID` | 문자열 | 예약 번호 또는 식별자. |
| `agentID` | 문자열 | 호텔 예약과 연계된 에이전트 ID. |
| `basePrice` | 문자열 | 할인이 추가되기 전의 기본 가격. |
| `bookingID` | 문자열 | 호텔 예약과 연계된 예약 ID. |
| `cancellation` | 정수 | 이 값은 예약이 취소되면 캡처됩니다. |
| `checkInDate` | 날짜/시간 | 룸 예약을 위한 체크인 날짜. |
| `checkOutDate` | 날짜/시간 | 룸 예약을 위한 체크아웃 날짜. |
| `confirmationNumber` | 문자열 | 예약 확인 번호 또는 식별자. |
| `couponCode` | 문자열 | 호텔 예약과 연계된 쿠폰 코드. |
| `created` | 정수 | 이 값은 예약이 생성되면 캡처됩니다. |
| `currencyCode` | 문자열 | 구매 시 사용되는 ISO 4217 통화 코드. |
| `discountPercent` | 더블 | 예약과 연계된 할인율. |
| `freeCancelation` | 부울 | 룸에 무료 취소 정책이 있는지 여부를 나타냅니다. |
| `guestID` | 문자열 | 호텔 예약과 연계된 게스트 ID. |
| `length` | 정수 | 총 예약 일수. |
| `loyaltyID` | 문자열 | 예약에 나열된 게스트에 대한 고객 충성도 프로그램 ID입니다. |
| `modification` | 정수 | 이 값은 예약이 수정되면 캡처됩니다. |
| `modificationDate` | 날짜/시간 | 예약을 마지막으로 수정한 시간입니다. |
| `numberOfAdults` | 정수 | 예약한 성인 수입니다. |
| `numberOfChildren` | 정수 | 예약과 연계된 하위 항목 수. |
| `numberOfRooms` | 정수 | 예약과 연계된 룸 수. |
| `propertyID` | 문자열 | 예약용 호텔 또는 리조트 식별자. |
| `propertyName` | 문자열 | 예약용 호텔 또는 리조트 이름. |
| `purpose` | 문자열 | 예약 목적(일반적으로 비즈니스 또는 개인). |
| `ratePlan` | 문자열 | 특가 상품으로 룸 판매. |
| `refundable` | 부울 | 룸을 환불 가능한지 여부를 나타냅니다. |
| `reservationStatus` | 문자열 | 예약 상태. |
| `roomAccessibilityType` | 문자열 | 이동성, 청력 또는 기타 룸의 접근성 유형. |
| `roomCapacity` | 정수 | 호텔의 수용 인원수. |
| `roomType` | 문자열 | 예약 중인 룸 유형. |
| `smoking` | 부울 | 룸에서 흡연을 허용하는지 여부를 나타냅니다. |
| `tripType` | 문자열 | 예약이 편도 여행인지, 왕복인지, 아니면 여러 도시인지 여부를 나타냅니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
