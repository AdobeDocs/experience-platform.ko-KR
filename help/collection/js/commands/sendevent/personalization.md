---
title: 개인화
description: 다양한 사용자에게 다양한 콘텐츠를 렌더링하여 개인화된 환경을 만듭니다.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

`personalization` 개체는 요청된 개인화 결정(오퍼 또는 제안)과 요청 및 응답에서 처리되는 방법을 구성합니다. 이 기능은 사용자별로 표시된 콘텐츠를 사용자 지정할 수 있는 원동력이므로 Adobe Target 또는 Adobe Journey Optimizer 구현에서 특히 중요합니다.

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

`personalization` 개체에 다음 속성이 포함되어 있습니다.

## `personalization.decisionScopes`

`decisionScopes` 속성은 웹 SDK에서 개인화 결정을 검색하고 반환하도록 지시하는 문자열 배열입니다. 배열의 각 항목은 개인화된 콘텐츠가 필요한 위치, 컨텍스트 또는 논리적 배치를 식별합니다.

이 속성은 페이지의 특정 영역 또는 구성 요소에 대해 개인화된 콘텐츠를 명시적으로 가져오려는 경우에 유용합니다. 특히 사용자의 탐색 또는 보기 변경 시 다른 오퍼 세트가 필요할 수 있는 단일 페이지 애플리케이션에서 유용합니다. 이 속성을 사용하면 사용자와 관련된 UI 요소에 대한 오퍼만 검색하여 성능을 최적화할 수도 있습니다.

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

Adobe Target에서 각 결정 범위는 mbox 또는 활동에 매핑됩니다. Adobe Journey Optimizer에서 각 의사 결정 범위는 의사 결정 기반 웹 콘텐츠 배치 또는 캠페인에 매핑됩니다. Offer Decisioning에서 결정 범위는 방문자가 받아야 하는 오퍼 또는 제안에 매핑됩니다.

