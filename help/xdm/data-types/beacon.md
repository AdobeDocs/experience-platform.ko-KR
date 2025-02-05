---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;비콘;상호 작용 세부 정보;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 비콘 데이터 유형
description: XDM 개별 프로필 클래스에 대해 알아봅니다.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 17%

---

# [!UICONTROL Beacon] 데이터 형식

[!UICONTROL Beacon]은 모바일 장치가 범위 내에 있을 때 모바일 응용 프로그램에 ID 정보를 전달하는 무선 장치를 설명하는 표준 XDM 데이터 형식입니다.

![](../images/data-types/beacon.png){width=450}

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `beaconMajor` | 더블 | 메이저 값은 1~65,535 간의 그룹 및 부호 없는 정수 값을 식별하고 구별합니다. |
| `beaconMinor` | 더블 | 마이너 값은 1~65,535 간의 개별 및 부호 없는 정수 값을 식별하고 구별합니다. |
| `proximity` | 문자열 | 비콘과의 예상 거리. 허용되는 값 및 정의는 [부록](#proximity)을 참조하십시오. |
| `proximityUUID` | 문자열 | 근접 UUID(Universally Unique Identifier)는 네트워크 내부의 비콘과 네트워크 외부의 다른 비콘을 식별하는 데 사용되는 특수 식별자입니다. 근접 UUID는 비콘으로 구성되어 조직의 비콘을 식별하기 위한 범위의 모바일 디바이스로 전송됩니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## 부록

다음 섹션에는 [!UICONTROL Beacon] 데이터 형식에 대한 추가 정보가 포함되어 있습니다.

## 근접성에 대해 허용되는 값 {#proximity}

다음 표에서는 `proximity`에 대해 허용되는 값과 관련된 의미를 설명합니다.

| 값 | 설명 |
| --- | --- |
| `immediate` | 몇 센티미터 이내입니다. |
| `near` | 10미터도 안 남았어요 |
| `far` | 10미터 이상 떨어져 있습니다. |
| `unknown` | 신호가 약해 거리를 확인할 수 없었다. |
