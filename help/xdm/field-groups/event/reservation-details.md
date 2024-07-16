---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;예약;예약 세부 정보;
title: 예약 세부 정보 스키마 필드 그룹
description: 예약 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 6%

---

# [!UICONTROL 예약 세부 정보] 스키마 필드 그룹

[!UICONTROL 예약 세부 정보]는 길이, 수정, 환불 상태 및 룸 수를 포함하여 예약과 관련된 정보를 캡처하는 데 사용되는 [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다.

필드 그룹은 단일 개체 유형 필드 `reservations`을(를) 제공합니다. 이 개체에 포함된 속성은 아래에 설명되어 있습니다.

![예약 세부 정보 구조](../../images/field-groups/reservation-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `nonRefundableAmount` | [통화](../../data-types/currency.md) | 환불불가로 표시된 예약금. |
| `transaction` | [트랜잭션](../../data-types/transaction.md) | 예약에 대한 통화 트랜잭션을 설명합니다. |
| `id` | 문자열 | 예약에 대한 고유 식별자. |
| `cancellation` | 정수 | 이 값은 예약이 취소되면 캡처됩니다. |
| `confirmationNumber` | 문자열 | 예약에 대한 확인 번호 또는 식별자입니다. |
| `created` | 정수 | 이 값은 예약이 생성되면 캡처됩니다. |
| `currencyCode` | 문자열 | 구매 시 사용되는 ISO 4217 통화 코드. |
| `endDate` | 날짜/시간 | 최종 예약 드롭오프, 반환 또는 체크아웃 날짜. |
| `length` | 정수 | 총 예약 일수. |
| `modification` | 정수 | 이 값은 예약이 수정되면 캡처됩니다. |
| `modificationDate` | 날짜/시간 | 예약을 마지막으로 수정한 시간입니다. |
| `numberOfAdults` | 정수 | 예약한 성인 수입니다. |
| `numberOfChildren` | 정수 | 예약과 연계된 하위 항목 수. |
| `purpose` | 문자열 | 예약 목적(일반적으로 비즈니스 또는 개인). |
| `startDate` | 날짜/시간 | 예약 시작 픽업, 아웃바운드 또는 체크인 날짜. |
| `triptype` | 문자열 | 예약이 편도 여행인지, 왕복인지, 아니면 여러 도시인지 여부를 나타냅니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## 산업별 예약 필드 그룹

산업별 사용 사례에 맞게 [!UICONTROL 예약 세부 정보] 스키마를 확장하는 다른 표준 필드 그룹이 몇 개 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [[!UICONTROL 식사 예약]](./dining-reservation.md)
* [[!UICONTROL 비행 예약]](./flight-reservation.md)
* [[!UICONTROL 숙박 예약]](./lodging-reservation.md)
