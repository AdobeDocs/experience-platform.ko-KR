---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;장치;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 장치 데이터 유형
description: 장치 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 5%

---

# [!UICONTROL 장치] 데이터 유형

[!UICONTROL 장치] 는 식별된 디바이스를 설명하는 표준 XDM 데이터 유형입니다. 디바이스는 일반적으로 쿠키를 통해 세션에서 추적할 수 있는 애플리케이션 또는 브라우저 인스턴스입니다.

<img src="../images/data-types/device.png" width="450" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `colorDepth` | 정수 | 디스플레이에 표시될 수 있는 색상 수. |
| `manufacturer` | 문자열 | 장치의 디자인과 제작을 담당하는 조직의 이름입니다. |
| `model` | 문자열 | 장치의 모델 이름입니다. 사람이 인식할 수 있는 일반 이름 또는 장치의 마케팅 이름입니다. 예를 들어 &quot;iPhone 6S&quot;는 휴대 전화의 특정 모델입니다. |
| `modelNumber` | 문자열 | 제조업체가 해당 디바이스에 할당한 고유 모델 번호 지정. 모델 번호는 버전이 아니라 특정 모델 구성을 식별하는 고유 식별자입니다. |
| `screenHeight` | 정수 | 기본 방향인 디바이스 활성화 디스플레이의 세로 픽셀 수. |
| `screenOrientation` | 문자열 | 현재 화면 방향입니다. 허용되는 값은 다음과 같습니다 `portrait` 및 `landscape`. |
| `screenWidth` | 문자열 | 기본 방향인 디바이스 활성화 디스플레이의 가로 픽셀 수. |
| `type` | 문자열 | 추적 중인 디바이스 유형. 허용되는 값은 다음과 같습니다. <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | 문자열 | 디바이스용 식별자. 이는 사용 중인 하드웨어를 식별하는 DeviceAtlas 또는 다른 서비스의 식별자일 수 있습니다. |
| `typeIDService` | 문자열 | 장치 유형을 식별하는 데 사용되는 서비스의 네임스페이스입니다. 다음을 참조하십시오. [부록](#typeIDService) 허용되는 값에 대한 세부 정보. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## 부록

다음 섹션은 다음에 대한 추가 정보를 포함합니다. [!UICONTROL 장치] 데이터 유형.

## typeIDService에 대해 허용되는 값 {#typeIDService}

다음 표에서 허용되는 값을 간략하게 설명합니다. `typeIDService` 및 관련 의미:

| 값 | 설명 |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | DeviceAtlas를 사용하여 장치를 확인했습니다. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Adobe Campaign을 사용하여 장치를 확인했습니다. |
