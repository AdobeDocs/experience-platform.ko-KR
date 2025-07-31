---
title: Adobe Experience Platform Web SDK을 사용하여 개인화된 콘텐츠 렌더링
description: Adobe Experience Platform 웹 SDK을 사용하여 개인화된 콘텐츠를 렌더링하는 방법을 알아봅니다.
keywords: 개인화;renderDecisions;sendEvent;의사 결정 범위;제안;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 개인화된 콘텐츠 렌더링

Adobe Experience Platform Web SDK은 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html), [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=ko) 및 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=ko)을(를) 포함하여 Adobe 개인화 솔루션에서 개인화된 콘텐츠 검색을 지원합니다.

또한 웹 SDK은 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 지정 개인화 연결](../../destinations/catalog/personalization/custom-personalization.md)과 같은 Adobe Experience Platform 개인화 대상을 통해 동일 페이지 및 다음 페이지 개인화 기능을 지원합니다. 동일 페이지 및 다음 페이지 개인화를 위해 Experience Platform을 구성하는 방법에 대해 알아보려면 [전용 안내서](../../destinations/ui/activate-edge-personalization-destinations.md)를 참조하십시오.

Adobe Target의 [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=ko) 및 Adobe Journey Optimizer의 [웹 캠페인 UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=ko) 내에서 만든 콘텐츠는 SDK에서 자동으로 검색하고 렌더링할 수 있습니다. Adobe Target의 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=ko), Adobe Journey Optimizer의 [코드 기반 경험 채널](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/code-based-experience/get-started-code-based) 또는 Offer Decisioning 내에서 만들어진 콘텐츠는 SDK에서 자동으로 렌더링할 수 없습니다. 대신 SDK을 사용하여 이 콘텐츠를 요청한 다음 콘텐츠를 직접 수동으로 렌더링해야 합니다.

## 자동으로 콘텐츠 렌더링 {#automatic}

서버에 이벤트를 보낼 때 `renderDecisions` 옵션을 `true`(으)로 설정할 수 있습니다. 이렇게 하면 SDK에서 자동 렌더링에 적합한 개인화된 콘텐츠를 자동으로 렌더링하도록 할 수 있습니다.

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

## 수동으로 컨텐츠 렌더링 {#manual}

개인화 콘텐츠에 액세스하려면 SDK이 서버로부터 성공적인 응답을 받은 후에 호출되는 콜백 함수를 제공할 수 있습니다. 콜백에는 반환된 개인화 콘텐츠가 포함된 `result` 속성이 포함될 수 있는 `propositions` 개체가 제공됩니다. 다음은 이벤트를 전송할 때 콜백 함수를 제공하는 방법의 예입니다.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

이 예에서 `result.propositions`은(는) 존재하는 경우 이벤트와 관련된 개인화 제안이 포함된 배열입니다. 기본적으로 자동 렌더링에 적합한 제안만 포함됩니다.

`propositions` 배열은 다음 예제와 유사할 수 있습니다.

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

이 예제에서 `renderDecisions` 명령을 실행할 때 `true` 옵션이 `sendEvent`(으)로 설정되지 않았으므로 SDK은 자동으로 콘텐츠를 렌더링하지 않았습니다. 그러나 SDK은 자동 렌더링에 적합한 콘텐츠를 여전히 자동으로 검색했으며, 원하는 경우 수동으로 렌더링하도록 제공했습니다. 각 제안 개체의 `renderAttempted` 속성이 `false`(으)로 설정되어 있습니다.

이벤트를 보낼 때 대신 `renderDecisions` 옵션을 `true`(으)로 설정했다면 SDK에서 자동 렌더링에 적합한 제안을 렌더링하려고 시도했을 것입니다(앞에서 설명한 대로). 따라서 각 제안 객체의 `renderAttempted` 속성은 `true`(으)로 설정됩니다. 이 경우 이러한 제안을 수동으로 렌더링할 필요가 없습니다.

지금까지 자동 렌더링에 적합한 개인화 콘텐츠(즉, Adobe Target의 시각적 경험 작성기 또는 Adobe Journey Optimizer의 웹 캠페인 UI에서 만들어진 모든 콘텐츠)에 대해서만 논의했습니다. 자동 렌더링에 적합하지 않은 _개인화 콘텐츠를 검색하려면 이벤트를 전송할 때_ 옵션을 채워 콘텐츠를 요청해야 합니다. `decisionScopes` 범위는 서버에서 검색할 특정 제안을 식별하는 문자열입니다.

다음은 한 예입니다.

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

