---
title: 스키마 필드 그룹 업셀 세부 정보
description: 이 문서에서는 업셀 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL 스키마 ] 필드 그룹 업셀 세부 정보

[!UICONTROL 업셀 ] 세부 사항은 트랜잭션 세부 사항 및 오퍼가 고객에게  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 표시된 다른 방법 등 업셀 마케팅 이벤트에 대한 정보를 캡처하는 데 사용되는 클래스에 대한 표준 스키마 필드 그룹을 나타냅니다.

필드 그룹은 단일 객체 유형 필드인 `upsells`을 제공합니다. 이 개체에 포함된 속성은 아래에 설명되어 있습니다.

![업셀 세부 정보 구조](../../images/field-groups/upsell-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `upsellImpressions` | [노출 횟수](../../data-types/impressions.md) 배열 | 고객에 대해 기록된 노출(디지털 보기 또는 상향 판매 오퍼로 참여)을 나열하는 배열입니다. |
| `upsellTransaction` | [트랜잭션](../../data-types/transaction.md) | 업셀용 통화 거래를 설명합니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
