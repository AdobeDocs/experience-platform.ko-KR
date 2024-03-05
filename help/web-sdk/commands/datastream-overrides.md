---
title: 데이터 스트림 구성 재정의
description: Web SDK를 통해 데이터 스트림 재정의를 구성하는 방법에 대해 알아봅니다.
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

---


# 데이터스트림 재정의 구성

다음 `edgeConfigOverrides` 개체를 사용하면 현재 페이지에서 실행되는 명령에 대한 구성 설정을 재정의할 수 있습니다. 이 재정의 개체는 명령이 아니라 대부분의 웹 SDK 명령에 포함할 수 있는 개체입니다.

이 개체는 국가별로 다른 웹 사이트 또는 하위 도메인이 있거나 여러 비즈니스 단위에 맞는 데이터를 저장할 여러 개의 Experience Platform 샌드박스가 있는 경우에 유용합니다.

>[!IMPORTANT]
>
>데이터 스트림 재정의에 대한 자세한 전체 구성 지침은 다음을 참조하십시오. [데이터 스트림 구성 무시](../../datastreams/overrides.md#configure-overrides) 설명서를 참조하십시오.

데이터 스트림 구성 재정의는 2단계 프로세스입니다.

1. 먼저, 데이터 스트림 구성 재정의를 [데이터스트림 구성 페이지](../../datastreams/configure.md): 데이터 스트림 UI 내에서 실행할 수 있습니다. 다음을 참조하십시오. [데이터 스트림 구성 무시](../../datastreams/overrides.md#configure-overrides) 재정의 구성 방법에 대한 지침은 설명서를 참조하십시오.
2. UI에서 데이터 스트림 재정의를 구성한 후에는 다음 방법 중 하나로 재정의를 Edge Network에 보내야 합니다.
   * Web SDK를 통해 [태그 확장](#tag-extension).
   * 다음을 통해 `sendEvent` 또는 `configure` Web SDK 명령.
   * Mobile SDK를 통해 `sendEvent` 명령입니다.

웹 SDK 구성과 특정 명령(예: )에서 모두 재정의를 설정하는 경우 [`sendEvent`](sendevent/overview.md)), 특정 명령의 재정의가 우선합니다.

## 개체 속성

이 개체 내에서 다음 속성을 사용할 수 있습니다.

* **데이터 스트림 재정의**: 다른 데이터스트림으로 호출을 전송합니다. 이 값을 설정하는 경우 데이터 스트림 구성이 필요한 다른 재정의는 여기에 설정된 데이터 스트림에서 구성해야 합니다.
* **타사 ID 동기화 컨테이너**: Adobe Audience Manager의 대상 타사 ID 동기화 컨테이너의 ID입니다. 이 필드를 사용하기 전에 데이터 스트림의 설정에서 타사 ID 컨테이너 재정의를 구성해야 합니다.
* **대상 속성 토큰**: Adobe Target의 대상 속성에 대한 토큰입니다. 이 필드를 사용하기 전에 데이터 스트림의 설정에서 Target 속성 토큰 재정의를 구성해야 합니다.
* **보고서 세트**: Adobe Analytics에서 재정의할 보고서 세트 ID입니다. 이 필드를 사용하기 전에 데이터 스트림의 설정에서 보고서 세트 재정의를 구성해야 합니다.

## 웹 SDK 태그 확장을 통해 Edge Network에 데이터 스트림 재정의 전송 {#tag-extension}

다음에서 설명서를 참조하십시오. [데이터 스트림 재정의 구성](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) 자세한 구성 지침은 Web SDK 태그 확장 을 참조하십시오.

웹 SDK 태그 확장에서 데이터 스트림 재정의를 구성하려면 아래에서 원하는 각 필드를 설정하십시오. **[!UICONTROL 데이터 스트림 구성 재정의]** 조건 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 **[!UICONTROL 데이터 스트림 구성 재정의]** 섹션. 원하는 각 재정의 값을 설정합니다.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

특정 명령에 대해서만 재정의를 설정하려면 태그 규칙의 작업 내에서 원하는 각 필드를 설정합니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 이벤트 보내기]**.
1. 라는 섹션으로 스크롤합니다. **[!UICONTROL 데이터 스트림 구성 재정의]**.
1. 이 섹션의 각 필드를 원하는 재정의 값으로 설정합니다.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

에 대해 별도의 필드가 제공됩니다. [!UICONTROL 개발], [!UICONTROL 스테이징], 및 [!UICONTROL 프로덕션] 환경. 각 환경에 대해 원하는 각 필드를 입력해야 합니다.

## 웹 SDK JavaScript 라이브러리를 통해 Edge Network에 재정의 전송 {#library}

다음 이후 [데이터 스트림 재정의 구성](../../datastreams/overrides.md) 데이터 수집 UI에서 이제 웹 SDK JavaScript 라이브러리를 통해 Edge Network에 재정의를 전송할 수 있습니다.

웹 SDK를 사용하는 경우 다음을 통해 Edge Network에 재정의를 전송합니다. `edgeConfigOverrides` 명령은 데이터 스트림 구성 재정의를 활성화하는 두 번째이자 마지막 단계입니다.

데이터스트림 구성 재정의는 `edgeConfigOverrides` Web SDK 명령을 통해 Edge Network로 전송됩니다. 이 명령은 로 전달되는 데이터 스트림 재정의를 생성합니다. [!DNL Edge Network] 다음 명령에서. 를 사용하는 경우 `configure` 명령을 실행하면 모든 요청에 대해 재정의가 전달됩니다.

다음 `edgeConfigOverrides` 이 명령은에 전달되는 데이터 스트림 재정의를 생성합니다. [!DNL Edge Network] 다음 명령에서.

구성 재정의가 `configure` 명령과 함께 전송되면 해당 재정의는 다음 Web SDK 명령에 포함됩니다.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [구성](../commands/configure/overview.md)

전역적으로 지정된 옵션은 개별 명령의 구성 옵션으로 재정의할 수 있습니다.

### 웹 SDK를 통해 구성 재정의 전송 `sendEvent` 명령 {#send-event}

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
          datasetId: "SampleEventDatasetIdOverride"
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
| `edgeConfigOverrides.datastreamId` | 이 매개변수를 사용하면 단일 요청이 `configure` 명령에서 정의한 데이터스트림과 다른 데이터스트림으로 이동할 수 있습니다. |
| `com_adobe_analytics.reportSuites[]` | Analytics 데이터를 전송할 보고서 세트를 결정하는 문자열 배열입니다. |
| `com_adobe_identity.idSyncContainerId` | Audience Manager 시 사용할 서드파티 ID 동기화 컨테이너입니다. |
| `com_adobe_target.propertyToken` | Adobe Target 대상 속성에 대한 토큰입니다. |

### 웹 SDK를 통해 구성 재정의 전송 `configure` 명령 {#send-configure}

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
          datasetId: "SampleProfileDatasetIdOverride"
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

| 매개변수 | 설명 |
|---|---|
| `edgeConfigOverrides.datastreamId` | 이 매개변수를 사용하면 단일 요청이 `configure` 명령에서 정의한 데이터스트림과 다른 데이터스트림으로 이동할 수 있습니다. |
| `com_adobe_analytics.reportSuites[]` | Analytics 데이터를 전송할 보고서 세트를 결정하는 문자열 배열입니다. |
| `com_adobe_identity.idSyncContainerId` | Audience Manager 시 사용할 서드파티 ID 동기화 컨테이너입니다. |
| `com_adobe_target.propertyToken` | Adobe Target 대상 속성에 대한 토큰입니다. |