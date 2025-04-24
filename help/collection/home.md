---
keywords: Experience Platform;홈;인기 항목;데이터 수집;launch;웹 sdk
solution: Experience Platform
title: 데이터 수집 개요
description: Adobe Experience Platform에서 고객 경험에 대한 데이터를 수집하는 것과 관련된 다양한 기술에 대해 알아봅니다.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---

# 데이터 수집 개요

Adobe Experience Platform은 클라이언트측 소스에서 고객 경험 데이터를 수집하고 이를 Adobe Experience Platform Edge Network으로 전송하여 몇 초 만에 보강 및 변형하고 Adobe 또는 Adobe이 아닌 대상으로 배포할 수 있는 기술 제품군을 제공합니다.

데이터 수집은 다음 클라이언트측 소스에 대해 지원됩니다.

* 웹 기반 애플리케이션
* 기본 모바일 애플리케이션
* OTT(Over-the-Top) 애플리케이션

데이터 수집은 다음을 포함하여 수집된 데이터 세트의 검색 가능성과 액세스 가능성에 중점을 둡니다.

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [태그](../tags/home.md)
* [데이터스트림](../datastreams/overview.md)
* [이벤트 전달](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform 웹 SDK](../web-sdk/home.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


이 안내서에서는 데이터 수집에 대한 높은 수준의 소개와 Experience Platform Edge Network을 통해 Adobe Experience Cloud 제품 및 Adobe이 아닌 애플리케이션으로 데이터를 전송하는 작동 방법을 제공합니다.

## 태그, Web SDK 및 Mobile SDK

Experience Platform Web SDK 및 Experience Platform Mobile SDK은 모든 Adobe 제품 라이브러리를 웹 및 모바일 플랫폼용 단일 개발 키트로 각각 축소 및 압축합니다. 원시 코드를 사용하거나 데이터 수집 UI 또는 Adobe Experience Platform UI를 통해 [태그](../tags/home.md)를 사용하여 구현할 수 있습니다.

이러한 라이브러리를 압축하면 데이터 수집 속도가 빨라지고 클라이언트측 디바이스에서 Experience Platform Edge Network으로 단일 스트림으로 작업을 통합합니다.

![태그, 웹 SDK, 모바일 SDK](./images/home/tags-sdks.png)

## Experience Platform Edge Network 및 데이터스트림 {#edge}

Experience Platform Edge Network은 엄청난 규모로 데이터를 수신하고 처리할 수 있는 전 세계에 분포하고 빠르고 안정적인 서버 네트워크입니다. 태그를 사용하면 Adobe Target, Adobe Audience Manager 및 Adobe Analytics과 같은 제품에 대해 [데이터스트림](../datastreams/overview.md)을 설정할 수 있으며, 이를 통해 클라이언트측 코드를 변경하지 않고 서버측에서 이러한 제품을 활성화할 수 있습니다.

또한 데이터 스트림은 여러 Experience Platform 기능과 통합되어 전송 중인 모든 중요한 데이터가 조직 정책 및 법적 규정과 관련하여 적절하게 처리되도록 합니다. 자세한 내용은 데이터스트림 설명서에서 [중요한 데이터 처리](../datastreams/overview.md#sensitive)에 대한 섹션을 참조하십시오.

![데이터스트림 및 Adobe 솔루션](./images/home/adobe-solutions.png)

## 이벤트 전달

[이벤트 전달](../tags/ui/event-forwarding/overview.md)을(를) 통해 모든 Experience Platform 데이터 스트림을 이용할 수 있으므로 클라이언트 장치에 타사 코드를 추가하지 않고 매우 짧은 대기 시간으로 Adobe이 아닌 대상으로 데이터를 변환, 강화 및 전송할 수 있습니다.

![이벤트 전달](./images/home/event-forwarding.png)

>[!NOTE]
>
>이벤트 전달은 Adobe Real-Time Customer Data Platform 연결, Prime 또는 Ultimate 오퍼링의 일부로 포함된 유료 기능입니다.

## 다음 단계

이 문서에서는 데이터 수집이 작동하여 수집된 고객 경험 데이터를 Adobe 제품 및 타사 대상으로 전송하는 프로세스를 자동화하는 방법에 대한 높은 수준의 개요를 제공합니다.

![데이터 수집 프레임워크](./images/home/collection.png)

Edge Network을 통해 이벤트 데이터를 보내는 것과 관련된 일반 워크플로에 대한 자세한 내용은 [전체 개요](./e2e.md)를 참조하십시오.
