---
title: 미디어 이벤트 정보 데이터 유형
description: 미디어 이벤트 정보 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 6%

---

# [!UICONTROL 미디어 이벤트 정보] 데이터 유형

[!UICONTROL 미디어 이벤트 정보] 는 경험 이벤트와 관련된 미디어 세부 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

![미디어 이벤트 정보 데이터 유형의 다이어그램입니다.](../images/data-types/media-event-information.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | 경험 이벤트와 관련된 미디어 세부 정보. |
| `mediaEventTimestamp` | [!UICONTROL 문자열] | 미디어 이벤트가 발생한 시간입니다. |
| `mediaEventType` | [!UICONTROL 문자열] | 미디어 이벤트 유형. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
