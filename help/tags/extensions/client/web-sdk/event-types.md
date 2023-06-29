---
title: Adobe Experience Platform 웹 SDK 확장의 이벤트 유형
description: Adobe Experience Platform Launch의 Adobe Experience Platform Web SDK 확장에서 제공하는 이벤트 유형을 사용하는 방법에 대해 알아봅니다.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 2772660936444e39124a75deda6f78d97f7793f2
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# 이벤트 유형

이 페이지에서는 Adobe Experience Platform Web SDK 태그 확장에서 제공하는 Adobe Experience Platform 이벤트 유형에 대해 설명합니다. 다음 용도로 사용됩니다. [규칙 작성](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) 와 혼동해서는 안 됩니다. [`eventType` XDM의 필드](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=ko-KR).

## [!UICONTROL 이벤트 전송 완료]

일반적으로 속성에는 [[!UICONTROL 이벤트 보내기] 작업](action-types.md#send-event) Adobe Experience Platform Edge Network로 이벤트를 전송합니다. 이벤트가 Edge Network로 전송될 때마다 유용한 데이터가 포함된 응답이 브라우저에 반환됩니다. 없이 [!UICONTROL 이벤트 전송 완료] 이벤트 유형, 이 반환된 데이터에 대한 액세스 권한이 없습니다.

반환된 데이터에 액세스하려면 별도의 규칙을 만든 다음 [!UICONTROL 이벤트 전송 완료] 이벤트를 규칙에 추가합니다. 이 규칙은 의 결과로 서버에서 성공적인 응답을 받을 때마다 트리거됩니다. [!UICONTROL 이벤트 보내기] 작업.

다음과 같은 경우 [!UICONTROL 이벤트 전송 완료] 이벤트는 규칙을 트리거하며, 특정 작업을 수행하는 데 유용할 수 있는 서버에서 반환된 데이터를 제공합니다. 일반적으로 다음을 추가합니다 [!UICONTROL 사용자 지정 코드] 작업(출처: [!UICONTROL 코어] 확장명)을 추가하여 [!UICONTROL 이벤트 전송 완료] 이벤트. 다음에서 [!UICONTROL 사용자 지정 코드] 매크로 함수, 사용자 지정 코드는 이라는 변수에 액세스할 수 있습니다. `event`. 이 `event` 변수에는 서버에서 반환된 데이터가 포함됩니다.

Edge Network에서 반환되는 데이터를 처리하는 규칙은 다음과 같습니다.

![](assets/send-event-complete.png)

다음은 를 사용하여 특정 작업을 수행하는 방법에 대한 몇 가지 예입니다. [!UICONTROL 사용자 지정 코드] 이 규칙의 작업입니다.

### 개인화된 콘텐츠 수동 렌더링

응답 데이터 처리 규칙에 있는 사용자 지정 코드 작업에서 서버에서 반환된 개인화 제안에 액세스할 수 있습니다. 이렇게 하려면 다음 사용자 지정 코드를 입력합니다.

```javascript
var propositions = event.propositions;
```

If `event.propositions` 존재함. 개인화 제안 객체가 포함된 배열입니다. 배열에 포함된 제안은 대부분 이벤트를 서버에 보낸 방식에 따라 결정됩니다.

이 첫 번째 시나리오에서는 을(를) 선택하지 않았다고 가정합니다. [!UICONTROL 렌더링 결정] 확인란 및 을(를) 제공하지 않음 [!UICONTROL 결정 범위] 의 내부 [!UICONTROL 이벤트 보내기] 이벤트 전송을 담당하는 작업입니다.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

이 예에서는 `propositions` 배열에는 자동 렌더링에 적합한 이벤트와 관련된 제안만 포함됩니다.

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

이벤트를 보낼 때 [!UICONTROL 렌더링 결정] 확인란을 선택하지 않았으므로 SDK가 자동으로 콘텐츠를 렌더링하지 않았습니다. 그러나 SDK는 자동 렌더링에 적합한 콘텐츠를 계속 자동으로 검색했으며, 원하는 경우 수동으로 렌더링하도록 제공했습니다. 각 제안 객체에는 다음과 같은 항목이 있습니다 `renderAttempted` 속성이 로 설정됨 `false`.

대신 다음을 확인하고자 했다면 [!UICONTROL 렌더링 결정] 확인란을 선택하면 SDK가 자동 렌더링에 적합한 제안을 렌더링하려고 시도했을 수 있습니다. 그 결과, 각각의 제안 대상은 다음을 가질 것이다 `renderAttempted` 속성이 로 설정됨 `true`. 이 경우 이러한 제안을 수동으로 렌더링할 필요가 없습니다.

지금까지 자동 렌더링에 적합한 개인화 콘텐츠(예: Adobe Target의 시각적 경험 작성기에서 만든 콘텐츠)만 살펴보았습니다. 개인화 콘텐츠를 검색하려면 _아님_ 자동 렌더링에 적격인 경우 다음을 사용하여 결정 범위를 제공하여 콘텐츠를 요청합니다. [!UICONTROL 결정 범위] 의 필드 [!UICONTROL 이벤트 보내기] 작업. 범위는 서버에서 검색할 특정 제안을 식별하는 문자열입니다.

다음 [!UICONTROL 이벤트 보내기] 작업은 다음과 같습니다.

![img.png](assets/send-event-render-unchecked-with-scopes.png)

이 예제에서 일치하는 서버에 제안이 있는 경우 `salutation` 또는 `discount` 범위, 반환되고 `propositions` 배열입니다. 자동 렌더링에 적합한 제안이 계속 `propositions` 스토리지 시스템(구성 방식에 관계없이) [!UICONTROL 렌더링 결정] 또는 [!UICONTROL 결정 범위] 의 필드 [!UICONTROL 이벤트 보내기] 작업. 다음 `propositions` 이 경우 배열은 다음 예제와 유사합니다.

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

이 시점에서 맞춤법이 보이는 대로 제안 콘텐츠를 렌더링할 수 있습니다. 이 예에서 제안과 일치하는 `discount` scope는 Adobe Target의 양식 기반 경험 작성기를 사용하여 작성된 HTML 제안입니다. 페이지에 ID가 인 요소가 있다고 가정합니다. `daily-special` 및 의 콘텐츠를 렌더링하고 싶습니다. `discount` 제안 내용: `daily-special` 요소를 생성하지 않습니다. 다음을 수행합니다.

1. 에서 제안 추출 `event` 개체.
1. 각 제안을 반복하고 다음 범위의 제안을 찾습니다. `discount`.
1. 명제를 찾으면 명제의 각 항목을 반복하여 HTML 콘텐츠인 항목을 찾습니다. (가정하는 것보다 확인하는 것이 좋습니다.)
1. HTML 콘텐츠가 들어 있는 항목을 찾으면 `daily-special` 요소를 만들고 해당 HTML을 개인화된 콘텐츠로 바꿉니다.

내의 사용자 지정 코드 [!UICONTROL 사용자 지정 코드] 작업은 다음과 같이 표시될 수 있습니다.

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

Adobe Target에서 반환된 개인화 컨텐츠에는 다음이 포함됩니다 [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html): 활동, 오퍼, 경험, 사용자 프로필, 지역 정보 등에 대한 세부 사항입니다. 이러한 세부 정보는 서드파티 도구와 공유하거나 디버깅에 사용할 수 있습니다. Adobe Target 사용자 인터페이스에서 응답 토큰을 구성할 수 있습니다.

응답 데이터 처리 규칙에 있는 사용자 지정 코드 작업에서 서버에서 반환된 개인화 제안에 액세스할 수 있습니다. 이렇게 하려면 다음 사용자 지정 코드를 입력합니다.

```javascript
var propositions = event.propositions;
```

If `event.propositions` 존재함. 개인화 제안 객체가 포함된 배열입니다. 다음을 참조하십시오 [개인화된 콘텐츠 수동 렌더링](#manually-render-personalized-content) 의 콘텐츠에 대한 자세한 내용은 `result.propositions`.

웹 SDK에서 자동으로 렌더링된 모든 명제에서 모든 활동 이름을 수집하여 단일 배열로 푸시한다고 가정합니다. 그런 다음 단일 스토리지를 서드파티로 전송할 수 있습니다. 이 경우 내부에 사용자 지정 코드를 작성합니다. [!UICONTROL 사용자 지정 코드] 작업 대상:

1. 에서 제안 추출 `event` 개체.
1. 각 제안을 반복합니다.
1. SDK가 제안을 제공했는지 확인합니다.
1. 그렇다면, 명제의 각 항목을 반복해라.
1. 에서 활동 이름 검색 `meta` 속성 : 응답 토큰이 포함된 객체입니다.
1. 활동 이름을 배열에 푸시합니다.
1. 활동 이름을 서드파티에 보냅니다.

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
