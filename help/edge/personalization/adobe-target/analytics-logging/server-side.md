---
title: Platform Web SDK의 A4T 데이터에 대한 서버 측 로깅
description: Experience Platform Web SDK를 사용하여 A4T(Adobe Analytics for Target)에 대한 서버측 로깅을 활성화하는 방법을 알아봅니다.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;웹;sdk;플랫폼;로깅;
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Platform Web SDK의 A4T 데이터에 대한 서버 측 로깅

Adobe Experience Platform Web SDK를 사용하면 Platform Edge 네트워크에서 Adobe Analytics for A4T(Target) 기능을 구현할 수 있습니다. 서버측 로깅이 활성화되면 히트 결합 프로세스를 수행하지 않고도 Edge 네트워크를 통해 전송된 모든 Analytics 히트가 서버 측의 Target 세부 사항으로 강화됩니다.

Analytics가 데이터 스트림 구성에서 활성화되면 Analytics에 대한 서버 측 로깅이 활성화됩니다.

![Analytics 데이터 스트림 구성이 활성화됨](../assets/enable-analytics-datastream.png)

다음 다이어그램은 서버측 Analytics 로깅이 활성화될 때 데이터를 시스템을 통해 이동하는 방법을 보여줍니다.

![서버 측 로깅 흐름](../assets/analytics-server-side-logging.png)

## 다음 단계

이 안내서에서는 웹 SDK의 A4T 데이터에 대한 서버 측 로깅을 다룹니다. 다음 안내서를 참조하십시오. [클라이언트 측 로깅](./client-side.md) 를 참조하십시오.
