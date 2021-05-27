---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;컨텍스트 배치;컨텍스트 배치;데이터 유형;데이터 유형;
solution: Experience Platform
title: 컨텍스트 데이터 유형 배치
topic-legacy: overview
description: 이 문서에서는 Place Context XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# [!UICONTROL contextdata ] 형식 배치

[!UICONTROL 컨텍스트] 를 관심 영역 정보 및 지리적 좌표를 포함하여 관찰된 이벤트의 위치를 설명하는 표준 XDM 데이터 형식으로 배치합니다.

<img src="../images/data-types/place-context.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 관심 영역 상호 작용]](./poi-interaction.md) | POI(관심 영역) 상호 작용에 대한 세부 사항을 설명합니다. |
| `activePOIs` | [[!UICONTROL 관심 영역 세부 정보의 배열]](./poi-details.md) | 이벤트를 발생시킨 POI를 설명합니다. |
| `geo` | [[!UICONTROL 지역]](./geo.md) | 경험이 전달되는 지리적 위치를 설명합니다. |
| `localTime` | DateTime | [RFC 3339](https://tools.ietf.org/html/rfc3339) 형식의 타임스탬프가 지정된 시간대 오프셋을 사용하여 을 사용하는 로컬 시간을 나타냅니다. 서식 패턴은 `yyyy-MM-dd'T'HH:mm:ssXXX`(예: `2001-07-04T12:08:56-07:00`)입니다. |
| `localTimezoneOffset` | 정수 | `localTime` 값에 대한 UTC로부터 분 단위의 현재 로컬 시간대 오프셋입니다. 해당되는 경우 현재 DST 오프셋이 포함되어야 합니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
