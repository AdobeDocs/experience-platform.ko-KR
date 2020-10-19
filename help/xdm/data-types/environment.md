---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;environment;datatype;data-type;data type;
solution: Experience Platform
title: 환경 데이터 유형
topic: overview
description: 이 문서에서는 환경 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 4%

---


# [!UICONTROL 환경] 데이터 유형

[!UICONTROL 환경] (Environment)은 관찰된 이벤트의 주변 환경을 설명하는 표준 XDM 데이터 유형입니다. 특히 네트워크 및 소프트웨어 버전과 같은 임시 정보를 자세히 다룹니다.

>[!IMPORTANT]
>
>모든 값은 Adobe에 의해 라이선스가 부여된 [DeviceAtlas](https://deviceatlas.com) 데이터베이스에 맞춰 정렬되어야 합니다.

<img src="../images/data-types/environment.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_dc` | 개체 | 데이터 프레젠테이션에 대한 사용자의 언어적, 지리적 또는 문화적 환경 설정을 나타내는 단일 필드 `language`가 들어 있는 개체 언어는 IETF RFC [3066에 정의된 언어 코드에 지정됩니다](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [브라우저 세부 사항](./browser-details.md) | 브라우저 이름, 버전, JavaScript 버전, 사용자 에이전트 문자열, 수락 언어 등 환경에 대한 브라우저 특정 세부 사항을 설명합니다. |
| `ISP` | 문자열 | 사용자의 인터넷 서비스 공급자의 이름입니다. |
| `carrier` | 문자열 | 사용자에게 통신 서비스를 판매 및 전달하는 이동통신사 또는 MNO(무선 서비스 제공업체, 무선 통신사, 휴대폰 회사 또는 이동통신사라고도 함)의 이름입니다. |
| `colorDepth` | 정수 | 단일 픽셀의 각 색상 구성 요소에 사용된 비트 수입니다. |
| `connectionType` | 문자열 | 인터넷 연결 유형입니다. 허용되는 값은 다음과 같습니다. <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 문자열 | 사용자 ISP의 도메인. |
| `ipV4` | 문자열 | 통신(32비트)을 위해 인터넷 프로토콜을 사용하는 컴퓨터 네트워크에 참여하는 장치에 지정된 숫자 레이블입니다. |
| `ipV6` | 문자열 | 통신용 인터넷 프로토콜(128비트)을 사용하는 컴퓨터 네트워크에 참여하는 장치에 할당된 숫자 레이블입니다. |
| `operatingSystem` | 문자열 | OS의 이름. 속성에는 버전 정보와 같은 버전 정보가 포함되어서는 안 `10.5.3`되며, 대신 `Ultimate` 또는 `Professional`같은 &quot;에디션&quot; 디자인이 포함되어야 합니다. |
| `operatingSystemVendor` | 문자열 | 관찰 시 사용된 운영 체제 공급업체의 이름입니다. |
| `operatingSystemVersion` | 문자열 | 관찰이 수행되었을 때 사용된 운영 체제의 전체 버전 식별자입니다. 버전은 일반적으로 숫자로 구성되지만 공급업체가 정의한 형식일 수 있습니다. |
| `type` | 문자열 | 응용 프로그램 환경의 유형입니다. 허용된 값은 [부록을](#type) 참조하십시오. |
| `viewportHeight` | 정수 | 경험이 내부에 표시된 창의 세로 크기(픽셀)입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 높이입니다. |
| `viewPortWidth` | 정수 | 경험이 내부에 표시된 창의 가로 크기(픽셀)입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 너비입니다. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 부록

다음 섹션에는 장치 [!UICONTROL 데이터 유형에 대한 추가 정보가] 포함되어 있습니다.

## 허용되는 유형 값 {#type}

다음 표에서는 해당 의미와 관련하여 허용된 값에 대해 `type` 개괄적으로 설명합니다.

| 값 | 설명 |
| --- | --- |
| `browser` | 브라우저 |
| `application` | 애플리케이션 |
| `iot` | 사물의 인터넷 |
| `external` | 외부 시스템 |
| `widget` | 애플리케이션 확장 |