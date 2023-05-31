---
title: Adobe Experience Platform Web SDK를 사용하여 개인화된 콘텐츠 렌더링
description: Adobe Experience Platform Web SDK를 사용하여 개인화된 콘텐츠를 렌더링하는 방법에 대해 알아봅니다.
keywords: 개인화;renderDecisions;sendEvent;의사 결정 범위;제안;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 378f222b5c673632ce5792c52fc32410106def37
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 개인화된 콘텐츠 렌더링

Adobe Experience Platform Web SDK는 다음을 포함한 Adobe 개인화 솔루션에서 개인화된 콘텐츠 검색을 지원합니다. [Adobe Target](https://business.adobe.com/products/target/adobe-target.html), [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=ko) 및 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=ko).

또한 웹 SDK는 다음과 같은 Adobe Experience Platform 개인화 대상을 통해 동일한 페이지 및 다음 페이지 개인화 기능을 지원합니다. [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 지정 개인화 연결](../../destinations/catalog/personalization/custom-personalization.md). 동일 페이지 및 다음 페이지 개인화에 대한 Experience Platform을 구성하는 방법에 대해 알아보려면 다음을 참조하십시오. [전용 안내서](../../destinations/ui/activate-edge-personalization-destinations.md).

Adobe Target 내에서 만들어진 컨텐츠 [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 그리고 Adobe Journey Optimizer [웹 캠페인 UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 는 SDK를 통해 자동으로 검색 및 렌더링할 수 있습니다. Adobe Target 내에서 만들어진 컨텐츠 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 또는 Offer decisioning은 SDK에서 자동으로 렌더링할 수 없습니다. 대신 SDK를 사용하여 이 콘텐츠를 요청한 다음 직접 콘텐츠를 수동으로 렌더링해야 합니다.

## 자동으로 콘텐츠 렌더링

서버에 이벤트를 보낼 때 `renderDecisions` 옵션 대상 `true`. 이렇게 하면 SDK가 자동 렌더링에 적합한 개인화된 콘텐츠를 자동으로 렌더링합니다.

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

개인화된 콘텐츠를 렌더링하는 것은 비동기적이므로 특정 콘텐츠가 렌더링을 완료한 시기에 대해 가정해서는 안 됩니다.

## 수동으로 컨텐츠 렌더링

개인화 콘텐츠에 액세스하려면 SDK가 서버로부터 성공적인 응답을 받은 후에 호출되는 콜백 함수를 제공할 수 있습니다. 콜백에 대한 `result` 개체(포함 가능) `propositions` 반환된 개인화 콘텐츠가 포함된 속성입니다. 다음은 이벤트를 전송할 때 콜백 함수를 제공하는 방법의 예입니다.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

이 예에서는 `result.propositions`가 존재하는 경우 는 이벤트와 관련된 개인화 제안이 포함된 배열입니다. 기본적으로 자동 렌더링에 적합한 제안만 포함됩니다.

다음 `propositions` 배열은 다음 예제와 유사할 수 있습니다.

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

이 예에서는 `renderDecisions` 옵션이 로 설정되지 않았습니다. `true` 다음과 같은 경우 `sendEvent` 명령이 실행되었으므로 SDK는 콘텐츠를 자동으로 렌더링하지 않았습니다. 그러나 SDK는 자동 렌더링에 적합한 콘텐츠를 계속 자동으로 검색했으며, 원하는 경우 수동으로 렌더링하도록 제공했습니다. 각 제안 객체에는 다음과 같은 항목이 있습니다 `renderAttempted` 속성이 로 설정됨 `false`.

대신 를 설정했다면 `renderDecisions` 옵션 대상 `true` 이벤트를 보낼 때 SDK는 자동 렌더링에 적합한 제안을 렌더링하려고 시도했을 것입니다(앞에서 설명한 대로). 그 결과, 각각의 제안 대상은 다음을 가질 것이다 `renderAttempted` 속성이 로 설정됨 `true`. 이 경우 이러한 제안을 수동으로 렌더링할 필요가 없습니다.

지금까지 자동 렌더링에 적합한 개인화 콘텐츠(즉, Adobe Target의 시각적 경험 작성기 또는 Adobe Journey Optimizer의 웹 캠페인 UI에서 만들어진 모든 콘텐츠)에 대해서만 논의했습니다. 개인화 콘텐츠를 검색하려면 _아님_ 자동 렌더링에 사용할 수 있는 경우 `decisionScopes` 이벤트를 보낼 때 옵션을 선택합니다. 범위는 서버에서 검색할 특정 제안을 식별하는 문자열입니다.

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

이 예제에서 일치하는 서버에 제안이 있는 경우 `salutation` 또는 `discount` 범위, 반환되고 `result.propositions` 배열입니다. 자동 렌더링에 적합한 제안이 계속 `propositions` 구성 방식에 관계없이 스토리지 시스템 `renderDecisions` 또는 `decisionScopes` 옵션. 다음 `propositions` 이 경우 배열은 다음 예제와 유사합니다.

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

이 시점에서 맞춤법이 보이는 대로 제안 콘텐츠를 렌더링할 수 있습니다. 이 예에서 제안과 일치하는 `discount` scope는 Adobe Target의 양식 기반 경험 작성기를 사용하여 작성된 HTML 제안입니다. 페이지에 ID가 인 요소가 있다고 가정합니다. `daily-special` 및 의 콘텐츠를 렌더링하고 싶습니다. `discount` 제안 내용: `daily-special` 요소를 만들려면 다음을 수행하십시오.

1. 에서 제안 추출 `result` 개체.
1. 각 제안을 반복하고 다음 범위의 제안을 찾습니다. `discount`.
1. 명제를 찾으면 명제의 각 항목을 반복하여 HTML 콘텐츠인 항목을 찾습니다. (가정하는 것보다 확인하는 것이 좋습니다.)
1. HTML 콘텐츠가 들어 있는 항목을 찾으면 `daily-special` 요소를 만들고 해당 HTML을 개인화된 콘텐츠로 바꿉니다.
1. 콘텐츠가 렌더링되면 `display` 이벤트.

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
>Adobe Target을 사용하는 경우 범위는 서버의 mbox에 해당하지만 개별적으로 요청되는 것이 아니라 한 번에 모두 요청됩니다. 글로벌 mbox는 항상 반환됩니다.

### 플리커 관리

SDK는에 기능을 제공합니다. [깜박임 관리](../personalization/manage-flicker.md) 개인화 프로세스 동안.

## 지표를 증가시키지 않고 단일 페이지 애플리케이션에서 제안 렌더링 {#applypropositions}

다음 `applyPropositions` 명령을 사용하면 제안 배열을 렌더링하거나 다음에서 실행할 수 있습니다 [!DNL Target] 을 증가시키지 않고 단일 페이지 애플리케이션으로 [!DNL Analytics] 및 [!DNL Target] 지표. 이렇게 하면 보고 정확도가 높아집니다.

>[!IMPORTANT]
>
>에 대한 제안인 경우 `__view__` 범위(또는 웹 표면)가 페이지 로드 시 렌더링됩니다. `renderAttempted` 플래그가 로 설정됩니다. `true`. 다음 `applyPropositions` 명령은 를 다시 렌더링하지 않습니다. `__view__` 다음과 같은 범위(또는 웹 표면) 제안 `renderAttempted: true` 플래그.

### 사용 사례 1: 단일 페이지 애플리케이션 뷰 제안 다시 렌더링

아래 샘플에 설명된 사용 사례는 디스플레이 알림을 보내지 않고 이전에 가져와서 렌더링된 장바구니 보기 제안을 다시 렌더링합니다.

아래 예에서는 `sendEvent` 명령은 보기 변경 시 트리거되고 결과 개체를 상수에 저장합니다.

다음으로, 보기 또는 구성 요소가 업데이트되면 `applyPropositions` 명령을 호출하면 앞의 명제를 사용합니다. `sendEvent` 명령을 사용하여 뷰 제안을 다시 렌더링합니다.

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

### 사용 사례 2: 선택기가 없는 제안 렌더링

이 사용 사례는 다음을 사용하여 작성된 활동 오퍼에 적용됩니다. [!DNL Target Form-based Experience Composer].

에 선택기, 작업 및 범위를 제공해야 합니다. `applyPropositions` 호출합니다.

지원됨 `actionTypes` 은(는)

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

결정 범위에 대한 메타데이터를 제공하지 않으면 관련 제안이 렌더링되지 않습니다.
