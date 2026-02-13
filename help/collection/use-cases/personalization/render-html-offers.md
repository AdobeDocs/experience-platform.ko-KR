---
title: 선택기 없이 HTML 오퍼 렌더링
description: 메타데이터를 applyPropositions에 제공하여 선택기를 포함하지 않는 HTML 제안 항목을 렌더링한 다음 표시 이벤트를 기록합니다.
keywords: 개인화;적용 제안;메타데이터;actionType;의사 결정 범위;이벤트 표시;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 선택기 없이 HTML 오퍼 렌더링

제안에 HTML 컨텐츠가 포함되어 있지만 적용할 위치(선택기)와 적용 방법(작업 유형)을 제공해야 하는 경우 이 패턴을 사용하십시오. 범위를 기준으로 [`applyPropositions`](/help/collection/js/commands/applypropositions.md) 개체를 사용하여 `metadata`을(를) 호출하여 이 작업을 수행할 수 있습니다. 지원되는 `actionType` 값은 `setHtml`, `replaceHtml` 및 `appendHtml`입니다.

## &#x200B;1. 플리커 관리(선택 사항)

렌더링하는 동안 컨텐츠를 숨기면 렌더링이 완료된 후 표시할 책임이 있습니다. 자세한 내용은 [깜박임 관리](manage-flicker.md)를 참조하십시오.

## &#x200B;2. 렌더링하려는 범위에 대한 제안 요청

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

자세한 내용은 [`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md)을(를) 참조하십시오.

## &#x200B;3. `applyPropositions` 메타데이터로 오퍼 렌더링

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## &#x200B;4. 렌더링된 제안에 대한 표시 이벤트 기록

`applyPropositions`을(를) 호출할 때 디스플레이 이벤트가 자동으로 전송되지 않습니다. 렌더링이 완료된 후 렌더링된 제안을 참조하는 `sendEvent` 호출을 사용합니다.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

자세한 내용은 [디스플레이 이벤트 관리](display-events.md)를 참조하십시오.

>[!TIP]
>
>[상위 및 하위 페이지 이벤트](top-bottom-page-events.md)를 사용하는 경우 일반적으로 이 &quot;레코드 표시&quot; 호출은 하위 `sendEvent` 호출에서 구현됩니다.

## &#x200B;5. 다시 렌더링

구현이 나중에 다시 렌더링해야 하는 경우(예: 단일 페이지 애플리케이션) 동일한 제안 및 메타데이터로 `applyPropositions`을(를) 다시 호출하십시오.

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

다시 렌더링할 표시 이벤트를 기록해야 하는 경우 [표시 이벤트 관리](display-events.md)를 참조하십시오.
