---
title: 미디어 이벤트 정보 데이터 유형
description: 미디어 이벤트 정보 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# [!UICONTROL 미디어 이벤트 정보] 데이터 형식

[!UICONTROL 미디어 이벤트 정보]는 경험 이벤트와 관련된 미디어 세부 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다.

![미디어 이벤트 정보 데이터 형식의 다이어그램입니다.](../images/data-types/media-event-information.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | 경험 이벤트와 관련된 미디어 세부 정보. 이 데이터 형식은 [미디어 데이터 수집](./media-collection-details.md) 및 [미디어 데이터 보고](./media-reporting-details.md)에 모두 사용됩니다. |
| `mediaEventTimestamp` | [!UICONTROL 문자열] | 미디어 이벤트가 발생한 시간입니다. |
| `mediaEventType` | [!UICONTROL 문자열] | 미디어 이벤트 유형. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)를 참조하세요.
