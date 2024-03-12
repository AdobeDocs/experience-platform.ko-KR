---
title: Web SDK에서 페이지 이벤트의 상단 및 하단 구성
description: 이 문서에서는 Web SDK에서 페이지 이벤트의 상단과 하단을 사용하는 방법에 대해 설명합니다.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 4d0895c6ad38523f5527c9630931c3c0b8ef83c0
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 1%

---


# Web SDK에서 페이지 이벤트의 상단 및 하단 구성

개인화된 경험을 고객에게 전달하려면 웹 페이지의 로딩 시간이 필수적입니다.

로드 시간을 최적화하고 개인화를 가능한 한 빨리 제공하기 위해 Web SDK는 페이지 이벤트의 상단과 하단의 구성을 지원합니다.

페이지 이벤트의 상단 및 하단은 페이지 로드 시간을 최소로 유지하면서 페이지에 있는 다양한 요소를 비동기적으로 로드하는 방법을 설명합니다.

이 구성은 개인화된 콘텐츠가 로드될 때까지 사용자가 기다려야 하는 시간을 최소화합니다.

지표 정확도 측면에서 Adobe Analytics은 페이지 이벤트의 위쪽을 무시할 수 있으므로, 페이지 히트가 한 개만 기록되므로(페이지 이벤트의 아래쪽) 더 정확한 지표 기록으로 이어집니다.

## 사용 사례 {#use-cases}

스포츠 의류 소매업체는 방문자 지표를 정확하게 수집하는 동시에 웹 사이트를 방문할 때 사용자 마찰을 최소화하면서 쇼핑객에게 개인화된 경험을 전달하려고 합니다.

마케팅 팀은 Web SDK에서 페이지 이벤트의 맨 위와 아래를 사용하여 최적의 방식으로 개인화 게재를 구성할 수 있습니다.

* Web SDK는 페이지가 로드되기 시작하는 즉시 로드되는 개인화 요청을 전송합니다. 페이지 이벤트의 맨 위입니다.
* 페이지 로드가 완료되면 페이지 보기 이벤트가 기록됩니다. 이 문제는 페이지 로드 프로세스 뒷부분에서 발생합니다. 페이지 이벤트 아래입니다.

## 페이지 상단 이벤트 예 {#top-of-page}

