---
title: Sitetool 세부 정보 스키마 필드 그룹
description: Sitetool 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 5%

---

# [!UICONTROL Sitetool 세부 정보] 스키마 필드 그룹

[!UICONTROL Sitetool 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `sitetool` 개체를 스키마로 복사합니다. 스키마는 사이트 도구에서 수집한 정보를 캡처합니다.

![필드 그룹 구조](../../images/field-groups/sitetool-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `dataGatheringEvent` | 오브젝트 | 이 이벤트가 기타 관련 세부 정보와 함께 데이터 수집 이벤트인지 여부를 나타냅니다. 다음 속성을 포함합니다.<ul><li>`data`: (지도) 퀴즈, 설문 조사 또는 투표 제출 이벤트의 일부로 수집되고 제출되는 JSON 데이터가 포함되어 있습니다.</li><li>`isTrue`: (부울) 이 이벤트가 퀴즈, 설문 조사 또는 설문 조사와 같은 데이터 수집 이벤트인지 여부를 나타냅니다.</li><li>`score`: (정수) 이벤트 응답을 기반으로 행위자가 확보한 점수입니다.</li></ul> |
| `actor` | 문자열 | 작업을 수행한 개인/멤버입니다. |
| `actorID` | 문자열 | 작업을 수행한 사람/구성원에 대한 고유 식별자. |
| `isKeyEvent` | 부울 | 이 이벤트가 주요 이벤트인지 여부를 나타냅니다. |
| `name` | 문자열 | 챗봇, 설문 조사 등 사이트 도구의 이름입니다. |
| `section` | 문자열 | 메인 또는 서브와 같은 사이트 도구의 관련 섹션. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
