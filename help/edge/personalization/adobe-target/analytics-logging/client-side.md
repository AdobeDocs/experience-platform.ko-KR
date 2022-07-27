---
title: Platform Web SDK의 A4T 데이터에 대한 클라이언트측 로깅
description: Experience Platform Web SDK를 사용하여 A4T(Adobe Analytics for Target)에 대해 클라이언트 측 로깅을 활성화하는 방법을 알아봅니다.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;로깅;웹 sdk;experience;platform
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: de420d3bbf35968fdff59b403a0f2b18110f3c17
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 4%

---

# Platform Web SDK의 A4T 데이터에 대한 클라이언트측 로깅

## 개요 {#overview}

Adobe Experience Platform 웹 SDK를 통해 다음을 수집할 수 있습니다 [Target용 Adobe Analytics(A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) 웹 응용 프로그램의 클라이언트 측에 있는 데이터입니다.

클라이언트 측 로깅은 관련 [!DNL Target] 데이터는 클라이언트 측에서 반환되므로 이를 수집하여 Analytics와 공유할 수 있습니다. 을 사용하여 데이터를 Analytics에 수동으로 보내려면 이 옵션을 활성화해야 합니다. [데이터 삽입 API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>를 사용하여 이 작업을 수행하는 방법 [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ko-KR) 는 현재 개발 중이며 곧 출시될 예정입니다.

이 문서에서는 웹 SDK에 대한 클라이언트측 A4T 로깅을 설정하는 단계를 설명하고 일반적인 사용 사례에 대한 몇 가지 구현 예를 제공합니다.

## 전제 조건 {#prerequisites}

이 자습서에서는 개인화를 위해 웹 SDK를 사용하는 것과 관련된 기본 개념 및 프로세스를 잘 알고 있다고 가정합니다. 소개가 필요한 경우 다음 설명서를 검토하십시오.

* [웹 SDK 구성](../../../fundamentals/configuring-the-sdk.md)
* [이벤트 보내기](../../../fundamentals/tracking-events.md)
* [개인화 콘텐츠 렌더링](../../rendering-personalization-content.md)

## Analytics 클라이언트 측 로깅 설정 {#set-up-client-side-logging}

다음 하위 섹션에서는 웹 SDK 구현에 대해 Analytics 클라이언트 측 로깅을 활성화하는 방법을 간략하게 설명합니다.

### Analytics 클라이언트 측 로깅 활성화 {#enable-analytics-client-side-logging}

구현에 대해 Analytics 클라이언트 측 로깅이 활성화되었다고 가정하려면, 에서 Adobe Analytics 구성을 비활성화해야 합니다 [데이터 스트림](../../../datastreams/overview.md).

![Analytics 데이터 스트림 구성을 사용할 수 없습니다.](../assets/disable-analytics-datastream.png)

### 검색 [!DNL A4T] sdk의 데이터를 Analytics에 전송합니다 {#a4t-to-analytics}

이 보고 방법이 제대로 작동하려면 [!DNL A4T] 에서 검색한 관련 데이터 [`sendEvent`](../../../fundamentals/tracking-events.md) 명령을 반환합니다.

Target Edge에서 proposition 응답을 계산할 때 Analytics 클라이언트 측 로깅이 활성화되었는지 확인합니다(예: 데이터 스트림에서 Analytics가 비활성화된 경우). 클라이언트측 로깅이 활성화되면 응답의 각 제안에 Analytics 토큰을 추가합니다.

흐름은 다음과 유사합니다.

![클라이언트 측 로깅 흐름](../assets/analytics-client-side-logging.png)

다음은 의 예입니다 `interact` Analytics 클라이언트측 로깅이 활성화되면 응답합니다. Analytics 보고가 있는 활동에 대한 제안인 경우 다음과 같은 항목이 있습니다 `scopeDetails.characteristics.analyticsToken` 속성을 사용합니다.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

양식 기반 경험 작성기 활동의 Proposition에는 동일한 제안 아래에 콘텐츠와 클릭 지표 항목이 모두 포함될 수 있습니다. 따라서 컨텐츠에 대한 단일 분석 토큰이 있는 대신 `scopeDetails.characteristics.analyticsToken` 속성, 여기에는 표시 및 클릭 분석 토큰이 모두 지정되어 있을 수 있습니다. `scopeDetails.characteristics.analyticsDisplayToken` 및 `scopeDetails.characteristics.analyticsClickToken` 이에 상응한다.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

의 모든 값 `scopeDetails.characteristics.analyticsToken`뿐만 아니라 `scopeDetails.characteristics.analyticsDisplayToken` (표시된 컨텐츠에 대해) 및 `scopeDetails.characteristics.analyticsClickToken` (클릭 지표의 경우) 은 수집하고 다음과 같이 포함해야 하는 A4T 페이로드입니다. `tnta` 태그를에서 지정합니다. [데이터 삽입 API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) 호출.

>[!IMPORTANT]
>
>다음 `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` 속성에는 여러 토큰을 포함할 수 있으며, 하나의 쉼표로 구분된 문자열로 연결됩니다.
>
>다음 섹션에 제공된 구현 예에서 여러 Analytics 토큰이 반복적으로 수집됩니다. Analytics 토큰 배열을 연결하려면 다음과 유사한 함수를 사용하십시오.
>
>
```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## 구현 예 {#implementation-examples}

다음 하위 섹션에서는 일반적인 사용 사례에 대해 Analytics 클라이언트 측 로깅을 구현하는 방법을 보여줍니다.

### 양식 기반 경험 작성기 활동 {#form-based-composer}

웹 SDK를 사용하여 [Adobe Target 양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 활동.

특정 결정 범위에 대한 제안을 요청하면 반환되는 제안에 해당 Analytics 토큰이 포함됩니다. 가장 좋은 방법은 Platform Web SDK를 체인하는 것입니다 `sendEvent` 명령을 실행하고 반환된 속성을 반복하여 Analytics 토큰을 동시에 수집하는 동안 이를 실행합니다.

을(를) 트리거할 수 있습니다 `sendEvent` 다음과 같은 양식 기반 경험 작성기 활동 범위에 대한 명령:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

여기에서 코드를 구현하여 proposition을 실행하고 궁극적으로 Analytics로 전송할 페이로드를 구성해야 합니다. 이것은 `results.propositions` 다음을 포함할 수 있습니다.

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

컨텐츠 항목이 있는 제안에서 Analytics 토큰을 추출하려면 다음과 유사한 함수를 구현할 수 있습니다.

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

제안에는 `schema` 해당 항목의 속성입니다. 양식 기반 경험 작성기 활동에 대해 지원되는 4가지 제안 항목 스키마가 있습니다.

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` 및 `JSON_SCHEMA` 오퍼의 유형을 반영하는 스키마입니다 `MEASUREMENT_SCHEMA` 은 DOM 요소에 연결해야 하는 지표를 반영합니다.

클릭 지표에 대한 Analytics 페이로드는 방문자가 이전에 표시된 콘텐츠를 실제로 클릭하는 시점에 컨텐츠 항목과 별도로 수집하여 Analytics로 전송해야 합니다.

클릭 지표 A4T 페이로드를 가져오기 위한 다음 도우미 함수를 이 경우 사용할 수 있습니다.

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### 구현 요약 {#implementation-summary}

요약하면 Platform Web SDK에 양식 기반 경험 작성기 활동을 적용할 때 다음 단계를 실행해야 합니다.

1. 양식 기반 경험 작성기 활동 오퍼를 가져오는 이벤트를 보냅니다.
1. 페이지에 컨텐츠 변경 사항을 적용합니다.
1. 보내기 `decisioning.propositionDisplay` 알림 이벤트;
1. SDK 응답에서 Analytics 표시 토큰을 수집하고 Analytics 히트에 대한 페이로드를 구성합니다.
1. 를 사용하여 페이로드를 Analytics에 보냅니다. [데이터 삽입 API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. 전달된 Proposition에 클릭 지표가 있는 경우, 클릭이 수행될 때 Click Listener를 전송하도록 설정해야 합니다 `decisioning.propositionInteract` 알림 이벤트. 다음 `onBeforeEventSend` 핸들러를 구성할 때 `decisioning.propositionInteract` events에 할당되면 다음 작업이 수행됩니다.
   1. 클릭 Analytics 토큰을 수집하는 위치 `xdm._experience.decisioning.propositions`
   1. 를 통해 수집된 Analytics 페이로드로 클릭 분석 히트 전송 [데이터 삽입 API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### 시각적 경험 작성기 활동 {#visual-experience-composer-acitivties}

웹 SDK를 사용하면 [VEC(시각적 경험 작성기)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>이 사용 사례를 구현하는 단계는 [양식 기반 경험 작성기 활동](#form-based-composer). 자세한 내용은 이전 섹션을 참조하십시오.

자동 렌더링이 활성화되면 페이지에서 실행된 프로필에서 Analytics 토큰을 수집할 수 있습니다. 가장 좋은 방법은 Platform Web SDK를 체인하는 것입니다 `sendEvent` 명령을 실행하고 반환된 속성을 반복하여 웹 SDK에서 렌더링하려고 한 항목을 필터링합니다.

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### 사용 `onBeforeEventSend` 페이지 지표를 처리하려면 {#using-onbeforeeventsend}

Adobe Target 활동을 사용하여 DOM에 수동으로 첨부하거나 DOM에 자동으로 첨부된 페이지에서 다른 지표를 설정할 수 있습니다(VEC 작성 활동). 두 유형 모두 웹 페이지에서 지연된 최종 사용자 상호 작용입니다.

이를 설명하기 위해 우수 사례는 `onBeforeEventSend` Adobe Experience Platform Web SDK 후크. 다음 `onBeforeEventSend` 후크는 `configure` 및 가 데이터 스트림을 통해 전송되는 모든 이벤트에 반영됩니다.

다음은 다음과 같은 방법의 예입니다 `onBeforeEventSent` analytics 히트를 트리거하도록 구성할 수 있습니다.

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## 다음 단계 {#next-steps}

이 안내서에서는 웹 SDK의 A4T 데이터에 대한 클라이언트측 로깅을 다룹니다. 다음 안내서를 참조하십시오. [서버측 로깅](server-side.md) edge Network에서 A4T 데이터를 처리하는 방법에 대한 자세한 정보.
