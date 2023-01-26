---
title: Adobe Experience Platform Web SDK를 사용하여 개인화된 컨텐츠 렌더링
description: Adobe Experience Platform Web SDK를 사용하여 개인화된 컨텐츠를 렌더링하는 방법을 알아봅니다.
keywords: 개인화;renderDecisions;sendEvent;decisions;proposition;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: c75a8bdeaba67259b5f4b4ce025d5e128d763040
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 개인화된 콘텐츠 렌더링

Adobe Experience Platform Web SDK는 다음을 포함한 Adobe 개인화 솔루션에서 개인화된 컨텐츠 검색을 지원합니다 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html), [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=ko) 및 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=ko).

또한 웹 SDK는 다음과 같은 Adobe Experience Platform 개인화 대상을 통한 동일한 페이지 및 다음 페이지 개인화 기능을 지원합니다 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 그리고 [사용자 지정 개인화 연결](../../destinations/catalog/personalization/custom-personalization.md). 동일한 페이지 및 다음 페이지 개인화에 대한 Experience Platform을 구성하는 방법에 대해 알아보려면 [전용 안내서](../../destinations/ui/configure-personalization-destinations.md).

Adobe Target 내에서 만들어진 컨텐츠 [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 및 Adobe Journey Optimizer [웹 캠페인 UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 는 SDK에서 자동으로 검색 및 렌더링할 수 있습니다. Adobe Target 내에서 만들어진 컨텐츠 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 또는 SDK에서 자동으로 Offer decisioning을 렌더링할 수 없습니다. 대신 SDK를 사용하여 이 콘텐츠를 요청한 다음, 직접 콘텐츠를 수동으로 렌더링해야 합니다.

## 컨텐츠 자동 렌더링

이벤트를 서버로 보낼 때 `renderDecisions` 옵션 `true`. 이렇게 하면 SDK가 자동 렌더링에 적합한 개인화된 콘텐츠를 자동으로 렌더링합니다.

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

개인화 컨텐츠에 액세스하기 위해 SDK가 서버로부터 성공적인 응답을 받은 후 호출되는 콜백 함수를 제공할 수 있습니다. 콜백에서 `result` 개체를 포함할 수 있습니다. `propositions` 반환된 개인화 콘텐츠를 포함하는 속성입니다. 다음은 이벤트를 전송할 때 콜백 함수를 제공하는 방법의 예입니다.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

이 예제에서는 `result.propositions`인 경우 은 이벤트와 관련된 개인화 proposition이 포함된 배열입니다. 기본적으로 자동 렌더링에 적합한 포지션만 포함됩니다.

다음 `propositions` 배열은 다음 예제와 비슷합니다.

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
    "scopeDetails": {
      ...
    },
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
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

예제에서는 `renderDecisions` 옵션을 로 설정하지 않았습니다. `true` http 화이트보드 `sendEvent` 명령이 실행되었으므로 SDK는 컨텐츠를 자동으로 렌더링하지 않았습니다. 그러나 SDK는 자동 렌더링에 적합한 콘텐츠를 여전히 자동으로 검색하며, 원할 경우 수동으로 렌더링하도록 이 콘텐츠를 사용자에게 제공했습니다. 각 제안 객체에는 `renderAttempted` 속성 설정 `false`.

대신 를 설정했다면 `renderDecisions` 옵션 `true` 이벤트를 전송할 때 SDK는 이전에 설명한 대로 자동 렌더링에 적합한 모든 제안을 렌더링하려고 했습니다. 따라서 각각의 제안 객체에는 `renderAttempted` 속성 설정 `true`. 이 경우 이러한 제안을 수동으로 렌더링할 필요가 없습니다.

지금까지 자동 렌더링이 가능한 개인화 콘텐츠(즉, Adobe Target의 시각적 경험 작성기 또는 Adobe Journey Optimizer의 웹 캠페인 UI에서 만든 모든 콘텐츠)에 대해서만 논의했습니다. 개인화 콘텐츠를 검색하려면 _not_ 자동 렌더링에 적합한 경우 `decisionScopes` 옵션을 선택합니다. 범위는 서버에서 검색할 특정 제안을 식별하는 문자열입니다.

다음은 한 예입니다.

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

이 예에서, `salutation` 또는 `discount` 범위, 반환 및 `result.propositions` 배열입니다. 자동 렌더링에 대한 Proposition은 `propositions` 구성 방식에 관계없이 `renderDecisions` 또는 `decisionScopes` 옵션. 다음 `propositions` 이 경우 array 는 다음 예제와 비슷합니다.

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
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
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
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
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
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
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
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

이 시점에서 제안 콘텐츠를 적절히 렌더링할 수 있습니다. 이 예에서 다음과 일치하는 제안 `discount` 범위는 Adobe Target의 양식 기반 경험 작성기를 사용하여 작성된 HTML 제안입니다. 페이지에 ID가 인 요소가 있다고 가정할 때 `daily-special` 에서 콘텐츠를 렌더링하려는 경우 `discount` 제안 `daily-special` 요소를 만들려면 다음을 수행하십시오.

1. 에서 proposition 추출 `result` 개체.
1. 각각의 제안을 반복하고, 다음 범위의 제안을 찾습니다. `discount`.
1. 제안을 찾으면, 제안에 있는 각 항목을 반복하여 HTML 콘텐츠인 항목을 찾습니다. (가정하는 것보다 확인하는 것이 낫다.)
1. HTML 컨텐츠가 들어 있는 항목을 찾으면 `daily-special` HTML을 페이지의 요소로 바꾸고 콘텐츠를 개인화합니다.
1. 컨텐츠가 렌더링되면 `display` 이벤트.

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
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Adobe Target을 사용하는 경우 범위가 서버의 mbox에 해당하며 개별적으로 요청되지 않고 한 번에 모두 요청된다는 점을 제외하면 입니다. 글로벌 mbox는 항상 반환됩니다.

### 플리커 관리

SDK는 [플리커 관리](../personalization/manage-flicker.md) 개인화 프로세스 중에

## 지표를 증가시키지 않고 단일 페이지 애플리케이션에서 제안 렌더링 {#applypropositions}

다음 `applyPropositions` 명령 를 사용하면 [!DNL Target] 단일 페이지 애플리케이션에 [!DNL Analytics] 및 [!DNL Target] 지표 를 참조하십시오. 따라서 보고 정확도가 높아집니다.

>[!IMPORTANT]
>
>에 대한 `__view__` 페이지 로드 시 범위(또는 웹 서피스)가 렌더링되었습니다. `renderAttempted` 플래그가 로 설정됩니다. `true`. 다음 `applyPropositions` 명령은 다시 렌더링되지 않습니다. `__view__` 범위(또는 웹 서피스) proposition이 `renderAttempted: true` 플래그.

### 사용 사례 1: 단일 페이지 애플리케이션 보기 제안 다시 렌더링

아래 샘플에 설명된 사용 사례는 디스플레이 알림을 보내지 않고 이전에 가져온 후 렌더링된 장바구니 보기 제안을 다시 렌더링합니다.

아래 예에서는 `sendEvent` 명령은 뷰 변경 시 트리거되며 결과 객체를 상수로 저장합니다.

그런 다음 보기 또는 구성 요소가 업데이트되면 `applyPropositions` 이전 명령의 proposition과 함께 명령이 호출됩니다. `sendEvent` 명령, 보기 등록 정보를 다시 렌더링합니다.

```js
var cartPropositions = alloy("sendEvent", {
    renderDecisions: true,
    xdm: {
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    propositions: cartPropositions
});
```

### 사용 사례 2: 선택기가 없는 프로필 렌더링

이 사용 사례는 를 사용하여 작성된 활동 오퍼에 적용됩니다. [!DNL Target Form-based Experience Composer].

에서 선택기, 작업 및 범위를 제공해야 합니다 `applyPropositions` 호출.

지원됨 `actionTypes` 입니다.

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    decisionScopes: ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        propositions: retrievedPropositions,
        metadata: {
            salutation: {
                selector: "#first-form-based-offer",
                actionType: "setHtml"
            },
            discount: {
                selector: "#second-form-based-offer",
                actionType: "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: renderedPropositions
                    }
                }
            }
        });
    });
});
```

결정 범위에 대한 메타데이터를 제공하지 않으면 연결된 제안이 렌더링되지 않습니다.
