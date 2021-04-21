---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;지역;좌표;데이터 유형;데이터 유형;데이터 유형;;home;popular topics;schema;XDM;fields;schemas;geo;좌표;datatype;data-type;data-type;
solution: Experience Platform
title: 지역 좌표 데이터 유형
topic-legacy: overview
description: 이 문서에서는 지리적 좌표 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

# [!UICONTROL Geo Coordinates] 데이터 유형

[!UICONTROL Geo Coordinates] 는 장소의 지리적 좌표를 설명하는 표준 XDM 데이터 유형입니다. 이 데이터 유형은 [schema.org](https://schema.org/GeoCoordinates)에 문서화된 공개 사양을 기반으로 합니다.

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.description` | 문자열 | 좌표가 식별하는 내용에 대한 설명입니다. |
| `_schema.elevation` | 이중 | 정의된 좌표의 특정 승급입니다. 이 값은 [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) 데이텀을 따라야 하며 미터 단위로 측정됩니다. |
| `_schema.latitude` | 이중 | 지리적 점의 서명된 세로 좌표입니다. |
| `_schema.longitude` | 이중 | 지리적 점의 서명된 가로 좌표입니다. |
| `_id` | 문자열 | 좌표에 대한 고유한 시스템 생성 ID. |
