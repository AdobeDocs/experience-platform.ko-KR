---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: 비콘 데이터 유형
topic: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---


# [!UICONTROL 비콘] 데이터 유형

[!UICONTROL 비콘] (Beacon)은 모바일 장치가 범위 내에 들어올 때 ID 정보를 모바일 애플리케이션에 전달하는 무선 장치를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/beacon.png" width="450" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `beaconMajor` | 이중 | 주요 값은 1과 65,535 사이의 그룹과 부호 없는 정수 값을 식별하고 구별합니다. |
| `beaconMinor` | 이중 | 작은 값은 1과 65,535 사이의 개별 및 부호 없는 정수 값을 식별하고 구별합니다. |
| `proximity` | 문자열 | 비콘과의 예상 거리. 허용되는 값 및 정의는 [부록을](#proximity) 참조하십시오. |
| `proximityUUID` | 문자열 | 근접 UUID(범용 고유 식별자)는 네트워크의 비콘을 사용자 제어 외부의 네트워크의 다른 모든 비콘과 구별하는 데 사용되는 특수한 식별자입니다. 근접 UUID는 비콘으로 구성되며 조직의 비콘을 식별하기 위해 범위 내에서 모바일 장치로 전송됩니다. |

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## 부록

다음 섹션에는 [!UICONTROL 비콘 데이터 유형에 대한 추가 정보가] 포함되어 있습니다.

## 근접성에 허용된 값 {#proximity}

다음 표에서는 해당 의미와 관련하여 허용된 값에 대해 `proximity` 개괄적으로 설명합니다.

| 값 | 설명 |
| --- | --- |
| `immediate` | 몇 센티미터내로 |
| `near` | 10미터 미만 거리에 있습니다 |
| `far` | 10미터 이상 떨어져 있습니다. |
| `unknown` | 약한 신호 때문에 거리를 확인할 수 없었다. |