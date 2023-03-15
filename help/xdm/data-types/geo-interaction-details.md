---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;비콘;상호 작용 세부 정보;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지역 상호 작용 세부 정보 데이터 유형
description: 이 문서에서는 지역 상호 작용 세부 사항 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---

# [!UICONTROL 지리적 인터랙션 세부 정보] 데이터 유형

[!UICONTROL 지리적 인터랙션 세부 정보] 는 지리적으로 정의된 영역에 포함된 현재 상태를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 지역 모습]](./geo-shape.md) | 상호 작용 중인 영역의 지역 모양을 설명합니다. 이 필드는 상자, 원 또는 다각형을 설명할 수 있습니다. |
| `deviceGeoAccuracy` | 이중 | 지리 측정 장치 또는 메커니즘의 정확도(측정단위: 미터). |
| `distanceToCenter` | 이중 | 지역 서클의 경우 지역 중심까지의 거리(미터 단위)입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
