---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지역;좌표;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지역 좌표 데이터 유형
description: 이 문서에서는 지리적 좌표 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL 지역 좌표] 데이터 유형

[!UICONTROL 지역 좌표] 는 위치의 지리적 좌표를 설명하는 표준 XDM 데이터 유형입니다. 이 데이터 유형은 [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.description` | 문자열 | 좌표가 식별하는 내용에 대한 설명입니다. |
| `_schema.elevation` | 이중 | 정의된 좌표의 특정 승급입니다. 값은 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 데이텀 및 는 미터 단위로 측정됩니다. |
| `_schema.latitude` | 이중 | 지리적 지점의 서명된 수직 좌표입니다. |
| `_schema.longitude` | 이중 | 지리적 지점의 서명된 수평 좌표입니다. |
| `_id` | 문자열 | 좌표용의 고유한 시스템 생성 ID. |
