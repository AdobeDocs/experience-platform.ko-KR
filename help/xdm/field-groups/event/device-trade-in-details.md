---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;장치;트레이드;트레이드 인;트레이드 인;
solution: Experience Platform
title: 장치 거래 세부 정보 스키마 필드 그룹
description: Device Trade-In Details 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# [!UICONTROL 디바이스 거래 세부 정보] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 다음에 대한 문서 보기: [필드 그룹 이름 업데이트](../name-updates.md) 추가 정보.

[!UICONTROL 디바이스 거래 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 단일 필드(`deviceTradeInDetails`)는 트레이드 인 값, 원래 디바이스 ID 및 새 디바이스 ID를 포함하여 디바이스 트레이드 인 거래를 설명합니다.

![디바이스 거래 세부 정보 구조](../../images/field-groups/device-trade-in-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `tradeInValue` | [통화](../../data-types/currency.md) | 교환 중인 디바이스 값. |
| `newDeviceID` | 문자열 | 거래 중인 새 디바이스의 ID입니다. |
| `originalDeviceID` | 문자열 | 거래 중인 디바이스 ID입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
