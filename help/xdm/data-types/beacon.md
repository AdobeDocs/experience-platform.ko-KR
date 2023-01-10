---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;비콘;상호 작용 세부 사항;데이터 유형;데이터 유형;
solution: Experience Platform
title: 비콘 데이터 유형
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 4%

---

# [!UICONTROL 비콘] 데이터 유형

[!UICONTROL 비콘] 는 모바일 장치가 범위 내에 있으므로 모바일 애플리케이션에 ID 정보를 전달하는 무선 장치를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/beacon.png" width="450" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `beaconMajor` | 이중 | 주 값은 1과 65,535 사이의 그룹 및 부호 없는 정수 값을 식별하고 구분합니다. |
| `beaconMinor` | 이중 | 작은 값은 1과 65,535 사이의 개인 및 부호 없는 정수 값을 식별하고 구분합니다. |
| `proximity` | 문자열 | 비콘으로부터의 예상 거리. 자세한 내용은 [부록](#proximity) 참조하십시오. |
| `proximityUUID` | 문자열 | Proximity UUID(Universally Unique Identifier)는 네트워크의 비콘과 컨트롤 외부의 네트워크에 있는 다른 모든 비콘을 구분하는 데 사용되는 특별한 유형의 식별자입니다. 근접 UUID는 비콘으로 구성되며 다양한 범위의 모바일 장치로 전송되어 조직의 비콘을 식별합니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## 부록

다음 섹션에는 [!UICONTROL 비콘] 데이터 유형.

## 근접에 대해 허용되는 값 {#proximity}

다음 표에서는 `proximity` 그리고 그들의 연관 의미는 다음과 같습니다.

| 값 | 설명 |
| --- | --- |
| `immediate` | 몇 센티미터 안에 있어요 |
| `near` | 10미터 미만 거리에 있습니다. |
| `far` | 10미터 이상 떨어져 있습니다. |
| `unknown` | 신호가 약하여 거리를 확인할 수 없었다. |
