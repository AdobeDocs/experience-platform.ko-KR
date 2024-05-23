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

다음 `applyResponse` 명령을 사용하면 Edge Network의 응답에 따라 다양한 작업을 수행할 수 있습니다. 일반적으로 서버가 Edge Network을 처음 호출하는 하이브리드 배포에서 사용됩니다. 이 명령은 해당 호출에서 응답을 가져와 브라우저에서 웹 SDK를 초기화합니다.

## 웹 SDK 태그 확장을 사용하여 응답 적용

응답 적용은 Adobe Experience Platform 데이터 수집 태그 인터페이스의 규칙 내에서 작업으로 수행됩니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 응답 적용]**.
1. 오른쪽에서 원하는 필드를 설정합니다.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 응답 적용

실행 `applyResponse` 명령을 사용하여 웹 SDK의 구성된 인스턴스를 호출할 수 있습니다. 구성 옵션이 포함된 개체는 다음 필드를 지원합니다.

* **`renderDecisions`**: 자동 렌더링에 적합한 개인화된 콘텐츠를 웹 SDK가 렌더링하도록 하는 부울입니다. 다음과 같음 [`renderDecisions`](sendevent/renderdecisions.md) 다음에서 [`sendEvent`](sendevent/overview.md) 명령입니다.
* **`responseHeaders`**: 문자열 헤더 이름을 문자열 헤더 값에 매핑합니다.
* **`responseBody`**: 필수. 서버 호출의 Edge Network JSON 응답 본문.
* **`personalization.sendDisplayEvent`**: 와 동일하게 작동하는 부울 [`personalization.sendDisplayEvent`](sendevent/personalization.md) 다음에서 `sendEvent` 명령입니다.

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

다음을 결정하시면 [응답 처리](command-responses.md) 이 명령을 사용하면 응답 개체에서 다음 속성을 사용할 수 있습니다.

* **`propositions`**: Edge Network에서 반환되는 제안 배열. 자동으로 렌더링되는 제안에 플래그가 포함됩니다 `renderAttempted` 을 로 설정 `true`.
* **`inferences`**: 이 사용자에 대한 머신 러닝 정보가 포함된 추론 개체의 배열입니다.
* **`destinations`**: Edge Network이 반환하는 대상 개체의 배열입니다.
