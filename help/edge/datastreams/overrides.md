---
title: 데이터 스트림 무시 구성
description: 데이터 스트림 UI에서 데이터 스트림 무시를 구성하고 웹 SDK를 통해 활성화하는 방법을 알아봅니다.
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# 데이터 스트림 무시 구성

데이터 스트림 무시를 사용하면 웹 SDK를 통해 Edge 네트워크에 전달되는 데이터 세트에 대한 추가 구성을 정의할 수 있습니다.

이렇게 하면 새 데이터 스트림을 만들거나 기존 설정을 수정하지 않고 기본 데이터 스트림 동작과 다른 데이터 스트림 동작을 트리거하는 데 도움이 됩니다.

데이터 스트림 구성 재정의는 다음 두 가지 단계로 구성됩니다.

1. 먼저, [데이터 스트림 구성 페이지](configure.md).
2. 그런 다음 웹 SDK 명령을 통해 또는 웹 SDK를 사용하여 Edge Network에 무시를 보내야 합니다 [태그 확장](../extension/web-sdk-extension-configuration.md).

이 문서에서는 지원되는 모든 유형의 재지정에 대한 종단 간 데이터 스트림 구성 재정의 프로세스에 대해 설명합니다.

## 데이터 스트림 UI에서 데이터 스트림 무시 구성 {#configure-overrides}

데이터 스트림 구성 무시를 사용하면 다음 데이터 스트림 구성을 수정할 수 있습니다.

* Experience Platform 이벤트 데이터 세트
* Adobe Target 속성 토큰
* Audience Manager ID 동기화 컨테이너
* Adobe Analytics 보고서 세트

### Adobe Target에 대한 데이터 스트림 무시 {#target-overrides}

