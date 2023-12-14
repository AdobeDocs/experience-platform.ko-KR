---
title: MediaAnalytics 상호 작용 세부 정보 스키마 필드 그룹
description: MediaAnalytics 상호 작용 세부 사항 스키마 필드 그룹에 대해 알아봅니다.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL MediaAnalytics 인터랙션 세부 정보] 스키마 필드 그룹

[!UICONTROL MediaAnalytics 인터랙션 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 이 필드 그룹을 사용하여 다양한 플랫폼 또는 채널에서 미디어 콘텐츠와의 상호 작용을 종합적으로 모니터링하고 분석하는 보강된 데이터 필드를 캡처합니다.

![의 스키마 다이어그램 [!UICONTROL MediaAnalytics 인터랙션 세부 정보] 스키마 필드 그룹.](../../images/field-groups/mediaanalytics-interaction.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|---| --- | --- | --- |
| [!UICONTROL 미디어 컬렉션 세부 사항] | `mediaCollection` | [[!UICONTROL 미디어 세부 정보]](../../data-types/media-details-information.md) | 미디어 항목 컬렉션과 관련된 속성입니다. |
| [!UICONTROL 미디어 보고 세부 정보] | `mediaReporting` | [[!UICONTROL 미디어 세부 정보]](../../data-types/media-details-information.md) | 미디어 콘텐츠와 연계된 보고 세부 정보 및 지표. |
| [!UICONTROL 미디어 컬렉션 다운로드 콘텐츠 이벤트 목록] | `mediaDownloadedEvents` | [!UICONTROL 배열] / [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | 미디어 컬렉션 내의 콘텐츠 다운로드를 추적하는 이벤트입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
