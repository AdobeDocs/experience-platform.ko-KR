---
title: applyResponse
description: Edge Network의 응답을 사용하여 웹 SDK을 초기화합니다.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

`applyResponse` 명령을 사용하면 Edge Network의 응답을 기반으로 다양한 작업을 수행할 수 있습니다. 일반적으로 서버가 Edge Network을 처음 호출하는 하이브리드 배포에서 사용됩니다. 이 명령은 해당 호출에서 응답을 가져와 브라우저에서 웹 SDK을 초기화합니다.

웹 SDK의 구성된 인스턴스를 호출할 때 `applyResponse` 명령을 실행합니다. 구성 옵션이 포함된 개체는 다음 필드를 지원합니다.

* **`renderDecisions`**: 웹 SDK에서 자동 렌더링에 적합한 개인화된 콘텐츠를 렌더링하도록 하는 부울입니다. [`renderDecisions`](sendevent/renderdecisions.md) 명령의 [`sendEvent`](sendevent/overview.md)과(와) 동일합니다.
* **`responseHeaders`**: 문자열 헤더 이름과 문자열 헤더 값의 맵입니다.
* **`responseBody`**: 필수 항목입니다. Edge Network에 대한 서버 호출의 JSON 응답 본문.
* **`personalization.sendDisplayEvent`**: [`personalization.sendDisplayEvent`](sendevent/personalization.md) 명령에서 `sendEvent`과(와) 동일하게 작동하는 부울입니다.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## 응답 개체

이 명령을 사용하여 [응답을 처리](command-responses.md)하기로 결정하는 경우 응답 개체에서 다음 속성을 사용할 수 있습니다.

* **`propositions`**: Edge Network에서 반환된 제안 배열. 자동으로 렌더링되는 제안에 `renderAttempted`(으)로 설정된 `true` 플래그가 포함되어 있습니다.
* **`inferences`**: 이 사용자에 대한 기계 학습 정보가 포함된 추론 개체의 배열입니다.
* **`destinations`**: Edge Network에서 반환된 대상 개체의 배열입니다.

## 웹 SDK 태그 확장을 사용하여 응답 적용

이 명령에 해당하는 웹 SDK 태그 확장은 [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) 작업입니다.
