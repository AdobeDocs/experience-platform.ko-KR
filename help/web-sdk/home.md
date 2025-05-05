---
title: Adobe Experience Platform 웹 소프트웨어 개발 키트(SDK) 개요
description: Adobe Experience Platform Web SDK을 사용하여 Experience Platform 기능을 웹 사이트에 통합하는 방법에 대해 알아봅니다.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Adobe Experience Platform 웹 SDK {#overview}

Adobe Experience Platform Web SDK은 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network을 통해 해당 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다.

다음 두 가지 방법으로 웹 SDK을 구현할 수 있습니다.

* [웹 SDK 태그 확장](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)입니다. 자세한 내용은 [Web SDK에서 Adobe Experience Cloud을 구현](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR)하는 방법에 대한 자습서를 참조하십시오.
* [웹 SDK JavaScript 라이브러리](install/library.md)를 사용한 수동 구현입니다.

이 안내서에는 웹 SDK JavaScript 라이브러리와 태그 확장을 모두 사용하여 Experience Cloud 솔루션과 상호 작용하기 위한 지침이 포함되어 있습니다.

## Experience Platform Edge Network {#edge-network}



Experience Platform 웹 SDK은 Adobe Experience Platform Edge Network의 일부이며 다음을 포함합니다.

* **[Experience Platform Web SDK](#overview)**: Adobe 기술 배포를 단순화하기 위한 JavaScript 라이브러리 및 태그 확장입니다.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)**: 새로운 배포 방법에 대한 v5 Mobile SDK의 확장입니다.
* **[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)**: 데이터 수집, 개인화, 광고 및 마케팅 사용 사례를 위한 서버측 API입니다. 서버, IoT 디바이스, 셋톱 박스 및 기타 디바이스에서 사용할 수 있습니다.

Edge Network은 모든 지정 가능한 채널에서 지연 시간이 짧은 데이터 수집, 플러그형 컴퓨팅 및 신속한 데이터 활성화를 제공합니다. 웹, 모바일 및 서버측 채널을 위한 단일 통합 SDK을 제공하여 데이터를 공통 Adobe 도메인(`adobedc.net`)으로 전송하고 데이터 및 경험 전달을 위한 단일 페이로드를 받습니다.

서버측에서 통합 에지 게이트웨이 및 공통 플랫폼 서비스 프레임워크는 다음과 같은 이점을 제공하면서 새로운 기능의 배포를 단순화합니다.

* 고객 가치 창출 시간 단축
* &quot;포인트&quot; 통합의 필요성 종결
* 구립 도서관에 비해 성능 향상
* 운영 비용 감소
* 혁신 속도 향상
* Adobe 고객을 위한 지속적인 경쟁 우위 확보

통합 에지 시스템을 사용하면 모든 채널에서 광고, 마케팅 및 개인화 캠페인을 관리할 수 있습니다. 총 소유 비용을 줄이고 다양한 데이터 유형을 지원하므로 여러 Experience Cloud 제품에 사용할 데이터 모델을 매핑할 수 있습니다.

## 비디오 개요 {#video}

Adobe Experience Platform [!DNL Web SDK] 및 [!DNL Edge Network]에 대한 개요를 보려면 아래 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 라이브러리가 웹 SDK으로 대체됨 {#sdks}

웹 SDK은 기존 라이브러리의 기능을 통합하기 위해 처음부터 빌드된 새로운 오픈 소스 라이브러리입니다. 태그 실행 순서, 버전 불일치 및 종속성 관리 문제를 해결하여 [!DNL Experience Cloud]을(를) 구현하는 새로운 [오픈 소스](https://github.com/adobe/alloy) 방법을 제공합니다.

웹 SDK은 다음을 대체합니다.

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

또한 Adobe 솔루션에 대한 HTTP 요청을 간소화하는 새 엔드포인트를 도입했습니다. 이전에는 `Visitor.js`, `AT.js`, `DIL.js` 및 `AppMeasurement.js`에 대해 여러 호출이 필요했습니다. 이제 한 번의 호출로 ID를 검색하고 [!DNL Target] 경험을 가져와 데이터를 [!DNL Audience Manager]에 보내고 데이터를 Adobe Experience Platform에 전달할 수 있습니다.

한 번의 호출로 [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] 및 [!DNL Target]&#x200B;(으)로 데이터를 전송하여 아래 비디오를 통해 Adobe Experience Platform [!DNL Web SDK] 및 [!DNL Edge Network]의 작동 방식을 확인하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 기존 라이브러리에서 Web SDK으로 마이그레이션 {#migrating-to-web-sdk}

Adobe은 [기존 라이브러리](#sdks)에서 Web SDK으로 마이그레이션하는 작업을 간소화하는 능률적인 업그레이드 경로를 제공합니다. 한 번에 전체 사이트를 마이그레이션할 필요 없이 웹 사이트의 각 페이지를 개별적으로 마이그레이션할 수 있습니다. 기존 라이브러리가 다른 페이지에 남아 있는 동안 일부 페이지에서 웹 SDK을 사용하여 점진적으로 전환할 수 있습니다.

### `AT.js`을(를) 웹 SDK으로 마이그레이션 고려 사항 {#considerations}

`AT.js`을(를) 사용하여 Web SDK으로 페이지를 마이그레이션하기 전에 다음 Web SDK 구성 옵션을 활성화하여 페이지 간 탐색 시 방문자 프로필이 유지되도록 하십시오.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&#39;targetMigrationEnabled&#39;](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>다음 Target 기능은 `at.js`에서 Web SDK으로 마이그레이션할 때 지원되지 않습니다.
>
>* [오퍼 리디렉션](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=ko)
>* [CNAME 및 도메인 간 지원](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html?lang=ko)

`AT.js`에서 웹 SDK으로 마이그레이션한 후 구성에서 `targetMigrationEnabled` 옵션을 제거하십시오.
