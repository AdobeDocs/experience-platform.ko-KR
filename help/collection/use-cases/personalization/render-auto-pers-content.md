---
title: DOM 작업 제안 자동 렌더링
description: 웹 SDK을 사용하여 적격한 DOM 작업 제안을 자동으로 렌더링하고 일반적인 SPA 다시 렌더링 시나리오를 처리할 수 있습니다.
keywords: 개인화;renderDecisions;dom-action;sendEvent;applyPropositions;단일 페이지 애플리케이션;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# DOM 작업 제안 자동 렌더링

개인화 응답에 스키마가 있는 제안 항목이 포함된 경우 이 패턴을 사용합니다.

**`https://ns.adobe.com/personalization/dom-action`**

이러한 항목에는 일반적으로 선택기와 `setHtml`이(가) 활성화되면 웹 SDK이 자동으로 적용할 수 있는 작업 유형(예: `renderDecisions`)이 포함됩니다.

## &#x200B;1. 플리커 관리(선택 사항)

개인화된 콘텐츠를 적용하는 동안 깜박임을 방지해야 하는 경우 구현에 권장되는 깜박임 관리 접근 방식을 사용하십시오. 사용 가능한 옵션은 [깜박임 관리](manage-flicker.md)를 참조하십시오.

## &#x200B;2. 자동 렌더링에 대한 요청 및 렌더링 결정

`renderDecisions` 명령을 호출할 때 `true`을(를) `sendEvent`(으)로 설정합니다. 생략하면 `renderDecisions` 속성의 기본값이 false로 설정됩니다.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

필요한 경우 특정 배치를 요청하려면 `personalization.decisionScopes`을(를) 포함합니다.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

자세한 내용은 [`personalization`](/help/collection/js/commands/sendevent/personalization.md) 명령의 [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) 개체를 참조하십시오.

## &#x200B;3. 이벤트 표시

`renderDecisions`을(를) `true`(으)로 설정하고 `personalization.sendDisplayEvent`을(를) `true`(으)로 설정하거나 생략하면 Web SDK에서 개인화가 렌더링된 직후 디스플레이 이벤트를 보냅니다.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

[상위 및 하위 페이지 이벤트](display-events.md)를 사용하는 경우와 같이 구현의 요구 사항에 맞는 대체 옵션을 보려면 [표시 이벤트 관리](top-bottom-page-events.md)를 참조하십시오.

## &#x200B;4. SPA 보기 변경 사항 및 다시 렌더링

단일 페이지 응용 프로그램의 경우 보기 변경 이벤트에 `viewName`을(를) 포함하십시오.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

SPA에서 새 의사 결정 가져오기 없이 동일한 보기에 대한 UI를 다시 렌더링하는 경우 이전에 반환된 제안을 다시 적용할 수 있습니다.

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

자세한 내용은 [`applyPropositions`](/help/collection/js/commands/applypropositions.md)을(를) 참조하십시오.

>[!NOTE]
>
>`applyPropositions` 명령은 표시 이벤트를 자동으로 보내지 않습니다. 시나리오를 다시 렌더링하기 위해 &quot;표시&quot;를 기록해야 하는 경우 [표시 이벤트 관리](display-events.md)를 참조하십시오.
