---
keywords: Experience Platform;홈;인기 항목;데이터 수집;실행;웹 sdk
solution: Experience Platform
title: 데이터 수집 개요
topic-legacy: overview
description: Adobe Experience Platform의 고객 경험에 대한 데이터 수집과 관련된 다양한 기술에 대해 알아봅니다.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 2%

---

# 데이터 수집 개요

Adobe Experience Platform은 클라이언트측 소스에서 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 몇 초 내에 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

데이터 수집은 다음 클라이언트측 소스에 대해 지원됩니다.

* 웹 기반 애플리케이션
* 기본 모바일 애플리케이션
* OTT(Over-the-top) 애플리케이션

Experience Platform이 제공하는 데이터 수집 기술은 수집된 데이터 세트의 검색 기능 및 액세스 가능성에 중점을 둡니다. 이러한 기술은 다음과 같습니다.

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [태그](../tags/home.md)
* [이벤트 전달](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform 웹 SDK](../edge/home.md)
* [XDM(경험 데이터 모델)](../xdm/home.md)

![](./images/Collection.png)

## 구현이 간단하여 클라이언트측 성능이 향상됩니다.

Adobe Experience Platform Web 및 Mobile SDK는 모든 Adobe 제품 라이브러리를 웹 또는 모바일 플랫폼용 단일 개발 키트로 축소하고 압축합니다. 이러한 라이브러리를 압축하면 데이터 수집이 빨라지고 작업을 클라이언트 측 장치에서 Adobe Experience Platform Edge Network로 단일 스트림으로 통합할 수 있습니다.

## Adobe 기술을 배포하기 위한 스위치 프로세스 전환

Platform Edge Network는 광범위한 규모로 데이터를 수신하고 처리할 수 있는 전 세계적으로 분산된 빠르고 안정적인 서버 네트워크입니다. 태그를 사용하여 Adobe Target, Adobe Audience Manager 및 Adobe Analytics과 같은 제품에 대해 [데이터 세트](../edge/fundamentals/datastreams.md)를 설정할 수 있습니다. 이 경우 클라이언트측 코드를 변경하지 않고 서버 측에서 이러한 제품을 활성화할 수 있습니다.

![](./images/deploy.png)

## 데이터를 빠르고 안전하게 변환, 품질 향상 및 전송

[Adobe Experience Platform의 이벤트 전달](../tags/ui/event-forwarding/overview.md) 은 모든 플랫폼 데이터 스트림에 탭할 수 있습니다. 보다 빠르고 안전한 데이터 수집 및 배포를 제공하는 클라이언트 장치에 타사 코드를 추가하지 않고도 매우 짧은 지연 시간으로 Adobe이 아닌 대상에 데이터를 변환, 보강 및 전송할 수 있습니다.

![](./images/launch.png)
