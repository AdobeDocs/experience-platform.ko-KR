---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;장치;트레이드인;트레이드인;트레이드인;
solution: Experience Platform
title: 장치 트레이드인 세부 정보 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 장치 트레이드인 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 4%

---

# [!UICONTROL 장치 트레이드인 세부 ] 정보스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL Device Trade-] In 클래스에 대한 표준 스키마 필드  [[!DNL XDM ExperienceEvent] 그룹을 자세히 설명합니다](../../classes/experienceevent.md). 여기에는 트레이드인 값, 원래 장치 ID 및 새 장치 ID를 포함하여 장치 트레이드인 트랜잭션을 설명하는 단일 필드(`deviceTradeInDetails`)가 제공됩니다.

![장치 거래 세부 사항 구조](../../images/field-groups/device-trade-in-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `tradeInValue` | [통화](../../data-types/currency.md) | 거래되는 장치의 값입니다. |
| `newDeviceID` | 문자열 | 매매되는 새 장치의 ID입니다. |
| `originalDeviceID` | 문자열 | 거래되는 장치의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
