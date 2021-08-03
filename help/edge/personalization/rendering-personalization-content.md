---
title: Adobe Experience Platform Web SDK를 사용하여 개인화된 컨텐츠 렌더링
description: Adobe Experience Platform Web SDK를 사용하여 개인화된 컨텐츠를 렌더링하는 방법을 알아봅니다.
keywords: 개인화;renderDecisions;sendEvent;decisions;proposition;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# 개인화된 콘텐츠 렌더링

Adobe Experience Platform 웹 SDK는 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) 및 [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=ko)을 포함하여 Adobe의 개인화 솔루션에서 개인화된 콘텐츠를 검색할 수 있도록 지원합니다. Adobe Target의 [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 내에서 만들어진 컨텐츠는 SDK에 의해 자동으로 검색되고 렌더링될 수 있습니다. Adobe Target의 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 또는 Offer decisioning 내에서 만들어진 컨텐츠는 SDK에서 자동으로 렌더링할 수 없습니다. 대신 SDK를 사용하여 이 콘텐츠를 요청한 다음, 직접 콘텐츠를 수동으로 렌더링해야 합니다.

## 컨텐츠 자동 렌더링

이벤트를 서버로 보낼 때 `renderDecisions` 옵션을 `true`(으)로 설정할 수 있습니다. 이렇게 하면 SDK가 자동 렌더링에 적합한 개인화된 콘텐츠를 자동으로 렌더링합니다.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

개인화된 컨텐츠를 렌더링하는 것은 비동기적이므로 특정 컨텐츠 조각이 렌더링을 완료했을 때를 가정해서는 안 됩니다.

## 수동으로 컨텐츠 렌더링

개인화 컨텐츠에 액세스하기 위해 SDK가 서버로부터 성공적인 응답을 받은 후 호출되는 콜백 함수를 제공할 수 있습니다. 콜백은 반환된 개인화 콘텐츠를 포함하는 `propositions` 속성을 포함할 수 있는 `result` 개체를 제공합니다. 다음은 이벤트를 전송할 때 콜백 함수를 제공하는 방법의 예입니다.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

이 예에서 `result.propositions`이 존재하면 은 이벤트와 관련된 개인화 proposition이 포함된 배열입니다. 기본적으로 자동 렌더링에 적합한 포지션만 포함됩니다.

`propositions` 배열은 다음 예제와 비슷합니다.

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

이 예제에서 `renderDecisions` 옵션이 `sendEvent` 명령이 실행될 때 `true` 로 설정되지 않았으므로 SDK가 콘텐츠를 자동으로 렌더링하려고 하지 않았습니다. 그러나 SDK는 자동 렌더링에 적합한 콘텐츠를 여전히 자동으로 검색하며, 원할 경우 수동으로 렌더링하도록 이 콘텐츠를 사용자에게 제공했습니다. 각 제안 객체에는 `renderAttempted` 속성이 `false`로 설정되어 있습니다.

이벤트를 전송할 때 대신 `renderDecisions` 옵션을 `true`(으)로 설정한 경우, SDK에서 이전에 설명한 대로 자동 렌더링에 적합한 모든 proposition을 렌더링하려고 했습니다. 따라서 각 제안 개체는 `renderAttempted` 속성이 `true`로 설정되었을 것입니다. 이 경우 이러한 제안을 수동으로 렌더링할 필요가 없습니다.

지금까지 자동 렌더링이 가능한 개인화 콘텐츠(즉, Adobe Target의 시각적 경험 작성기에서 만든 모든 콘텐츠)에만 대해 논의했습니다. 자동 렌더링에 적합하지 않은 _개인화 콘텐츠를 검색하려면 이벤트를 보낼 때 `decisionScopes` 옵션을 채워서 컨텐츠를 요청해야 합니다._ 범위는 서버에서 검색할 특정 제안을 식별하는 문자열입니다.

다음은 한 예입니다.

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

이 예에서 `salutation` 또는 `discount` 범위와 일치하는 서버에 proposition이 있으면 반환되고 `result.propositions` 배열에 포함됩니다. 자동 렌더링을 위해 자격이 있는 Proposition은 `renderDecisions` 또는 `decisionScopes` 옵션을 구성하는 방법에 관계없이 `propositions` 배열에 계속 포함됩니다. 이 경우 `propositions` 배열은 다음 예제와 비슷합니다.

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

이 시점에서 제안 콘텐츠를 적절히 렌더링할 수 있습니다. 이 예에서 `discount` 범위와 일치하는 제안은 Adobe Target의 양식 기반 경험 작성기를 사용하여 작성된 HTML 제안입니다. 페이지에 ID가 `daily-special`인 요소가 있고 `discount` 제안의 컨텐츠를 `daily-special` 요소로 렌더링하려는 경우 다음을 수행합니다.

1. `result` 개체에서 proposition을 추출합니다.
1. 각 제안을 반복하고 `discount` 범위가 있는 제안을 찾습니다.
1. 제안을 찾으면 제안에 있는 각 항목을 반복하며 HTML 콘텐츠인 항목을 찾습니다. (가정하는 것보다 확인하는 것이 낫다.)
1. HTML 콘텐츠가 들어 있는 항목을 찾으면 페이지에서 `daily-special` 요소를 찾아 해당 HTML을 개인화된 콘텐츠로 바꾸십시오.

코드는 다음과 같습니다.

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        break;
      }
    }
  }

  if (discountHtml) {
    // Discount HTML exists. Time to render it.
    var dailySpecialElement = document.getElementById("daily-special");
    dailySpecialElement.innerHTML = discountHtml;
  }
});
```


>[!TIP]
>
>Adobe Target을 사용하는 경우 범위가 서버의 mbox에 해당하며 개별적으로 요청되지 않고 한 번에 모두 요청된다는 점을 제외하면 입니다. 글로벌 mbox는 항상 반환됩니다.

### 플리커 관리

SDK는 개인화 프로세스 중에 [플리커 관리](../personalization/manage-flicker.md)에 기능을 제공합니다.
