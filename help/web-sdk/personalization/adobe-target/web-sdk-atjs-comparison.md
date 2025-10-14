---
title: at.js와 Experience Platform Web SDK 비교
description: at.js 기능을 Experience Platform Web SDK과 비교하는 방법에 대해 알아봅니다
keywords: target;adobe target;activity.id;experience.id;renderDecisions;의사 결정 범위;코드 조각 사전 숨김;vec;양식 기반 경험 작성기;xdm;대상;의사 결정;범위;스키마;시스템 다이어그램;다이어그램
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 2%

---

# at.js 라이브러리와 웹 SDK 비교

## 개요

이 문서에서는 `at.js` 라이브러리와 Experience Platform 웹 SDK 간의 차이점에 대한 개요를 제공합니다.

## 라이브러리 설치

### at.js 설치

고객이 Adobe Experience Cloud의 구현 탭에서 직접 라이브러리를 다운로드할 수 있습니다. at.js 라이브러리는 고객이 like를 가진 clientCode, imsOrgId 등의 설정으로 사용자 정의됩니다.

### 웹 SDK 설치

사전 빌드된 버전은 CDN에서 사용할 수 있습니다. 페이지에서 직접 CDN의 라이브러리를 참조하거나, 자체 인프라에서 다운로드하여 호스팅할 수 있습니다. 축소 및 축소 해제된 형식으로 사용할 수 있습니다. 축소되지 않은 버전은 디버깅에 유용합니다.

자세한 내용은 [JavaScript 라이브러리를 사용하여 웹 SDK 설치](/help/web-sdk/install/library.md)를 참조하십시오.

## 라이브러리 구성

### at.js 구성

모든 at.js 파일이 끝나면 설정 개체를 인스턴스화하고 전달하는 섹션이 있습니다. 사용자 지정할 수 있습니다. 다운로드에서 해당 섹션을 현재 고객 설정으로 채웁니다.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=ko)


### 웹 SDK 구성

SDK 구성은 [`configure`](/help/web-sdk/commands/configure/overview.md) 명령을 사용하여 수행됩니다. `configure` 명령은 먼저 호출된 *always*&#x200B;입니다.

## 페이지 로드 타겟 오퍼를 요청하고 자동으로 렌더링하는 방법

### at.js 사용

at.js 2.x를 사용하는 경우 설정 `pageLoadEnabled`을(를) 사용하면 라이브러리가 `execute -> pageLoad`(으)로 Target Edge 호출을 트리거합니다. 모든 설정이 기본값으로 설정되어 있으면 사용자 지정 코딩이 필요하지 않습니다. at.js가 페이지에 추가되고 브라우저에 의해 로드되면 Target Edge 호출이 실행됩니다.

### 웹 SDK 사용

Adobe Target의 [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=ko) 내에서 만든 콘텐츠는 SDK에서 자동으로 검색하고 렌더링할 수 있습니다.

Target 오퍼를 요청하고 자동으로 렌더링하려면 `sendEvent` 명령을 사용하고 `renderDecisions` 옵션을 `true`(으)로 설정하십시오. 이렇게 하면 SDK에서 자동 렌더링에 적합한 개인화된 콘텐츠를 자동으로 렌더링하도록 할 수 있습니다.

예:

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

Experience Platform Web SDK은 웹 SDK에서 실행한 오퍼와 함께 알림을 자동으로 전송합니다. 이는 알림 요청 페이로드의 예입니다.

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[자세히 알아보기](../rendering-personalization-content.md)

## 페이지 로드 타겟 오퍼를 요청하고 자동으로 렌더링하지 않는 방법

### at.js 사용

페이지 로드에 대한 오퍼를 가져오는 Target Edge 호출을 실행할 수 있는 두 가지 방법이 있습니다.

예 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

예 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=ko)

### 웹 SDK 사용

`sendEvent`: `decisionScopes`에서 특수 범위로 `__view__` 명령을 실행합니다. 이 범위는 Target에서 모든 페이지 로드 활동을 가져오고 모든 보기를 미리 가져오는 신호로 사용됩니다. 웹 SDK은 또한 모든 VEC 보기 기반 활동을 평가하려고 합니다. 현재 웹 SDK에서는 보기 프리페치를 비활성화할 수 없습니다.

