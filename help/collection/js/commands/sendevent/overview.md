---
title: sendEvent
description: Adobe Experience Platform Edge Network으로 데이터를 전송합니다.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

`sendEvent` 명령은 Adobe으로 데이터를 보내는 기본 방법입니다. 응답 개체는 개인화된 콘텐츠, ID 및 대상자 대상을 검색하는 주요 방법입니다. [`xdm`](xdm.md) 개체를 사용하여 Adobe Experience Platform 스키마에 매핑되는 데이터를 보냅니다. [`data`](data.md) 개체를 사용하여 XDM이 아닌 데이터를 보냅니다. Adobe으로 데이터를 전송할 때 페이로드의 최대 제한은 64KB입니다.

웹 SDK의 구성된 인스턴스를 호출할 때 `sendEvent` 명령을 실행합니다. [`configure`](../configure/overview.md) 명령을 호출하기 전에 `sendEvent` 명령을 호출해야 합니다.

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## 응답 개체

이 명령을 사용하여 [응답을 처리](../command-responses.md)하기로 결정하는 경우 응답 개체에서 다음 속성을 사용할 수 있습니다.

* **`propositions`**: Edge Network에서 반환된 제안 배열. 자동으로 렌더링되는 제안에 `renderAttempted`(으)로 설정된 `true` 플래그가 포함되어 있습니다.
* **`inferences`**: 이 사용자에 대한 기계 학습 정보가 포함된 추론 개체의 배열입니다.
* **`destinations`**: Edge Network에서 반환된 대상 개체의 배열입니다.

## 웹 SDK 태그 확장을 사용하여 이벤트 보내기

이 명령에 해당하는 웹 SDK 태그 확장은 [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) 작업입니다.
