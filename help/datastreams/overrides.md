---
title: 데이터스트림 재정의 구성
description: 데이터스트림 UI에서 데이터스트림 재정의를 구성하고 Web SDK를 통해 활성화하는 방법에 대해 알아봅니다.
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: 32f36d96e3aa6beb72121adcc74f2da0bd2c9473
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 97%

---

# 데이터스트림 재정의 구성

데이터스트림 재정의를 사용하면 Web SDK를 통해서 Edge Network에 전달되는 데이터스트림에 대한 추가 구성을 정의할 수 있습니다.

이렇게 하면 새 데이터스트림을 생성하거나 기존 설정을 수정하지 않고도 기본 비헤이비어와 다른 데이터스트림 비헤이비어를 트리거할 수 있습니다.

데이터스트림 구성 재정의는 2단계 프로세스입니다.

1. 먼저 [데이터스트림 구성 페이지](configure.md)에서 데이터스트림 구성 재정의를 정의해야 합니다.
2. 그런 다음 Web SDK 명령 또는 Web SDK [태그 확장 기능](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)을 사용하여 Edge Network에 해당 재정의를 보내야 합니다.

이 문서에서는 지원되는 모든 재정의에 대한 전반적인 데이터스트림 구성 재정의 프로세스를 설명합니다.

>[!IMPORTANT]
>
>데이터 스트림 재정의는 다음에 대해서만 지원됩니다. [웹 SDK](../edge/home.md) 통합. [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) 및 [서버 API](../server-api/overview.md) 통합은 현재 데이터 스트림 재정의를 지원하지 않습니다.

## Datastreams UI에서 데이터스트림 재정의 구성 {#configure-overrides}

데이터스트림 구성 재정의를 사용하여 다음 데이터스트림 구성을 수정할 수 있습니다.

* Experience Platform 이벤트 데이터 세트
* Adobe Target 속성 토큰
* Audience Manager ID 동기화 컨테이너
* Adobe Analytics 보고서 세트

### Adobe Target에 대한 데이터스트림 재정의 {#target-overrides}

