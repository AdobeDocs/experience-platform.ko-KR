---
title: 데이터 스트림 구성 재정의
description: Web SDK를 통해 데이터 스트림 재정의를 구성하는 방법에 대해 알아봅니다.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 10%

---

# 데이터스트림 재정의 구성

`edgeConfigOverrides` 개체를 사용하면 현재 페이지에서 실행되는 명령에 대한 구성 설정을 재정의할 수 있습니다. 이 재정의 개체는 명령이 아니라 대부분의 웹 SDK 명령에 포함할 수 있는 개체입니다.

이 개체는 국가별로 다른 웹 사이트 또는 하위 도메인이 있거나 여러 비즈니스 단위에 맞는 데이터를 저장할 여러 개의 Experience Platform 샌드박스가 있는 경우에 유용합니다.

>[!IMPORTANT]
>
>데이터스트림 재정의에 대한 자세한 전체 구성 지침은 [데이터스트림 구성 재정의](../../datastreams/overrides.md#configure-overrides) 설명서를 참조하십시오.

데이터 스트림 구성 재정의는 2단계 프로세스입니다.

1. 먼저 데이터 스트림 UI 내의 [데이터 스트림 구성 페이지](../../datastreams/configure.md)에서 데이터 스트림 구성 재정의를 정의해야 합니다. 재정의를 구성하는 방법에 대한 지침은 [데이터스트림 구성 재정의](../../datastreams/overrides.md#configure-overrides) 설명서를 참조하십시오.
2. UI에서 데이터 스트림 재정의를 구성한 후에는 다음 방법 중 하나로 재정의를 Edge Network에 보내야 합니다.
   * 웹 SDK를 통해 [태그 확장](#tag-extension).
   * [`sendEvent`](../commands/sendevent/overview.md) 또는 [`configure`](../commands/configure/overview.md) 웹 SDK 명령을 통해.
   * Mobile SDK [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network) 명령을 통해.

웹 SDK 구성과 특정 명령(예: [`sendEvent`](sendevent/overview.md))에서 모두 재정의를 설정하면 특정 명령의 재정의가 우선합니다.

>[!NOTE]
>
>Experience Cloud 서비스를 *비활성화*&#x200B;하도록 구성을 재정의하려면 데이터 스트림 구성에서 서비스가 먼저 *활성화*&#x200B;되었는지 확인해야 합니다. 데이터 스트림에 서비스를 추가하는 방법에 대한 자세한 내용은 [데이터 스트림을 구성](../../datastreams/configure.md#add-services)하는 방법에 대한 설명서를 참조하십시오.

## 웹 SDK 태그 확장을 통해 Edge Network에 데이터스트림 재정의 전송 {#tag-extension}

자세한 구성 지침은 Web SDK 태그 확장에서 [데이터 스트림 재정의 구성](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides)에 대한 설명서를 참조하십시오.

웹 SDK 태그 확장에서 데이터 스트림 재정의를 구성하려면 [태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL 데이터 스트림 구성 재정의]**&#x200B;에서 원하는 각 필드를 설정하십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. 아래로 스크롤하여 **[!UICONTROL 데이터 스트림 구성 재정의]** 섹션으로 이동합니다. 원하는 각 재정의 값을 설정합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

특정 명령에 대해서만 재정의를 설정하려면 태그 규칙의 작업 내에서 원하는 각 필드를 설정합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 작업]에서 기존 작업을 선택하거나 작업을 만드십시오.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 이벤트 보내기]**(으)로 설정합니다.
1. **[!UICONTROL 데이터 스트림 구성 재정의]** 섹션까지 아래로 스크롤합니다.
1. 이 섹션의 각 필드를 원하는 재정의 값으로 설정합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

[!UICONTROL 개발], [!UICONTROL 스테이징] 및 [!UICONTROL 프로덕션] 환경에 대해 별도의 필드가 제공됩니다. 각 환경에 대해 원하는 각 필드를 입력해야 합니다.

## 웹 SDK JavaScript 라이브러리를 통해 Edge Network에 재정의 전송 {#library}

데이터 수집 UI에서 [데이터 스트림 재정의를 구성](../../datastreams/overrides.md)한 후 이제 Web SDK JavaScript 라이브러리를 통해 Edge Network에 재정의를 보낼 수 있습니다.

Web SDK를 사용하는 경우 `edgeConfigOverrides` 명령을 통해 Edge Network에게 재정의를 전송하는 것은 데이터스트림 구성 재정의를 활성화하는 두 번째 마지막 단계입니다.

데이터스트림 구성 재정의는 `edgeConfigOverrides` Web SDK 명령을 통해 Edge Network로 전송됩니다. 이 명령은 다음 명령의 [!DNL Edge Network]에 전달되는 데이터 스트림 재정의를 만듭니다. `configure` 명령을 사용하는 경우 모든 요청에 대해 재정의가 전달됩니다.

`edgeConfigOverrides` 명령은 다음 명령의 [!DNL Edge Network]에 전달되는 데이터 스트림 재정의를 만듭니다.

구성 재정의가 `configure` 명령과 함께 전송되면 해당 재정의는 다음 Web SDK 명령에 포함됩니다.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [구성](../commands/configure/overview.md)

전역적으로 지정된 옵션은 개별 명령의 구성 옵션으로 재정의할 수 있습니다.

### 웹 SDK `sendEvent` 명령을 통해 구성 재정의 보내기 {#send-event}

아래 예제는 `sendEvent` 호출에서 지원되는 모든 동적 데이터스트림 구성 옵션을 보여 줍니다.

데이터 스트림 구성에 지원되는 모든 서비스가 활성화되어 있으면 아래 샘플은 이 설정을 무시하고 모든 서비스를 비활성화합니다(각 서비스의 `enabled: false` 설정 참조).

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
      reportSuites: ["ujslconfigoverrides3"],
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

| 매개변수 | 설명 |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | 이 매개변수를 사용하면 단일 요청이 `configure` 명령에서 정의한 데이터스트림과 다른 데이터스트림으로 이동할 수 있습니다. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Experience Platform 서비스에 대한 동적 데이터스트림 구성을 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | 이벤트를 Experience Platform 서비스로 전송할지 여부를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | 이벤트에 사용되는 데이터 세트를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | 이벤트가 Offer decisioning 서비스로 전송되는지 여부를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | 이벤트가 에지 세분화 서비스로 전송되는지 여부를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | 이벤트 데이터가 Edge 대상으로 전송되는지 여부를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | 이벤트 데이터가 Adobe Journey Optimizer 서비스로 전송되는지 여부를 정의합니다. |
| `com_adobe_analytics.enabled` | 이벤트 데이터가 Adobe Analytics으로 전송되는지 여부를 정의합니다. |
| `com_adobe_analytics.reportSuites[]` | Analytics 데이터를 전송할 보고서 세트를 결정하는 문자열 배열입니다. |
| `com_adobe_identity.idSyncContainerId` | Audience Manager 시 사용할 서드파티 ID 동기화 컨테이너입니다. 이 ID 동기화 컨테이너가 작동하려면 `com_adobe_audience_manager.enabled`을(를) `true`(으)로 설정해야 합니다. 그렇지 않으면 Audience Manager 서비스가 비활성화됩니다. |
| `com_adobe_target.enabled` | 이벤트 데이터가 Adobe Target으로 전송되는지 여부를 정의합니다. |
| `com_adobe_target.propertyToken` | Adobe Target 대상 속성에 대한 토큰입니다. |
| `com_adobe_audience_manager.enabled` | 이벤트 데이터가 Audience Manager 서비스로 전송되는지 여부를 정의합니다. |
| `com_adobe_launch_ssf` | 이벤트 데이터가 서버측 전달로 전송되는지 여부를 정의합니다. |

### 웹 SDK `configure` 명령을 통해 구성 재정의 보내기 {#send-configure}

아래 예의 `configure` 명령에서 구성 재정의는 다음과 같습니다.

데이터 스트림 구성에 지원되는 모든 서비스가 활성화되어 있으면 아래 샘플은 이 설정을 무시하고 모든 서비스를 비활성화합니다(각 서비스의 `enabled: false` 설정 참조).

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
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
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
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

| 매개변수 | 설명 |
|---|---|
| `orgId` | Adobe 계정에 해당하는 IMS 조직 ID. |
| `edgeConfigOverrides.datastreamId` | 이 매개변수를 사용하면 단일 요청이 `configure` 명령에서 정의한 데이터스트림과 다른 데이터스트림으로 이동할 수 있습니다. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Experience Platform 서비스에 대한 동적 데이터스트림 구성을 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | 이벤트를 Experience Platform 서비스로 전송할지 여부를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | 이벤트에 사용되는 데이터 세트를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | 이벤트가 Offer decisioning 서비스로 전송되는지 여부를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | 이벤트가 에지 세분화 서비스로 전송되는지 여부를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | 이벤트 데이터가 Edge 대상으로 전송되는지 여부를 정의합니다. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | 이벤트 데이터가 Adobe Journey Optimizer 서비스로 전송되는지 여부를 정의합니다. |
| `com_adobe_analytics.enabled` | 이벤트 데이터가 Adobe Analytics으로 전송되는지 여부를 정의합니다. |
| `com_adobe_analytics.reportSuites[]` | Analytics 데이터를 전송할 보고서 세트를 결정하는 문자열 배열입니다. |
| `com_adobe_identity.idSyncContainerId` | Audience Manager 시 사용할 서드파티 ID 동기화 컨테이너입니다. 이 ID 동기화 컨테이너가 작동하려면 `com_adobe_audience_manager.enabled`을(를) `true`(으)로 설정해야 합니다. 그렇지 않으면 Audience Manager 서비스가 비활성화됩니다. |
| `com_adobe_target.enabled` | 이벤트 데이터가 Adobe Target으로 전송되는지 여부를 정의합니다. |
| `com_adobe_target.propertyToken` | Adobe Target 대상 속성에 대한 토큰입니다. |
| `com_adobe_audience_manager.enabled` | 이벤트 데이터가 Audience Manager 서비스로 전송되는지 여부를 정의합니다. |
| `com_adobe_launch_ssf` | 이벤트 데이터가 서버측 전달로 전송되는지 여부를 정의합니다. |

