---
title: MediaAnalytics 상호 작용 세부 정보 스키마 필드 그룹
description: MediaAnalytics 상호 작용 세부 사항 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 2%

---

# [!UICONTROL MediaAnalytics 상호 작용 세부 정보] 스키마 필드 그룹

[!UICONTROL MediaAnalytics 상호 작용 세부 정보]은(는) [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다. 이 필드 그룹을 사용하여 다양한 플랫폼 또는 채널에서 미디어 콘텐츠와의 상호 작용을 종합적으로 모니터링하고 분석하는 보강된 데이터 필드를 캡처합니다.

![[!UICONTROL MediaAnalytics 상호 작용 세부 정보] 스키마 필드 그룹의 스키마 다이어그램입니다.](../../images/field-groups/mediaanalytics-interaction.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|---| --- | --- | --- |
| [!UICONTROL 미디어 컬렉션 세부 정보] | `mediaCollection` | [[!UICONTROL 미디어 컬렉션 세부 정보]](../../data-types/media-collection-details.md) | 미디어 항목 컬렉션과 관련된 속성입니다. 미디어 컬렉션 필드를 사용하여 데이터를 캡처하고 추가 처리를 위해 다른 Adobe 서비스로 전송합니다. |
| [!UICONTROL 미디어 보고 세부 정보] | `mediaReporting` | [[!UICONTROL 미디어 보고 세부 정보]](../../data-types/media-reporting-details.md) | 미디어 콘텐츠와 연계된 보고 세부 정보 및 지표. * 미디어 보고 필드는 Adobe 서비스에서 사용자가 보낸 미디어 컬렉션 필드를 분석하는 데 사용됩니다. 이 데이터는 다른 특정 사용자 지표와 함께 계산되고 보고됩니다. |
| [!UICONTROL 다운로드한 미디어 컬렉션 콘텐츠 목록] | `mediaDownloadedEvents` | [!UICONTROL 배열]/[[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | 미디어 컬렉션 내의 콘텐츠 다운로드를 추적하는 이벤트입니다. |

{style="table-layout:auto"}

>[!TIP]
>
>Media Edge API에서 사용되지 않는 필드를 숨길 수 있습니다. 이러한 필드를 숨기면 스키마를 읽고 이해하는 것이 쉬워지지만 필수는 아닙니다. 이 필드는 [!UICONTROL MediaAnalytics 상호 작용 세부 정보] 필드 그룹의 필드만 참조합니다. Experience Platform UI에서 가독성을 향상시키려면 [Media Analytics 설명서에서 사용하지 않는 필드를 숨기는 방법](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html?lang=ko#set-up-the-schema-in-adobe-experience-platform)의 지침을 따르십시오.

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html?lang=ko#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
