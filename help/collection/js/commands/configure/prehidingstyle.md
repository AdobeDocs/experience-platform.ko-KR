---
title: prehidingStyle
description: 개인화된 콘텐츠를 깜박임 없이 로드할 수 있는 CSS 정의를 만듭니다.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

`prehidingStyle` 속성을 사용하면 CSS 선택기를 정의하여 개인화된 콘텐츠가 로드될 때까지 숨길 수 있습니다. 이 속성은 깜박임을 방지하기 위해 동기식 웹 SDK 구현에서 유용합니다. Adobe에서는 비동기 Web SDK 구현을 위해 [코드 조각 사전 숨김](/help/collection/use-cases/personalization/manage-flicker.md)을 사용하는 것이 좋습니다.

이 속성에서 정의하는 CSS 선택기는 페이지에서 첫 번째 [`sendEvent`](../sendevent/overview.md) 명령을 실행할 때 콘텐츠를 숨깁니다. Adobe에서 응답을 받으면 컨텐츠가 숨김 취소되며, 여기에는 일반적으로 개인화된 컨텐츠가 포함됩니다. `sendEvent` 명령이 실패하거나 시간이 초과되면 콘텐츠도 숨김 취소됩니다.

구현에 `prehidingStyle`과(와) 코드 조각 사전 숨김을 모두 포함하는 경우 코드 조각 사전 숨김이 이 구성 속성보다 우선합니다.

`prehidingStyle` 명령을 실행할 때 `configure` 문자열을 설정합니다. 웹 SDK을 구성할 때 이 속성을 생략하면 페이지에서 첫 번째 `sendEvent` 명령을 실행할 때 아무것도 숨겨지지 않습니다. 이 값을 동기적으로 로드된 라이브러리에 대해 원하는 CSS 선택기 및 선언 블록으로 설정합니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## 웹 SDK 태그 확장을 사용하여 스타일 미리 숨기기

이러한 설정은 [Personalization 구성 설정](/help/tags/extensions/client/web-sdk/configure/personalization.md)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다.
