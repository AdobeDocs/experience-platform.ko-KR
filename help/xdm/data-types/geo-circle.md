---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;지역;원;데이터 유형;데이터 유형;데이터 유형;;home;popular topics;schema;XDM;fields;schemas;geo;circle;data-type;data-type;
solution: Experience Platform
title: 지역 서클 데이터 유형
topic: overview
description: 이 문서에서는 지역 서클 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---


# [!UICONTROL 지역 ] 기호 데이터 유형

[!UICONTROL 지역 ] 순환은 특정 좌표 집합을 중심으로 하는 특정 반경이 주어지면 원형 지리적 영역을 설명하는 표준 XDM 데이터 유형입니다. 이 데이터 유형은 [schema.org](http://schema.org/GeoCircle)에 문서화된 공개 사양을 기반으로 합니다.

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 지역 좌표]](./geo-coordinates.md) | 원 중앙에 있는 지리적 좌표를 설명합니다. |
| `_schema.description` | 문자열 | 서클에 포함된 내용에 대한 설명입니다. |
| `_schema.radius` | 이중 | 원의 반경 길이입니다. 이 값은 [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) 데이텀을 따르고 미터 단위로 측정됩니다. |
| `_id` | 문자열 | 서클에 대한 고유한 시스템 생성 ID. |