Adobe Target 데이터스트림에 대한 데이터스트림 재정의를 구성하려면 먼저 Adobe Target 데이터스트림을 만들어야 합니다. 지침에 따라 [Adobe Target](configure.md#target) 서비스로 [데이터스트림을 구성](configure.md)합니다.

데이터스트림이 생성되면 추가한 [Adobe Target](configure.md#target) 서비스를 편집하고 **[!UICONTROL 속성 토큰 재정의]** 섹션을 사용하여 아래 이미지에 표시된 대로 원하는 데이터스트림 재정의를 추가합니다. 한 줄에 하나의 속성 토큰을 추가합니다.

![속성 토큰 재정의가 강조 표시되면 Adobe Target 서비스 설정을 표시하는 데이터스트림 UI 스크린샷.](assets/overrides/override-target.png)

원하는 재정의가 추가되면 데이터스트림 설정을 저장합니다.

이제 Adobe Target 데이터스트림 재정의를 구성해야 합니다. [Web SDK를 통해 재정의를 Edge Network로 전송](#send-overrides)할 수 있습니다.

### Adobe Analytics에 대한 데이터스트림 재정의 {#analytics-overrides}

Adobe Analytics 데이터스트림에 대한 데이터스트림 재정의를 구성하려면 먼저 [Adobe Analytics](configure.md#analytics) 데이터스트림을 만들어야 합니다. 지침에 따라 [Adobe Analytics](configure.md#analytics) 서비스로 [데이터스트림을 구성](configure.md)합니다.

데이터스트림이 생성되면 추가한 [Adobe Analytics](configure.md#target) 서비스를 편집하고 **[!UICONTROL 보고서 세트 재정의]** 섹션을 사용하여 아래 이미지에 표시된 대로 원하는 데이터스트림 재정의를 추가합니다.

**[!UICONTROL 배치 모드 표시]**&#x200B;를 선택하여 보고서 세트 재정의의 일괄 편집을 활성화합니다. 보고서 세트 재정의 목록을 복사하여 붙여넣으면 한 줄에 하나의 보고서 세트를 입력할 수 있습니다.

![보고서 세트 재정의가 강조 표시되면 Adobe Analytics 서비스 설정을 표시하는 데이터스트림 UI 스크린샷.](assets/overrides/override-analytics.png)

원하는 재정의가 추가되면 데이터스트림 설정을 저장합니다.

이제 Adobe Analytics 데이터스트림 재정의를 구성해야 합니다. [Web SDK를 통해 재정의를 Edge Network로 전송](#send-overrides)할 수 있습니다.

### Experience Platform 이벤트 데이터 세트에 대한 데이터스트림 재정의 {#event-dataset-overrides}

Experience Platform 이벤트 데이터세트에 대한 데이터스트림 재정의를 구성하려면 먼저 [Adobe Experience Platform](configure.md#aep) 데이터스트림을 만들어야 합니다. 지침에 따라 [Adobe Experience Platform](configure.md#aep) 서비스로 [데이터스트림을 구성](configure.md)합니다.

데이터스트림이 생성되면, 추가한 [Adobe Experience Platform](configure.md#aep) 서비스를 편집하고 아래 이미지에 표시된 대로 **[!UICONTROL 이벤트 데이터 세트 추가]** 옵션을 선택하여 하나 이상의 재정의 이벤트 데이터 세트를 추가합니다.

![이벤트 데이터 세트 재정의가 강조 표시되면 Adobe Experience Platform 서비스 설정을 표시하는 데이터스트림 UI 스크린샷.](assets/overrides/override-aep.png)

원하는 재정의가 추가되면 데이터스트림 설정을 저장합니다.

이제 Adobe Experience Platform 데이터스트림 재정의를 구성해야 합니다. [Web SDK를 통해 재정의를 Edge Network로 전송](#send-overrides)할 수 있습니다.

### 서드파티 ID 동기화 컨테이너에 대한 데이터스트림 재정의 {#container-overrides}

서드파티 ID 동기화 컨테이너에 대한 데이터스트림 재정의를 구성하려면 먼저 데이터스트림을 만들어야 합니다. 다음 지침에 따라 [데이터스트림을 구성](configure.md)하여 하나의 데이터스트림을 만듭니다.

데이터스트림이 생성되면, **[!UICONTROL 고급 옵션]**&#x200B;으로 이동하고 **[!UICONTROL 서드파티 ID 동기화]** 옵션을 활성화합니다.

그런 다음 **[!UICONTROL 컨테이너 ID 재정의]** 섹션을 사용하여 아래 이미지에 표시된 대로 기본 설정을 재정의하려는 컨테이너 ID를 추가합니다.

>[!IMPORTANT]
>
>컨테이너 ID는 `"1234567"`과 같은 문자열이 아니라 `1234567`과 같은 숫자 값이어야 합니다. Web SDK를 통해 컨테이너 ID 재정의로 문자열 값을 전송하면 오류가 발생합니다.

![서드파티 ID 동기화 컨테이너 재정의가 강조 표시되면 데이터스트림 설정을 표시하는 데이터스트림 UI 스크린샷.](assets/overrides/override-container.png)

원하는 재정의가 추가되면 데이터스트림 설정을 저장합니다.

이제 ID 동기화 컨테이너 재정의를 구성해야 합니다. [Web SDK를 통해 재정의를 Edge Network로 전송](#send-overrides)할 수 있습니다.

## Web SDK를 통해 Edge Network로 재정의 전송 {#send-overrides}

>[!NOTE]
>
>Web SDK 명령을 통해 구성 재정의를 전송하는 대신 구성 재정의를 Web SDK [태그 확장 기능](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)에 추가할 수 있습니다.

데이터 수집 UI에서 [데이터스트림 재정의를 구성](#configure-overrides)하고 나서 Web SDK를 통해 재정의를 Edge Network로 전송할 수 있습니다.

Web SDK를 통해 재정의를 Edge Network로 전송하는 단계는 데이터스트림 구성 재정의를 활성화하는 두 번째이자 마지막 단계입니다.

데이터스트림 구성 재정의는 `edgeConfigOverrides` Web SDK 명령을 통해 Edge Network로 전송됩니다. 이 명령은 다음 명령에서 [!DNL Edge Network]로 전달되는 데이터스트림 재정의를 생성하거나 `configure` 명령의 경우에는 모든 요청마다 해당 재정의를 생성합니다.

`edgeConfigOverrides` 명령은 다음 명령에서 [!DNL Edge Network]로 전달되는 데이터스트림 재정의를 생성하거나 `configure`의 경우에는 모든 요청마다 해당 재정의를 생성합니다.

구성 재정의가 `configure` 명령과 함께 전송되면 해당 재정의는 다음 Web SDK 명령에 포함됩니다.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [구성](../edge/fundamentals/configuring-the-sdk.md)

전역적으로 지정된 옵션은 개별 명령의 구성 옵션으로 재정의할 수 있습니다.

### `sendEvent` 명령을 통해 구성 재정의 전송 {#send-event}

아래 예의 `sendEvent` 명령에서 구성 재정의는 다음과 같습니다.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| 매개변수 | 설명 |
|---|---|
| `edgeConfigOverrides.datastreamId` | 이 매개 변수를 사용하면 단일 요청이 `configure` 명령에서 정의한 데이터스트림과 다른 데이터스트림으로 이동할 수 있습니다. |

### `configure` 명령을 통해 구성 재정의 전송 {#send-configure}

아래 예의 `configure` 명령에서 구성 재정의는 다음과 같습니다.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": { 
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

### 페이로드 예제 {#payload-example}

위 예는 다음과 유사한 [!DNL Edge Network] 페이로드를 생성합니다.

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
          }
        }
      },
      "com_adobe_analytics": {
        "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
      },
      "com_adobe_identity": {
        "idSyncContainerId": "1234567"
      },
      "com_adobe_target": {
        "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
      }
    },
    "state": {  }
  },
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```
