---
title: 수동으로 제안 렌더링
description: 고유한 UI 논리(HTML, JSON 또는 사용자 지정 스키마)를 사용하여 제안 콘텐츠를 렌더링한 다음 표시 이벤트를 기록합니다.
keywords: 개인화;제안;수동 렌더링;sendEvent;의사 결정 범위;이벤트 표시;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 수동으로 제안 렌더링

제안 항목이 적용되는 방식을 완전히 제어해야 하는 경우 이 패턴을 사용하십시오. 예를 들어, JSON 콘텐츠에서 복잡한 UI를 작성하거나 렌더링하기 전에 사용자 지정 비즈니스 규칙을 적용하려고 합니다.

## &#x200B;1. 제안 요청

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

자세한 내용은 [`personalization`](/help/collection/js/commands/sendevent/personalization.md) 명령의 [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) 개체를 참조하십시오.

## &#x200B;2. 렌더링 제안 항목(예)

수동으로 제안을 렌더링할 때 다양한 형태나 모양을 사용할 수 있습니다. 다음은 범위로 제안을 찾은 다음 찾은 첫 번째 HTML 콘텐츠 항목을 적용하는 최소 예입니다.

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>HTML을 렌더링하는 경우 환경에 안전한지 확인하십시오. 콘텐츠 렌더링을 보안 경계(정리, 신뢰할 수 있는 소스 및 CSP 고려 사항)로 처리합니다.

## &#x200B;3. 렌더링한 내용에 대한 표시 이벤트를 기록합니다

수동으로 렌더링된 제안에 대해 디스플레이 이벤트는 렌더링된 제안을 참조하는 `sendEvent` 호출을 통해 기록됩니다.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

자세한 내용은 [디스플레이 이벤트 관리](display-events.md)를 참조하십시오.

## &#x200B;4. 재렌더링

UI 변경 사항에 다시 렌더링이 필요한 경우 캐시한 제안 데이터에 대해 수동 렌더링 논리를 다시 실행합니다(또는 필요한 경우 다시 가져오기). 시나리오를 다시 렌더링하기 위해 표시를 기록해야 하는 경우 [표시 이벤트 관리](display-events.md)를 참조하십시오.
