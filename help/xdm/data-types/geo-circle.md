---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data-type;data type;
solution: Experience Platform
title: 지역 서클 데이터 유형
topic: overview
description: 이 문서에서는 지리 기반 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 4%

---


# [!UICONTROL 지역 서클] 데이터 유형

[!UICONTROL 지리적 서클은] 특정 좌표 집합 중심 특정 반경이 주어지면 원형 지리적 영역을 설명하는 표준 XDM 데이터 유형입니다. 이 데이터 유형은 schema.org에 문서화된 공개 사양을 [기반으로 합니다](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 지역 좌표]](./geo-coordinates.md) | 원 중심에 대한 지리적 좌표를 설명합니다. |
| `_schema.description` | 문자열 | 서클에 포함된 내용에 대한 설명입니다. |
| `_schema.radius` | 이중 | 원의 반경 길이입니다. 이 값은 [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) 데이텀을 따르고 미터 단위로 측정됩니다. |
| `_id` | 문자열 | 서클에 대한 고유한 시스템 생성 ID. |
