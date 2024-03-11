---
title: Adobe Experience Platform 웹 소프트웨어 개발 키트(SDK) 개요
description: Adobe Experience Platform Web SDK를 사용하여 Platform 기능을 웹 사이트에 통합하는 방법에 대해 알아봅니다.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---


# Adobe Experience Platform 웹 SDK {#overview}

>[!IMPORTANT]
>
>2024년 4월 말에 Adobe Experience Platform Web SDK는 모든 버전의 Internet Explorer에 대한 지원을 제거할 예정입니다.

Adobe Experience Platform 웹 SDK(소프트웨어 개발 키트)는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network를 통해 해당 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다.

Adobe은 웹 SDK를 구현하는 두 가지 방법을 제공합니다.

* 다음 [Web SDK 태그 확장](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 다음 방법에 대한 튜토리얼 보기 [웹 SDK를 사용하여 Adobe Experience Cloud 구현](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR) 추가 정보.
* 웹 SDK JavaScript 라이브러리를 사용한 수동 구현입니다.

이 사용 안내서에는 해당되는 경우 웹 SDK JavaScript 라이브러리와 태그 확장 모두를 통해 Experience Cloud 솔루션과 상호 작용하는 방법에 대한 지침이 포함되어 있습니다.

## Experience Platform 에지 네트워크 {#edge-network}

Experience Platform 웹 SDK는 Adobe Experience Platform Edge Network를 구성하는 도구 모음의 일부입니다.

Edge Network는 다음 구성 요소로 구성됩니다.

* **[Experience Platform Web SDK](#overview):** Adobe 기술 배포를 단순화하는 데 도움이 되는 JavaScript 라이브러리 및 태그 확장입니다.
* **[Experience Platform 모바일 SDK](https://developer.adobe.com/client-sdks/home/):** 새로운 배포 방법을 사용할 수 있는 v5 모바일 SDK에 대한 확장입니다.
* **[Edge Network Server API](../server-api/overview.md):** 다양한 데이터 수집, 개인화, 광고 및 마케팅 사용 사례에 사용할 수 있는 서버측 API입니다. 서버 API는 서버, IoT 디바이스, 셋톱 박스 및 기타 다양한 디바이스에서 사용할 수 있습니다.

에지 네트워크는 지연 시간이 짧은 데이터 수집, 플러그형 컴퓨팅 및 모든 지정 가능 채널에서 신속한 데이터 활성화를 위한 프레임워크입니다. 모든 채널(웹, 모바일, 서버측)에 대해 단일 통합 SDK를 제공하여 공통 Adobe 도메인(`adobedc.net`) 및 는 데이터 및 경험 전달을 위한 단일 페이로드를 다시 받습니다.

서버측에서는 통합 에지 게이트웨이와 공통 플랫폼 서비스 프레임워크를 통해 새로운 기능을 이러한 실시간 컴퓨팅 환경에 손쉽게 배포할 수 있습니다. 이 아키텍처는

* 고객 가치 창출 시간 단축
* &quot;포인트&quot; 통합의 필요성 종료
* 이전 라이브러리에 비해 성능이 향상되었습니다.
* 비용 절감
* 혁신의 속도 향상
* Adobe 고객을 위한 지속적인 경쟁 우위 확보

통합된 단일 에지 시스템을 통해 모든 채널의 광고, 마케팅 또는 개인화 캠페인을 통합 경험으로 관리할 수 있습니다. 또한 Adobe은 TCO를 절감하는 서비스를 제공할 수 있습니다. 에지 시스템은 대부분의 데이터 유형을 수용하도록 설계되어 있으므로 여러 Experience Cloud 제품에서 수집할 자체 데이터 모델을 매핑할 수 있습니다.

## 비디오 개요 {#video}

Adobe Experience Platform에 대한 개요는 아래 비디오를 참조하십시오 [!DNL Web SDK] 및 [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 라이브러리가 웹 SDK로 대체됨 {#sdks}

Web SDK는 기존 라이브러리에 대한 래퍼일 뿐만 아니라, 기존 라이브러리의 기능을 통합하기 위해 처음부터 새로 작성된 라이브러리입니다. 그 목적은 올바른 순서로 태그를 실행해야 하는 문제, 라이브러리 버전 관리 문제와의 불일치 및 더 나은 종속성 관리 문제를 해결하는 것입니다. 를 구현하는 새로운 방법입니다 [!DNL Experience Cloud] and it is [오픈 소스](https://github.com/adobe/alloy).

Web SDK는 다음 SDK를 대체합니다.

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

새 라이브러리 외에도 Adobe 솔루션에 대한 HTTP 요청을 간소화하는 새 엔드포인트가 있습니다. 이전, `Visitor.js` 방문자 ID 서비스에 차단 호출을 보낸 다음 `AT.js` 이(가) Adobe Target에 호출을 보냈습니다. `DIL.js` Adobe Audience Manager으로 호출을 보내고 `AppMeasurement.js` 이(가) Adobe Analytics에 호출을 보냈습니다. 이 새 라이브러리 및 끝점은 ID를 검색하고 [!DNL Target] 경험, 데이터 보내기 [!DNL Audience Manager]한 번의 호출로 Adobe Experience Platform에 데이터를 전달합니다.

다음 비디오에서는 Adobe Experience Platform을 보여 줍니다 [!DNL Web SDK] 및 Adobe Experience Platform [!DNL Edge Network] 작동 중입니다. 이 비디오 예제에서는 데이터를 로 전송하는 Adobe에 대한 단일 호출을 사용합니다 [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], 및 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 기존 라이브러리에서 Web SDK로 마이그레이션 {#migrating-to-web-sdk}

마이그레이션 간소화 [기존 라이브러리](#sdks) 웹 SDK에 대한 Adobe은 간소화된 업그레이드 경로를 제공합니다. 이 경로를 사용하면 전체 웹 사이트를 한 번에 마이그레이션할 필요 없이 웹 사이트의 각 개별 페이지를 Web SDK로 마이그레이션할 수 있습니다. 기존 라이브러리가 다른 페이지에 있는 동안 특정 페이지에서 웹 SDK를 사용할 수 있습니다. 준비가 되면 다른 페이지도 마이그레이션할 수 있습니다.

### 마이그레이션 `AT.js` Web SDK 고려 사항 {#considerations}

를 사용하는 페이지를 마이그레이션하기 전에 `AT.js` Web SDK에 대해 다음 Web SDK 구성 옵션을 활성화해야 합니다. 이러한 옵션을 사용하면 을 사용하여 페이지에서 탐색하는 동안 방문자 프로필이 유지됩니다. `AT.js` Web SDK를 사용하여 페이지를 만듭니다.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&#39;targetMigrationEnabled&#39;](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>다음 Target 기능은 at.js에서 Web SDK로 마이그레이션할 때 지원되지 않습니다.
>
>* [리디렉션 오퍼](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME 및 도메인 간 지원](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

에서 마이그레이션 후 `AT.js` Web SDK에서 `targetMigrationEnabled` 옵션입니다.
