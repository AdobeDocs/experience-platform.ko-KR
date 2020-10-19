---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;place context;placeContext;datatype;data-type;data type;
solution: Experience Platform
title: 컨텍스트 데이터 유형 배치
topic: overview
description: 이 문서에서는 Place Context XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---


# [!UICONTROL 컨텍스트] 데이터 유형 배치

[!UICONTROL 장소 컨텍스트는] 관심 영역 정보 및 지리적 좌표 등 관측 이벤트의 위치를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/place-context.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 관심 영역 상호 작용]](./poi-interaction.md) | POI(Point Of Interest) 상호 작용에 대한 세부 사항을 설명합니다. |
| `activePOIs` | 관심 [[!UICONTROL 영역 세부 정보 배열]](./poi-details.md) | 이벤트를 발생시킨 POI에 대해 설명합니다. |
| `geo` | [[!UICONTROL 지역]](./geo.md) | 경험이 전달되는 지리적 위치를 설명합니다. |
| `localTime` | DateTime | 지정된 표준 시간대 오프셋을 사용하여 [현지 시간을 나타내는 RFC 339](https://tools.ietf.org/html/rfc3339) 형식의 타임스탬프입니다. 서식 패턴은 `yyyy-MM-dd'T'HH:mm:ssXXX` (예: `2001-07-04T12:08:56-07:00`) |
| `localTimezoneOffset` | 정수 | 값에 대한 UTC로부터 분 단위의 현재 현지 표준 시간대 `localTime` 오프셋입니다. 해당되는 경우 현재 DST 오프셋을 포함해야 합니다. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)