이 예제에서 `salutation` 또는 `discount` 범위와 일치하는 서버에 제안이 있으면 반환되어 `result.propositions` 배열에 포함됩니다. `propositions` 또는 `renderDecisions` 옵션을 구성하는 방법에 관계없이 자동 렌더링에 적합한 제안이 `decisionScopes` 배열에 계속 포함됩니다. 이 경우 `propositions` 배열은 다음 예제와 비슷합니다.

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

이 시점에서 맞춤법이 보이는 대로 제안 콘텐츠를 렌더링할 수 있습니다. 이 예에서 `discount` 범위와 일치하는 제안은 Adobe Target의 양식 기반 경험 작성기를 사용하여 빌드된 HTML 제안입니다. 페이지에 ID가 `daily-special`인 요소가 있고 `discount` 제안의 콘텐츠를 `daily-special` 요소로 렌더링하려는 경우 다음을 수행하십시오.

1. `result` 개체에서 제안을 추출합니다.
1. `discount` 범위의 제안을 찾아 각 제안을 반복합니다.
1. 제안을 찾으면 제안의 각 항목을 반복하여 HTML 콘텐츠인 항목을 찾습니다. (가정하는 것보다 확인하는 것이 좋습니다.)
1. HTML 콘텐츠가 포함된 항목을 찾으면 페이지에서 `daily-special` 요소를 찾아 해당 HTML을 개인화된 콘텐츠로 바꾸십시오.
1. 콘텐츠가 렌더링되면 `display` 이벤트를 보냅니다.

코드는 다음과 같습니다.

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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
    // Rather than assuming there is a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "display" event 
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
              }
            ],
            "propositionEventType": {
              "display": 1
            }
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

SDK은 개인화 프로세스 동안 [깜박임을 관리](../personalization/manage-flicker.md)할 기능을 제공합니다.

## 지표를 증가시키지 않고 단일 페이지 애플리케이션에서 제안 렌더링 {#applypropositions}

`applyPropositions` 명령을 사용하면 [!DNL Target] 및 [!DNL Analytics] 지표를 증가시키지 않고 [!DNL Target] 또는 Adobe Journey Optimizer의 제안 배열을 단일 페이지 애플리케이션으로 렌더링하거나 실행할 수 있습니다. 이렇게 하면 보고 정확도가 높아집니다.

>[!IMPORTANT]
>
>페이지 로드 시 `__view__` 범위(또는 웹 표면)에 대한 제안이 렌더링되면 해당 `renderAttempted` 플래그가 `true`(으)로 설정됩니다. `applyPropositions` 명령은 `__view__` 플래그가 있는 `renderAttempted: true` 범위(또는 웹 표면) 제안을 다시 렌더링하지 않습니다.

### 사용 사례 1: 단일 페이지 애플리케이션 뷰 제안 다시 렌더링

아래 샘플에 설명된 사용 사례는 디스플레이 알림을 보내지 않고 이전에 가져와서 렌더링된 장바구니 보기 제안을 다시 렌더링합니다.

아래 예에서 `sendEvent` 명령은 보기 변경 시 트리거되고 결과 개체를 상수에 저장합니다.

그런 다음 보기 또는 구성 요소가 업데이트되면 이전 `applyPropositions` 명령의 제안을 사용하여 `sendEvent` 명령을 호출하여 보기 제안을 다시 렌더링합니다.

```js
var cartPropositions = alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
        "web": {
            "webPageDetails": {
                "viewName": "cart"
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
    "propositions": cartPropositions
});
```

### 사용 사례 2: 선택기가 없는 제안 렌더링

이 사용 사례는 [!DNL Target Form-based Experience Composer] 또는 Adobe Journey Optimizer의 [코드 기반 경험 채널](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/code-based-experience/get-started-code-based)을 사용하여 작성된 경험에 적용됩니다.

`applyPropositions` 호출에 선택기, 작업 및 범위를 제공해야 합니다.

지원되는 `actionTypes`은(는)

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
            "salutation": {
                "selector": "#first-form-based-offer",
                "actionType": "setHtml"
            },
            "discount": {
                "selector": "#second-form-based-offer",
                "actionType": "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        function sendDisplayEvent(proposition) {
            const {
                id,
                scope,
                scopeDetails = {}
            } = proposition;

            alloy("sendEvent", {
                "xdm": {
                    "eventType": "decisioning.propositionDisplay",
                    "_experience": {
                        "decisioning": {
                            "propositions": [{
                              	"id": id,
                                "scope": scope,
                              	"scopeDetails": scopeDetails
                            }],
                            "propositionEventType": {
                                "display": 1
                            }
                        }
                    }
                }
            });
        }
    });
});
```

결정 범위에 대한 메타데이터를 제공하지 않으면 관련 제안이 렌더링되지 않습니다.
