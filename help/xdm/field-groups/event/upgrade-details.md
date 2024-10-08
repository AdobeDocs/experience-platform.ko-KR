---
title: 업그레이드 세부 정보 스키마 필드 그룹
description: 업그레이드 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL 업그레이드 세부 정보] 스키마 필드 그룹

[!UICONTROL 업그레이드 세부 정보]은(는) 거래 세부 정보 및 고객에게 오퍼가 표시되는 다양한 방법을 포함하여 업그레이드 마케팅 이벤트 관련 정보를 캡처하는 데 사용되는 [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다.

필드 그룹은 단일 개체 유형 필드 `upgrades`을(를) 제공합니다. 이 개체에 포함된 속성은 아래에 설명되어 있습니다.

![업그레이드 세부 정보 구조](../../images/field-groups/upgrade-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `upgradeImpressions` | [노출 횟수](../../data-types/impressions.md) 배열 | 고객을 위해 기록된 노출 횟수(디지털 보기 또는 업그레이드 오퍼와의 계약)를 나열하는 배열입니다. |
| `upgradeTransaction` | [트랜잭션](../../data-types/transaction.md) | 업그레이드에 대한 통화 트랜잭션을 설명합니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