Adobe Target 데이터 스트림에 대한 데이터 스트림 무시를 구성하려면 먼저 Adobe Target 데이터 스트림을 만들어야 합니다. 지침에 따라 다음을 수행합니다 [데이터 스트림 구성](configure.md) 사용 [Adobe Target](configure.md#target) 서비스.

데이터 스트림을 만들면 [Adobe Target](configure.md#target) 추가한 서비스 및 **[!UICONTROL 속성 토큰 무시]** 섹션을 추가하여 아래 이미지와 같이 원하는 데이터 스트림 재정의를 추가합니다. 행당 하나의 속성 토큰을 추가합니다.

![속성 토큰 무시가 강조 표시된 Adobe Target 서비스 설정을 보여주는 데이터 스트림 UI 스크린샷입니다.](../assets/datastreams/overrides/override-target.png)

원하는 무시를 추가한 후 데이터 스트림 설정을 저장합니다.

이제 Adobe Target 데이터 스트림 재정의가 구성되어 있어야 합니다. 이제 다음을 수행할 수 있습니다 [웹 SDK를 통해 Edge 네트워크에 무시를 보냅니다.](#send-overrides).

### Adobe Analytics에 대한 데이터 스트림 무시 {#analytics-overrides}

Adobe Analytics 데이터 스트림에 대한 데이터 스트림 무시를 구성하려면 먼저 다음에 가 있어야 합니다 [Adobe Analytics](configure.md#analytics) 데이터 스트림이 생성되었습니다. 지침에 따라 다음을 수행합니다 [데이터 스트림 구성](configure.md) 사용 [Adobe Analytics](configure.md#analytics) 서비스.

데이터 스트림을 만들면 [Adobe Analytics](configure.md#target) 추가한 서비스 및 **[!UICONTROL 보고서 세트 무시]** 섹션을 추가하여 아래 이미지와 같이 원하는 데이터 스트림 재정의를 추가합니다.

선택 **[!UICONTROL 일괄 처리 모드 표시]** 보고서 세트를 일괄적으로 편집할 수 있도록 하려면 다음을 무시합니다. 보고서 세트 무시 목록을 복사하여 줄 당 하나의 보고서 세트를 입력하여 붙여넣을 수 있습니다.

![보고서 세트 무시를 강조 표시한 Adobe Analytics 서비스 설정을 보여주는 데이터 스트림 UI 스크린샷입니다.](../assets/datastreams/overrides/override-analytics.png)

원하는 무시를 추가한 후 데이터 스트림 설정을 저장합니다.

이제 Adobe Analytics 데이터 스트림 재정의가 구성되어 있어야 합니다. 이제 다음을 수행할 수 있습니다 [웹 SDK를 통해 Edge 네트워크에 무시를 보냅니다.](#send-overrides).

### Experience Platform 이벤트 데이터 세트에 대해 데이터 스트림 무시 {#event-dataset-overrides}

Experience Platform 이벤트 데이터 세트에 대해 데이터 스트림 무시를 구성하려면 먼저 데이터 세트에 대한 [Adobe Experience Platform](configure.md#aep) 데이터 스트림이 생성되었습니다. 지침에 따라 다음을 수행합니다 [데이터 스트림 구성](configure.md) 사용 [Adobe Experience Platform](configure.md#aep) 서비스.

데이터 스트림을 만들면 [Adobe Experience Platform](configure.md#aep) 추가한 서비스를 선택하고 선택합니다 **[!UICONTROL 이벤트 데이터 세트 추가]** 아래 이미지와 같이 하나 이상의 무시 이벤트 데이터 세트를 추가하는 옵션.

![이벤트 데이터 세트 무시를 강조 표시한 Adobe Experience Platform 서비스 설정을 보여주는 데이터 스트림 UI 스크린샷입니다.](../assets/datastreams/overrides/override-aep.png)

원하는 무시를 추가한 후 데이터 스트림 설정을 저장합니다.

이제 Adobe Experience Platform 데이터 스트림 재정의가 구성되어 있어야 합니다. 이제 다음을 수행할 수 있습니다 [웹 SDK를 통해 Edge 네트워크에 무시를 보냅니다.](#send-overrides).

### 타사 ID 동기화 컨테이너에 대해 데이터 스트림 무시 {#container-overrides}

타사 ID 동기화 컨테이너에 대한 데이터 스트림 무시를 구성하려면 먼저 생성된 데이터 스트림을 가져야 합니다. 지침에 따라 다음을 수행합니다 [데이터 스트림 구성](configure.md) 만들 수 있습니다.

데이터 스트림을 만든 후 다음 위치로 이동합니다. **[!UICONTROL 고급 옵션]** 그리고 **[!UICONTROL 타사 ID 동기화]** 선택 사항입니다.

그런 다음 **[!UICONTROL 컨테이너 ID 무시]** 섹션을 추가하여 아래 이미지와 같이 기본 설정을 재정의할 컨테이너 ID를 추가합니다.

>[!IMPORTANT]
>
>컨테이너 ID는 와 같은 숫자 값이어야 합니다. `1234567`와 같이 문자열이 아님 `"1234567"`. 웹 SDK를 통해 문자열 값을 컨테이너 ID 무시로 전송하는 경우 오류가 표시됩니다.

![타사 ID 동기화 컨테이너 재정의가 강조 표시된 데이터 스트림 설정을 보여주는 데이터 스트림 UI 스크린샷입니다.](../assets/datastreams/overrides/override-container.png)

원하는 무시를 추가한 후 데이터 스트림 설정을 저장합니다.

이제 ID 동기화 컨테이너 무시를 구성해야 합니다. 이제 다음을 수행할 수 있습니다 [웹 SDK를 통해 Edge 네트워크에 무시를 보냅니다.](#send-overrides).

## 웹 SDK를 통해 Edge Network에 무시를 보냅니다. {#send-overrides}

>[!NOTE]
>
>웹 SDK 명령을 통해 구성 무시를 전송하는 대신 웹 SDK에 구성 무시를 추가할 수 있습니다 [태그 확장](../extension/web-sdk-extension-configuration.md).

후 [데이터 스트림 무시 구성](#configure-overrides) 이제 데이터 수집 UI에서 웹 SDK를 통해 Edge Network에 무시를 보낼 수 있습니다.

웹 SDK를 통해 Edge 네트워크에 오버라이드를 전송하는 것은 데이터 스트림 구성 오버라이드를 활성화하는 두 번째 및 마지막 단계입니다.

데이터 스트림 구성 재정의는 `edgeConfigOverrides` 웹 SDK 명령. 이 명령은 다음 위치에 전달되는 데이터 스트림 재지정을 만듭니다 [!DNL Edge Network] 다음 명령에서 또는 `configure` 명령을 실행합니다.

다음 `edgeConfigOverrides` 명령은 로 전달되는 데이터 스트림 재지정을 생성합니다 [!DNL Edge Network] 다음 명령에서 또는 `configure`를 반환합니다.

구성 무시를 `configure` 명령, 지원되는 다음 명령에 포함됩니다.

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [구성](../fundamentals/configuring-the-sdk.md)

전역적으로 지정된 옵션은 개별 명령의 구성 옵션에 의해 대체할 수 있습니다.

### 를 통해 구성 무시 전송 `sendEvent` 명령 {#send-event}

아래 예제는 구성 재정의가 `sendEvent` 명령.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
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

### 를 통해 구성 무시 전송 `configure` 명령 {#send-configure}

아래 예제는 구성 재정의가 `configure` 명령.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  edgeConfigId: "etc",
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

### 페이로드 예 {#payload-example}

위의 예는 를 생성합니다 [!DNL Edge Network] 페이로드는 다음과 같습니다.

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

