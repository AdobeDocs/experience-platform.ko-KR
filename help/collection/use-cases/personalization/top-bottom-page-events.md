---
title: 웹 SDK에서 페이지 이벤트의 상단 및 하단 구성
description: 이 문서에서는 Web SDK에서 페이지 이벤트의 상단과 하단을 사용하는 방법에 대해 설명합니다.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# 웹 SDK에서 페이지 이벤트의 상단 및 하단 구성

개인화된 경험을 제공할 때 웹 페이지의 로드 시간은 필수적입니다. 웹 SDK에서는 사용자가 개인화된 컨텐츠를 기다리는 시간을 최소화하기 위해 페이지 이벤트의 상단과 하단의 구성을 지원합니다.

페이지 이벤트의 상단 및 하단은 페이지 로드 시간을 최소로 유지하면서 페이지에 있는 다양한 요소를 비동기적으로 로드하는 방법을 설명합니다.

* 페이지 이벤트 상단은 페이지 로드가 시작되자마자 개인화를 요청합니다.
* 페이지 이벤트 하단은 페이지 로드가 완료되면 페이지 보기를 기록합니다.

Adobe Analytics에서는 페이지 상단 이벤트를 무시하므로 하나의 페이지 히트만 기록되므로(페이지 이벤트 하단) 더 정확한 지표 기록으로 이어집니다.

웹 SDK JavaScript 라이브러리(`alloy()`)를 직접 호출하거나 Adobe Experience Platform 태그 UI에서 웹 SDK 태그 확장 기능을 사용하여 페이지 이벤트의 맨 위와 맨 아래 부분을 구성할 수 있습니다. 태그 확장의 [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) 작업에는 &#39;[!UICONTROL Use guided events]&#39;(페이지 상단) 및 &#39;[!UICONTROL Request personalization]&#39;(페이지 하단) 시나리오에 대한 필드 값을 미리 구성하는 &#39;[!UICONTROL Collect analytics]&#39; 옵션이 포함되어 있습니다. 아래의 각 예제는 두 구현을 모두 보여 줍니다.

## 페이지 상단 이벤트 {#top-of-page}

아래 예제는 개인화를 요청하지만 자동으로 렌더링된 제안에 대해 [이벤트 표시](display-events.md)를 제외하는 페이지 이벤트의 맨 위를 구성합니다. 이러한 디스플레이 이벤트는 페이지 이벤트 하단과 함께 대신 전송됩니다.

>[!BEGINTABS]

>[!TAB JavaScript 라이브러리]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| 매개변수 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| `type` | 필수 여부 | 이 매개 변수를 `decisioning.propositionFetch`(으)로 설정하십시오. 이 특수 이벤트 유형은 Adobe Analytics에 이 이벤트를 삭제하도록 지시합니다. Customer Journey Analytics을 사용할 때 이러한 이벤트를 삭제하는 필터를 설정할 수도 있습니다. 자세한 내용은 [Adobe Analytics의 Edge Network 이벤트 유형](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types)을 참조하십시오. |
| `renderDecisions` | 필수 여부 | 이 매개 변수를 `true`(으)로 설정하십시오. 이 매개 변수는 Web SDK에 Edge Network에서 반환한 결정을 렌더링하도록 지시합니다. |
| `personalization.sendDisplayEvent` | 필수 여부 | 이 매개 변수를 `false`(으)로 설정하십시오. 이 매개 변수는 디스플레이 이벤트의 전송을 중지합니다. |

>[!TAB 웹 SDK 태그 확장]

페이지 맨 위에서 실행되는 규칙에서 [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) 작업을 구성합니다. **[!UICONTROL Use guided events]**&#x200B;을(를) 사용하도록 설정한 다음 **[!UICONTROL Request personalization]**&#x200B;을(를) 선택합니다. 이 옵션은 &#39;[!UICONTROL Type]&#39;을(를) &#39;[!UICONTROL Decisioning Proposition Fetch]&#39;(으)로 잠그고, &#39;[!UICONTROL Render visual personalization decisions]&#39;을(를) 사용하도록 설정하고, &#39;[!UICONTROL Automatically send a display event]&#39;을(를) 사용하지 않도록 설정합니다.

이러한 필드를 수동으로 설정하려면 **[!UICONTROL Use guided events]**&#x200B;을(를) 사용하지 않도록 설정하고 각 필드를 직접 구성하십시오.

>[!ENDTABS]

## 페이지 하단 이벤트 예 {#bottom-of-page}

### 자동 렌더링된 제안 {#bottom-auto-rendered}

