---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;예약;플라이트;
title: 플라이트 예약 스키마 필드 그룹
description: 이 문서에서는 비행기 예약 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 4%

---


# [!UICONTROL 플라이트 ] 예약 스키마 필드 그룹

[!UICONTROL Flight ] Reserve는 비행 예약에 대한 정보를 캡처하는  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 데 사용되는 클래스에 대한 표준 스키마 필드 그룹입니다.

필드 그룹은 [!UICONTROL 예약 세부 정보] 필드 그룹의 확장이며 단일 개체 유형 필드 `reservations` 아래에 동일한 모든 필드를 포함합니다. 이러한 일반 필드 외에 [!UICONTROL 플라이트 예약]에도 `flightReservations` 배열이 포함되어 있습니다. 이 일련의 물건들은 비행기 여행에 고유한 속성을 가진 하나 이상의 예약을 설명하는 데 사용됩니다.

>[!NOTE]
>
>이 문서에서는 `flightReservations` 배열의 세부 정보를 다룹니다. `reservations` 개체 아래에 제공된 다른 필드에 대한 자세한 내용은 [[!UICONTROL 예약 세부 정보] 필드 그룹 참조](./reservation-details.md)를 참조하십시오.

![비행 예약 구조](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` 는 비행 예약 목록을 나타내는 객체의 배열입니다. 예약 이벤트에 이동 중 여러 연결 비행에 대한 예약이 포함된 경우, 예를 들어 이러한 예약은 단일 이벤트에 대해 `flightReservations` 아래에 개별 객체로 나열될 수 있습니다.

`flightReservations` 아래에 제공된 각 개체의 구조는 아래에 나와 있습니다.

![flightReservations 구조](../../images/field-groups/flight-reservation/flightReservations.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `flightCheckIn` | 개체 | 플라이트 체크 인에 대한 세부 사항을 캡처합니다. 객체에는 다음 속성이 포함됩니다.<ul><li>`arrivalAirportCode`: (문자열) 도착 시의 공항 코드입니다.</li><li>`boardingGroup`: (문자열) 탑승 주문의 항공별 지표입니다.</li><li>`checkInMethod`: (문자열) 체크인을 사용한 방법(예: 카운터, 온라인, 키오스크 또는 셀프 서비스)입니다.</li><li>`checkedBags`: (정수) 비행기에 대해 체크된 가방 수입니다.</li><li>`checkedPassengers`: (정수) 동일한 예약 번호에 대해 여러 명의 승객이 있는 경우, 비행을 위해 탑승 수속을 한 승객의 수입니다.</li><li>`confirmationNumber`: (문자열) 예약 확인 번호 또는 식별자입니다.</li><li>`departureAirportCode`: (문자열) 출발 도시의 공항 코드입니다.</li><li>`flightNumber`: (문자열) 예약되는 비행편의 비행 번호입니다.</li></ul> |
| `flightStatusSearch` | 개체 | 비행 상태를 검색할 때 반환되는 세부 정보를 캡처합니다. 객체에는 다음 속성이 포함됩니다.<ul><li>`arrivalAirportCode`: (문자열) 도착 시의 공항 코드입니다.</li><li>`boardingGroup`: (문자열) 탑승 주문의 항공별 지표입니다.</li><li>`departureAirportCode`: (문자열) 출발 도시의 공항 코드입니다.</li><li>`departureDate`: (DateTime) 예약되는 비행의 출발일입니다.</li><li>`flightNumber`: (문자열) 예약되는 비행편의 비행 번호입니다.</li><li>`searchCount`: (정수) 예약된 비행의 상태를 검색한 횟수입니다.</li></ul> |
| `agentID` | 문자열 | 해당되는 경우 예약 업무를 담당하는 대리인이나 부서입니다. |
| `aircraftID` | 문자열 | 항공기의 식별자입니다. |
| `aircraftType` | 문자열 | 항공기의 유형입니다. |
| `arrivalAirportCode` | 문자열 | 도착시의 공항번호. |
| `arrivalDate` | DateTime | 예약중인 비행편의 도착일자입니다. |
| `cancellation` | 정수 | 이 값은 예약이 취소된 경우 캡처됩니다. |
| `confirmationNumber` | 문자열 | 예약 확인 번호 또는 식별자입니다. |
| `created` | 문자열 | 이 값은 예약이 만들어지면 캡처됩니다. |
| `currencyCode` | 문자열 | 구매에 사용되는 ISO 4217 통화 코드입니다. |
| `departureAirportCode` | 문자열 | 출발 도시의 공항번호. |
| `departureDate` | DateTime | 예약중인 비행기 출발일자입니다. |
| `fareClass` | 문자열 | 항공편의 요금 등급은 예약되어 있습니다 |
| `flightNumber` | 문자열 | 예약하고 있는 비행편 번호입니다. |
| `length` | 정수 | 예약의 총 일수입니다. |
| `loyaltyID` | 문자열 | 예약에 나열된 승객에 대한 충성도 또는 보상 프로그램 ID입니다. |
| `modification` | 정수 | 이 값은 예약이 수정되었을 때 캡처됩니다. |
| `modificationDate` | DateTime | 예약을 마지막으로 수정한 시간입니다. |
| `numberOfAdults` | 정수 | 예약과 연관된 성인 수입니다. |
| `numberOfChildren` | 정수 | 예약과 연관된 하위 수입니다. |
| `passengerID` | 문자열 | 예약과 관련된 승객 정보입니다. |
| `purpose` | 문자열 | 예약의 목적(일반적으로 업무 또는 개인). |
| `salesChannel` | 문자열 | 예약한 영업 채널입니다. |
| `securityScreening` | 문자열 | 탑승객의 보안검색의 종류는 대상이 된다. |
| `status` | 문자열 | 비행기 예약 상태입니다. |
| `ticketNumber` | 문자열 | 예약 번호 또는 식별자입니다. |
| `tripType` | 문자열 | 일방향 여행, 왕복 또는 다중 도시 여행을 예약했는지 여부를 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
