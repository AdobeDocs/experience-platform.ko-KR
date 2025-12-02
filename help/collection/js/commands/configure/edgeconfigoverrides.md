---
title: edgeConfigOverrides
description: 구현에 대한 데이터 스트림 재정의를 구성합니다.
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides`(`configure` 명령)

`edgeConfigOverrides` 개체를 사용하면 현재 페이지에서 실행되는 명령에 대한 구성 설정을 재정의할 수 있습니다. 이 개체는 국가별로 다른 웹 사이트 또는 하위 도메인이 있거나 여러 비즈니스 단위에 맞는 데이터를 저장할 여러 개의 Experience Platform 샌드박스가 있는 경우에 유용합니다. 페이지의 단일 명령에 대해서만 구성 설정을 재정의하려면 [`edgeConfigOverrides` 명령`sendEvent`에서 ](../sendevent/edgeconfigoverrides.md) 개체를 사용하는 것이 좋습니다.

데이터 스트림 구성 재정의 프로세스는 다음 두 가지 주요 단계로 구성됩니다.

1. 먼저 데이터 스트림 UI에서 [데이터 스트림을 구성](/help/datastreams/configure.md)할 때 데이터 스트림 구성 재정의를 정의해야 합니다. 재정의를 구성하는 방법에 대한 지침은 데이터스트림 설명서에서 [데이터스트림 구성 재정의](/help/datastreams/overrides.md)를 참조하십시오.
1. 데이터 스트림 UI에서 데이터 스트림 재정의를 구성한 후 `edgeConfigOverrides` 개체를 구성할 수 있습니다.

`edgeConfigOverrides` 명령에서 `configure` 개체를 설정하면 Adobe으로 보낸 모든 데이터에 적용됩니다. 다음 명령 _also_&#x200B;은(는) `edgeConfigOverrides` 개체를 지원합니다.

* [`sendEvent`](../sendevent/edgeconfigoverrides.md)
* [`setConsent`](../setconsent.md)
* [&#39;getIdentity&#39;](../getidentity.md)
* [&#39;appendIdentityToUrl&#39;](../appendidentitytourl.md)

위의 명령 중 하나에서 `edgeConfigOverrides`을(를) 설정하는 것은 둘 다 설정된 경우 `edgeConfigOverrides` 명령의 `configure` 개체보다 우선합니다. 이러한 명령에 `edgeConfigOverrides` 개체가 없으면 `edgeConfigOverrides` 명령의 `configure` 개체가 사용됩니다.

## 예

데이터 스트림 구성에 지원되는 모든 서비스가 활성화되어 있으면 아래 샘플은 이 설정을 무시하고 모든 서비스를 비활성화합니다.

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| 매개변수 | 유형 | 설명 |
| --- | --- | --- |
| **`orgId`** | `string` | 회사의 IMS 조직 ID입니다. |
| **`datastreamId`** | `string` | 데이터를 보낼 데이터 스트림 ID입니다. |
| **`com_adobe_experience_platform`** | `object` | Adobe Experience Platform 서비스에 대한 동적 데이터스트림 구성을 정의합니다. |
| **`com_adobe_experience_platform.enabled`** | `boolean` | 이벤트가 Adobe Experience Platform으로 전송되는지 여부를 결정합니다. |
| **`com_adobe_experience_platform.datasets`** | `object` | 이벤트에 사용되는 데이터 세트를 정의합니다. |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | 이벤트가 Offer Decisioning으로 전송되는지 여부를 결정합니다. |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | 이벤트가 Edge 세그먼테이션으로 전송되는지 여부를 결정합니다. |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | 이벤트가 Edge 대상으로 전송되는지 여부를 결정합니다. |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | 이벤트가 Adobe Journey Optimizer으로 전송되는지 여부를 결정합니다. |
| **`com_adobe_analytics.enabled`** | `boolean` | 이벤트가 Adobe Analytics으로 전송되는지 여부를 결정합니다. |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | Analytics 데이터를 전송할 보고서 세트를 결정하는 문자열 배열입니다. |
| **`com_adobe_audience_manager.enabled`** | `boolean` | 이벤트가 Adobe Audience Manager으로 전송되는지 여부를 결정합니다. |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | Audience Manager에서 사용할 서드파티 ID 동기화 컨테이너입니다. `com_adobe_audience_manager.enabled`(으)로 설정된 `true`이(가) 필요합니다. 그렇지 않으면 Audience Manager 서비스가 비활성화됩니다. |
| **`com_adobe_target.enabled`** | `boolean` | 이벤트가 Adobe Target으로 전송되는지 여부를 결정합니다. |
| **`com_adobe_target.propertyToken`** | `string` | Adobe Target 대상 속성에 대한 토큰입니다. |
| **`com_adobe_launch_ssf`** | `boolean` | 이벤트가 서버측 전달로 전송되는지 여부를 결정합니다. |

## 웹 SDK 태그 확장을 사용한 구성 재정의

태그 확장을 구성할 때 이 필드에 해당하는 웹 SDK 태그 확장이 [구성 재정의](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) 아래에 있습니다.
