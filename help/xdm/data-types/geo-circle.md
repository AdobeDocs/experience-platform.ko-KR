---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지역;원;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지역 원 데이터 유형
description: 지역 서클 XDM 데이터 유형에 대해 알아봅니다.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 11%

---

# [!UICONTROL 지역 서클] 데이터 형식

[!UICONTROL 지역 원]은(는) 특정 좌표 집합을 중심으로 특정 반경이 지정된 순환 지역 지역을 설명하는 표준 XDM 데이터 형식입니다. 이 데이터 형식은 [schema.org](https://schema.org/GeoCircle)에 설명된 공개 사양을 기반으로 합니다.

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 지리적 좌표]](./geo-coordinates.md) | 원의 중심에 대한 지리적 좌표를 설명합니다. |
| `_schema.description` | 문자열 | 서클에 포함된 내용에 대한 설명. |
| `_schema.radius` | 더블 | 원 반지름의 길이입니다. 이 값은 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 데이터에 해당되며 미터 단위로 측정됩니다. |
| `_id` | 문자열 | 서클에 대해 시스템에서 생성한 고유한 ID입니다. |
