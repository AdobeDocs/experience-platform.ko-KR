---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;환경;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 환경 데이터 유형
description: 이 문서에서는 환경 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 4%

---

# [!UICONTROL 환경] 데이터 유형

[!UICONTROL 환경] 는 관찰된 이벤트의 주변 환경을 설명하는 표준 XDM 데이터 유형으로, 특히 네트워크 및 소프트웨어 버전과 같은 임시 정보가 자세히 설명되어 있습니다.

>[!IMPORTANT]
>
>모든 값은 [DeviceAtlas](https://deviceatlas.com) Adobe에 의해 사용이 허가된 데이터베이스.

<img src="../images/data-types/environment.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_dc` | 오브젝트 | 단일 필드가 포함된 개체 `language`: 데이터 표시에 대한 사용자의 언어적, 지리적 또는 문화적 선호도를 나타내는 환경 언어를 나타냅니다. 언어는에 정의된 대로 언어 코드에 지정됩니다. [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [브라우저 세부 정보](./browser-details.md) | 브라우저 이름, 버전, JavaScript 버전, 사용자 에이전트 문자열 및 수락 언어와 같은 환경의 브라우저별 세부 정보를 설명합니다. |
| `ISP` | 문자열 | 사용자의 인터넷 서비스 공급자 이름. |
| `carrier` | 문자열 | 사용자에게 통신 서비스를 판매 및 전달하는 모바일 네트워크 통신사 또는 MNO(무선 서비스 제공업체, 무선 통신사, 셀룰러 회사 또는 모바일 네트워크 통신사라고도 함)의 이름입니다. |
| `colorDepth` | 정수 | 단일 픽셀의 각 색상 구성 요소에 사용되는 비트 수. |
| `connectionType` | 문자열 | 인터넷 연결 유형. 허용되는 값은 다음과 같습니다. <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 문자열 | 사용자 ISP의 도메인입니다. |
| `ipV4` | 문자열 | 통신용 인터넷 프로토콜(32비트)을 사용하는 컴퓨터 네트워크에 참여하는 장치에 할당된 숫자 레이블입니다. |
| `ipV6` | 문자열 | 통신용 인터넷 프로토콜(128비트)을 사용하는 컴퓨터 네트워크에 참여하는 장치에 할당된 숫자 레이블입니다. |
| `operatingSystem` | 문자열 | 관찰 시 사용된 운영 체제의 이름입니다. 속성에는 버전 정보(예: )가 없어야 합니다. `10.5.3`대신 와 같은 &quot;편집&quot; 지정이 포함됩니다. `Ultimate` 또는 `Professional`. |
| `operatingSystemVendor` | 문자열 | 관찰 시 사용된 운영 체제 공급업체의 이름. |
| `operatingSystemVersion` | 문자열 | 관찰 시 사용되는 운영 체제에 대한 전체 버전 식별자입니다. 버전은 일반적으로 숫자로 구성되지만 공급업체가 정의한 형식일 수 있습니다. |
| `type` | 문자열 | 애플리케이션 환경 유형. 다음을 참조하십시오. [부록](#type) (허용된 값). |
| `viewportHeight` | 정수 | 내부에 경험이 표시되는 윈도우 픽셀의 세로 크기입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 높이입니다. |
| `viewPortWidth` | 정수 | 내부에 경험이 표시되는 윈도우 픽셀의 가로 크기. 웹 보기 이벤트의 경우 브라우저 뷰포트 폭입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 부록

다음 섹션은 다음에 대한 추가 정보를 포함합니다. [!UICONTROL 장치] 데이터 유형.

## 유형에 대해 허용되는 값 {#type}

다음 표에서 허용되는 값을 간략하게 설명합니다. `type` 및 관련 의미:

| 값 | 설명 |
| --- | --- |
| `browser` | 브라우저 |
| `application` | 애플리케이션 |
| `iot` | 사물 인터넷 |
| `external` | 외부 시스템 |
| `widget` | 애플리케이션 확장 |
