---
title: 스트리밍 미디어
description: 웹 속성에서 미디어 사용과 관련된 데이터를 수집하도록 웹 SDK를 구성합니다.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# `streamingMedia`

`streamingMedia` 구성 요소를 사용하여 웹 사이트에서 미디어 세션과 관련된 데이터를 수집할 수 있습니다.

수집된 데이터에는 미디어 재생, 일시 정지, 완료 및 기타 관련 이벤트에 대한 정보가 포함될 수 있습니다. 수집되면 이 데이터를 Adobe Experience Platform 및/또는 Adobe Analytics으로 전송하여 보고서를 생성할 수 있습니다. 이 기능은 웹 사이트에서의 미디어 소비 행동을 추적하고 이해하는 포괄적인 솔루션을 제공합니다.

## 전제 조건 {#prerequisites}

Web SDK의 `streamingMedia` 구성 요소를 사용하려면 다음 사전 요구 사항을 충족해야 합니다.

* Adobe Experience Platform 및/또는 Adobe Analytics에 액세스할 수 있는지 확인하십시오.
* 웹 SDK 버전 2.20.0 이상을 사용해야 합니다. 최신 버전을 설치하는 방법을 알아보려면 [웹 SDK 설치 개요](../../install/overview.md)를 참조하세요.
* 사용 중인 데이터 스트림에 대해 **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** 옵션을 사용하도록 설정하십시오.
* 데이터 스트림에서 사용하는 스키마에 미디어 컬렉션 스키마 필드가 포함되어 있는지 확인합니다.
* [태그 확장](#tag-extension) 또는 [JavaScript 라이브러리](#library)를 통해 이 페이지에 표시된 대로 웹 SDK 구성에서 Streaming Media 기능을 구성합니다.

## 웹 SDK 태그 확장을 사용하여 Streaming Media 구성 {#tag-extension}

웹 SDK 태그 확장에서 스트리밍 미디어를 구성하려면 아래 단계를 따르십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [Web SDK 태그 확장 구성 페이지](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection)에 설명된 대로 **[!UICONTROL Streaming Media]** 설정을 구성합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 Streaming Media 구성 {#library}

Web SDK에서 Streaming Media를 구성하려면 아래에 설명된 속성을 사용합니다.

`configure` 명령을 호출할 때 `streamingMedia` 개체를 추가합니다.

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
| `mainPingInterval` | 정수 | 아니요 | 기본 콘텐츠에 대한 Ping 빈도(초). 기본값은 `10`입니다. 값의 범위는 `10`초에서 `50`초까지입니다.  값을 지정하지 않으면 [자동으로 추적된 세션](../createmediasession.md#automatic)을 사용할 때 기본값이 사용됩니다. |
| `adPingInterval` | 정수 | 아니요 | 광고 콘텐츠에 대한 Ping 빈도(초)입니다. 기본값은 `10`입니다. 값의 범위는 `1`초에서 `10`초까지입니다. 값을 지정하지 않으면 [자동으로 추적된 세션](../createmediasession.md#automatic)을 사용할 때 기본값이 사용됩니다. |
