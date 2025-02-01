---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;poi;poi 세부 정보;관심 영역;관심 영역 세부 정보;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 관심 영역 세부 정보 데이터 유형
description: 관심 영역 세부 정보 XDM 데이터 유형에 대해 알아봅니다.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 15%

---

# [!UICONTROL 관심 영역 세부 정보] 데이터 형식

[!UICONTROL 관심 영역 세부 정보]은(는) 이벤트가 관찰된 지리적 관련 데이터를 설명하는 표준 XDM 데이터 형식입니다.

![](../images/data-types/poi-details.png){width=550}

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL 비콘]](./beacon.md) | POI 인터랙션에 대해 활성화된 비콘 세부 정보를 설명합니다. |
| `geoInteractionDetails` | [[!UICONTROL 지리적 인터랙션 세부 정보]](./geo-interaction-details.md) | POI 인터랙션에 대해 활성화된 지리적 세부 정보를 설명합니다. |
| `category` | 문자열 | POI 정의 관리자가 POI를 구성하기 위해 할당한 일반 범주. |
| `distanceToPOICenter` | 더블 | POI 중앙에서 예상되는 거리(단위: 미터). |
| `locatingType` | 문자열 | 위치를 결정하는 데 사용되는 메커니즘입니다. 허용되는 값은 다음과 같습니다. <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 문자열 | POI에 붙여진 이름. |
| `poiID` | 문자열 | POI에 대한 고유 식별자. |
| `type` | 문자열 | POI 정의 관리자가 선택한 입력 스키마를 사용하는 POI에 대한 일반적인 유형. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
