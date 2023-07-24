---
title: 데이터 스트림 재정의 구성
description: 데이터스트림 UI에서 데이터스트림 재정의를 구성하고 웹 SDK를 통해 활성화하는 방법에 대해 알아봅니다.
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 4%

---

# 데이터 스트림 재정의 구성

데이터 스트림 재정의를 사용하면 웹 SDK를 통해 Edge Network에 전달되는 데이터 스트림에 대한 추가 구성을 정의할 수 있습니다.

이렇게 하면 새 데이터 스트림을 만들거나 기존 설정을 수정하지 않고도 기본 데이터 스트림 비헤이비어와 다른 데이터 스트림 비헤이비어를 트리거할 수 있습니다.

데이터 스트림 구성 재정의는 2단계 프로세스입니다.

1. 먼저 [데이터스트림 구성 페이지](configure.md)에서 데이터스트림 구성 재정의를 정의해야 합니다.
2. 그런 다음 Web SDK 명령 또는 Web SDK [태그 확장 기능](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)을 사용하여 Edge Network에 해당 재정의를 보내야 합니다.

이 문서에서는 지원되는 모든 재정의 유형에 대한 종단간 데이터스트림 구성 재정의 프로세스에 대해 설명합니다.

## 데이터스트림 UI에서 데이터스트림 재정의 구성 {#configure-overrides}

데이터 스트림 구성 재정의를 사용하면 다음 데이터 스트림 구성을 수정할 수 있습니다.

* Experience Platform 이벤트 데이터 세트
* Adobe Target 속성 토큰
* Audience Manager ID 동기화 컨테이너
* Adobe Analytics 보고서 세트

### Adobe Target에 대한 데이터 스트림 재정의 {#target-overrides}

