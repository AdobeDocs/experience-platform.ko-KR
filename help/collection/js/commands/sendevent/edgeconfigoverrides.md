---
title: edgeConfigOverrides
description: sendEvent 명령에 대한 데이터스트림 재정의를 구성합니다.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides`(`sendEvent` 명령)

`edgeConfigOverrides` 개체를 사용하면 현재 `sendEvent` 명령에 대한 구성 설정을 재정의할 수 있습니다. 이 개체는 웹 SDK 구현의 나머지 부분과 다른 구성 설정으로 실행하려는 동일한 페이지에 특정 명령이 있을 때 유용합니다. 지정된 페이지의 모든 명령에 대한 구성 설정을 무시하려면 [`edgeConfigOverrides` 명령`configure`에서 &#x200B;](../configure/edgeconfigoverrides.md) 개체를 사용하는 것이 좋습니다.

중요한 데이터스트림 구성 재정의 프로세스는 다음 두 가지 주요 단계로 구성됩니다.

1. 먼저 데이터 스트림 UI에서 [데이터 스트림을 구성](/help/datastreams/configure.md)할 때 데이터 스트림 구성 재정의를 정의해야 합니다. 재정의를 구성하는 방법에 대한 지침은 데이터스트림 설명서에서 [데이터스트림 구성 재정의](/help/datastreams/overrides.md)를 참조하십시오.
1. 데이터 스트림 UI에서 데이터 스트림 재정의를 구성한 후 `edgeConfigOverrides` 개체를 구성할 수 있습니다.

`configure` 명령도 `edgeConfigOverrides` 개체를 지원합니다. [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) 명령의 `configure`을(를) 참조하십시오. 둘 다 설정된 경우 `edgeConfigOverrides` 명령의 `sendEvent` 개체가 `edgeConfigOverrides` 명령의 `configure` 개체보다 우선합니다.

## 예

데이터 스트림 구성에 지원되는 모든 서비스가 활성화되어 있으면 아래 샘플은 이 설정을 무시하고 모든 서비스를 비활성화합니다(각 서비스의 `enabled: false` 설정 참조). 이 개체는 [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) 명령에서 `configure` 개체와 동일한 속성을 지원합니다.

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## 웹 SDK 태그 확장을 사용하여 데이터 스트림 구성 재정의

이 개체에 해당하는 웹 SDK 태그 확장은 &#39;[&#39; 작업을 구성할 때 &#x200B;](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides)데이터 스트림 구성 재정의[!UICONTROL Send event] 섹션입니다.
