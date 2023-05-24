---
title: Adobe Experience Platform Assurance 개요
description: Adobe Experience Platform Assurance를 사용하면 모바일 애플리케이션 내에서 데이터를 수집하거나 경험을 제공하는 방식을 검사하고, 증명하고, 시뮬레이트하고, 검증할 수 있습니다.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 4%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance는 다음 제품의 일부입니다. [Adobe Experience Cloud](https://www.adobe.com/kr/experience-cloud.html) 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 됩니다.

>[!IMPORTANT]
>
> 이제 Griffson 프로젝트는 다음과 같습니다. **보증**!
>
> 이제 Project Grifson을 일반적으로 사용할 수 있습니다. **모두** Adobe Experience Cloud 고객은 보증입니다. 이 전환에 대한 자세한 내용은 [사용자 액세스 안내서](./user-access.md).

>[!INFO]
>
>보증 공개 API를 사용할 수 있습니다!
>
>[보증 API](https://developer.adobe.com/adobe-assurance-public-apis/) 는 Adobe 보증 모바일 SDK가 장착되어 있을 때 사용자가 웹 및 모바일 앱을 테스트하고 디버깅할 수 있도록 지원하는 API 컬렉션입니다.

## 일반 가용성

2022년 10월 15일부터 모든 Adobe Experience Cloud에서 보증 을 일반적으로 사용할 수 있습니다.

### 무엇이 바뀌고 있습니까?

10월 15일 - Assurance에 대한 액세스는 Admin Console을 통해 관리됩니다. 다음을 읽으십시오. [사용자 액세스 안내서](./user-access.md) 계속 액세스할 수 있도록 합니다.

기존 Assurance 통합, 세션 및 이벤트에 대해 다른 변경 사항이나 중단은 발생하지 않습니다. 보증 은 을 통해 계속 액세스할 수 있습니다. [https://griffon.adobe.com](https://griffon.adobe.com) **또는** (및 책갈피)를 사용할 수 있습니다. [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Assurance가 제공하는 이점

### 빠른 설정

코드 줄 몇 개를 사용하여 서둘러 시작하십시오. 모바일 앱의 경우, Assurance는 Adobe Experience Platform Mobile SDK와 함께 작동하여 앱 이벤트, 위치 신호, 구성 매개 변수, SDK 로그, 디바이스 정보 등을 검사, 시뮬레이션 및 확인할 수 있도록 합니다.

### 간편한 연결

Assurance를 사용하면 앱을 Platform과 연결할 때 편리하고 신뢰할 수 있습니다. 네트워크 프록시를 사용할 필요가 없습니다. [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) 및 기타 네트워크 체조 - 앱을 Assurance에 연결하는 것은 QR 코드를 스캔하거나 버튼을 탭하는 것만큼 쉽습니다.

![](./images/index/no-hassle-connection.png)

### 실시간 검사, 시뮬레이션 및 검증

Assurance에 연결한 후 실시간 스트리밍 앱 이벤트 및 활동을 검사하고 소음을 제거하기 위해 필터링하고 검색할 수 있습니다. 이벤트에는 모바일 앱 구현의 유효성 검사, 디버깅 및 문제 해결에 대한 세부 정보가 포함되어 있습니다. 또한 Assurance를 사용하여 스크린샷, 위치 신호 등을 실시간으로 시뮬레이션할 수 있습니다.

![](./images/index/real-time-insepction.png)

### Adobe Experience Cloud과 통합

클라이언트측 데이터와 경험은 사용자가 마케터 중심의 사용자 인터페이스에서 보고 규칙, 활동 및 캠페인을 설정하는 방법에 따라 컨텍스트가 지정됩니다. 두 점 사이를 연결하는 데 도움이 되도록 Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service 등과 같은 Adobe Experience Cloud 솔루션과 통합합니다.

![](./images/index/integration.png)

## 기능

### Adobe Experience Platform Mobile SDK 이벤트, 로그 등

보증은 Adobe Experience Platform Mobile SDK에서 생성한 원시 SDK 이벤트를 검사하는 데 도움이 됩니다. SDK에서 수집한 모든 이벤트를 검사할 수 있습니다. SDK 이벤트는 시간별로 정렬된 목록 보기에 로드됩니다. 각 이벤트에는 추가 세부 정보를 제공하는 세부 보기가 있습니다. SDK 구성, 데이터 요소, 공유 상태 및 SDK 확장 버전을 검색할 수 있는 추가 보기도 제공됩니다.

### Adobe Analytics

Adobe Analytics > Analytics 이벤트 보기는 Adobe Analytics 모바일 구현과 관련된 이벤트를 보여 주는 집중 보기입니다. 목록 보기에는 특정 형식의 보기에서 필수 이벤트 세부 사항과 함께 라이프사이클 또는 작업/상태 이벤트인 후 처리된 &quot;상태&quot;가 표시됩니다. 사후 처리 상태는 이벤트에 처리 규칙이 적용된 후 Adobe Analytics에서 이벤트를 처리한 방식을 보여 줍니다.

### 스트리밍 미디어용 Adobe Analytics

Adobe Analytics > Media Analytics 이벤트 보기에는 오디오 및 비디오 분석 구현에 대한 이벤트가 표시됩니다. 이벤트 세부 사항 보기에는 각 재생 세션에 대해 추적되는 표준 및 사용자 지정 메타데이터가 표시됩니다. 또한 미디어 체류 시간 또는 총 버퍼 지속 시간과 같은 후처리된 상태 및 후처리된 미디어 분석 데이터를 볼 수 있습니다.

### 장소(위치 서비스)

위치 서비스 보기는 쉽게 확인할 수 있도록 사용자 위치 시작 및 종료 이벤트를 보여 주는 장치 내 보기입니다. 이 편리한 뷰는 컨텍스트 내 디버깅을 위해 클라이언트에서 검사할 위치별 데이터 포인트를 볼 수 있는 편리한 인터페이스를 제공합니다.

## 안전합니까?

보증에는 다음과 같은 보안 조치가 적용됩니다.

* Assurance와 Assurance Web UI는 연결을 위한 안전한 PIN 기반 핸드셰이크를 제공합니다. 사용자는 최종 사용자가 &quot;우발적&quot; 보증 연결을 만들 수 없도록 악수를 명시적으로 만들어야 합니다.
* Assurance와 동일한 Adobe Experience Cloud 조직 ID에 속하는 Assurance 웹 UI 간의 연결만 지원됩니다.
* Adobe Experience Platform Mobile SDK 이벤트는 HTTPS를 통해 전송됩니다.
* 보증 및 Adobe Experience Platform Mobile SDK에서 TLS 1.2 사용
* 보증 세션은 30일 후 삭제됩니다.
* Assurance 세션 데이터는 스토리지 모범 사례에 따라 사용하지 않을 때 암호화됩니다.

## 시작하기

Assurance를 설정하려면 먼저 애플리케이션에 Assurance 확장을 설치해야 합니다. 이 작업을 수행하는 방법에 대해 알아보려면 의 자습서를 참조하십시오. [assurance 확장 구현](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

앱에 Assurance를 추가한 후 장치에 연결할 수 있는 Assurance 세션을 만들 수 있습니다. Assurance 사용 방법을 알아보려면 [보증 사용에 대한 안내서](./tutorials/using-assurance.md).