>[!TIP]
>
>전역 범위를 요청(또는 차단)하려면 [`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled)에서 지정하지 않고 `decisionScopes`을(를) 사용하십시오.

## `personalization.surfaces`

`surfaces` 속성은 개인화가 요청된 채널, 장치 또는 컨텍스트를 수동으로 정의하는 [표면 URI](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri) 문자열의 배열입니다. 이를 통해 크로스 채널 생태계 내에서 도메인, 앱 또는 디바이스 플랫폼과 같은 서로 다른 디지털 경험을 구별할 수 있습니다. 기본적으로 라이브러리는 현재 페이지의 기본 표면을 유추합니다. 이 속성을 사용하여 현재 페이지에 대해 자동으로 추론된 표면을 재정의할 수 있습니다.

이 속성은 크로스 채널 개인화를 사용하려는 경우 유용하며, 개별 채널 간에 개인화가 작동하는 방식을 구별해야 합니다. 이를 통해 동일한 Adobe Experience Platform 조직 아래에 있는 서로 다른 사이트에 대해 고유한 오퍼를 만들 수 있습니다.

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

이 속성은 Adobe Journey Optimizer 캠페인 및 표면 관리에서 설정된 표면과 일치하므로 Journey Optimizer에서 기본적으로 사용됩니다.

## `personalization.schemas`

`schemas` 속성은 Edge Network에서 요청한 개인화 콘텐츠 형식을 필터링하는 스키마 URI 문자열의 배열입니다. 이 속성을 설정하면 Adobe에서 받는 응답이 지정한 콘텐츠 유형 정의와 일치하는 오퍼만 포함하도록 제한됩니다. 생략하면 라이브러리는 일치하는 범위 또는 표면에 대해 사용 가능한 모든 스키마의 오퍼를 요청합니다.

이 속성은 응답 크기를 최적화하는 데 도움이 되며 웹 사이트 또는 애플리케이션이 처리할 수 있는 오퍼 형식만 받도록 합니다. 또한 DOM 작업만 사용하거나 JSON 개체만 사용하는 등 특정 방식으로 개인화된 콘텐츠를 렌더링하는 단일 페이지 애플리케이션과 함께 사용할 때도 유용합니다.

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

지원되는 스키마 URI:

* **`https://ns.adobe.com/personalization/dom-action`**: 직접 DOM 작업이며 일반적으로 Adobe Target의 시각적 경험 작성기에서 생성되는 오퍼입니다. 여기에는 추가 코드 없이 페이지에서 요소를 자동으로 조작하는 지침이 포함되어 있습니다. 자동 렌더링된 웹 개인화의 표준입니다.
* **`https://ns.adobe.com/personalization/html-content-item`**: 문자열로 전달된 원시 HTML이 포함된 오퍼입니다. 구현에서는 일반적으로 이 콘텐츠를 페이지의 원하는 위치에 삽입하므로 DOM 작업보다 더 세밀하게 제어할 수 있습니다. 배너, 코드 조각 또는 모달 콘텐츠에 일반적으로 사용됩니다.
* **`https://ns.adobe.com/personalization/json-content-item`**: JSON 개체 형식의 오퍼입니다. HTML 또는 DOM 변경 대신 구조화된 데이터를 기대하는 API 기반 구현 또는 프론트엔드에서 가장 일반적으로 사용됩니다.
* **`https://ns.adobe.com/personalization/redirect-item`**: 다른 URL로 리디렉션하는 오퍼입니다. 랜딩 페이지나 온보딩 흐름과 같은 타겟팅 또는 의사 결정 논리를 기반으로 사용자를 새 페이지로 이동하는 데 사용됩니다.
* **`https://ns.adobe.com/personalization/ruleset-item`**: 클라이언트측 규칙 엔진을 구동하는 비즈니스 논리 블록을 제공합니다. 논리적 조건 및 결과(if/then personalization logic)를 정의하는 버전이 지정된 규칙 세트를 포함합니다.
* **`https://ns.adobe.com/personalization/message/in-app`**: Adobe Journey Optimizer 인앱 메시지를 위해 특별히 형식이 지정된 오퍼로서, 일반적으로 모달, 배너, 팝업 또는 오버레이로 렌더링됩니다.
* **`https://ns.adobe.com/personalization/message/content-card`**: 웹 또는 모바일 앱에서 영구적 또는 받은 편지함 스타일 피드를 위해 설계된 Adobe Journey Optimizer 콘텐츠 카드용으로 특별히 형식이 지정된 오퍼입니다.
* **`https://ns.adobe.com/personalization/message/native-alert`**: 특히 Adobe Journey Optimizer 기본 알림용으로 형식이 지정된 오퍼로서, 플랫폼 기본 알림 대화 상자를 트리거합니다.
* **`https://ns.adobe.com/personalization/measurement`**: 개인화된 오퍼의 클릭 수 및 상호 작용을 추적하는 데 사용됩니다. 렌더링할 수 있는 콘텐츠를 포함하지 않습니다.
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**: 로컬 저장소에서 방문자의 이벤트 내역을 변경하기 위한 스키마입니다. 게재되거나 차단된 경험을 추적하기 위해 SDK에서 내부적으로 사용됩니다. 렌더링할 수 있는 콘텐츠를 포함하지 않습니다.
* **`https://ns.adobe.com/personalization/default-content-item`**: 대체 콘텐츠 또는 기본 콘텐츠(일반적으로 적합한 개인화된 오퍼가 없을 때). 이렇게 하면 자격을 갖추지 않은 사용자도 일관되게 컨텐츠를 받을 수 있습니다.

## `personalization.sendDisplayEvent`

`sendDisplayEvent` 속성은 개인화된 콘텐츠가 페이지에서 렌더링되는 즉시 표시 알림 이벤트가 Edge Network으로 자동으로 전송되는지 여부를 결정하는 부울입니다. 생략하면 기본값은 `true`입니다. 개인화된 콘텐츠가 노출 추적을 위해 렌더링되었음을 표시하지 않으려면 이 변수를 `false`(으)로 설정하십시오.

이 변수를 `false`(으)로 설정하는 가장 일반적인 사용 사례는 표시 이벤트에 플래그를 지정하는 다른 명령을 구현에 보낼 때입니다. 일부 구현에는 노출 횟수와 Analytics 이벤트가 모두 있습니다. 이 속성을 사용하면 노출 횟수를 늘리는 `sendEvent` 명령을 완벽하게 제어할 수 있습니다.

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>이전 버전의 웹 SDK(버전 2.12.0 및 이전 버전)에서는 대신 `sendDisplayNotifications`을(를) 사용합니다.

## `personalization.includePendingDisplayNotifications`

`includePendingDisplayNotifications` 속성은 보류 중인 표시 알림이 현재 `sendEvent` 호출에 번들로 제공되는지 여부를 제어하는 부울입니다. 보류 중인 표시 알림은 렌더링되었지만 표시 이벤트로 Edge Network에 아직 보고되지 않은 개인화된 콘텐츠에 대한 노출입니다. 이 속성은 개인화된 콘텐츠와 `sendEvent` 호출이 서로 비동기화될 수 있으므로 단일 페이지 응용 프로그램을 사용할 때 유용합니다.

이 속성의 기본값은 `false`입니다. 대기 중인 표시 알림을 일괄 처리하여 그 노출 횟수를 정확하게 기록하려면 이 속성을 `true`(으)로 설정하십시오. 기존 웹 사이트와 같은 동기식 구현은 일반적으로 이 속성을 설정할 필요가 없습니다.

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

`defaultPersonalizationEnabled` 속성은 웹 SDK에서 기본 페이지 단위 개인화 범위(`__view__`)를 요청하고 이 `sendEvent` 명령에 대해 표시되는 방법을 명시적으로 제어할 수 있는 부울입니다. 기본적으로 페이지 로드 후 첫 번째 `sendEvent` 명령에서 웹 SDK 요청은 기본 페이지 단위 개인화 범위 및 관련 표면에 대한 오퍼를 제공합니다. 후속 `sendEvent` 명령은 기본 개인화를 요청하지 않습니다. 이 속성을 사용하여 해당 동작을 재정의할 수 있습니다. 사용자가 사이트를 탐색할 때 기본 개인화를 다시 요청할 수 있는 단일 페이지 애플리케이션 구현에서 유용합니다. 오퍼 검색을 복제하지 않고 _only_&#x200B;에서 표시 이벤트를 보내려는 경우에도 이 속성을 사용할 수 있습니다.

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

이 속성은 설정 방법에 따라 다음 논리를 사용합니다.

* **설정되지 않음**: 아직 요청되지 않은 경우 기본 개인화를 요청합니다. 기본 개인화는 일반적으로 페이지 로드 후 첫 번째 `sendEvent`에 요청되지만, 동일한 페이지의 후속 `sendEvent` 호출에서는 다시 요청되지 않습니다. 이 속성을 설정하면 이 동작이 무시됩니다.
* **`true`**: 이 `sendEvent` 명령이 페이지 로드 후 처음이 아닌 경우에도 페이지 범위 및 기본 표면을 명시적으로 요청합니다. 이 속성을 `true`(으)로 설정하는 데 이상적인 시간은 단일 페이지 애플리케이션 시나리오와 같이 기본 개인화 요청을 적용해야 하는 때입니다.
* **`false`**: 이 `sendEvent` 명령이 페이지 로드 후 처음인 경우에도 페이지 범위 및 기본 표면에 대한 요청을 명시적으로 표시하지 않습니다. 이 속성을 `false`(으)로 설정하는 데 이상적인 시간은 지정된 `sendEvent` 명령이 새 오퍼를 요청하지 않고 대신 Analytics로 데이터를 보내거나 디스플레이 이벤트를 보내도록 하는 경우입니다.

## 웹 SDK 태그 확장을 사용하는 Personalization 구성 요소

&#39;[**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields)&#39; 작업을 구성할 때 이 속성에 해당하는 웹 SDK 태그 확장은 [!UICONTROL Send event] 섹션입니다.
