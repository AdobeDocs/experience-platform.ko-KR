---
title: 데이터 스트림 구성 재정의
description: Web SDK를 통해 데이터 스트림 재정의를 구성하는 방법에 대해 알아봅니다.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

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
   * `sendEvent` 또는 `configure` 웹 SDK 명령을 통해.
   * Mobile SDK `sendEvent` 명령을 통해.

웹 SDK 구성과 특정 명령(예: [`sendEvent`](sendevent/overview.md))에서 모두 재정의를 설정하면 특정 명령의 재정의가 우선합니다.

## 개체 속성

이 개체 내에서 다음 속성을 사용할 수 있습니다.

* **데이터스트림 재정의**: 다른 데이터스트림으로 호출을 보냅니다. 이 값을 설정하는 경우 데이터 스트림 구성이 필요한 다른 재정의는 여기에 설정된 데이터 스트림에서 구성해야 합니다.
* **타사 ID 동기화 컨테이너**: Adobe Audience Manager의 대상 타사 ID 동기화 컨테이너에 대한 ID입니다. 이 필드를 사용하기 전에 데이터 스트림의 설정에서 타사 ID 컨테이너 재정의를 구성해야 합니다.
* **대상 속성 토큰**: Adobe Target의 대상 속성에 대한 토큰입니다. 이 필드를 사용하기 전에 데이터 스트림의 설정에서 Target 속성 토큰 재정의를 구성해야 합니다.
* **보고서 세트**: Adobe Analytics에서 재정의할 보고서 세트 ID. 이 필드를 사용하기 전에 데이터 스트림의 설정에서 보고서 세트 재정의를 구성해야 합니다.

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

### 웹 SDK `configure` 명령을 통해 구성 재정의 보내기 {#send-configure}

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
