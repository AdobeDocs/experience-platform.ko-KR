---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;환경;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 환경 데이터 유형
description: 이 문서에서는 환경 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 5%

---

# [!UICONTROL 환경] 데이터 유형

[!UICONTROL 환경] 는 관찰된 이벤트의 주변 환경을 설명하는 표준 XDM 데이터 유형이며, 특히 네트워크 및 소프트웨어 버전과 같은 임시 정보를 자세히 설명합니다.

>[!IMPORTANT]
>
>모든 값은 [DeviceAtlas](https://deviceatlas.com) Adobe에 의해 라이선스가 부여된 데이터베이스.

<img src="../images/data-types/environment.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_dc` | 오브젝트 | 단일 필드를 포함하는 객체입니다. `language`: 데이터 프레젠테이션에 대한 사용자의 언어, 지리적 또는 문화적 환경 설정을 나타내는 환경의 언어를 나타냅니다. 언어는 정의된 대로 언어 코드에 지정됩니다. [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [브라우저 세부 사항](./browser-details.md) | 브라우저 이름, 버전, JavaScript 버전, 사용자 에이전트 문자열, 수락 언어 등 환경에 대한 브라우저 특정 세부 사항을 설명합니다. |
| `ISP` | 문자열 | 사용자의 인터넷 서비스 공급자의 이름입니다. |
| `carrier` | 문자열 | 사용자에게 통신 서비스를 판매 및 전달하는 모바일 네트워크 통신사 또는 MNO(무선 서비스 제공자, 무선 통신사, 셀룰러 회사 또는 이동통신사라고도 함)의 이름입니다. |
| `colorDepth` | 정수 | 단일 픽셀의 각 색상 구성 요소에 사용되는 비트 수입니다. |
| `connectionType` | 문자열 | 인터넷 연결 유형입니다. 허용되는 값은 다음과 같습니다. <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 문자열 | 사용자의 ISP의 도메인입니다. |
| `ipV4` | 문자열 | 상기 통신용 인터넷 프로토콜(32비트)을 사용하는 컴퓨터 네트워크에 참여하는 장치에 할당되는 수치적 라벨. |
| `ipV6` | 문자열 | 상기 통신용 인터넷 프로토콜(128비트)을 사용하는 컴퓨터 네트워크에 참여하는 장치에 할당되는 수치적 라벨. |
| `operatingSystem` | 문자열 | 관찰이 수행될 때 사용되는 운영 체제의 이름입니다. 속성에는 다음과 같은 버전 정보를 포함해서는 안 됩니다. `10.5.3`, 대신 과 같은 &quot;edition&quot; 지정을 포함합니다 `Ultimate` 또는 `Professional`. |
| `operatingSystemVendor` | 문자열 | 관찰이 수행될 때 사용되는 운영 체제 공급업체의 이름입니다. |
| `operatingSystemVersion` | 문자열 | 관찰이 수행될 때 사용되는 운영 체제의 전체 버전 식별자입니다. 버전은 일반적으로 숫자로 구성되지만 공급업체에서 정의한 형식일 수 있습니다. |
| `type` | 문자열 | 애플리케이션 환경의 유형입니다. 자세한 내용은 [부록](#type) 참조하십시오. |
| `viewportHeight` | 정수 | 경험이 내부에 표시된 창의 세로 크기(픽셀 단위)입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 높이입니다. |
| `viewPortWidth` | 정수 | 경험이 내부에 표시된 창의 가로 크기(픽셀 단위)입니다. 웹 보기 이벤트의 경우 브라우저 뷰포트 너비입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 부록

다음 섹션에는 [!UICONTROL 장치] 데이터 유형.

## 유형에 대해 허용되는 값 {#type}

다음 표에서는 `type` 그리고 그들의 연관 의미는 다음과 같습니다.

| 값 | 설명 |
| --- | --- |
| `browser` | 브라우저 |
| `application` | 애플리케이션 |
| `iot` | 사물의 인터넷 |
| `external` | 외부 시스템 |
| `widget` | 애플리케이션 확장 |
