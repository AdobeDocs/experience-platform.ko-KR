---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;비콘;상호 작용 세부 사항;데이터 유형;데이터 유형;데이터 유형;;home;popular topics;schema;fields;schemas;interaction details;data-type;data-type;
solution: Experience Platform
title: 비콘 데이터 유형
topic-legacy: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 3%

---

# [!UICONTROL Beacon] 데이터 유형

[!UICONTROL Beacon] 는 모바일 장치가 범위 내에 있을 때 ID 정보를 모바일 응용 프로그램에 전달하는 무선 장치를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/beacon.png" width="450" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `beaconMajor` | 이중 | 주요 값은 1에서 65,535 사이의 그룹 및 부호 없는 정수 값을 식별 및 구별합니다. |
| `beaconMinor` | 이중 | 작은 값은 1에서 65,535 사이의 개별 및 부호 없는 정수 값을 식별하고 구별합니다. |
| `proximity` | 문자열 | 비콘과의 예상 거리. 허용되는 값과 정의는 [부록](#proximity)을 참조하십시오. |
| `proximityUUID` | 문자열 | 근접 UUID(범용 고유 식별자)는 네트워크의 비콘을 사용자 제어 외부의 네트워크의 다른 모든 비콘과 구별하는 데 사용되는 특별한 유형의 식별자입니다. 근접 UUID는 비콘에 구성되어 범위 내에서 모바일 장치에 전송되어 조직의 비콘을 식별할 수 있습니다. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## 부록

다음 섹션에는 [!UICONTROL Beacon] 데이터 유형에 대한 추가 정보가 포함되어 있습니다.

## 근접성 {#proximity}에 대해 허용된 값

다음 표는 `proximity`에 대해 허용된 값과 이와 관련된 의미를 대략적으로 설명합니다.

| 값 | 설명 |
| --- | --- |
| `immediate` | 몇 센티미터만 안 돼요 |
| `near` | 10m 미만 거리에 있습니다. |
| `far` | 10미터 이상 떨어져 있습니다. |
| `unknown` | 약한 신호 때문에 거리를 확인할 수 없었다. |
