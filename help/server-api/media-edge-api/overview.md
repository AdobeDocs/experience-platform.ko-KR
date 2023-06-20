---
solution: Experience Platform
title: Media Edge API
description: Media Edge API 개요
source-git-commit: ff4bc64843e3d05277f56ab67b60400fb9e65c4f
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 5%

---


# Media Edge API 개요

Media Edge API는 의 프레임워크 내에서 미디어 이벤트 추적 데이터를 제공하기 위해 Adobe Experience Platform에 구축됩니다. [XDM 스키마](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Media Analytics 고객의 경우 다음과 같은 기능을 사용할 수 있습니다.

* 포함 [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=ko), 고객은 지속 시간, 시작 및 중지에 대한 세부 정보를 거의 실시간으로 가져와 미디어 지표를 평가하고 결합할 수 있습니다. Adobe Analytics에서 마이그레이션하는 고객은 Adobe Customer Journey Analytics에서 모든 보고 지표를 사용할 수 있습니다.

* 포함 [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=ko), 고객은 미디어 사용량 데이터로 실시간 프로필을 보강할 수 있습니다.

* 포함 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en), 고객은 옴니채널 캠페인을 최적화하고 미디어 소비 신호로 여정을 자동화할 수 있습니다.


## 미디어 추적 데이터 흐름 최적화

모두 [Media Collection API](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) 및 Media Edge API는 미디어 추적 데이터를 RESTful 서비스로 제공합니다. 그러나 Media Edge 서비스를 사용하면 다음과 같은 이점이 있습니다.

* XDM 스키마를 데이터 흐름에 통합하는 가장 쉬운 방법입니다.

* 호출은 미디어 플레이어에서 [Experience Edge 플랫폼 네트워크](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* 최소한의 서버 간 호출로 미디어 이벤트를 효율적으로 추적합니다.

다음 표는 다양한 미디어 분석 사례에 대해 가능한 Adobe API 서비스를 보여 줍니다.

| 사용 사례 | API 서비스 |
| -------- | ----------- |
| Adobe Experience Platform 솔루션 | Media Edge |
| Real-Time CDP + Customer Journey Analytics | Media Edge |
| Adobe Analytics + Adobe Experience Platform 솔루션 | Media Edge |
| Adobe Analytics만(이미 추적) | 미디어 컬렉션 |

>[!NOTE]
>
> Analytics용 Media Collection API 서비스는 여전히 XDM 데이터를 수신하지만, Media Edge 서비스가 있는 범위 내에서는 최적화되지 않습니다. Media Player에서 전송한 데이터에 따라 일부 Analytics 전용 데이터도 Media Edge API 서비스를 통해 라우팅될 수 있습니다.

다음 그래픽은 두 API 서비스에 대한 데이터 흐름을 보여 줍니다.

![Media analytics 데이터 흐름](../assets/edge-api-dataflow.png)

## 다음 단계

* Media Edge API 사용에 대한 자세한 내용은 [시작 설명서](getting-started.md).

* Platform Edge 작업에 대한 자세한 내용은 [Experience Platform 에지로 Media Analytics 설치](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).




