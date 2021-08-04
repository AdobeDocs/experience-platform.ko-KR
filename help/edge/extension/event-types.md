---
title: Adobe Experience Platform Web SDK Extension의 이벤트 유형
description: Adobe Experience Platform Launch에서 Adobe Experience Platform Web SDK 확장에서 제공하는 이벤트 유형을 사용하는 방법에 대해 알아봅니다.
solution: Experience Platform
feature: 웹 SDK
source-git-commit: 4bddd9f23ae885468148d1592af219290d6fafd9
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 1%

---

# 이벤트 유형

이 페이지에서는 Adobe Experience Platform Web SDK 태그 확장에서 제공하는 Adobe Experience Platform 이벤트 유형을 설명합니다. 이러한 매개 변수는 [빌드 규칙](https://experienceleague.adobe.com/docs/launch-learn/tutorials/fundamentals/building-rules-in-launch.html)에 사용되며 XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=ko-KR)의 [`eventType` 필드와 혼동해서는 안 됩니다.

## [!UICONTROL 이벤트 보내기 완료]

일반적으로 속성에는 이벤트를 Adobe Experience Platform Edge Network에 전송하기 위해 [[!UICONTROL 이벤트 보내기] 작업](action-types.md#send-event)을 사용하여 하나 이상의 규칙이 있습니다. 이벤트가 Edge Network에 전송될 때마다 유용한 데이터가 있는 브라우저로 응답이 반환됩니다. [!UICONTROL 이벤트 보내기 완료] 이벤트 유형이 없으면 이 반환된 데이터에 액세스할 수 없습니다.

반환된 데이터에 액세스하려면 별도의 규칙을 만든 다음 [!UICONTROL 이벤트 완료] 이벤트를 규칙에 추가합니다. 이 규칙은 [!UICONTROL Send event] 작업의 결과로 서버에서 성공한 응답을 받을 때마다 트리거됩니다.

[!UICONTROL 이벤트 보내기 완료] 이벤트가 규칙을 트리거하면 특정 작업을 수행하는 데 유용할 수 있는 서버에서 반환된 데이터를 제공합니다. 일반적으로 [!UICONTROL 사용자 지정 코드] 작업([!UICONTROL Core] 확장에서)을 [!UICONTROL 이벤트 완료 보내기] 이벤트를 포함하는 동일한 규칙에 추가합니다. [!UICONTROL 사용자 지정 코드] 작업에서 사용자 지정 코드는 `event` 변수에 액세스할 수 있습니다. 이 `event` 변수에는 서버에서 반환된 데이터가 포함됩니다.

Edge Network에서 반환된 데이터를 처리하는 규칙은 다음과 같을 수 있습니다.

![](./assets/send-event-complete.png)

다음은 이 규칙에서 [!UICONTROL 사용자 지정 코드] 작업을 사용하여 특정 작업을 수행하는 방법에 대한 몇 가지 예입니다.

### 개인화된 콘텐츠를 수동으로 렌더링합니다.

응답 데이터 처리 규칙에 있는 사용자 지정 코드 작업에서 서버에서 반환된 개인화 속성에 액세스할 수 있습니다. 이렇게 하려면 다음 사용자 지정 코드를 입력합니다.

```javascript
var propositions = event.propositions;
```

`event.propositions`이 존재하는 경우 개인화 제안 개체가 포함된 배열입니다. 배열에 포함된 프로필은 주로 이벤트가 서버로 전송되는 방식에 의해 결정됩니다.

이 첫 번째 시나리오에서 [!UICONTROL 결정 렌더링] 확인란을 선택하지 않고 [!UICONTROL 이벤트 전송을 담당하는 이벤트 보내기] 작업 내에 [!UICONTROL 결정 범위]를 제공하지 않았다고 가정합니다.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

이 예에서 `propositions` 배열에는 자동 렌더링에 적합한 이벤트와 관련된 Proposition만 포함됩니다.

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

이벤트를 보낼 때 [!UICONTROL 결정 렌더링] 확인란이 선택되어 있지 않으므로 SDK가 컨텐츠를 자동으로 렌더링하려고 하지 않았습니다. 그러나 SDK는 자동 렌더링에 적합한 콘텐츠를 여전히 자동으로 검색하며, 원할 경우 수동으로 렌더링하도록 제공된 것입니다. 각 제안 객체에는 `renderAttempted` 속성이 `false`로 설정되어 있습니다.

이벤트를 전송할 때 대신 [!UICONTROL 결정 렌더링] 확인란을 선택했다면 SDK에서 자동 렌더링에 적합한 제안을 렌더링하려고 했을 것입니다. 따라서 각 제안 개체는 `renderAttempted` 속성이 `true`로 설정되었을 것입니다. 이 경우 이러한 제안을 수동으로 렌더링할 필요가 없습니다.

지금까지 자동 렌더링이 가능한 개인화 콘텐츠(예: Adobe Target의 시각적 경험 작성기에서 만든 콘텐츠)만 보았습니다. 자동 렌더링에 적합하지 않은 _개인화 콘텐츠를 검색하려면 [!UICONTROL 이벤트 보내기] 작업에서 [!UICONTROL 결정 범위] 필드를 사용하여 결정 범위를 제공하여 콘텐츠를 요청합니다._ 범위는 서버에서 검색할 특정 제안을 식별하는 문자열입니다.

[!UICONTROL 이벤트 보내기] 작업은 다음과 같습니다.

![img.png](assets/send-event-render-unchecked-with-scopes.png)

이 예에서 `salutation` 또는 `discount` 범위와 일치하는 서버에 proposition이 있으면 반환되고 `propositions` 배열에 포함됩니다. [!UICONTROL 이벤트 보내기] 작업에서 [!UICONTROL 결정] 또는 [!UICONTROL 결정 범위] 필드를 구성하는 방법에 관계없이 자동 렌더링에 대한 자격 있는 Proposition은 `propositions` 배열에 계속 포함됩니다. 이 경우 `propositions` 배열은 다음 예제와 비슷합니다.

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

이 시점에서 제안 콘텐츠를 적절히 렌더링할 수 있습니다. 이 예에서 `discount` 범위와 일치하는 제안은 Adobe Target의 양식 기반 경험 작성기를 사용하여 작성된 HTML 제안입니다. 페이지에 ID가 `daily-special`인 요소가 있고 `discount` 제안의 컨텐츠를 `daily-special` 요소로 렌더링하려 한다고 가정합니다. 다음을 수행합니다.

1. `event` 개체에서 proposition을 추출합니다.
1. 각 제안을 반복하고 `discount` 범위가 있는 제안을 찾습니다.
1. 제안을 찾으면 제안에 있는 각 항목을 반복하며 HTML 콘텐츠인 항목을 찾습니다. (가정하는 것보다 확인하는 것이 낫다.)
1. HTML 콘텐츠가 들어 있는 항목을 찾으면 페이지에서 `daily-special` 요소를 찾아 해당 HTML을 개인화된 콘텐츠로 바꾸십시오.

[!UICONTROL 사용자 지정 코드] 작업 내의 사용자 지정 코드는 다음과 같이 표시될 수 있습니다.

```javascript
var propositions = event.propositions;

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
```

### Adobe Target 응답 토큰 액세스

Adobe Target에서 반환된 개인화 컨텐츠에는 활동, 오퍼, 경험, 사용자 프로필, 지역 정보 등에 대한 세부 사항인 [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)이 포함됩니다. 이러한 세부 사항은 타사 도구와 공유하거나 디버깅에 사용할 수 있습니다. Adobe Target 사용자 인터페이스에서 응답 토큰을 구성할 수 있습니다.

응답 데이터 처리 규칙에 있는 사용자 지정 코드 작업에서 서버에서 반환된 개인화 속성에 액세스할 수 있습니다. 이렇게 하려면 다음 사용자 지정 코드를 입력합니다.

```javascript
var propositions = event.propositions;
```

`event.propositions`이 존재하는 경우 개인화 제안 개체가 포함된 배열입니다. `result.propositions`의 콘텐츠에 대한 자세한 내용은 [개인화된 콘텐츠를 수동으로 렌더링합니다](#manually-render-personalized-content) 를 참조하십시오.

웹 SDK에서 자동으로 렌더링한 모든 프로필에서 모든 활동 이름을 수집하고 단일 배열에 푸시하려고 한다고 가정합니다. 그런 다음 단일 스토리지를 타사 시스템으로 보낼 수 있습니다. 이 경우 [!UICONTROL 사용자 지정 코드] 작업 내에 사용자 지정 코드를 다음과 같이 작성합니다.

1. `event` 개체에서 proposition을 추출합니다.
1. 각각의 제안을 반복하세요.
1. SDK가 제안을 렌더링했는지 확인합니다.
1. 만약 그렇다면, 제안에 있는 각 항목들을 반복합니다.
1. 응답 토큰이 포함된 객체인 `meta` 속성에서 활동 이름을 검색합니다.
1. 활동 이름을 배열에 푸시합니다.
1. 활동 이름을 타사에 보냅니다.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```





