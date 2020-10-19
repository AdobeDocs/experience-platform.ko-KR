---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: 지역 상호 작용 세부 정보 데이터 유형
topic: overview
description: 이 문서에서는 지리 상호 작용 세부 정보 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# [!UICONTROL 지역 상호 작용 세부 사항] 데이터 유형

[!UICONTROL 지리적 상호 작용 세부] 정보는 지리적으로 정의된 영역에 포함되는 현재 상태를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 지역 모양]](./geo-shape.md) | 상호 작용하는 영역의 지리 모양을 설명합니다. 이 필드는 상자, 원 또는 다각형을 설명할 수 있습니다. |
| `deviceGeoAccuracy` | 이중 | 미터 단위로 측정되는 지역 측정 장치 또는 메커니즘의 정확성. |
| `distanceToCenter` | 이중 | 지역 원의 경우 지역 중심까지의 거리가 미터로 측정됩니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
