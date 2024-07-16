---
title: applyResponse
description: Edge Network의 응답을 사용하여 웹 SDK를 초기화합니다.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

`applyResponse` 명령을 사용하면 Edge Network의 응답을 기반으로 다양한 작업을 수행할 수 있습니다. 일반적으로 서버가 Edge Network을 처음 호출하는 하이브리드 배포에서 사용됩니다. 이 명령은 해당 호출에서 응답을 가져와 브라우저에서 웹 SDK를 초기화합니다.

## 웹 SDK 태그 확장을 사용하여 응답 적용

응답 적용은 Adobe Experience Platform 데이터 수집 태그 인터페이스의 규칙 내에서 작업으로 수행됩니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 작업]에서 기존 작업을 선택하거나 작업을 만드십시오.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 응답 적용]**(으)로 설정합니다.
1. 오른쪽에서 원하는 필드를 설정합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

## 웹 SDK JavaScript 라이브러리를 사용하여 응답 적용

웹 SDK의 구성된 인스턴스를 호출할 때 `applyResponse` 명령을 실행합니다. 구성 옵션이 포함된 개체는 다음 필드를 지원합니다.

* **`renderDecisions`**: 자동 렌더링에 적합한 개인화된 콘텐츠를 웹 SDK가 렌더링하도록 하는 부울입니다. [`sendEvent`](sendevent/overview.md) 명령의 [`renderDecisions`](sendevent/renderdecisions.md)과(와) 동일합니다.
* **`responseHeaders`**: 문자열 헤더 이름과 문자열 헤더 값의 맵입니다.
* **`responseBody`**: 필수 항목입니다. 서버 호출의 Edge Network JSON 응답 본문.
* **`personalization.sendDisplayEvent`**: `sendEvent` 명령에서 [`personalization.sendDisplayEvent`](sendevent/personalization.md)과(와) 동일하게 작동하는 부울입니다.

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

* **`propositions`**: Edge Network이 반환한 제안 배열. 자동으로 렌더링되는 제안에 `true`(으)로 설정된 `renderAttempted` 플래그가 포함되어 있습니다.
* **`inferences`**: 이 사용자에 대한 기계 학습 정보가 포함된 추론 개체의 배열입니다.
* **`destinations`**: Edge Network이 반환한 대상 개체의 배열입니다.
