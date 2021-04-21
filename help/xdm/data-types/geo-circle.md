---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;지역;원;데이터 유형;데이터 유형;데이터 유형;;home;popular topics;schema;fields;schemas;geo;circle;data-type;data-type;
solution: Experience Platform
title: 지역 서클 데이터 유형
topic-legacy: overview
description: 이 문서에서는 지역 서클 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# [!UICONTROL Geo Circle] 데이터 유형

[!UICONTROL Geo Circle] 는 특정 좌표 집합을 중심으로 하는 특정 반지름이 주어지면 원형 지리적 영역을 설명하는 표준 XDM 데이터 유형입니다. 이 데이터 유형은 [schema.org](http://schema.org/GeoCircle)에 문서화된 공개 사양을 기반으로 합니다.

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | 원 중앙에 있는 지리적 좌표를 설명합니다. |
| `_schema.description` | 문자열 | 서클에 포함된 내용에 대한 설명입니다. |
| `_schema.radius` | 이중 | 원의 반경 길이입니다. 이 값은 [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) 데이텀을 따르고 미터 단위로 측정됩니다. |
| `_id` | 문자열 | 서클에 대한 고유한 시스템 생성 ID. |
