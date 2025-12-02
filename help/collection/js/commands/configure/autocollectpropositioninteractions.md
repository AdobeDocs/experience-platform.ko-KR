---
title: autoCollectPropositionInteractions
description: 링크를 클릭하면 자동으로 데이터를 수집합니다.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

`autoCollectPropositionInteractions` 속성은 웹 SDK에서 제안 상호 작용을 자동으로 수집하는지 여부를 결정하는 선택적 설정입니다. 이 값은 의사 결정 공급자의 맵으로, 각각은 자동 제안 상호 작용이 어떻게 처리되어야 하는지를 나타내는 값을 갖습니다.

자동 제안 상호 작용 추적을 활성화하면 DOM에 렌더링된 제안 요소 내의 모든 클릭 수가 웹 SDK에 의해 자동으로 수집됩니다. 이 컬렉션에는 웹 SDK에 의해 DOM에 자동으로 렌더링된 모든 경험과 [`applyPropositions`](../applypropositions.md) 명령을 사용하여 DOM에 렌더링된 경험이 포함됩니다.

웹 SDK을 구성할 때 이 속성을 생략하면 기본적으로 `{"AJO": "always", "TGT": "never"}`이(가) 됩니다. 제안 상호 작용을 자동으로 추적하지 않으려면 값을 `{"AJO": "never", "TGT": "never"}`(으)로 설정하십시오.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

이 개체에서 지원되는 속성은 다음과 같습니다.

| 속성 | 설명 |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer. |
| **`TGT`** | Adobe Target. |

각 속성에 대해 가능한 값은 다음과 같습니다.

| 값 | 설명 |
| --- | --- |
| **`always`** | 명제와 연결된 모든 요소에 대해 항상 `interact` 이벤트를 자동으로 수집합니다. |
| **`never`** | 명제와 연결된 요소에 대한 `interact` 이벤트를 자동으로 수집하지 않습니다. |
| **`decoratedElementsOnly`** | 요소에 레이블이나 토큰을 지정하는 데이터 특성이 포함된 경우 명제와 연결된 요소에 대한 `interact` 이벤트를 자동으로 수집합니다. |

## 데이터 속성 {#data-attributes}

요소에 대한 데이터 속성을 사용하여 상호 작용에 특수성을 추가할 수 있습니다.

| 이름 | 데이터 속성 | 설명 |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | 레이블 데이터 속성이 클릭한 요소에 있으면 Edge Network으로 전송된 상호 작용 세부 정보에 포함됩니다. 웹 SDK은 클릭한 요소로 시작하여 DOM 트리 위로 이동하는 레이블 데이터 속성을 찾습니다. 웹 SDK은 처음 찾은 레이블을 사용합니다. |
| **[!UICONTROL Token]** | `data-aep-click-token` | [Adobe Journey Optimizer 코드 기반 캠페인](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/code-based-experience/get-started-code-based)에서 의사 결정 정책을 활용할 때 이 토큰을 사용하십시오. 토큰을 사용하여 클릭한 결정 정책 항목을 구분할 수 있습니다. 토큰 데이터 속성은 클릭한 요소에 있으면 Edge Network으로 전송된 상호 작용 세부 정보에 포함됩니다. 웹 SDK은 클릭한 요소로 시작하여 DOM 트리를 올라가는 토큰 데이터 속성을 찾습니다. 웹 SDK은 찾은 첫 번째 토큰을 사용합니다. |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | 웹 SDK은 제안을 렌더링할 때 이 고유 ID를 컨테이너 요소에 자동으로 추가합니다. 웹 SDK은 이 ID를 사용하여 DOM 요소와 제안을 상호 연관시킵니다. 웹 SDK에 필요한 ID이므로 어떤 식으로든 변경해서는 안 됩니다. 무시해도 됩니다. |

## 예

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### `autoCollectPropositionInteractions` 명령과 함께 `applyPropositions` 사용 {#apply-propositions}

[`applyPropositions`](../applypropositions.md) 명령은 DOM에 제안을 렌더링하는 편리한 방법입니다. 그러나 JSON이 있는 코드 기반 캠페인의 경우 이 명령을 사용하여 기존 DOM 요소(또는 JSON 값을 기반으로 화면에 렌더링된 애플리케이션 코드)를 명제와 상호 연관시킬 수 있습니다.

이러한 상관관계는 해당 요소에 대한 자동 상호 작용 추적을 활성화하고 해당 요소에 적절한 명제를 할당합니다. 이렇게 하려면 `actionType`을(를) `track`(으)로 설정합니다.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## 웹 SDK 태그 확장에 대한 자동 제안 상호 작용 구성

웹 SDK 태그 확장을 구성할 때 다음 두 드롭다운 메뉴는 이 오브젝트와 동일한 태그입니다.

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
