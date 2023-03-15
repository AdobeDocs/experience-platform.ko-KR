---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지역;지역 모양;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지역 셰이프 데이터 유형
description: 이 문서에서는 지역 셰이프 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# [!UICONTROL 지역 모습] 데이터 유형

[!UICONTROL 지역 모습] 는 지리적 영역의 모양을 설명하는 표준 XDM 데이터 유형입니다. 이 데이터 유형은에 문서화된 공개 사양을 기반으로 합니다 [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema.box` | 배열 [[!UICONTROL 지리적 좌표]](./geo-coordinates.md) | 두 개의 좌표로 구성된 사각형으로 둘러싸인 지리적 영역을 설명합니다. 첫 번째 좌표는 사각형의 아래쪽 모서리이고 두 번째 좌표는 위쪽 모서리입니다. |
| `_schema.circle` | 배열 [[!UICONTROL 지리적 좌표]](./geo-coordinates.md) | 지리적 좌표 중심에 있는 특정 반경의 원형 영역을 설명합니다. |
| `_schema.polygon` | [[!UICONTROL 지역 서클]](./geo-circle.md) | 첫 번째 좌표와 마지막 좌표가 동일한 4개 이상의 좌표 시리즈. |
| `_schema.description` | 문자열 | 모양이 정의하는 내용에 대한 설명. |
| `_schema.elevation` | 이중 | 특정 또는 최소 모양 높이기. 이 값은 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 데이텀 및 측정 단위는 미터입니다. 과 조화하여 `ceiling`, 이 속성은 위치에 대한 3차원 테두리 상자를 표현하는 데 사용할 수 있습니다. |
| `_id` | 문자열 | 셰이프에 대한 시스템에서 생성한 고유 식별자입니다. |
| `ceiling` | 이중 | 모양의 최대 높이입니다. 이 속성은 와 함께 사용할 때만 유효합니다. `elevation`. 값은 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 데이텀 및 측정 단위는 미터입니다. 과 조화하여 `elevation`, 이 속성은 위치에 대한 3차원 테두리 상자를 표현하는 데 사용할 수 있습니다. |
