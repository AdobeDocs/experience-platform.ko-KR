---
title: autoTrackPropositionInteractionsEnabled
description: 링크 데이터를 자동으로 수집하도록 Experience Platform Web SDK를 구성하는 방법에 대해 알아봅니다.
source-git-commit: ec5fd1c8228388ced96f58476e0174c8a0ff00df
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---


# `autoTrackPropositionInteractionsEnabled`

`autoTrackPropositionInteractionsEnabled` 속성은 웹 SDK에서 제안 상호 작용을 자동으로 수집해야 하는지 여부를 결정하는 선택적 설정입니다.

이 값은 의사 결정 공급자의 맵으로, 각각은 자동 제안 상호 작용이 어떻게 처리되어야 하는지를 나타내는 값을 갖습니다.

## 지원되는 값 {#supported-values}

기본적으로 자동 제안 상호 작용은 Adobe Journey Optimizer(`AJO`)에 대해 _항상_&#x200B;이 수집되고 Adobe Target(`TGT`)에 대해 _절대_&#x200B;이 수집됩니다.

`autoTrackPropositionInteractions`의 기본값이 아래에 표시되어 있습니다.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

각 의사 결정 공급자에 대해 지원되는 구성 값은 아래 표를 참조하십시오.

| 값 | 설명 |
| --- | --- |
| `always` | [!DNL Web SDK]은(는) 명제와 연결된 모든 요소에 대해 항상 `interact`개의 이벤트를 자동으로 수집합니다. |
| `never` | [!DNL Web SDK]은(는) 명제와 연결된 요소에 대해 `interact` 이벤트를 자동으로 수집하지 않습니다. |
| `decoratedElementsOnly` | [!DNL Web SDK]은(는) 명제와 연결된 요소에 대해 `interact` 이벤트를 자동으로 수집하지만, 요소에 레이블이나 토큰을 지정하는 데이터 특성이 포함된 경우에만 수집됩니다. |

## 자동 제안 상호 작용 추적 {#logic}

자동 제안 상호 작용 추적을 활성화하면 DOM에 렌더링된 제안 요소 내의 모든 클릭 수가 [!DNL Web SDK]에 의해 자동으로 수집됩니다. 여기에는 [!DNL Web SDK]에 의해 DOM에 자동으로 렌더링된 모든 경험과 [`applyPropositions`](../applypropositions.md) 명령을 사용하여 DOM에 렌더링된 경험이 포함됩니다.

### 데이터 속성 {#data-attributes}

요소에 대한 데이터 속성을 사용하여 상호 작용에 특수성을 추가할 수 있습니다.

| 이름 | 데이터 속성 | 설명 |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | 레이블 데이터 특성이 클릭한 요소에 있으면 [!DNL Edge Network](으)로 전송된 상호 작용 세부 정보에 포함됩니다. [!DNL Web SDK]은(는) 클릭한 요소로 시작하여 DOM 트리 위로 이동하는 레이블 데이터 특성을 찾습니다. [!DNL Web SDK]은(는) 찾은 첫 번째 레이블을 사용합니다. |
| [!DNL Token] | `data-aep-click-token` | [Adobe Journey Optimizer 코드 기반 캠페인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based)에서 의사 결정 정책을 활용할 때 이 토큰을 사용하십시오. 토큰을 사용하여 클릭한 결정 정책 항목을 구분할 수 있습니다. 토큰 데이터 속성은 클릭한 요소에 있으면 Edge Network에게 전송된 상호 작용 세부 정보에 포함됩니다. [!DNL Web SDK]은(는) 클릭한 요소로 시작하여 DOM 트리 위로 이동하는 토큰 데이터 특성을 찾습니다. [!DNL Web SDK]이(가) 찾은 첫 번째 토큰을 사용합니다. |
| [!DNL Interact ID] | `data-aep-interact-id` | [!DNL Web SDK]은(는) 제안을 렌더링할 때 이 고유 ID를 컨테이너 요소에 자동으로 추가합니다. Web SDK는 이 ID를 사용하여 [!DNL DOM] 요소를 제안에 상호 연결합니다. [!DNL Web SDK]에 필요한 ID이므로 어떤 식으로든 변경해서는 안 됩니다. 무시해도 됩니다. |

**예**

데이터 속성 사용의 예를 보려면 아래의 코드 조각을 참조하십시오.

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### `applyPropositions` 명령 {#apply-propositions}

이 명령의 작동 방식에 대한 자세한 내용은 [`applyPropositions`](../applypropositions.md) 설명서를 참조하세요.

`applyPropositions` 명령은 제안을 [!DNL DOM]에 렌더링하는 편리한 방법입니다. 그러나 `JSON`이(가) 있는 코드 기반 캠페인의 경우 이 명령을 사용하여 기존 [!DNL DOM] 요소(또는 `JSON` 값을 기반으로 화면에 렌더링된 애플리케이션 코드)를 명제와 상호 연관시킬 수 있습니다.

이러한 상관관계는 해당 요소에 대한 자동 상호 작용 추적을 활성화하고 해당 요소에 적절한 명제를 할당합니다. 이렇게 하려면 `actionType`을(를) `track`(으)로 설정합니다.

**예**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## 웹 SDK 태그 확장을 통해 자동 제안 및 상호 작용 클릭 추적 활성화 {#tag-extension}

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
2. **데이터 수집** > **태그**(으)로 이동합니다.
3. 원하는 태그 속성을 선택합니다.
4. **확장**(으)로 이동한 다음 Adobe Experience Platform Web SDK 카드에서 **구성**&#x200B;을 선택합니다.
5. **[!UICONTROL 데이터 수집]** 섹션까지 아래로 스크롤한 다음 **제안 및 상호 작용 링크 추적 활성화** 확인란을 선택하십시오.
6. **저장**&#x200B;을 선택한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 통해 자동 제안 및 상호 작용 링크 추적 활성화 {#library}

제안 추적은 기본적으로 [!DNL Web SDK]에서 사용할 수 있습니다. 그러나 [`configure`](../configure/overview.md) 명령을 실행할 때 `autoTrackPropositionInteractionsEnabled` 값을 사용하여 추가로 구성할 수 있습니다.

Web SDK를 구성할 때 이 속성을 생략하면 기본적으로 `{"AJO": "always", "TGT": "never"}`(으)로 설정됩니다. 제안 상호 작용을 자동으로 추적하지 않으려면 값을 `{"AJO": "never", "TGT": "never"}`(으)로 설정하십시오.

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoTrackPropositionInteractionsEnabled": {"AJO": "always", "TGT": "never"}
});
```
