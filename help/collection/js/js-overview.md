---
title: JavaScript 개요
description: JavaScript을 사용하여 Adobe Experience Platform Edge Network에 데이터를 전송합니다.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# JavaScript 개요

**Adobe Experience Platform Web SDK**&#x200B;은(는) Adobe Experience Platform Edge Network으로 데이터를 보낼 수 있는 클라이언트측 JavaScript 라이브러리입니다.

웹 SDK은 솔루션과 관계없는 방식(XDM)으로 데이터를 Experience Platform Edge Network으로 보낸 다음, 해당 데이터를 솔루션별 형식 및 대상에 매핑하여 실시간으로 전송합니다.

다음 두 가지 방법으로 웹 SDK을 구현할 수 있습니다.

* [JavaScript 라이브러리](install/library.md)를 사용한 수동 구현(이 설명서)
* [웹 SDK 태그 확장](/help/tags/extensions/client/web-sdk/overview.md)

이 안내서에는 웹 SDK JavaScript 라이브러리를 사용하여 Experience Cloud 솔루션과 상호 작용하기 위한 지침이 포함되어 있습니다.

## Experience Platform Edge Network {#edge-network}

Adobe Experience Platform Edge Network은 모든 지정 가능한 채널에서 지연 시간이 짧은 데이터 수집, 플러그형 컴퓨팅 및 신속한 데이터 활성화를 제공합니다. 웹, 모바일 및 서버측 채널을 위한 단일 통합 SDK을 제공하여 데이터를 공통 Adobe 도메인(`adobedc.net`)으로 전송하고 데이터 및 경험 전달을 위한 단일 페이로드를 받습니다.

서버측에서 통합 에지 게이트웨이 및 공통 플랫폼 서비스 프레임워크는 다음과 같은 이점을 제공하면서 새로운 기능의 배포를 단순화합니다.

* 고객 가치 창출 시간 단축
* &quot;포인트&quot; 통합의 필요성 종결
* 구립 도서관에 비해 성능 향상
* 운영 비용 감소
* 혁신 속도 향상
* Adobe 고객을 위한 지속적인 경쟁 우위 확보

통합 에지 시스템을 사용하면 모든 채널에서 광고, 마케팅 및 개인화 캠페인을 관리할 수 있습니다. 총 소유 비용을 줄이고 다양한 데이터 유형을 지원하므로 여러 Experience Cloud 제품에 사용할 데이터 모델을 매핑할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/37266?captions=kor&quality=12&learn=on)

## 라이브러리가 웹 SDK으로 대체됨 {#sdks}

웹 SDK은 기존 라이브러리의 기능을 통합하기 위해 처음부터 빌드된 오픈 소스 라이브러리입니다. 태그 실행 순서, 버전 불일치 및 종속성 관리 문제를 해결하여 많은 Experience Cloud 제품을 구현하는 방법을 제공합니다. 웹 SDK은 다음 서비스에 대한 데이터 수집을 대체합니다.

* Adobe Experience Platform 방문자 ID 서비스(`Visitor.js`)
* Adobe Analytics(`AppMeasurement.js`)
* Adobe Target(`AT.js`)
* Adobe Audience Manager(`DIL.js`)
* Adobe 미디어 분석
* Adobe Advertising

또한 Adobe 솔루션에 대한 HTTP 요청을 간소화하는 새 엔드포인트를 도입했습니다. 이전에는 각 데이터 수집 라이브러리에 대해 여러 호출이 필요했습니다. 이제 한 번의 호출로 ID를 검색하고 [!DNL Target] 경험을 가져와 데이터를 [!DNL Audience Manager]에 보내고 데이터를 Adobe Experience Platform에 전달할 수 있습니다.

## 기존 라이브러리에서 Web SDK으로 마이그레이션 {#migrating-to-web-sdk}

Adobe은 기존 라이브러리에서 웹 SDK으로의 마이그레이션을 단순화하는 능률적인 업그레이드 경로를 제공합니다. 한 번에 전체 사이트를 마이그레이션할 필요 없이 웹 사이트의 각 페이지를 개별적으로 마이그레이션할 수 있습니다. 기존 라이브러리가 다른 페이지에 남아 있는 동안 일부 페이지에서 웹 SDK을 사용하여 점진적으로 전환할 수 있습니다.
