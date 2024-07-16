---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지역;좌표;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지리적 좌표 데이터 유형
description: 지역 좌표 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 13%

---

# [!UICONTROL 지리적 좌표] 데이터 형식

[!UICONTROL 지리적 좌표]는 위치의 지리적 좌표를 설명하는 표준 XDM 데이터 형식입니다. 이 데이터 형식은 [schema.org](https://schema.org/GeoCoordinates)에 설명된 공개 사양을 기반으로 합니다.

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.description` | 문자열 | 좌표가 식별한 내용에 대한 설명. |
| `_schema.elevation` | 더블 | 정의된 좌표의 특정 높이기. 값은 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 데이터에 맞아야 하며 미터 단위로 측정됩니다. |
| `_schema.latitude` | 더블 | 지리적 위치에 대한 로그인한 세로 좌표. |
| `_schema.longitude` | 더블 | 지리적 위치에 대한 로그인한 가로 좌표. |
| `_id` | 문자열 | 좌표에 대한 시스템 생성 고유 ID. |
