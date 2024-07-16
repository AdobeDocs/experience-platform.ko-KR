---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지역;지역 모양;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지역 셰이프 데이터 유형
description: 지역 셰이프 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 6%

---

# [!UICONTROL 지역 셰이프] 데이터 형식

[!UICONTROL 지역 셰이프]는 지역 셰이프를 설명하는 표준 XDM 데이터 형식입니다. 이 데이터 형식은 [schema.org](https://schema.org/GeoShape)에 설명된 공개 사양을 기반으로 합니다.

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.box` | [[!UICONTROL 지리적 좌표]](./geo-coordinates.md) 배열 | 두 개의 좌표로 구성된 사각형으로 둘러싸인 지리적 영역을 설명합니다. 첫 번째 좌표는 사각형의 아래쪽 모서리이고 두 번째 좌표는 위쪽 모서리입니다. |
| `_schema.circle` | [[!UICONTROL 지리적 좌표]](./geo-coordinates.md) 배열 | 지리적 좌표 중심에 있는 특정 반경의 원형 영역을 설명합니다. |
| `_schema.polygon` | [[!UICONTROL 지역 서클]](./geo-circle.md) | 첫 번째 좌표와 마지막 좌표가 동일한 4개 이상의 좌표 시리즈. |
| `_schema.description` | 문자열 | 모양이 정의한 내용에 대한 설명. |
| `_schema.elevation` | 더블 | 특정 또는 최소 모양 높이기. 이 값은 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 데이터에 해당되며 미터 단위로 측정됩니다. `ceiling`과(와) 함께 이 속성을 사용하여 위치에 대한 3차원 테두리 상자를 표시할 수 있습니다. |
| `_id` | 문자열 | 셰이프에 대한 시스템에서 생성한 고유 식별자입니다. |
| `ceiling` | 더블 | 모양의 최대 높이입니다. 이 속성은 `elevation`과(와) 함께 사용할 때만 유효합니다. 값은 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 데이터에 해당되며 미터 단위로 측정됩니다. `elevation`과(와) 함께 이 속성을 사용하여 위치에 대한 3차원 테두리 상자를 표시할 수 있습니다. |
