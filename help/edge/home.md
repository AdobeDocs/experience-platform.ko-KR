---
title: Adobe Experience Platform 웹 SDK 개요
description: Adobe Experience Platform Web SDK를 사용하여 Platform 기능을 웹 사이트에 통합하는 방법에 대해 알아봅니다.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;Web SDK;SDK;Web SDK;Launch;Launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK 개요 {#overview}

Adobe Experience Platform Web SDK는 Adobe Experience Cloud 고객이 의 다양한 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다 [!DNL Experience Cloud] Adobe Experience Platform Edge Network를 통해 JavaScript 라이브러리 외에도 [태그 확장](./extension/web-sdk-extension-configuration.md) 웹 SDK 구성에 도움이 됩니다.

태그를 사용하여 웹 SDK를 설정하고 솔루션으로 데이터를 전송하는 방법에 대한 단계별 안내서는 다음을 참조하십시오. [Web SDK 튜토리얼을 사용하여 Adobe Experience Cloud 구현](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>이 제품은 점점 더 많은 사용 사례를 지원하기 위해 끊임없이 진화하고 발전하고 있습니다. 최신 정보를 계속 살펴보고 현재 지원되는 내용을 보려면 다음을 참조하십시오. [지원되는 사용 사례 페이지](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] 은(는) 다음을 구성하는 컬렉션의 일부입니다. [!DNL Adobe Experience Edge]. [!DNL Experience Edge] 다음 기술로 구성됩니다.

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** 배포를 크게 단순화하는 JavaScript SDK 및 태그 확장 [!DNL Adobe] 기술.
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** 고객이 새로운 배포 방법을 사용할 수 있도록 v5 모바일 SDK에 대한 확장
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** 새로운 배포 방식을 구현하는 글로벌 분산 서버 네트워크 [!DNL Adobe] products

다음 [!DNL Adobe Experience Edge] 는 모든 지정 가능한 채널에서 대기 시간이 짧은 데이터 수집, 플러그형 컴퓨팅 및 신속한 데이터 활성화를 위한 새로운 프레임워크입니다.

[!DNL Adobe Experience Edge] 는 데이터를 공통 Adobe 도메인( )으로 전송하는 모든 채널(JavaScript, 모바일, 서버측)에 대해 단일 통합 SDK를 제공합니다.`adobedc.net`) 및 는 데이터 및 경험 전달을 위한 단일 페이로드를 다시 받습니다.

서버측에서는 통합 에지 게이트웨이와 공통 플랫폼 서비스 프레임워크를 통해 손쉽게 플러그인하고 새로운 기능을 이러한 실시간 컴퓨팅 환경에 배포할 수 있습니다.  이 아키텍처는

* 고객 가치 창출 시간 단축
* &quot;포인트&quot; 통합의 필요성 종료
* 이전 라이브러리에 비해 성능이 향상되었습니다.
* 비용 절감
* 혁신의 속도 향상
* Adobe 고객을 위한 지속적인 경쟁 우위 확보

통합된 단일 에지 시스템을 통해 고객은 모든 채널에서 광고, 마케팅 또는 개인화 캠페인을 통합 경험으로 관리할 수 있습니다. 허용 [!DNL Adobe] 고객의 TCO를 절감하여 서비스를 제공할 수 있습니다.  또한 실시간 엣지 플러그를 가능하게 하고 허용함으로써 제품 혁신의 속도를 높이는 데 도움이 됩니다 [!DNL Adobe] 또한 고객은 이러한 실시간 시스템에 새로운 기능과 고객 정의 논리를 더욱 신속하게 추가할 수 있습니다.

## 비디오 개요 {#video}

다음 비디오는 Adobe Experience Platform에 대한 개요를 제공합니다 [!DNL Web SDK] 및 Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 라이브러리가 웹 SDK로 대체됨 {#sdks}

Web SDK는 기존 라이브러리에 대한 래퍼일 뿐만 아니라, 그것은 완전히 새로운 라이브러리이며, 기존 라이브러리의 기능을 통합하기 위해 처음부터 작성되었습니다. 그 목적은 올바른 순서로 태그를 실행해야 하는 문제, 라이브러리 버전 관리 문제와의 불일치 및 더 나은 종속성 관리 문제를 해결하는 것입니다. 를 구현하는 새로운 방법입니다 [!DNL Experience Cloud] and it is [오픈 소스](https://github.com/adobe/alloy).

Web SDK는 다음 SDK를 대체합니다.

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

새 라이브러리 외에도 Adobe 솔루션에 대한 HTTP 요청을 간소화하는 새 엔드포인트가 있습니다. 이전에는 Visitor.js가 방문자 ID 서비스에 차단 호출을 보낸 다음, AT.js가 Adobe TargetDIL 에 호출을 보내고, Visitor.js가 Adobe Audience Manager에 호출을 보내고, 마지막으로 AppMeasurement.js가 Adobe Analytics에 호출을 보냈습니다. 이 새 라이브러리 및 끝점은 ID를 검색하고 [!DNL Target] 경험, 데이터 보내기 [!DNL Audience Manager]한 번의 호출로 Adobe Experience Platform에 데이터를 전달합니다.

다음 비디오에서는 Adobe Experience Platform을 보여 줍니다 [!DNL Web SDK] 및 Adobe Experience Platform [!DNL Edge Network] 작동 중입니다. 이 비디오 예제에서는 데이터를 로 전송하는 Adobe에 대한 단일 호출을 사용합니다 [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], 및 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 기존 라이브러리에서 Web SDK로 마이그레이션 {#migrating-to-web-sdk}

마이그레이션 간소화 [기존 라이브러리](#sdks) 웹 SDK에 대한 Adobe은 전체 웹 사이트를 한 번에 마이그레이션할 필요 없이 웹 사이트의 각 개별 페이지를 웹 SDK로 마이그레이션할 수 있는 간소화된 업그레이드 경로를 제공합니다.

즉, 한 페이지에서 Web SDK를 사용하고 기존 라이브러리를 마이그레이션할 수 있을 때까지 다른 페이지에는 그대로 둘 수 있습니다.

### at.js에서 Web SDK로 마이그레이션 고려 사항 {#considerations}

를 사용하는 페이지를 마이그레이션하기 전에 [!DNL at.js] Web SDK에 대해 다음 Web SDK 구성 옵션을 활성화해야 합니다. 이렇게 하면 를 사용하여 페이지에서 이동하는 동안 방문자 프로필이 유지됩니다. [!DNL at.js ] Web SDK를 사용하여 페이지를 만듭니다.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&#39;targetMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>at.js에서 Web SDK로 마이그레이션할 때 다음 Target 기능은 지원되지 않습니다.
> * [리디렉션 오퍼](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [CNAME 및 도메인 간 지원](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


at.js에서 Web SDK로 마이그레이션한 후에는 `targetMigrationEnabled` 옵션입니다.



