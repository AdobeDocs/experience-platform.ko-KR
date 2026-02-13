---
title: 웹 SDK에서 디스플레이 이벤트 관리
description: 디스플레이 이벤트의 정의와 웹 SDK에서 디스플레이 이벤트를 사용하는 방법에 대해 설명합니다.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: 개인화;이벤트 표시;sendEvent;renderDecisions;적용 제안;제안;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 웹 SDK에서 디스플레이 이벤트 관리

디스플레이 이벤트는 개인화된 특정 콘텐츠가 사용자에게 표시되었음을 개인화 또는 분석 서비스에 알려줍니다. 디스플레이 이벤트를 보내면 다운스트림 시스템에서 *요청된*&#x200B;콘텐츠와 *실제로 표시된*&#x200B;콘텐츠를 구별하여 보고 정확도가 향상됩니다.

## 디스플레이 이벤트를 자동으로 보내기

자동 표시 이벤트는 일반적으로 가장 간단한 옵션입니다. Web SDK에서 `sendEvent` 응답에서 적격한 콘텐츠 렌더링을 마치면 바로 전송됩니다. 이렇게 하면 보고 정확도가 향상될 수 있습니다.

표시 이벤트를 자동으로 보내려면 `sendEvent`을(를) `renderDecisions`(으)로 설정하고 `true`을(를) `personalization.sendDisplayEvent`(으)로 설정하는 `true` 호출을 사용합니다(또는 `true`이(가) 기본값이므로 생략).

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>자동 표시 이벤트는 SDK 관리 렌더링에 따라 다릅니다. 콘텐츠를 수동으로 렌더링하는 경우(`applyPropositions` 사용 포함) `sendEvent`을(를) 사용하여 디스플레이 이벤트를 명시적으로 보내야 합니다.

## 후속 `sendEvent` 호출에서 표시 이벤트 보내기

나중에 `sendEvent` 호출에 표시 이벤트를 포함하면 개인화를 요청할 때 사용할 수 없는 추가 페이지 로드 데이터를 첨부하려는 경우 유용합니다. [상위 및 하위 페이지 이벤트](/help/collection/use-cases/personalization/top-bottom-page-events.md)를 구현할 때 일반적으로 사용됩니다. 이 방식으로 디스플레이 이벤트를 올바르게 구현하면 Adobe Analytics에서 [바운스 비율](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/bounce-rate)에 문제가 발생하지 않습니다.

1. 초기 `sendEvent` 호출 시(종종 페이지 맨 위에서) 콘텐츠를 요청하고 렌더링하되, `renderDecisions`을(를) `true`(으)로, `personalization.sendDisplayEvent`을(를) `false`(으)로 설정하여 자동 표시 이벤트를 표시하지 않습니다.

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. 나중에(종종 페이지 맨 아래에서) `sendEvent`을(를) [`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md)(으)로 설정하여 이전 요청 이후 렌더링된 제안에 대한 표시 이벤트를 포함하는 XDM 페이로드로 `true`을(를) 호출합니다.

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>`includeRenderedPropositions`을(를) 사용할 때 표시되지 않은 자동으로 렌더링된 제안만 포함됩니다.

## 수동으로 렌더링된 제안에 대한 디스플레이 이벤트 보내기

콘텐츠를 직접 렌더링하는 경우(완전 수동 렌더링 또는 `applyPropositions` 사용) `sendEvent` 명령을 사용하여 디스플레이 이벤트를 명시적으로 보내야 합니다. 다음 속성을 포함하는 XDM 페이로드로 `sendEvent`을(를) 호출합니다.

* 렌더링된 제안 `_experience.decisioning.propositions`, `id` 및 `scope`이(가) 포함된 `scopeDetails`
* `_experience.decisioning.propositionEventType.display`이(가) `1`(으)로 설정됨

다음 두 예제에서는 이 도우미 함수를 사용하여 표시 이벤트 XDM 페이로드를 빌드합니다.

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

다음 예제에서는 디스플레이 이벤트와 함께 수동 렌더링을 사용합니다.

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

다음 예제에서는 디스플레이 이벤트에 `applyPropositions` 명령을 사용합니다. `sendEvent`, `applyPropositions`을(를) 연결한 다음 다른 `sendEvent`을(를) 함께 연결합니다.

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## 피해야 할 일반적인 실수

* **렌더링이 완료되기 전에 디스플레이 이벤트 보내기**: 자동 렌더링이 완료된 후, `applyPropositions`이(가) 해결된 후 또는 수동 렌더링 논리가 완료된 후 디스플레이 이벤트를 보냅니다.
* **렌더링하지 않은 제안에 대한 표시 이벤트를 보냅니다**: 사용자에게 실제로 표시된 제안만 포함합니다.
* **`scopeDetails`** 삭제: 표시 이벤트를 보낼 때 제안 개체에서 `scopeDetails`을(를) 포함합니다.
