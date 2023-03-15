---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;예약;비행;
title: 비행 예약 스키마 필드 그룹
description: 이 문서에서는 비행 예약 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 4%

---

# [!UICONTROL 비행 예약] 스키마 필드 그룹

[!UICONTROL 비행 예약] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md) 비행 예약 관련 정보를 캡처하는 데 사용됩니다.

필드 그룹은 의 확장입니다 [!UICONTROL 예약 세부 정보] 필드 그룹 및 단일 개체 유형 필드 아래에 있는 동일한 필드를 모두 포함합니다. `reservations`. 이러한 일반 필드 외에도 [!UICONTROL 비행 예약] 또한 다음을 포함 `flightReservations` 배열입니다. 이 객체 배열은 항공 여행에 고유한 속성을 가진 하나 이상의 예약을 설명하는 데 사용됩니다.

>[!NOTE]
>
>이 문서에서는 `flightReservations` 배열입니다. 아래에 제공된 다른 필드에 대한 자세한 내용은 `reservations` 개체를 참조하십시오. [[!UICONTROL 예약 세부 정보] 필드 그룹 참조](./reservation-details.md).

![비행 예약 구조](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` 는 비행 예약 목록을 나타내는 객체 배열입니다. 예를 들어, 예약 이벤트에 여행에서 여러 연결 항공편을 예약하는 경우 이러한 예약은 다음과 같은 개별 객체로 나열될 수 있습니다. `flightReservations` 단일 이벤트용

아래에 제공된 각 객체의 구조 `flightReservations` 아래에 제공됩니다.

![flightReservations 구조](../../images/field-groups/flight-reservation/flightReservations.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `flightCheckIn` | 오브젝트 | 비행 체크인에 대한 세부 정보를 캡처합니다. 객체에는 다음 속성이 포함됩니다.<ul><li>`arrivalAirportCode`: (문자열) 도착 도시의 공항 코드입니다.</li><li>`boardingGroup`: (문자열) 탑승 순서에 대한 항공사별 표시기입니다.</li><li>`checkInMethod`: (문자열) 카운터, 온라인, 키오스크 또는 셀프서비스 등 체크인을 사용한 메서드입니다.</li><li>`checkedBags`: (정수) 항공편에 대해 확인된 수하물 수입니다.</li><li>`checkedPassengers`: (정수) 동일한 예약 수에 여러 승객이 존재하는 경우, 항공편에 대해 체크인된 승객 수입니다.</li><li>`confirmationNumber`: (문자열) 예약 확인 번호 또는 식별자입니다.</li><li>`departureAirportCode`: (문자열) 출발 도시의 공항 코드입니다.</li><li>`flightNumber`: (문자열) 예약 중인 항공편의 항공편 번호입니다.</li></ul> |
| `flightStatusSearch` | 오브젝트 | 비행 상태를 검색할 때 반환되는 세부 정보를 캡처합니다. 객체에는 다음 속성이 포함됩니다.<ul><li>`arrivalAirportCode`: (문자열) 도착 도시의 공항 코드입니다.</li><li>`boardingGroup`: (문자열) 탑승 순서에 대한 항공사별 표시기입니다.</li><li>`departureAirportCode`: (문자열) 출발 도시의 공항 코드입니다.</li><li>`departureDate`: (DateTime) 예약 중인 항공기 출발일입니다.</li><li>`flightNumber`: (문자열) 예약 중인 항공편의 항공편 번호입니다.</li><li>`searchCount`: (정수) 예약된 항공편 상태가 검색된 횟수입니다.</li></ul> |
| `agentID` | 문자열 | 예약 담당 에이전트 또는 예약자(해당하는 경우). |
| `aircraftID` | 문자열 | 항공기용 식별자. |
| `aircraftType` | 문자열 | 항공기 유형. |
| `arrivalAirportCode` | 문자열 | 도착 도시의 공항 코드. |
| `arrivalDate` | DateTime | 예약 중인 항공기 도착일. |
| `cancellation` | 정수 | 이 값은 예약이 취소되면 캡처됩니다. |
| `confirmationNumber` | 문자열 | 예약 확인 번호 또는 식별자. |
| `created` | 문자열 | 이 값은 예약이 생성되면 캡처됩니다. |
| `currencyCode` | 문자열 | 구매 시 사용되는 ISO 4217 통화 코드. |
| `departureAirportCode` | 문자열 | 출발 도시의 공항 코드. |
| `departureDate` | DateTime | 예약 중인 항공기 출발일. |
| `fareClass` | 문자열 | 예약 중인 항공기 요금제. |
| `flightNumber` | 문자열 | 예약 중인 항공편의 항공편 번호. |
| `length` | 정수 | 총 예약 일수. |
| `loyaltyID` | 문자열 | 예약 목록에 있는 승객을 위한 고객 충성도 또는 보상 프로그램 ID. |
| `modification` | 정수 | 이 값은 예약이 수정되면 캡처됩니다. |
| `modificationDate` | DateTime | 예약을 마지막으로 수정한 시간입니다. |
| `numberOfAdults` | 정수 | 예약한 성인 수입니다. |
| `numberOfChildren` | 정수 | 예약과 연계된 하위 항목 수. |
| `passengerID` | 문자열 | 예약과 연계된 승객 정보. |
| `purpose` | 문자열 | 예약 목적(일반적으로 비즈니스 또는 개인). |
| `salesChannel` | 문자열 | 예약된 시점의 판매 채널. |
| `securityScreening` | 문자열 | 승객에 적용되는 보안 차단 유형. |
| `status` | 문자열 | 비행 예약 상태. |
| `ticketNumber` | 문자열 | 예약 번호 또는 식별자. |
| `tripType` | 문자열 | 예약이 편도 여행인지, 왕복인지, 아니면 여러 도시인지 여부를 나타냅니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
