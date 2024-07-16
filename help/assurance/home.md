---
title: Adobe Experience Platform Assurance 개요
description: Adobe Experience Platform Assurance를 사용하면 모바일 애플리케이션 내에서 데이터를 수집하거나 경험을 제공하는 방식을 검사하고, 증명하고, 시뮬레이션하고, 검증할 수 있습니다.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 100%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance는 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 되는 [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html)의 제품입니다.

>[!IMPORTANT]
>
> Project Griffon은 **Assurance**&#x200B;라고도 합니다!
>
> 이제 Project Griffon은 일반적으로 **모든** Adobe Experience Cloud 고객에게 Assurance로 제공됩니다. 이 전환에 대한 자세한 내용은 [사용자 액세스 안내서](./user-access.md)를 참조하십시오.

>[!INFO]
>
>Assurance 공개 API를 사용할 수 있습니다!
>
>[Assurance API](https://developer.adobe.com/adobe-assurance-public-apis/)는 Adobe Assurance Mobile SDK를 갖춘 경우 사용자가 자신의 웹 및 모바일 앱을 테스트하고 디버깅할 수 있도록 지원하는 API 모음입니다.

## 일반 가용성

2022년 10월 15일부터 Assurance는 모든 Adobe Experience Cloud에서 일반적으로 사용할 수 있습니다.

### 변경되는 사항은 무엇입니까?

10월 15일 - Assurance에 대한 액세스는 Admin Console을 통해 관리됩니다. 중단 없이 계속 액세스할 수 있도록 [사용자 액세스 안내서](./user-access.md)를 참조하십시오.

기존 Assurance 통합, 세션 및 이벤트에는 다른 변경이나 중단이 예상되지 않습니다. Assurance는 [https://griffon.adobe.com](https://griffon.adobe.com) **또는** 사용자가 사용할 수 있는 [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance)(및 책갈피)를 통해 계속 액세스할 수 있습니다.

## Assurance의 기능은 무엇입니까?

### 빠른 설정

몇 줄의 코드를 사용하여 신속하게 시작할 수 있습니다. 모바일 앱의 경우 Assurance는 Adobe Experience Platform Mobile SDK와 함께 작동하여 앱 이벤트, 위치 신호, 구성 매개변수, SDK 로그, 디바이스 정보 등을 검사, 시뮬레이션 및 확인할 수 있습니다.

### 간편한 연결

Assurance를 사용하면 Platform과 앱을 간단하고 안정적으로 연결할 수 있습니다. 네트워크 프록시, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 및 기타 네트워크 도구를 사용할 필요가 없이 QR 코드를 스캔하거나 버튼을 누르는 것처럼 손쉽게 앱을 Assurance에 연결할 수 있습니다.

![](./images/index/no-hassle-connection.png)

### 실시간 검사, 시뮬레이션 및 유효성 검사

Assurance에 연결하면 라이브 스트리밍된 앱 이벤트 및 활동을 검사하고 필터링 및 검색하여 노이즈를 제거할 수 있습니다. 이벤트에는 모바일 앱 구현의 유효성 검사, 디버깅 및 문제 해결에 대한 세부 정보가 포함되어 있습니다. Assurance를 사용하면 스크린샷을 찍고 위치 신호를 시뮬레이션하는 등의 작업을 실시간으로 수행할 수 있습니다.

![](./images/index/real-time-insepction.png)

### Adobe Experience Cloud와 통합

사용자가 마케터 중심의 사용자 인터페이스에서 보고 규칙, 활동 및 캠페인을 설정하는 방법에 따라 클라이언트측 데이터 및 경험에 컨텍스트가 제공됩니다. 둘 사이를 연결할 수 있도록 Adobe는 Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service 등과 같은 Adobe Experience Cloud 솔루션과 통합하고 있습니다.

![](./images/index/integration.png)

## 기능

### Adobe Experience Platform Mobile SDK 이벤트, 로그 등

Assurance를 통해 Adobe Experience Platform Mobile SDK에서 생성된 원시 SDK 이벤트를 검사할 수 있습니다. SDK에서 수집한 모든 이벤트를 검사할 수 있습니다. SDK 이벤트는 시간별로 정렬된 목록 보기에 로드됩니다. 각 이벤트에는 추가 정보를 제공하는 상세 보기가 있습니다. SDK 구성, 데이터 요소, 공유 상태 및 SDK 확장 기능 버전을 찾아볼 수 있는 추가 보기도 제공됩니다.

### Adobe Analytics

Adobe Analytics > Analytics 이벤트 보기는 Adobe Analytics 모바일 구현과 관련된 이벤트를 표시하는 집중 보기입니다. 목록 보기는 형식이 특별 지정된 보기에서 필수 이벤트 세부 정보와 함께 수명 주기 또는 작업/상태 이벤트, 후처리된 “상태”를 보여 줍니다. 후처리된 상태는 이벤트에 처리 규칙이 적용된 후 Adobe Analytics에서 이벤트를 처리하는 방법을 보여 줍니다.

### 스트리밍 미디어용 Adobe Analytics

Adobe Analytics > Media Analytics 이벤트 보기에는 오디오 및 비디오 분석 구현에 대한 이벤트가 표시됩니다. 이벤트 세부 정보 보기에는 각 재생 세션에 대해 추적되는 표준 및 사용자 정의 메타데이터가 표시됩니다. 또한 미디어 소요 시간 또는 총 버퍼 지속 시간과 같은 후처리 상태 및 후처리 미디어 분석 데이터를 볼 수 있습니다.

### 장소(위치 서비스)

위치 서비스 보기는 간편한 유효성 검사를 위해 사용자 위치 항목 및 종료 이벤트를 표시하는 온디바이스 보기입니다. 이 편리한 보기는 컨텍스트 내 디버깅을 위해 클라이언트에서 검사할 위치별 데이터 포인트를 볼 수 있는 편리한 인터페이스를 제공합니다.

## Assurance는 안전합니까?

Assurance에는 다음과 같은 보안 조치가 있습니다.

* Assurance와 Assurance 웹 UI에는 연결을 위한 안전한 PIN 기반의 핸드셰이크가 있습니다. 사용자는 핸드셰이크를 명시적으로 생성해야 최종 사용자가 “우발적인” Assurance 연결을 생성하는 것을 방지할 수 있습니다.
* Assurance와 동일한 Adobe Experience Cloud 조직 ID에 속하는 Assurance 웹 UI 간의 연결만 지원됩니다.
* Adobe Experience Platform Mobile SDK 이벤트는 HTTPS를 통해 전송됩니다.
* Assurance 및 Adobe Experience Platform Mobile SDK는 TLS 1.2를 사용합니다.
* Assurance 세션은 30일 후에 삭제됩니다.
* Assurance 세션 데이터는 스토리지 모범 사례에 따라 사용하지 않을 때 암호화됩니다.

## 시작하기

Assurance를 설정하려면 먼저 애플리케이션에 Assurance 확장 기능을 설치해야 합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [Assurance 확장 기능 구현](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app)에 대한 튜토리얼을 참조하십시오.

앱에 Assurance를 추가한 후에 디바이스에 연결할 수 있는 Assurance 세션을 생성할 수 있습니다. Assurance 사용 방법을 알아보려면 [Assurance 사용에 관한 안내서](./tutorials/using-assurance.md)를 참조하십시오.