아래 코드 샘플은 개인화를 요청하지만 요청하지 않는 페이지 이벤트 구성의 맨 위를 나타냅니다 [디스플레이 이벤트 보내기](../personalization/display-events.md#send-sendEvent-calls) 자동으로 렌더링된 제안에 사용됩니다. 다음 [이벤트 표시](../personalization/display-events.md#send-sendEvent-calls) 은 페이지 하단 이벤트의 일부로 전송됩니다.

>[!BEGINTABS]

>[!TAB 페이지 상단 이벤트]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| 매개 변수 | 필수/선택 사항 | 설명 |
|---|---|---|
| `type` | 필수 여부 | 이 매개 변수를 다음으로 설정 `decisioning.propositionFetch`. 이 특수 이벤트 유형은 Adobe Analytics에 이 이벤트를 삭제하도록 지시합니다. Customer Journey Analytics을 사용할 때 이러한 이벤트를 삭제하도록 필터를 설정할 수도 있습니다. |
| `renderDecisions` | 필수 여부 | 이 매개 변수를 다음으로 설정 `true`. 이 매개 변수는 Edge Network에서 반환한 결정을 렌더링하도록 Web SDK에 지시합니다. |
| `personalization.sendDisplayEvent` | 필수 여부 | 이 매개 변수를 다음으로 설정 `false`. 이렇게 하면 디스플레이 이벤트의 전송이 중지됩니다. |

>[!ENDTABS]

## 페이지 하단 이벤트 예 {#bottom-of-page}

>[!BEGINTABS]

>[!TAB 자동 렌더링된 제안]

아래 코드 샘플은 페이지에 자동으로 렌더링되었지만 에서 디스플레이 이벤트가 억제된 제안에 대한 디스플레이 이벤트를 전송하는 페이지 이벤트 구성의 아래쪽을 나타냅니다 [페이지 상단](#top-of-page) 이벤트.

>[!NOTE]
>
>이 시나리오에서는 페이지 이벤트의 하단을 호출해야 합니다 _이후_ 1페이지의 맨 위에 있습니다. 그러나 페이지 하단의 이벤트는 페이지 1의 상단이 완료될 때까지 기다릴 필요가 없습니다.

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| 매개변수 | 필수/선택 사항 | 설명 |
|---|---|---|
| `personalization.includeRenderedPropositions` | 필수 여부 | 이 매개 변수를 다음으로 설정 `true`. 이렇게 하면 페이지 이벤트의 맨 위에서 억제된 표시 이벤트를 보낼 수 있습니다. |
| `xdm` | 선택 사항입니다 | 이 섹션을 사용하여 페이지 이벤트 하단에 필요한 모든 데이터를 포함합니다. |

>[!TAB 수동으로 렌더링된 제안]

아래 코드 샘플은 페이지에 수동으로 렌더링된 제안에 대해(즉, 사용자 지정 결정 범위 또는 표면에 대해) 디스플레이 이벤트를 전송하는 페이지 이벤트 구성의 아래쪽을 구현합니다.

>[!NOTE]
>
>이 시나리오에서 페이지 이벤트의 하단은 페이지 이벤트의 상단이 완료될 때까지 기다렸다가 제안을 렌더링하고 페이지 이벤트의 하단을 기록해야 합니다.

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```



| 매개 변수 | 필수/선택 사항 | 설명 |
|---|---|---|
| `xdm._experience.decisioning.propositions` | 필수 여부 | 이 섹션에서는 수동으로 렌더링된 제안을 정의합니다. 이 제안을 포함해야 합니다. `ID`, `scope`, 및 `scopeDetails`. 방법 설명서 참조 [수동으로 개인화 렌더링](../personalization/rendering-personalization-content.md#manually) 수동으로 렌더링된 콘텐츠의 디스플레이 이벤트를 기록하는 방법에 대한 자세한 정보. 수동으로 렌더링된 개인화 콘텐츠는 페이지 조회수 하단에 포함되어야 합니다. |
| `xdm._experience.decisioning.propositionEventType` | 필수 여부 | 이 매개 변수를 다음으로 설정 `display: 1`. |
| `xdm` | 선택 사항입니다 | 이 섹션을 사용하여 페이지 이벤트 하단에 필요한 모든 데이터를 포함합니다. |

>[!ENDTABS]


## 상위 및 하위 페이지 히트가 있는 단일 페이지 애플리케이션 {#spa-example}


>[!BEGINTABS]

>[!TAB 첫 페이지 보기]

아래 예에는 필요한 를 추가하는 작업이 포함되어 있습니다 `xdm.web.webPageDetails.viewName` 매개 변수. 이것이 바로 단일 페이지 애플리케이션입니다. 다음 `viewName` 이 예제는 페이지 로드에서 로드되는 보기입니다.

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB 두 번째 페이지 보기(옵션 1)]

이 예제에서는 페이지에 대한 개인화를 이미 가져왔으므로 페이지 분할을 상단/하단으로 수행할 필요가 없습니다.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```


>[!TAB 두 번째 페이지 보기(옵션 2)]

여전히 페이지 히트의 하단을 지연해야 하는 경우 다음을 사용할 수 있습니다. `applyPropositions` 페이지 조회수의 맨 위에 사용됩니다. 개인화를 가져올 필요가 없고 Analytics 데이터를 기록할 필요가 없으므로 Edge Network에 요청할 필요가 없습니다.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!ENDTABS]

## GitHub 샘플 {#github-sample}

다음 위치에 있는 샘플: [이 주소](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) Experience Platform 및 Web SDK를 사용하여 페이지 맨 위에서 개인화를 요청하고 맨 아래에서 분석 지표를 전송하는 방법을 보여 줍니다. 샘플을 다운로드하여 로컬에서 실행하여 페이지 이벤트의 상단과 하단의 작동 방식을 이해할 수 있습니다.