아래 예제는 페이지에서 자동으로 렌더링되었지만 [페이지 상단](#top-of-page) 이벤트에서 제외된 제안에 대해 디스플레이 이벤트를 보내는 페이지 하단 이벤트를 구성합니다.

>[!BEGINTABS]

>[!TAB JavaScript 라이브러리]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| 매개변수 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | 필수 여부 | 이 매개 변수를 `true`(으)로 설정하십시오. 이 매개 변수를 사용하면 페이지 이벤트의 맨 위에서 억제된 디스플레이 이벤트를 전송할 수 있습니다. |
| `xdm` | 선택 사항입니다 | 이 개체를 사용하여 페이지 이벤트의 맨 아래에 사용할 모든 데이터를 포함합니다. |

>[!TAB 웹 SDK 태그 확장]

페이지 맨 아래에서 실행되는 규칙에서 [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) 작업을 구성하십시오. **[!UICONTROL Use guided events]**&#x200B;을(를) 사용하도록 설정한 다음 **[!UICONTROL Collect analytics]**&#x200B;을(를) 선택합니다. 이 옵션은 &#39;[!UICONTROL Include rendered propositions]&#39;을(를) 사용하도록 잠급니다.

이 필드를 수동으로 설정하려면 **[!UICONTROL Use guided events]**&#x200B;을(를) 사용하지 않도록 설정하고 **[!UICONTROL Include rendered propositions]**&#x200B;을(를) 직접 활성화하십시오. 필요한 경우 **[!UICONTROL XDM]** 필드를 페이지 데이터를 전송하는 [XDM 개체](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) 데이터 요소로 채웁니다.

>[!ENDTABS]

### 수동으로 렌더링된 제안 {#bottom-manually-rendered}

아래 예제는 페이지에서 수동으로 렌더링된 제안(즉, 사용자 지정 결정 범위 또는 표면)에 대한 표시 이벤트를 전송하는 페이지 이벤트의 하단을 구성합니다.

>[!NOTE]
>
>이 시나리오에서는 제안을 렌더링하고 기록할 수 있도록 페이지 이벤트의 하단이 페이지 이벤트의 상단이 완료될 때까지 기다려야 합니다.

>[!BEGINTABS]

>[!TAB JavaScript 라이브러리]

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

| 매개변수 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | 필수 여부 | 이 섹션에서는 수동으로 렌더링된 제안을 정의합니다. 제안 `id`, `scope` 및 `scopeDetails`을(를) 포함해야 합니다. 자세한 내용은 [디스플레이 이벤트 관리](display-events.md)를 참조하십시오. 수동으로 렌더링된 개인화 콘텐츠는 페이지 이벤트 하단에 포함되어야 합니다. |
| `xdm._experience.decisioning.propositionEventType` | 필수 여부 | 이 매개 변수를 `display: 1`(으)로 설정하십시오. |
| `xdm` | 선택 사항입니다 | 이 개체를 사용하여 페이지 이벤트의 맨 아래에 사용할 모든 데이터를 포함합니다. |

>[!TAB 웹 SDK 태그 확장]

&#39;[!UICONTROL Use guided events]&#39; 옵션은 이 시나리오를 다루지 않으므로 작업을 수동으로 구성하십시오.

1. 렌더링된 각 명제의 [, ](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) 및 [(으)로 ](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)을(를) 채우고 `_experience.decisioning.propositions`을(를) `id`(으)로 설정하는 `scope`XDM 개체`scopeDetails`(또는 `_experience.decisioning.propositionEventType.display`변수`1`) 데이터 요소를 만듭니다. 자세한 내용은 [디스플레이 이벤트 관리](display-events.md)를 참조하십시오.
1. 페이지 규칙의 맨 아래에 대한 [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) 작업에서 **[!UICONTROL Use guided events]**&#x200B;을(를) 사용하지 않도록 설정하고 **[!UICONTROL XDM]** 필드의 데이터 요소를 참조합니다.

>[!ENDTABS]

## 페이지 이벤트의 상단과 하단이 있는 단일 페이지 애플리케이션 {#spa-example}

단일 페이지 애플리케이션에서는 웹 SDK이 페이지 맨 위에서 올바른 개인화를 렌더링하고 페이지 맨 아래에 올바른 보기를 기록할 수 있도록 각 보기 변경 시 보기 이름을 지정해야 합니다.

### 첫 페이지 보기 {#spa-first-view}

이 예제에서 `home`은 초기 페이지 로드 시 로드되는 보기입니다.

>[!BEGINTABS]

>[!TAB JavaScript 라이브러리]

상위 호출이 Analytics 히트를 기록하거나 디스플레이 이벤트를 실행하지 않고 `home` 보기에 대한 개인화를 요청합니다. bottom 호출은 페이지 보기를 기록하고 억제된 디스플레이 이벤트를 실행합니다. 보기가 일관되게 기록되도록 두 호출에 동일한 `viewName`을(를) 포함하십시오.

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

>[!TAB 웹 SDK 태그 확장]

1. [을(를) 보기의 이름(예: ](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object))으로 설정하는 `web.webPageDetails.viewName`XDM 개체`home` 데이터 요소를 만듭니다.
1. 페이지 상단 [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) 작업을 구성하십시오. **[!UICONTROL Use guided events]**&#x200B;을(를) 활성화하고 **[!UICONTROL Request personalization]**&#x200B;을(를) 선택한 다음 **[!UICONTROL XDM]** 필드의 데이터 요소를 참조하십시오.
1. **[!UICONTROL Send event]** 페이지의 하단 작업을 구성하십시오. **[!UICONTROL Use guided events]**&#x200B;을(를) 활성화하고 **[!UICONTROL Collect analytics]**&#x200B;을(를) 선택한 다음 **[!UICONTROL XDM]** 필드에서 동일한 데이터 요소를 참조하여 `viewName`이(가) 두 이벤트에서 일치하게 하십시오.

>[!ENDTABS]

### 두 번째 페이지 보기 — 옵션 1 {#spa-second-view-option-1}

이 예에서는 페이지에 대한 개인화를 이미 가져왔으므로 단일 이벤트로 충분합니다.

>[!BEGINTABS]

>[!TAB JavaScript 라이브러리]

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

>[!TAB 웹 SDK 태그 확장]

1. [을(를) 새 보기의 이름(예: ](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object))으로 설정하는 `web.webPageDetails.viewName`XDM 개체`cart` 데이터 요소를 만듭니다.
1. 보기 변경 시 단일 [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) 작업을 구성하십시오. **[!UICONTROL Use guided events]**&#x200B;을(를) 사용하지 않도록 설정하고 **[!UICONTROL Render visual personalization decisions]**&#x200B;을(를) 사용하도록 설정하고 **[!UICONTROL XDM]** 필드의 데이터 요소를 참조합니다.

>[!ENDTABS]

### 두 번째 페이지 보기 — 옵션 2 {#spa-second-view-option-2}

페이지 이벤트의 하단을 지연해야 할 때(예: 보기 변경 시 페이지의 분석 데이터가 준비되지 않은 경우) 이 접근 방식을 사용합니다. 다음 두 단계로 보기 변경을 처리합니다.

1. 페이지 맨 위에서 Edge Network 호출을 수행하지 않고 이미 가져온 제안을 렌더링합니다.
1. 분석 데이터가 준비되면 페이지 이벤트의 맨 아래를 보냅니다.

보기가 일관되게 기록되도록 두 호출에 동일한 `viewName`을(를) 포함하십시오.

>[!BEGINTABS]

>[!TAB JavaScript 라이브러리]

페이지 맨 위에서 [`applyPropositions`](/help/collection/js/commands/applypropositions.md)을(를) 호출하여 새 보기에 대해 캐시된 제안을 렌더링합니다. 그런 다음 페이지 하단에 있는 `sendEvent`을(를) `includeRenderedPropositions: true`(으)로 호출하여 숨겨진 표시 이벤트가 실행되도록 합니다.

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
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

>[!TAB 웹 SDK 태그 확장]

1. [을(를) 새 보기의 이름(예: ](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object))으로 설정하는 `web.webPageDetails.viewName`XDM 개체`cart` 데이터 요소를 만듭니다.
1. 페이지 이벤트의 맨 위에 대해 [[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) 작업을 구성하고 **[!UICONTROL View name]** 필드를 보기의 이름(예: `cart`)으로 설정합니다. 이 작업은 Edge Network에 연결하지 않고 이미 가져온 제안을 렌더링합니다.
1. 페이지 이벤트의 맨 아래에 대해 [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) 작업을 구성하십시오. **[!UICONTROL Use guided events]**&#x200B;을(를) 활성화하고 **[!UICONTROL Collect analytics]**&#x200B;을(를) 선택한 다음 **[!UICONTROL XDM]** 필드의 데이터 요소를 참조하십시오.

>[!ENDTABS]

## GitHub 샘플 {#github-sample}

alloy-samples 저장소의 [최상위 및 최하위 샘플](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom)은 페이지 맨 위에서 개인화를 요청하고 맨 아래에서 분석 지표를 보내는 방법을 보여 줍니다. 샘플을 다운로드하고 로컬로 실행하여 페이지 이벤트의 상단과 하단의 작동 방식을 확인합니다. 이 샘플은 JavaScript 라이브러리를 직접 사용합니다. 웹 SDK 태그 확장에서 동일한 규칙을 구성할 때에도 동일한 패턴이 적용됩니다.
