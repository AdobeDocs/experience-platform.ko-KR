---
title: propositions 적용
description: 이미 sendEvent로 렌더링된 제안을 다시 렌더링합니다.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# `applyPropositions`

`applyPropositions` 명령을 사용하면 [`sendEvent`](sendevent/overview.md) 명령을 사용하여 이미 렌더링된 제안을 다시 렌더링할 수 있습니다. 이 명령은 페이지의 일부가 다시 렌더링되어 페이지에 이미 적용된 개인화를 덮어쓸 수 있는 단일 페이지 애플리케이션으로 작업할 때 유용합니다.

이 명령은 다음 필드를 지원합니다.

* **제안**: 다시 렌더링할 제안 개체의 배열입니다.
* **보기 이름**: 렌더링할 보기의 이름입니다. 이러한 결정에 대한 표시 알림은 캐시되며 `sendEvent` 옵션을 사용하여 후속 `personalization.includeRenderedPropositions` 명령에 포함될 수 있습니다.
* **Meta 데이터**: HTML 오퍼를 적용할 수 있는 방법을 결정하는 개체입니다. 여기에는 다음 속성이 포함됩니다.
   * 범위
   * 선택기
   * 작업 유형

>[!NOTE]
>
>`applyPropositions` 명령은 표시 이벤트를 자동으로 보내지 않습니다. 녹화 표시가 필요한 경우 `sendEvent`표시 이벤트 관리[에 설명된 대로 &#x200B;](/help/collection/use-cases/personalization/display-events.md) 명령을 사용하십시오.

웹 SDK의 구성된 인스턴스를 호출할 때 `applyPropositions` 명령을 실행합니다. 구성 옵션이 포함된 개체는 다음 필드를 지원합니다.

* **`propositions`**: 다시 렌더링할 제안 개체의 배열입니다. 일반적으로 `propositionScopes` 필드에 따라 다시 렌더링할 범위 또는 표면이 결정되므로 이 개체는 일반적으로 사용되지 않습니다.
* **`metadata`**: HTML 오퍼가 적용되는 방식을 결정합니다. 키가 범위 또는 표면이고 값이 `selector` 및 `actionType` 키를 포함하는 개체인 맵입니다.
   * `selector`: HTML을 적용할 위치의 CSS 선택기가 포함된 문자열입니다.
   * `actionType`: HTML에서 수행할 작업입니다. 유효한 값은 `setHtml`, `replaceHtml` 및 `appendHtml`입니다.
* **`viewName`**: 단일 페이지 응용 프로그램에서 렌더링할 보기의 이름입니다. 이러한 결정에 대한 표시 알림이 캐시되며 `sendEvent`을(를) 사용하여 후속 `personalization.includeRenderedPropositions` 명령에 포함될 수 있습니다.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## 웹 SDK 태그 확장을 사용하여 제안 적용

이 명령에 해당하는 웹 SDK 태그 확장은 [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) 작업입니다.