개인화 콘텐츠에 액세스하려면 SDK이 서버로부터 성공적인 응답을 받은 후에 호출되는 콜백 함수를 제공할 수 있습니다. 콜백에는 반환된 개인화 콘텐츠가 포함된 제안 속성이 포함될 수 있는 결과 개체가 제공됩니다.

예:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[자세히 알아보기](../rendering-personalization-content.md#manually-rendering-content)


## 특정 양식 기반 Target mbox를 요청하는 방법


### at.js 사용

`getOffer` 함수를 사용하여 양식 기반 작성기 활동을 가져올 수 있습니다.

예 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

예 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=ko)


### 웹 SDK 사용

`sendEvent` 명령을 사용하고 `decisionScopes` 옵션 아래에 mbox 이름을 전달하여 양식 기반 작성기 기반 활동을 가져올 수 있습니다. `sendEvent` 명령은 요청된 활동/제안을 포함하는 개체로 해결된 약속을 반환합니다.
다음은 `propositions` 배열의 모양입니다.

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

예:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[자세히 알아보기](../rendering-personalization-content.md#manually-rendering-content)

## Target 활동을 적용하는 방법

### at.js 사용

`applyOffers` 함수를 사용하여 Target 활동을 적용할 수 있습니다. `adobe.target.applyOffer(options)`

예:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

`applyOffers`전용 설명서[에서 &#x200B;](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=ko) 명령에 대해 자세히 알아보세요.


### 웹 SDK 사용

`applyPropositions` 명령을 사용하여 Target 활동을 적용할 수 있습니다.

예:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

`applyPropositions`전용 설명서[에서 &#x200B;](../../personalization/rendering-personalization-content.md#applypropositions) 명령에 대해 자세히 알아보세요.

## 이벤트 추적 방법

### at.js 사용

`trackEvent` 함수 또는 `sendNotifications`을(를) 사용하여 이벤트를 추적할 수 있습니다.

이 함수는 클릭 및 전환과 같은 사용자 작업을 보고하는 요청을 실행합니다. 응답의 활동은 전달하지 않습니다.


**예 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**예 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=ko)

### 웹 SDK 사용

`sendEvent` 명령을 호출하고 `_experience.decisioning.propositions` XDM 필드 그룹을 채우고 `eventType`을(를) 두 값 중 하나로 설정하여 이벤트와 사용자 작업을 추적할 수 있습니다.

* `decisioning.propositionDisplay`: Target 활동을 렌더링한다는 신호를 보냅니다.
* `decisioning.propositionInteract`: 마우스 클릭과 같이 사용자가 활동과 상호 작용하도록 신호를 보냅니다.

`_experience.decisioning.propositions` XDM 필드 그룹은 개체의 배열입니다. 각 개체의 속성은 `result.propositions` 명령에서 반환되는 `sendEvent`에서 파생됩니다. `{ id, scope, scopeDetails }`

**예 1 - 활동을 렌더링한 후 `decisioning.propositionDisplay` 이벤트를 추적합니다**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
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

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
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
```

**예 2 - 클릭 지표가 발생한 후 `decisioning.propositionInteract` 이벤트를 추적합니다**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[자세히 알아보기](../rendering-personalization-content.md#manually-rendering-content)

**예 3 - 작업을 수행한 후 실행된 이벤트 추적**

이 예제는 버튼을 클릭하는 등의 특정 작업을 수행한 후 실행된 이벤트를 추적합니다.
`__adobe.target` 데이터 개체를 통해 사용자 지정 매개 변수를 추가할 수 있습니다.

`commerce` XDM 개체를 추가할 수도 있습니다.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [
                    {
                        "scope": "orderConfirm" //example scope name
                    }
                ],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    },
    "commerce": {
        "order": {
            "purchaseID": "a8g784hjq1mnp3",
            "purchaseOrderNumber": "VAU3123",
            "currencyCode": "USD",
            "priceTotal": 999.98
        }
    },
    "data": {
        "__adobe": {
            "target": {
                "pageType": "Order Confirmation",
                "user.categoryId": "Insurance"
            }
        }
    }
})
```

## 단일 페이지 애플리케이션에서 보기 변경을 트리거하는 방법

### at.js 사용

`adobe.target.triggerView` 함수를 사용합니다. 이 함수는 새 페이지를 로드할 때마다 또는 페이지의 구성 요소가 다시 렌더링될 때 호출할 수 있습니다. 시각적 경험 작성기(VEC)를 사용하여 A/B 테스트 및 경험 타깃팅(XT) 활동을 만들려면 단일 페이지 애플리케이션(SPA)에 대해 adobe.target.triggerView()를 구현해야 합니다. 사이트에서 adobe.target.triggerView()가 구현되지 않으면 SPA에 VEC를 활용할 수 없습니다.

**예**

```javascript
adobe.target.triggerView("homeView")
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=ko)


### 웹 SDK 사용

단일 페이지 응용 프로그램 보기 변경을 트리거하거나 신호를 보내려면 `web.webPageDetails.viewName` 명령의 `xdm` 옵션 아래에 `sendEvent` 속성을 설정합니다. 웹 SDK에서 보기 캐시를 검사합니다. `viewName`에 지정된 `sendEvent`에 대한 오퍼가 있으면 이 오퍼를 실행하고 표시 알림 이벤트를 보냅니다.

**예**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[자세히 알아보기](./spa-implementation.md#implementing-xdm-views)

## 응답 토큰 활용 방법

Adobe Target에서 반환된 Personalization 콘텐츠에는 활동, 오퍼, 경험, 사용자 프로필, 지역 정보 등에 대한 세부 정보인 [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=ko)이 포함됩니다. 이러한 세부 정보는 서드파티 도구와 공유하거나 디버깅에 사용할 수 있습니다. Adobe Target 사용자 인터페이스에서 응답 토큰을 구성할 수 있습니다.

### at.js 사용

at.js 사용자 지정 이벤트를 사용하여 Target 응답을 수신하고 응답 토큰을 읽습니다.

**예**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=ko)


### 웹 SDK 사용

>[!IMPORTANT]
>
>Experience Platform Web SDK 버전 2.6.0 이상을 사용 중인지 확인하십시오.

응답 토큰은 `propositions` 명령의 결과에 노출된 `sendEvent`의 일부로 반환됩니다. 각 제안에는 `items`의 배열이 포함되어 있으며 Target 관리 UI에서 응답 토큰이 활성화된 경우 각 항목에는 응답 토큰으로 채워진 `meta` 개체가 있습니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=ko)

**예**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[자세히 알아보기](./accessing-response-tokens.md)

## 플리커를 관리하는 방법

### at.js 사용

at.js를 사용하면 at.js가 처리할 수 있도록 `bodyHidingEnabled: true`을(를) 설정하여 플리커를 관리할 수 있습니다.
dom 변경 사항을 가져오고 적용하기 전에 개인화된 컨테이너를 미리 숨깁니다.
at.js `bodyHiddenStyle`을(를) 재정의하여 개인화된 콘텐츠가 포함된 페이지 섹션을 미리 숨길 수 있습니다.
기본적으로 `bodyHiddenStyle`은(는) 전체 HTML `body`을(를) 숨깁니다.
두 설정 모두 `window.targetGlobalSettings`을(를) 사용하여 재정의할 수 있습니다. at.js를 로드하기 전에 `window.targetGlobalSettings`을(를) 배치해야 합니다.

### 웹 SDK 사용

고객은 Web SDK을 사용하여 아래 예제와 같이 configure 명령에서 사전 숨김 스타일을 설정할 수 있습니다.

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Web SDK async를 로드할 때 Web SDK이 삽입되기 전에 페이지에 다음 코드 조각을 삽입하는 것이 좋습니다.

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## A4T 처리 방법

### at.js 사용

at.js를 사용하여 지원되는 A4T 로깅에는 두 가지 유형이 있습니다.

* Analytics 클라이언트측 로깅
* Analytics 서버측 로깅

#### Analytics 클라이언트측 로깅

**예 1: Target 전역 설정 사용**

Analytics 클라이언트 측 로깅은 at.js 설정에서 `analyticsLogging: client_side`을(를) 설정하거나 `window.targetglobalSettings` 개체를 재정의하여 사용할 수 있습니다.
이 옵션이 설정되면 반환되는 페이로드의 형식은 다음과 같습니다.

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

그런 다음 데이터 삽입 API를 통해 페이로드를 Analytics에 전달할 수 있습니다.

예제 2: 모든 `getOffers` 함수에서 구성:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

다음은 응답 페이로드의 모습입니다.

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

Analytics 페이로드(`tnta` 토큰)는 [데이터 삽입 API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)를 사용하여 Analytics 히트에 포함해야 합니다.

#### Analytics 서버측 로깅

Analytics Server Side 로깅은 at.js 설정에서 `analyticsLogging: server_side`을(를) 설정하거나 `window.targetglobalSettings` 개체를 재정의하여 사용할 수 있습니다.
그런 다음 데이터는 다음과 같이 흐릅니다.

![Analytics 서버측 로깅 워크플로를 보여 주는 다이어그램](assets/a4t-server-side-atjs.png)

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=ko)

### 웹 SDK 사용

웹 SDK은 또한 다음을 지원합니다.

* Analytics 클라이언트측 로깅
* Analytics 서버측 로깅

#### Analytics 클라이언트측 로깅

해당 DataStream 구성에 대해 Adobe Analytics이 비활성화된 경우 Analytics 클라이언트 측 로깅이 활성화됩니다.

![Analytics 클라이언트 측 로깅 워크플로를 보여 주는 다이어그램](assets/analytics-disabled-datastream-config.png)

고객은 `tnta`데이터 삽입 API[를 사용하여 Analytics와 공유해야 하는 Analytics 토큰(](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md))에 액세스할 수 있습니다
에서 `sendEvent` 명령을 체인화하고 결과 제안 배열을 반복합니다.

**예**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

다음은 Analytics Client Side가 활성화되어 있을 때 데이터가 어떻게 이동하는지를 보여 주는 다이어그램입니다.

![Analytics Client Side 로깅의 데이터 흐름 다이어그램](assets/analytics-client-side-logging.png)

#### Analytics 서버측 로깅

해당 데이터 스트림 구성에 대해 Analytics가 활성화되면 Analytics Server Side 로깅이 활성화됩니다.

Analytics 설정을 표시하는 ![데이터스트림 UI.](assets/analytics-enabled-datastream-config.png)

서버측 분석 로깅을 활성화한 경우 Analytics 보고가 표시되도록 Analytics와 공유해야 하는 A4T 페이로드가 표시됩니다
정확한 노출 횟수 및 전환 횟수는 Edge Network 수준에서 공유되므로 고객이 추가 처리를 하지 않아도 됩니다.

다음은 Server Side Analytics 로깅이 활성화된 경우 데이터가 시스템으로 유입되는 방식입니다.

![서버측 분석 로깅의 데이터 흐름을 보여 주는 다이어그램](assets/analytics-server-side-logging.png)

## Target 전역 설정을 설정하는 방법

### at.js 사용

Target Standard/Premium UI에서 설정을 구성하거나 REST API를 사용하는 대신 `window.targetGlobalSettings`을(를) 사용하여 at.js 라이브러리의 설정을 재정의할 수 있습니다.

at.js가 로드되기 전에 또는 관리 > 구현 > at.js 설정 편집 > 코드 설정 > 라이브러리 헤더에서 재정의를 정의해야 합니다.

예:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=ko)

### 웹 SDK 사용

이 기능은 웹 SDK에서 지원되지 않습니다.

## Target 프로필 속성을 업데이트하는 방법

### at.js 사용

**예 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**예 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### 웹 SDK 사용

Target 프로필을 업데이트하려면 `sendEvent` 명령을 사용하고 `data.__adobe.target` 속성을 설정하여 `profile`을(를) 사용하여 키 이름 앞에 추가합니다.

**예**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Target Recommendations 사용 방법

### at.js 사용

**예 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**예 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=ko)


### 웹 SDK 사용

권장 사항 데이터를 보내려면 `sendEvent` 명령을 사용하고 `data.__adobe.target` 속성을 설정하여 `entity`을(를) 사용하여 키 이름 앞에 추가합니다.

**예**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## 타사 ID를 사용하는 방법

### at.js 사용

at.js를 사용하여 `mbox3rdPartyId`을(를) 보내고 `getOffer` 또는 `getOffers`을(를) 사용하는 방법은 여러 가지가 있습니다.

**예 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**예 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

또는 `mbox3rdPartyId` 또는 `targetPageParams`에서 `targetPageParamsAll`을(를) 설정하는 방법이 있습니다.
`targetPageParams`에서 설정하면 `target-global-mbox`이라고도 하는 `pag-lLoad`에 대한 요청에서 전송됩니다.
권장 사항은 모든 대상 요청에서 전송되므로 `targetPageParamsAll`을(를) 사용하여 설정됩니다.
`targetPageParamsAll`을(를) 사용하면 페이지에서 `mbox3rdPartyId`을(를) 한 번 정의할 수 있으므로 모든 대상 요청에 올바른 `mbox3rdPartyId`이(가) 있는지 확인할 수 있습니다.

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=ko)

### 웹 SDK 사용

웹 SDK은 Target 타사 ID를 지원합니다. 그러나 몇 가지 단계가 더 필요합니다. 해결 방법을 찾기 전에 `identityMap`에 대해 잠시 이야기해야 합니다.
ID 맵을 사용하면 여러 ID를 보낼 수 있습니다. 모든 ID는 네임스페이스가 지정됩니다. 각 네임스페이스에는 하나 이상의 ID가 있을 수 있습니다. 특정 ID를 기본 ID로 표시할 수 있습니다.
이 지식을 바탕으로 Target 타사 ID를 사용하도록 웹 SDK를 설정하는 데 필요한 단계를 확인할 수 있습니다.

1. 데이터 스트림 구성 페이지에서 Target 타사 ID를 포함할 네임스페이스를 설정합니다.

![Target 타사 ID 네임스페이스 필드를 표시하는 데이터스트림 UI](assets/mbox-3-party-id-setup.png)

1. 다음과 같이 모든 sendEvent 명령에 해당 ID 네임스페이스를 보냅니다.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## 속성 토큰을 설정하는 방법

### at.js 사용

at.js를 사용하여 속성 토큰을 설정하는 방법에는 `targetPageParams` 또는 `targetPageParamsAll`을 사용하는 두 가지가 있습니다. `targetPageParams`을(를) 사용하면 속성 토큰이 `target-global-mbox` 호출에 추가되지만 `targetPageParamsAll`을(를) 사용하면 토큰이 모든 대상 호출에 추가됩니다.

**예 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**예 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### 웹 SDK 사용

Web SDK을 사용하면 데이터 스트림 구성을 설정할 때 Adobe Target 네임스페이스 아래에 있는 속성을 더 높은 수준에서 설정할 수 있습니다.
![Adobe Target 설정을 표시하는 데이터스트림 UI.](assets/at-property-setup.png)
즉, 특정 데이터 스트림 구성에 대한 모든 Target 호출에 해당 속성 토큰이 포함됩니다.

## mbox를 미리 가져오는 방법

### at.js 사용

이 기능은 at.js 2.x에서만 사용할 수 있습니다. at.js 2.x에는 이름이 `getOffers`인 새 함수가 있습니다. `getOffers`을(를) 통해 고객은 하나 이상의 mbox에 대한 콘텐츠를 미리 가져올 수 있습니다. 다음은 한 예입니다.

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

참고: `mbox` 배열의 모든 `mboxes`에 자체 인덱스가 있는지 확인하는 것이 좋습니다. 일반적으로 첫 번째 mbox에는 `index=0`, 다음 mbox에는 `index=1` 등이 있습니다.

### 웹 SDK 사용

이 기능은 현재 웹 SDK에서 지원되지 않습니다.

## 내 Target 구현을 디버깅하는 방법

### at.js 사용

At.js는 다음 디버깅 기능을 노출합니다.

* Mbox 비활성화 - Target을 가져오고 렌더링하지 않도록 비활성화하여 페이지가 Target 상호 작용 없이 중단되었는지 확인
* Mbox 디버그 - at.js는 모든 작업을 기록합니다.
* 대상 추적 - Bullseye에서 생성된 mbox 추적 토큰을 사용하면 `window.___target_trace` 개체에서 의사 결정 프로세스에 참여한 세부 정보가 포함된 추적 개체를 사용할 수 있습니다.

참고: 이러한 모든 디버깅 기능은 [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)의 향상된 기능을 통해 사용할 수 있습니다

### 웹 SDK 사용

Web SDK을 사용할 때 여러 디버깅 기능을 사용할 수 있습니다.

* [Assurance](/help/assurance/home.md) 사용 중
* [웹 SDK 디버그 활성화됨](/help/web-sdk/use-cases/debugging.md)
* [웹 SDK 모니터링 후크 사용](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* [Adobe Experience Platform Debugger](/help/debugger/home.md) 사용
* 대상 추적
