---
title: Platform Web SDK의 A4T 데이터에 대한 서버측 로깅
description: Experience Platform Web SDK를 사용하여 Adobe Analytics for Target(A4T)에 대해 서버측 로깅을 활성화하는 방법을 알아봅니다.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;웹;sdk;플랫폼;로깅;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 1%

---

# Platform Web SDK의 A4T 데이터에 대한 서버측 로깅

Adobe Experience Platform Web SDK 를 사용하면 플랫폼 Edge Network에서 A4T(Adobe Analytics for Target) 기능을 구현할 수 있습니다. 서버측 로깅이 활성화되면 Edge Network을 통해 전송된 모든 Analytics 히트는 히트 결합 프로세스를 거치지 않고 서버측의 Target 세부 사항으로 보강됩니다.

Analytics에 대한 서버측 로깅은 데이터스트림 구성에서 Analytics가 활성화될 때 활성화됩니다.

![Analytics 데이터 스트림 구성 사용](../assets/enable-analytics-datastream.png)

다음 다이어그램은 서버측 분석 로깅이 활성화될 때 데이터가 시스템을 통해 이동하는 방식을 보여 줍니다.

![서버측 로깅 흐름](../assets/analytics-server-side-logging.png)

## 다음 단계

이 안내서에서는 Web SDK의 A4T 데이터에 대한 서버측 로깅을 다룹니다. 클라이언트측에서 A4T 데이터를 처리하는 방법에 대한 자세한 내용은 [클라이언트측 로깅](./client-side.md)에 대한 안내서를 참조하십시오.