Adobe Target 데이터스트림에 대한 데이터스트림 재정의를 구성하려면 먼저 Adobe Target 데이터스트림을 생성해야 합니다. 다음 지침을 따르십시오 [데이터 스트림 구성](configure.md) (으)로 [Adobe Target](configure.md#target) 서비스.

데이터 스트림을 생성했으면 [Adobe Target](configure.md#target) 을(를) 추가하고 사용하는 서비스 **[!UICONTROL 속성 토큰 재정의]** 섹션에 아래 이미지에 표시된 대로 원하는 데이터스트림 무시를 추가합니다. 라인당 하나의 속성 토큰을 추가합니다.

![속성 토큰 무시가 강조 표시된 Adobe Target 서비스 설정을 보여 주는 데이터 스트림 UI 스크린샷입니다.](assets/overrides/override-target.png)

원하는 재정의를 추가한 후 데이터스트림 설정을 저장합니다.

이제 Adobe Target 데이터 스트림 재정의를 구성해야 합니다. 이제 다음을 수행할 수 있습니다 [웹 SDK를 통해 Edge Network에 재정의 전송](#send-overrides).

### Adobe Analytics에 대한 데이터 스트림 재정의 {#analytics-overrides}

Adobe Analytics 데이터스트림에 대한 데이터스트림 재정의를 구성하려면 먼저 다음을 수행해야 합니다. [Adobe Analytics](configure.md#analytics) 데이터 스트림이 생성되었습니다. 다음 지침을 따르십시오 [데이터 스트림 구성](configure.md) (으)로 [Adobe Analytics](configure.md#analytics) 서비스.

데이터 스트림을 생성했으면 [Adobe Analytics](configure.md#target) 을(를) 추가하고 사용하는 서비스 **[!UICONTROL 보고서 세트 무시]** 섹션에 아래 이미지에 표시된 대로 원하는 데이터스트림 무시를 추가합니다.

선택 **[!UICONTROL 배치 모드 표시]** 보고서 세트 무시의 일괄 편집을 활성화하려면 을(를) 선택합니다. 한 줄에 하나의 보고서 세트를 입력하여 보고서 세트 무시 목록을 복사하여 붙여넣을 수 있습니다.

![보고서 세트 무시가 강조 표시된 Adobe Analytics 서비스 설정을 보여 주는 데이터 스트림 UI 스크린샷입니다.](assets/overrides/override-analytics.png)

원하는 재정의를 추가한 후 데이터스트림 설정을 저장합니다.

이제 Adobe Analytics 데이터 스트림 재정의를 구성해야 합니다. 이제 다음을 수행할 수 있습니다 [웹 SDK를 통해 Edge Network에 재정의 전송](#send-overrides).

### Experience Platform 이벤트 데이터 세트에 대한 데이터 스트림 무시 {#event-dataset-overrides}

Experience Platform 이벤트 데이터 세트에 대한 데이터 스트림 재정의를 구성하려면 먼저 [Adobe Experience Platform](configure.md#aep) 데이터 스트림이 생성되었습니다. 다음 지침을 따르십시오 [데이터 스트림 구성](configure.md) (으)로 [Adobe Experience Platform](configure.md#aep) 서비스.

데이터 스트림을 생성했으면 [Adobe Experience Platform](configure.md#aep) 추가한 서비스 및 선택 **[!UICONTROL 이벤트 데이터 세트 추가]** 아래 이미지에 표시된 대로 하나 이상의 재정의 이벤트 데이터 세트를 추가하는 옵션.

![이벤트 데이터 세트 무시가 강조 표시된 Adobe Experience Platform 서비스 설정을 보여 주는 데이터 스트림 UI 스크린샷입니다.](assets/overrides/override-aep.png)

원하는 재정의를 추가한 후 데이터스트림 설정을 저장합니다.

이제 Adobe Experience Platform 데이터 스트림 재정의를 구성해야 합니다. 이제 다음을 수행할 수 있습니다 [웹 SDK를 통해 Edge Network에 재정의 전송](#send-overrides).

### 타사 ID 동기화 컨테이너에 대한 데이터스트림 재정의 {#container-overrides}

타사 ID 동기화 컨테이너에 대한 데이터 스트림 재정의를 구성하려면 먼저 데이터 스트림을 생성해야 합니다. 다음 지침을 따르십시오 [데이터 스트림 구성](configure.md) 만들기.

데이터 스트림을 생성한 후에는 **[!UICONTROL 고급 옵션]** 및 활성화 **[!UICONTROL 타사 ID 동기화]** 옵션을 선택합니다.

그런 다음 를 사용합니다. **[!UICONTROL 컨테이너 ID 무시]** 섹션에 아래 이미지에 표시된 대로 기본 설정을 재정의할 컨테이너 ID를 추가합니다.

>[!IMPORTANT]
>
>컨테이너 ID는 다음과 같은 숫자 값이어야 합니다. `1234567`문자열 제외: 예 `"1234567"`. 컨테이너 ID 재정의로 웹 SDK를 통해 문자열 값을 전송하면 오류가 표시됩니다.

![타사 ID 동기화 컨테이너 무시가 강조 표시된 데이터 스트림 설정을 보여 주는 데이터 스트림 UI 스크린샷입니다.](assets/overrides/override-container.png)

원하는 재정의를 추가한 후 데이터스트림 설정을 저장합니다.

이제 ID 동기화 컨테이너 재정의가 구성되어 있어야 합니다. 이제 다음을 수행할 수 있습니다 [웹 SDK를 통해 Edge Network에 재정의 전송](#send-overrides).

## 웹 SDK를 통해 Edge Network에 재정의 전송 {#send-overrides}

>[!NOTE]
>
>웹 SDK 명령을 통해 구성 재정의를 전송하는 대신 웹 SDK에 구성 재정의를 추가할 수 있습니다 [태그 확장](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

다음 이후 [데이터 스트림 재정의 구성](#configure-overrides) 이제 데이터 수집 UI에서 웹 SDK를 통해 Edge Network에 재정의를 전송할 수 있습니다.

웹 SDK를 통해 Edge Network에 재정의를 전송하는 것은 데이터스트림 구성 재정의를 활성화하는 두 번째 마지막 단계입니다.

데이터 스트림 구성 재정의는 다음을 통해 Edge Network로 전송됩니다. `edgeConfigOverrides` Web SDK 명령. 이 명령은 로 전달되는 데이터 스트림 재정의를 생성합니다. [!DNL Edge Network] 다음 명령에서 또는 `configure` 모든 요청에 대해 명령을 실행합니다.

다음 `edgeConfigOverrides` 이 명령은에 전달되는 데이터 스트림 무시를 생성합니다. [!DNL Edge Network] 다음 명령에서 또는 의 경우 `configure`모든 요청에 대해

구성 재정의가 `configure` 다음 웹 SDK 명령에 포함되어 있습니다.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [구성](../edge/fundamentals/configuring-the-sdk.md)

전체적으로 지정된 옵션은 개별 명령의 구성 옵션으로 재정의할 수 있습니다.

### 를 통해 구성 재정의 전송 `sendEvent` 명령 {#send-event}

아래 예제는 다음에서 구성 재정의가 표시되는 모습을 보여 줍니다. `sendEvent` 명령입니다.

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
| `edgeConfigOverrides.datastreamId` | 단일 요청이 로 정의된 데이터 스트림이 아닌 다른 데이터 스트림으로 이동할 수 있도록 하려면 이 매개 변수를 사용하십시오. `configure` 명령입니다. |

### 를 통해 구성 재정의 전송 `configure` 명령 {#send-configure}

아래 예제는 다음에서 구성 재정의가 표시되는 모습을 보여 줍니다. `configure` 명령입니다.

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

### 페이로드 예 {#payload-example}

위의 예에서는 [!DNL Edge Network] 다음과 같은 페이로드:

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
