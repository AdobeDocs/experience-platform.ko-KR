---
title: Adobe Experience Platform 웹 SDK 개요
description: Adobe Experience Platform 웹 SDK를 사용하여 플랫폼 기능을 웹 사이트에 통합하는 방법을 살펴볼 수 있습니다.
keywords: Adobe Experience Platform 웹 SDK;플랫폼 웹 SDK;웹 SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;웹 sdk;SDK;웹 SDK;시작;시작
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 2%

---


# Adobe Experience Platform 웹 SDK 개요

Adobe Experience Platform 웹 SDK는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge 네트워크를 통해 [!DNL Experience Cloud]의 다양한 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다. JavaScript 라이브러리 외에도 웹 SDK 구성에 도움이 되는 [Experience Platform Launch 확장](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)이 있습니다.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] 는 Experience Edge를 구성하는 컬렉션의 일부입니다. Experience Edge는 다음 3가지 기술로 구성됩니다.

* **[!DNL Adobe Experience Platform Web SDK]:** JavaScript SDK 및  [!DNL Experience Platform Launch] 익스텐션을 사용하여  [!DNL Adobe] 기술 배포 간소화
* **Adobe Experience Platform Mobile SDK:** 고객이 새로운 배포 방법을 사용할 수 있도록 v5 모바일 SDK 확장
* **[!DNL Adobe Experience Platform Edge Network]:** 새로운  [!DNL Adobe] 제품 배포 방법론을 가능하게 하는 글로벌 분산 서버 네트워크

[!DNL Adobe Experience Edge]은 액세스 가능한 모든 채널에서 대기 시간이 짧은 데이터 수집, 플러그형 컴퓨팅 및 신속한 데이터 활성화를 위한 새로운 프레임워크입니다.

[!DNL Adobe Experience Edge] 는 데이터를 공통 Adobe 도메인(`adobedc.net`)으로 보내고 데이터 및 경험 전달을 위해 단일 페이로드를 받는 모든 채널(JavaScript, Mobile, Server-side)에 대해 단일 통합 SDK를 제공합니다.

통합된 Edge Gateway와 공통 플랫폼 서비스 프레임워크를 사용하면 서버측에서 이 실시간 컴퓨팅 환경에 새로운 기능을 쉽게 플러그-인하고 배포할 수 있습니다.  이 아키텍처는

* 가치 창출 시간 단축
* &quot;지점&quot; 통합에 대한 필요성 종료
* 이전 라이브러리에 비해 성능이 개선되었습니다.
* 비용 절감
* 혁신 속도 향상
* Adobe 고객에게 지속적인 경쟁 우위 창출

하나의 통합 에지 시스템을 통해 모든 채널에서 광고, 마케팅 또는 개인화 캠페인을 통합 경험으로 관리할 수 있습니다.  이를 통해 [!DNL Adobe]은(는) 고객에게 TCO가 낮은 서비스를 제공할 수 있습니다.  또한 실시간 에지 플러깅을 수행하고 [!DNL Adobe] 및 고객이 새로운 기능과 고객 정의 로직을 해당 실시간 시스템에 보다 신속하게 추가할 수 있도록 함으로써 제품 혁신 속도를 높이는 데 도움이 됩니다.

## 비디오 개요

다음 비디오는 Adobe Experience Platform [!DNL Web SDK] 및 Adobe Experience Platform [!DNL Edge Network]에 대한 개요를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Adobe Experience Platform 웹 SDK로 대체된 SDK

Adobe Experience Platform 웹 SDK는 다음 SDK를 대체합니다.

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

기존 라이브러리 주위에 있는 래퍼만 있는 것은 아닙니다. 그것은 완전히 다시 쓴 것이다. 이 솔루션의 목적은 태그가 올바른 순서로 실행되어야 하는 문제, 라이브러리 버전 관리 문제와 불일치, 향상된 종속성 관리 등을 해소하는 것입니다. 이것은 [!DNL Experience Cloud]을 구현하는 새로운 방법이며 [오픈 소스](https://github.com/adobe/alloy)입니다.

새 라이브러리 외에도 Adobe 솔루션에 대한 HTTP 요청을 간소화하는 새로운 종점이 있습니다. 이전에 Visitor.js는 방문자 ID 서비스로 차단 호출을 전송한 다음 AT.js는 Adobe Target에 대한 호출을 전송하고, DIL.js는 Adobe Audience Manager에 대한 호출을 전송했으며, 마지막으로 AppMeasurement.js는 Adobe Analytics에 대한 호출을 전송했습니다. 이 새 라이브러리와 종단점은 ID를 검색하고, [!DNL Target] 경험을 가져오고, 데이터를 [!DNL Audience Manager]에 보내고, 데이터를 한 번의 호출로 Adobe Experience Platform에 전달할 수 있습니다.

다음 비디오에서는 Adobe Experience Platform [!DNL Web SDK] 및 Adobe Experience Platform [!DNL Edge Network]의 실제 동작을 보여 줍니다. 비디오 예제에서는 데이터를 [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] 및 [!DNL Target]으로 보내는 Adobe에 대한 단일 호출을 사용합니다.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

이 제품은 점점 더 많은 활용 사례를 지원하기 위해 끊임없이 진화하고 증가하고 있습니다. 최신 정보를 얻으려면 [지원되는 사용 사례 보드](https://github.com/adobe/alloy/projects/5)를 확인하십시오. Adobe는 귀하가 최상의 결정을 내릴 수 있도록 Adobe가 현재 지원하는 사용 사례와 Adobe가 협력하고 있는 사례에 대해 이러한 최신 정보를 유지합니다.

* **아직 지원되지 않는 사용** 사례: 향후 지원을 받을 수 있도록 로드맵에 있는 사용 사례입니다.
* **진행 중인 사용 사례:** 팀이 현재 릴리스를 위해 완료하고 있는 사용 사례입니다.
* **지원되는 사용 사례:** 현재 지원되고 작동하는 사용 사례입니다.
* **Adobe가 지원하지 않을 사용 사례:** 이러한 경우는 지원하지 않기로 결정한 사용 사례입니다.
