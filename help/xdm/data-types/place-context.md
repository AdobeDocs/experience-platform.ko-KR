---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;배치 컨텍스트;배치 컨텍스트;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 위치 컨텍스트 데이터 유형
description: 이 문서에서는 위치 컨텍스트 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 4%

---

# [!UICONTROL 위치 컨텍스트] 데이터 유형

[!UICONTROL 위치 컨텍스트] 관심 영역 정보 및 지리적 좌표를 포함하여 관찰된 이벤트의 위치를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/place-context.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 관심 영역 인터랙션]](./poi-interaction.md) | 관심 영역(POI) 인터랙션에 대한 세부 정보를 설명합니다. |
| `activePOIs` | 배열 [[!UICONTROL 관심 영역 세부 정보]](./poi-details.md) | 이벤트를 발생시킨 POI를 설명합니다. |
| `geo` | [[!UICONTROL 지역]](./geo.md) | 경험이 전달된 지리적 위치를 설명합니다. |
| `localTime` | DateTime | 의 타임스탬프 [RFC 3339](https://tools.ietf.org/html/rfc3339) 지정된 시간대 오프셋으로 을 사용하는 현지 시간을 나타내는 형식입니다. 서식 패턴은 다음과 같습니다. `yyyy-MM-dd'T'HH:mm:ssXXX` (예: `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | 정수 | 에 대한 UTC의 현재 로컬 시간대 오프셋(분) `localTime` 값. 해당되는 경우 현재 DST 오프셋이 여기에 포함되어야 합니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
