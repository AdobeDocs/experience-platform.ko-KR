---
title: 명령 응답 처리
description: JavaScript 약속을 사용하여 명령의 응답을 처리합니다.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 명령 응답 처리

일부 웹 SDK 명령은 조직에 유용한 데이터가 포함된 개체를 반환할 수 있습니다. 원하는 경우 해당 데이터로 수행할 작업을 선택할 수 있습니다. 명령 응답은 효과적으로 작동하기 위해 Edge Network 데이터가 필요하므로 제안 및 대상에 유용합니다.

명령 응답에서는 JavaScript [약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise)을(를) 사용하며, 약속이 만들어질 때 알 수 없는 값에 대해 프록시 역할을 합니다. 값이 알려지면 해당 값으로 약속이 &quot;해결됨&quot;이 됩니다.

`then` 및 `catch` 메서드를 사용하여 명령의 성공 또는 실패 시기를 확인합니다. `then` 또는 `catch`의 목적이 구현에 중요하지 않은 경우 이를 생략할 수 있습니다.

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

명령에서 반환된 모든 약속은 `result` 개체를 사용합니다. 예를 들어 `result` 명령을 사용하여 [`getLibraryInfo`](getlibraryinfo.md) 개체에서 라이브러리 정보를 가져올 수 있습니다.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

이 `result` 개체의 내용은 사용하는 명령과 사용자의 동의의 조합에 따라 다릅니다. 사용자가 특정 목적을 위해 동의를 하지 않은 경우, 응답 대상에는 사용자가 동의한 내용의 맥락에서 제공할 수 있는 정보만 포함되어 있다.

## 웹 SDK 태그 확장을 사용한 명령 응답

명령 응답에 해당하는 웹 SDK 태그 확장은 [**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete) 이벤트를 구독하는 규칙입니다. 그런 다음 [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) 또는 [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) 등의 작업을 이 규칙에 포함할 수 있습니다.
