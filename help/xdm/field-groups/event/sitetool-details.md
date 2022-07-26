---
title: Sitetool 세부 정보 스키마 필드 그룹
description: 이 문서에서는 사이트 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---

# [!UICONTROL Sitetool 세부 정보] 스키마 필드 그룹

[!UICONTROL Sitetool 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `sitetool` 사이트에 의해 수집된 정보를 캡처하는 스키마 객체입니다.

![필드 그룹 구조](../../images/field-groups/sitetool-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `dataGatheringEvent` | 개체 | 이 이벤트가 다른 관련 세부 정보와 함께 데이터 수집 이벤트인지 여부를 나타냅니다. 다음 속성을 포함합니다.<ul><li>`data`: (맵) 퀴즈, 설문 조사 또는 투표 제출 이벤트의 일부로 수집 및 제출되는 JSON 데이터를 포함합니다.</li><li>`isTrue`: (부울) 이 이벤트가 퀴즈, 설문 조사 또는 폴링과 같은 데이터 수집 이벤트인지 여부를 나타냅니다.</li><li>`score`: (정수) 행위자가 이벤트 응답을 기반으로 하여 확보한 점수입니다.</li></ul> |
| `actor` | 문자열 | 작업을 수행한 사람/구성원. |
| `actorID` | 문자열 | 작업을 수행한 개인/구성원의 고유 식별자입니다. |
| `isKeyEvent` | 부울 | 이 이벤트가 주요 이벤트인지 여부를 나타냅니다. |
| `name` | 문자열 | Chatbot, 설문 조사 등과 같은 Sitetool의 이름입니다. |
| `section` | 문자열 | 주 섹션이나 하위 섹션처럼 사이트에서 관련된 섹션입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
