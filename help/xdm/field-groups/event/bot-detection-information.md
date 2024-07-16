---
title: 보트 탐지 필드 그룹
description: XDM(보트 탐지 필드 그룹) 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 7%

---

# [!UICONTROL 보트 감지] 필드 그룹

[!UICONTROL 보트 검색]은(는) [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다. 필드 그룹은 봇이 생성한 트래픽에 대한 정보를 제공합니다.

![[!UICONTROL 보트 검색] 필드 그룹의 다이어그램입니다.](../../images/field-groups/bot-detection-information.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL 보트 감지] | `botDetection` | 오브젝트 | 봇이 생성한 트래픽에 대한 정보를 제공합니다. |
| [!UICONTROL 점수] | `score` | 번호 | 보트 확률 점수는 0에서 1까지입니다. 점수가 0이면 트래픽이 봇이 아님을 의미합니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
