---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;예약;예약 세부 정보;
title: 예약 세부 정보 스키마 필드 그룹
description: 이 문서에서는 예약 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 5%

---


# [!UICONTROL 예약 ] 세부 정보스키마 필드 그룹

[!UICONTROL 예약 ] 세부 사항은 길이, 수정, 환불 가능 상태 및 객실 수 등 예약 정보를 캡처하는  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 데 사용되는 클래스에 대한 표준 스키마 필드 그룹입니다.

필드 그룹은 단일 객체 유형 필드인 `reservations`을 제공합니다. 이 개체에 포함된 속성은 아래에 설명되어 있습니다.

![예약 세부 정보 구조](../../images/field-groups/reservation-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `nonRefundableAmount` | [통화](../../data-types/currency.md) | 환불이 불가능한 것으로 표시된 예약 가격 금액입니다. |
| `transaction` | [트랜잭션](../../data-types/transaction.md) | 예약에 대한 통화 거래를 설명합니다. |
| `id` | 문자열 | 예약의 고유 식별자입니다. |
| `cancellation` | 정수 | 이 값은 예약이 취소된 경우 캡처됩니다. |
| `confirmationNumber` | 문자열 | 예약의 확인 번호 또는 식별자입니다. |
| `created` | 정수 | 이 값은 예약을 작성할 때 캡처됩니다. |
| `currencyCode` | 문자열 | 구매에 사용되는 ISO 4217 통화 코드입니다. |
| `endDate` | DateTime | 예약에 대한 종료 드롭, 반환 또는 체크아웃 일자. |
| `length` | 정수 | 예약의 총 일수입니다. |
| `modification` | 정수 | 이 값은 예약이 수정되었을 때 캡처됩니다. |
| `modificationDate` | DateTime | 예약을 마지막으로 수정한 시간입니다. |
| `numberOfAdults` | 정수 | 예약과 연관된 성인 수입니다. |
| `numberOfChildren` | 정수 | 예약과 연관된 하위 수입니다. |
| `purpose` | 문자열 | 예약의 목적(일반적으로 업무 또는 개인). |
| `startDate` | DateTime | 예약에 대한 시작 픽업, 아웃바운드 또는 체크인 날짜입니다. |
| `triptype` | 문자열 | 일방향 여행, 왕복 또는 다중 도시 여행을 예약했는지 여부를 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## 업종별 예약 필드 그룹

산업별 사용 사례에 대해 [!UICONTROL 예약 세부 정보] 스키마를 확장하는 다른 여러 표준 필드 그룹이 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [[!UICONTROL 식사 예약]](./dining-reservation.md)
* [[!UICONTROL 비행 예약]](./flight-reservation.md)
* [[!UICONTROL 숙박예약]](./lodging-reservation.md)