---
title: Adobe Experience Platform 웹 SDK 도움말
seo-title: Adobe Experience Platform 웹 SDK 도움말
description: Adobe Experience Platform 웹 SDK의 정의와 사용 방법을 살펴보십시오.
seo-description: adobe experience cloud 고객이 Experience Cloud의 다양한 서비스와 상호 작용할 수 있도록 허용
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---


# Adobe Experience Platform 웹 SDK 소개

Adobe Experience Platform 웹 SDK는 Adobe Experience Cloud 고객이 Adobe을 통해 다양한 서비스와 상호 작용할 수 있는 클라이언트측 JavaScript 라이브러리입니다 [!DNL Experience Cloud] [!DNL Experience Platform Edge Network]. JavaScript 라이브러리 외에도 웹 SDK 구성 [에 도움이 되는 Launch 익스텐션이](https://docs.adobe.com/content/help/ko-KR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) 있습니다.

## 경험 에지

[!DNL Adobe Experience Platform Web SDK] 는 Experience Edge를 구성하는 컬렉션의 일부입니다. Adobe Experience Edge는

* **[!DNL Adobe Experience Platform Web SDK]:** JavaScript SDK 및 [!DNL Launch] 익스텐션을 통해 [!DNL Adobe] 기술 배포 간소화
* **Adobe Experience Platform 모바일 SDK:** 고객이 새로운 배포 방법을 사용할 수 있도록 v5 모바일 SDK 확장
* **[!DNL Adobe Experience Platform Edge Network]:** 제품을 배포하는 새로운 방법을 제공하는 글로벌 분산 서버 [!DNL Adobe] 네트워크

이 [!DNL Adobe Experience Edge] 는 모든 지정 가능한 채널에서 낮은 지연 시간 데이터 수집, 플러그 가능 컴퓨팅 및 신속한 데이터 활성화를 위한 새로운 프레임워크입니다.

[!DNL Adobe Experience Edge] 는 모든 채널(JavaScript, Mobile, Server-side)에 대해 단일 통합 SDK를 제공하며, 이 SDK는 데이터를 공통 Adobe 도메인(`adobedc.net`)으로 보내고 데이터 및 경험 전달을 위해 다시 단일 페이로드를 수신합니다.

서버측 통합된 Edge Gateway와 공통 플랫폼 서비스 프레임워크를 사용하면 이러한 실시간 컴퓨팅 환경에 새로운 기능을 손쉽게 연결하여 배포할 수 있습니다.  이 아키텍처는

* 가치 창출 시간 단축
* &quot;포인트&quot; 통합의 필요성 종료
* 이전 라이브러리와 비교하여 성능 향상
* 비용 절감
* 혁신 속도 향상
* Adobe 고객에게 지속적인 경쟁 우위 창출

하나의 통합 에지 시스템을 통해 모든 채널에서 광고, 마케팅 또는 개인화 캠페인을 통합 경험으로 관리할 수 있습니다.  TCO(총 소유 비용)가 낮은 서비스를 고객에게 제공할 수 [!DNL Adobe] 있습니다.  또한 실시간 에지 플러그인을 만들고 고객 [!DNL Adobe] 이 새로운 기능과 고객 정의 로직을 해당 실시간 시스템에 보다 신속하게 추가할 수 있으므로 제품 혁신 속도를 높일 수 있습니다.

## 비디오 개요

다음 비디오에서는 Adobe Experience Platform [!DNL Web SDK] 와 [!DNL Edge Network]에 대한 개요를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Adobe Experience Platform 웹 SDK로 대체된 SDK

Adobe Experience Platform 웹 SDK는 다음 SDK를 대체합니다.

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

기존 라이브러리 주위에 있는 래퍼만이 아닙니다. 완전히 다시 쓴 거야 이 솔루션의 목적은 올바른 순서로 태그를 실행해야 하는 문제, 라이브러리 버전 관리 문제와 불일치, 향상된 종속성 관리 등을 해소하는 것입니다. 이를 구현하는 새로운 방식이며 [!DNL Experience Cloud] 오픈 소스로 [제공됩니다](https://github.com/adobe/alloy).

새로운 라이브러리 외에도 Adobe 솔루션에 대한 HTTP 요청을 간소화하는 새로운 종점이 있습니다. 이전에 Visitor.js는 방문자 ID 서비스에 차단 호출을 전송한 다음 AT.js에서 Adobe Target에 대한 호출을 전송하고, DIL.js는 Adobe Audience Manager에 대한 호출을 전송했으며, 마지막으로 AppMeasurement.js는 Adobe Analytics에 대한 호출을 전송했습니다. 이 새 라이브러리와 종단점은 ID를 검색하고, [!DNL Target] [!DNL Audience Manager]경험을 가져오고, 데이터를 보내고, 데이터를 한 번의 호출로 Adobe Experience Platform에 전달할 수 있습니다.

다음 비디오에서는 Adobe Experience Platform [!DNL Web SDK] 와 [!DNL Edge Network] 활용 방법을 보여 줍니다. 이 비디오 예제에서는 Adobe에 대한 단일 호출을 사용하여 데이터 [!DNL Experience Platform], [!DNL Analytics][!DNL Audience Manager]및 [!DNL Target]데이터를 보냅니다.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

## 시작하기

Adobe 시작 [을 사용하는 방법에 대한 빠른 자습서를 보려면 시작 가이드](getting-started/quick-start-with-launch.md) 를 확인해 보는 것이 좋습니다.

이 제품은 점점 더 많은 사용 사례를 지원하기 위해 끊임없이 진화하고 증가하고 있습니다. 최신 정보를 얻으려면 [지원되는 사용 사례 보드를 확인하십시오](https://github.com/adobe/alloy/projects/5). Adobe는 Adobe가 현재 지원하는 사용 사례와 귀하가 최상의 결정을 내릴 수 있도록 노력하고 있는 사례에 대해 이러한 최신 정보를 제공합니다.

* **아직 지원되지 않는 사용 사례:** 향후 지원이 제공될 예정인 사용 사례입니다.
* **진행 중인 사용 사례:** 팀이 현재 릴리스를 완료하기 위해 작업 중인 사용 사례입니다.
* **지원되는 사용 사례:** 다음은 현재 지원되고 작동하는 사용 사례입니다.
* **지원되지 않는 사용 사례:** 이것이 우리가 지지하지 않기로 결정한 사용 사례이다.
