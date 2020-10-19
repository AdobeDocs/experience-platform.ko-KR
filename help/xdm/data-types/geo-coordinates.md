---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinates;datatype;data-type;data type;
solution: Experience Platform
title: 지역 좌표 데이터 유형
topic: overview
description: 이 문서에서는 지리 좌표 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---


# [!UICONTROL 지역 좌표] 데이터 유형

[!UICONTROL 지리 좌표] 는 장소의 지리적 좌표를 설명하는 표준 XDM 데이터 유형입니다. 이 데이터 유형은 schema.org에 문서화된 공개 사양을 [기반으로 합니다](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.description` | 문자열 | 좌표가 식별하는 사항에 대한 설명입니다. |
| `_schema.elevation` | 이중 | 정의된 좌표의 특정 승격입니다. 값은 WGS84 [데이텀을](http://gisgeography.com/wgs84-world-geodetic-system/) 준수해야 하며 미터 단위로 측정됩니다. |
| `_schema.latitude` | 이중 | 지리적 점의 서명된 세로 좌표. |
| `_schema.longitude` | 이중 | 지리적 점의 서명된 수평 좌표입니다. |
| `_id` | 문자열 | 좌표에 대한 고유한 시스템 생성 ID. |
