---
keywords: Experience Platform;홈;인기 항목;데이터 수집;시작;웹 sdk
solution: Experience Platform
title: 데이터 수집 개요
topic-legacy: overview
description: Adobe Experience Platform에서 고객 경험에 대한 데이터를 수집하는 것과 관련된 다양한 기술에 대해 알아봅니다.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: a150c23dffde9431953a019509e9554159052d21
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 3%

---

# 데이터 수집 개요

Adobe Experience Platform은 고객 경험 데이터를 클라이언트측 소스에서 수집한 다음 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 몇 초 안에 농축하고 변환하여 배포할 수 있는 일련의 기술을 제공합니다.

데이터 수집은 다음 클라이언트측 소스에 대해 지원됩니다.

* 웹 기반 애플리케이션
* 기본 모바일 애플리케이션
* 오버더톱(OTT) 애플리케이션

Experience Platform에서 제공하는 데이터 수집 기술은 인제스트된 데이터 세트의 검색 기능과 액세스 가능성에 중점을 둡니다. 이러한 기술에는 다음이 포함됩니다.

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Adobe Experience Platform Launch](https://adobe.com/go/launch_help_en)
* [Adobe Experience Platform 웹 SDK](../edge/home.md)
* [경험 데이터 모델(XDM)](../xdm/home.md)

![](./images/Collection.png)

## 보다 간단한 구현, 더욱 빨라진 클라이언트측 성능

Adobe Experience Platform 웹 및 모바일 SDK가 축소되어 모든 Adobe 제품 라이브러리를 웹 또는 모바일 플랫폼을 위한 단일 개발 키트로 압축합니다. 이러한 라이브러리를 압축하면 데이터 수집 속도가 빨라지고 작업을 클라이언트측 디바이스에서 Adobe Experience Platform Edge Network로의 단일 스트림으로 통합할 수 있습니다.

## 전환 프로세스를 통한 Adobe 기술 배포

Platform Edge Network는 광범위한 규모로 데이터를 수신하고 처리할 수 있는 전 세계적으로 배포되고 빠르고 안정적인 서버 네트워크로, platform launch을 사용하면 클라이언트측 코드를 변경하지 않고 서버측에서 이러한 제품을 활성화할 수 있도록 Adobe Target, Adobe Audience Manager 및 Adobe Analytics과 같은 제품에 대해 [edge 구성](../edge/fundamentals/datastreams.md)을 설정할 수 있습니다.

![](./images/deploy.png)

## 신속하고 안전하게 데이터 변환, 강화 및 전송

[Adobe Experience Platform Launch Server ](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html) Sidecan은 모든 플랫폼 데이터 스트림을 탭합니다. 더욱 빠르고 안전한 데이터 수집 및 배포를 제공하는 클라이언트 장치에 제3자 코드를 추가하지 않고도 매우 짧은 지연을 통해 Adobe이 아닌 대상에 데이터를 변환, 장식 및 보낼 수 있습니다.

![](./images/launch.png)
