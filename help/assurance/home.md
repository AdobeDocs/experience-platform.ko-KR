---
title: Adobe Experience Platform Assurance 개요
description: Adobe Experience Platform Assurance를 사용하면 모바일 애플리케이션 내에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인할 수 있습니다.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---


# Adobe Experience Platform 보증

Adobe Experience Platform Assurance는 [Adobe Experience Cloud](https://www.adobe.com/kr/experience-cloud.html) 를 사용하여 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인할 수 있습니다.

>[!IMPORTANT]
>
> 프로젝트 그리폰은 이제 **보증**!
>
> 이제 Project Griffon을 일반적으로 사용할 수 있습니다. **모두** Adobe Experience Cloud 고객을 Assurance로 지원합니다. 이 전환에 대한 자세한 내용은 [사용자 액세스 안내서](./user-access.md).

>[!INFO]
>
>Assurance 공용 API를 사용할 수 있습니다.
>
>[보증 API](https://developer.adobe.com/adobe-assurance-public-apis/) 는 Adobe Assurance Mobile SDK와 함께 제공되는 경우 사용자가 웹 및 모바일 앱을 테스트 및 디버깅할 수 있도록 하는 API 모음입니다.

## 일반 가용성

2022년 10월 15일부터 Assurance는 모든 Adobe Experience Cloud에서 일반적으로 사용할 수 있습니다.

### 뭐가 변하죠?

10월 15일 - Assurance에 대한 액세스는 Admin Console을 통해 관리됩니다. 자세한 내용은 [사용자 액세스 안내서](./user-access.md) 계속 중단 없이 액세스할 수 있도록 합니다.

기존의 보증 통합, 세션 및 이벤트에는 다른 변경 사항이나 중단이 필요하지 않습니다. 은 을 통해 계속 액세스할 수 있습니다 [https://griffon.adobe.com](https://griffon.adobe.com) **또는** 및 책갈피를 사용할 수 있습니다. [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Assurance가 무엇을 해줄 수 있습니까?

### 빠른 설정

몇 줄의 코드를 사용하여 빠르게 시작하십시오. 모바일 앱의 경우, Assurance는 Adobe Experience Platform Mobile SDK와 함께 앱 이벤트, 위치 신호, 구성 매개 변수, SDK 로그, 장치 정보 등을 검사, 시뮬레이션 및 확인할 수 있도록 도와줍니다.

### 간편한 연결

Assurance를 통해 앱을 플랫폼에 연결하는 것은 간단하고 안정적입니다. 네트워크 프록시를 사용할 필요는 없습니다. [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) 및 기타 네트워크 체조 - Assurance에 앱을 연결하는 것은 QR 코드를 스캔하거나 단추를 탭하는 것만큼 쉽습니다.

![](./images/index/no-hassle-connection.png)

### 실시간 검사, 시뮬레이션 및 검증

Assurance에 연결한 후 실시간 스트리밍 앱 이벤트 및 활동을 검사하고 필터 및 검색을 통해 노이즈를 제거할 수 있습니다. 이벤트에는 모바일 앱 구현 확인, 디버깅 및 문제 해결에 대한 세부 사항이 포함되어 있습니다. 또한 Assurance를 통해 스크린샷을 하고 위치 신호를 시뮬레이션할 수 있으며 실시간으로 기타 정보를 얻을 수 있습니다.

![](./images/index/real-time-insepction.png)

### Adobe Experience Cloud과 통합

클라이언트측 데이터 및 경험에는 사용자가 마케터 중심의 사용자 인터페이스에 보고 규칙, 활동 및 캠페인을 설정하는 방법에 의해 컨텍스트가 제공됩니다. 두 요소 간의 관계를 연결하기 위해 Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service 등과 같은 Adobe Experience Cloud 솔루션과 통합하고 있습니다.

![](./images/index/integration.png)

## 기능

### Adobe Experience Platform Mobile SDK 이벤트, 로그 등

보증은 Adobe Experience Platform Mobile SDK에서 생성한 원시 SDK 이벤트를 검사하는 데 도움이 됩니다. SDK에서 수집한 모든 이벤트를 검사할 수 있습니다. SDK 이벤트는 시간별로 정렬된 목록 보기에 로드됩니다. 각 이벤트에는 세부 사항을 제공하는 세부 보기가 있습니다. SDK 구성, 데이터 요소, 공유 상태 및 SDK 확장 버전을 검색할 수 있는 추가 보기가 제공됩니다.

### Adobe Analytics

Adobe Analytics > Analytics 이벤트 보기는 Adobe Analytics 모바일 구현과 관련된 이벤트를 보여주는 집중 보기입니다. 목록 보기는 특별히 형식이 지정된 보기의 필수 이벤트 세부 정보와 함께 라이프사이클 또는 작업/상태 이벤트, 사후 처리 &quot;상태&quot;를 표시합니다. 사후 처리 상태는 처리 규칙이 이벤트에 적용된 후 Adobe Analytics에서 이벤트를 처리한 방식을 보여줍니다.

### 스트리밍 미디어용 Adobe Analytics

Adobe Analytics > Media Analytics 이벤트 보기에는 오디오 및 비디오 분석 구현에 대한 이벤트가 표시됩니다. 이벤트 세부 사항 보기에는 각 재생 세션에 대해 추적되는 표준 및 사용자 지정 메타데이터가 표시됩니다. 또한 사후 처리 상태 및 미디어 체류 시간 또는 총 버퍼 지속 시간과 같은 사후 처리 미디어 분석 데이터를 볼 수 있습니다.

### 위치(위치 서비스)

위치 서비스 보기는 쉽게 검증할 수 있도록 사용자 위치 시작 및 종료 이벤트를 표시하는 장치 상의 보기입니다. 이 편리한 뷰는 컨텍스트 내 디버깅을 위해 클라이언트에서 검사할 위치 특정 데이터 포인트를 보는 편리한 인터페이스를 제공합니다.

## Assurance가 안전합니까?

보증에는 다음과 같은 보안 조치가 있습니다.

* Assurance와 Assurance Web UI는 모두 연결을 위한 안전한 PIN 기반 핸드셰이크가 있습니다. 사용자는 핸드셰이크를 명시적으로 만들어야 하며, 이를 통해 최종 사용자가 &quot;우발적&quot; 보증 연결을 만들 수 없습니다.
* 동일한 Adobe Experience Cloud 조직 ID에 속하는 Assurance 및 Assurance 웹 UI 간의 연결만 지원됩니다.
* Adobe Experience Platform Mobile SDK 이벤트는 HTTPS를 통해 전송됩니다.
* Assurance 및 Adobe Experience Platform Mobile SDK는 TLS 1.2를 사용합니다
* 보증 세션은 30일 후에 삭제됩니다.
* 보증 세션 데이터는 저장 시 암호화되며, 스토리지 모범 사례를 따릅니다.

## 시작하기

확인을 설정하려면 먼저 응용 프로그램에 Assurance 확장을 설치해야 합니다. 이 작업을 수행하는 방법에 대해 알아보려면 다음 내용을 참조하십시오. [보증 확장 구현](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

앱에 보증을 추가한 후 장치에 연결할 수 있는 보증 세션을 만들 수 있습니다. Assurance 사용 방법을 알아보려면 [보증 사용 안내서](./tutorials/using-assurance.md).
