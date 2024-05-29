---
title: mediaCollection
description: 웹 속성에서 미디어 사용과 관련된 데이터를 수집하도록 웹 SDK를 구성합니다.
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---


# `streamingMedia`

다음 `streamingMedia` 구성 요소는 웹 사이트에서 미디어 세션과 관련된 데이터를 수집하는 데 도움이 됩니다.

수집된 데이터에는 미디어 재생, 일시 정지, 완료 및 기타 관련 이벤트에 대한 정보가 포함될 수 있습니다. 수집되면 이 데이터를 Adobe Experience Platform 및/또는 Adobe Analytics으로 전송하여 보고서를 생성할 수 있습니다. 이 기능은 웹 사이트에서의 미디어 소비 행동을 추적하고 이해하는 포괄적인 솔루션을 제공합니다.

## 전제 조건 {#prerequisites}

을(를) 사용하려면 `streamingMedia` Web SDK의 구성 요소에서는 다음 사전 요구 사항을 충족해야 합니다.

* Adobe Experience Platform 및/또는 Adobe Analytics에 액세스할 수 있는지 확인하십시오.
* 웹 SDK 버전 2.20.0 이상을 사용해야 합니다. 다음을 참조하십시오. [Web SDK 설치 개요](../../install/overview.md) 최신 버전을 설치하는 방법을 알아봅니다.
* 활성화 **[[!UICONTROL 미디어 분석]](../../../datastreams/configure.md#advanced-options)** 사용 중인 데이터 스트림에 대한 옵션입니다.
* 데이터 스트림에서 사용하는 스키마에 미디어 컬렉션 스키마 필드가 포함되어 있는지 확인합니다.
* 다음 페이지를 통해 이 페이지에 표시된 대로 웹 SDK 구성에서 Streaming Media 기능을 구성합니다 [태그 확장](#tag-extension) 또는 을 통해 [JavaScript 라이브러리](#library).

## 웹 SDK 태그 확장을 사용하여 Streaming Media 구성 {#tag-extension}

웹 SDK 태그 확장에서 스트리밍 미디어를 구성하려면 아래 단계를 따르십시오.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 구성 **[!UICONTROL 스트리밍 미디어]** 다음에 설명된 대로 설정 [웹 SDK 태그 확장 구성 페이지](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## 웹 SDK JavaScript 라이브러리를 사용하여 Streaming Media 구성 {#library}

Web SDK에서 Streaming Media를 구성하려면 아래에 설명된 속성을 사용합니다.

호출 시 `configure` 명령, 추가 `streamingMedia` 개체.

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| 속성 | 유형 | 필수 여부 | 설명 |
|---------|----------|---------|---------|
| `channel` | 문자열 | 예 | 스트리밍 미디어 컬렉션이 발생하는 채널의 이름입니다. 예: `Video channel`. |
| `playerName` | 문자열 | 예 | 미디어 플레이어의 이름입니다. |
| `appVersion` | 문자열 | 아니요 | 미디어 플레이어 애플리케이션의 버전입니다. |
| `mainPingInterval` | 정수 | 아니요 | 기본 콘텐츠에 대한 Ping 빈도(초). 기본값은 `10`입니다. 값의 범위는 다음과 같습니다. `10` 끝 `50` 초.  값을 지정하지 않으면 를 사용할 때 기본값이 사용됩니다 [자동으로 추적된 세션](../createmediasession.md#automatic). |
| `adPingInterval` | 정수 | 아니요 | 광고 콘텐츠에 대한 Ping 빈도(초)입니다. 기본값은 `10`입니다. 값의 범위는 다음과 같습니다. `1` 끝 `10` 초. 값을 지정하지 않으면 를 사용할 때 기본값이 사용됩니다 [자동으로 추적된 세션](../createmediasession.md#automatic). |
