---
title: renderDecisions
description: 자동 렌더링에 적합한 개인화된 콘텐츠를 렌더링합니다.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

`renderDecisions` 속성을 사용하면 웹 SDK에서 자동 렌더링에 적합한 개인화된 콘텐츠를 강제로 렌더링할 수 있습니다.

`renderDecisions` 명령을 실행할 때 `sendEvent` 부울을 설정합니다. 생략하면 이 속성은 기본적으로 `false`(으)로 설정됩니다. 개인화된 콘텐츠를 자동으로 렌더링하려면 이 속성을 `true`(으)로 설정하십시오.

>[!IMPORTANT]
>
>`renderDecisions` 속성이 [`documentUnloading`](documentunloading.md) 속성과 호환되지 않습니다. 두 속성을 동시에 `true`(으)로 설정하지 마십시오.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

이 속성을 `true`(으)로 설정할 때 연결된 범위나 표면도 포함되었는지 확인하십시오. 이러한 범위 또는 표면은 자동으로 요청되거나(페이지의 첫 번째 `sendEvent` 명령 등) 명시적으로([`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes) 또는 [`personalization.surfaces`](personalization.md#personalizationsurfaces) 사용) 요청될 수 있습니다. 개인화를 렌더링할 때 발생하는 일반적인 문제는 다음과 같은 시나리오입니다.

1. `sendEvent`이(가) 설정되지 않은 기본 개인화를 요청하는 페이지에서 `renderDecisions` 명령이 일찍 실행됩니다(기본값: `false`). 제안을 가져오지만 렌더링하지 않습니다.
1. 나중에 페이지에서 `sendEvent`이(가) `renderDecisions`(으)로 설정된 다른 `true`이(가) 트리거되지만 범위 또는 표면이 포함되지 않습니다. 이 두 번째 호출에는 범위나 서피스가 없으므로 아무것도 렌더링되지 않습니다.

다음 중 하나를 수행하여 이 문제를 방지할 수 있습니다.

* 첫 번째 `renderDecisions` 호출에서 `true`을(를) `sendEvent`(으)로 설정하는 중; 또는
* `decisionScopes`을(를) `surfaces`(으)로 설정할 때 후속 `sendEvent` 호출에서 `renderDecisions` 또는 `true`을(를) 명시적으로 설정하는 중입니다.

## 웹 SDK 태그 확장을 사용하여 의사 결정 렌더링

이 속성에 해당하는 웹 SDK 태그 확장은 &#39;[**&#39; 작업 내의**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields)&#x200B;시각적 개인화 결정 렌더링[!UICONTROL Send event] 확인란입니다.
