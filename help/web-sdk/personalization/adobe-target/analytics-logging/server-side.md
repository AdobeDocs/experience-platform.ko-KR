---
title: Experience Platform Web SDK의 A4T 데이터에 대한 서버측 로깅
description: Experience Platform Web SDK을 사용하여 Adobe Analytics for Target(A4T)에 대한 서버측 로깅을 활성화하는 방법을 알아봅니다.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;웹;sdk;플랫폼;로깅;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# Experience Platform Web SDK의 A4T 데이터에 대한 서버측 로깅

Adobe Experience Platform Web SDK을 사용하면 Experience Platform Edge Network에서 A4T(Adobe Analytics for Target) 기능을 구현할 수 있습니다. 서버측 로깅이 활성화되면 히트 결합 프로세스를 거치지 않고 Edge Network을 통해 전송된 모든 Analytics 히트가 서버측의 Target 세부 사항으로 강화됩니다.

Analytics에 대한 서버측 로깅은 데이터스트림 구성에서 Analytics가 활성화될 때 활성화됩니다.

![Analytics 데이터 스트림 구성 사용](../assets/enable-analytics-datastream.png)

다음 다이어그램은 서버측 분석 로깅이 활성화될 때 데이터가 시스템을 통해 이동하는 방식을 보여 줍니다.

![서버측 로깅 흐름](../assets/analytics-server-side-logging.png)

## 다음 단계

이 안내서에서는 웹 SDK의 A4T 데이터에 대한 서버측 로깅을 다룹니다. 클라이언트측에서 A4T 데이터를 처리하는 방법에 대한 자세한 내용은 [클라이언트측 로깅](./client-side.md)에 대한 안내서를 참조하십시오.
