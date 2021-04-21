---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;프로필;위치 정보;관심 영역 세부 사항;데이터 유형;데이터 유형;데이터 유형;;
solution: Experience Platform
title: 관심 영역 세부 사항 데이터 유형
topic-legacy: overview
description: 이 문서에서는 관심 영역 세부 정보 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 4%

---

# [!UICONTROL Point of interest details] 데이터 유형

[!UICONTROL Point of interest details] 는 이벤트가 관측된 지리적 관련 데이터를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | POI 상호 작용에 대해 활성화된 비콘 세부 사항을 설명합니다. |
| `geoInteractionDetails` | [[!UICONTROL Geo interaction details]](./geo-interaction-details.md) | POI 상호 작용에 대해 활성화된 지역 세부 사항을 설명합니다. |
| `category` | 문자열 | POI 정의 관리자가 POI를 구성하기 위해 지정한 일반 카테고리. |
| `distanceToPOICenter` | 이중 | POI 센터로부터의 예상 거리(미터)입니다. |
| `locatingType` | 문자열 | 위치를 결정하는 데 사용되는 메커니즘입니다. 허용되는 값은 다음과 같습니다. <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 문자열 | POI에 주어진 이름. |
| `poiID` | 문자열 | POI의 고유 식별자입니다. |
| `type` | 문자열 | POI 정의 관리자가 선택한 입력 스키마를 사용하는 POI의 일반 유형입니다. |

혼합에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
