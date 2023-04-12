---
keywords: Experience Platform;홈;인기 항목;데이터 수집;실행;웹 sdk
solution: Experience Platform
title: 데이터 수집 개요
description: Adobe Experience Platform의 고객 경험에 대한 데이터 수집과 관련된 다양한 기술에 대해 알아봅니다.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 13c02dd5930905e3851ff147c0ea4d914e3dc6c7
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 7%

---

# 데이터 수집 개요

Adobe Experience Platform은 클라이언트측 소스에서 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 몇 초 내에 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

데이터 수집은 다음 클라이언트측 소스에 대해 지원됩니다.

* 웹 기반 애플리케이션
* 기본 모바일 애플리케이션
* OTT(Over-the-top) 애플리케이션

데이터 수집은 다음을 포함하여 수집된 데이터 세트의 검색 기능 및 액세스 가능성에 중점을 둡니다.

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [태그](../tags/home.md)
* [데이터스트림](../edge/datastreams/overview.md)
* [이벤트 전달](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform 웹 SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [XDM(경험 데이터 모델)](../xdm/home.md)
* [Adobe Experience Platform ID 서비스](../identity-service/home.md)

이 안내서에서는 데이터 수집에 대한 높은 수준의 소개와 Platform Edge Network를 통해 Adobe Experience Cloud 제품 및 비Adobe 애플리케이션에 데이터를 전송하는 방법을 제공합니다.

## 태그, 웹 SDK 및 Mobile SDK

Platform Web SDK 및 Platform Mobile SDK는 모든 Adobe 제품 라이브러리를 웹 및 모바일 플랫폼용 단일 개발 키트로 각각 축소하고 압축합니다. 원시 코드를 사용하거나 [태그](../tags/home.md) 데이터 수집 UI 또는 Adobe Experience Platform UI 사용.

이러한 라이브러리를 압축하면 데이터 수집이 빨라지고 클라이언트 측 장치에서 Platform Edge 네트워크로 작업을 단일 스트림으로 통합할 수 있습니다.

![태그, 웹 SDK, Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge 네트워크 및 데이터 스트림 {#edge}

Platform Edge Network는 광범위한 규모로 데이터를 수신하고 처리할 수 있는 전 세계적으로 분산된 빠르고 안정적인 서버 네트워크입니다. 태그를 사용하여 다음을 설정할 수 있습니다 [데이터 세트](../edge/datastreams/overview.md) Adobe Target, Adobe Audience Manager, Adobe Analytics 등의 제품에 대해 클라이언트측 코드를 변경하지 않고 서버측에서 이러한 제품을 활성화할 수 있습니다.

또한 데이터 저장소는 전송하는 중요한 데이터가 조직 정책 및 법률 규정에 따라 적절하게 처리되도록 하는 몇 가지 플랫폼 기능과 통합됩니다. 의 섹션을 참조하십시오. [중요한 데이터 처리](../edge/datastreams/overview.md#sensitive) 자세한 내용은 데이터 스트림 설명서에서 를 참조하십시오.

![데이터 스트림 및 Adobe 솔루션](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Platform Edge 네트워크에 대한 높은 수준의 소개는 다음을 참조하십시오 [인터랙티브 제품 투어](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## 이벤트 전달

[이벤트 전달](../tags/ui/event-forwarding/overview.md) 은(는) 임의의 Experience Platform 데이터 스트림을 탭할 수 있으므로, 클라이언트 장치에 타사 코드를 추가하지 않고도 Adobe이 아닌 대상에 데이터를 변환, 보강 및 전송할 수 있습니다.

![이벤트 전달](./images/home/event-forwarding.png)

>[!NOTE]
>
>이벤트 전달은 Adobe Real-time Customer Data Platform 연결, Prime 또는 Ultimate 오퍼링의 일부로 포함된 유료 기능입니다.

## 다음 단계

이 문서에서는 수집된 고객 경험 데이터를 Adobe 제품 및 타사 대상으로 보내는 프로세스를 자동화하는 데이터 수집 작동 방식에 대한 높은 수준의 개요를 제공합니다.

![데이터 수집 프레임워크](./images/home/collection.png)

Edge 네트워크를 통해 이벤트 데이터를 전송하는 것과 관련된 일반 워크플로우에 대한 자세한 내용은 [종단 간 개요](./e2e.md).
