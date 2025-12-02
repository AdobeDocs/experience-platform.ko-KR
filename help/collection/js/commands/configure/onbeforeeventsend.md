---
title: onBeforeEventSend
description: 데이터가 Adobe으로 전송되기 바로 전에 전송하는 데이터를 변경할 수 있는 JavaScript 함수를 등록하도록 웹 SDK을 구성하는 방법에 대해 알아봅니다.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# `onBeforeEventSend`

`onBeforeEventSend` 콜백을 사용하면 데이터가 Adobe으로 전송되기 바로 전에 전송하는 데이터를 변경할 수 있는 JavaScript 함수를 등록할 수 있습니다. 이 콜백을 사용하면 요소를 추가, 편집 또는 제거하는 기능을 포함하여 `xdm` 또는 `data` 개체를 조작할 수 있습니다. 감지된 클라이언트측 보트 트래픽과 같이 조건부로 데이터 전송을 모두 취소할 수도 있습니다.

>[!WARNING]
>
>이 콜백에서는 사용자 지정 코드를 사용할 수 있습니다. 콜백에 포함하는 코드에서 발견되지 않은 예외가 발생하면 이벤트 처리가 중지되고 **데이터가 Adobe으로 전송되지 않습니다.**

`onBeforeEventSend` 명령을 실행할 때 `configure` 콜백을 등록합니다. 인라인 함수 내에서 매개 변수 변수를 변경하여 `content` 변수 이름을 원하는 값으로 변경할 수 있습니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

인라인 함수 대신 자체 함수를 등록할 수도 있습니다.

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```

## 웹 SDK 태그 확장을 사용하여 이벤트 전송 전 콜백 구성

이러한 설정은 [데이터 수집 구성 설정](/help/tags/extensions/client/web-sdk/configure/data-collection.md#on-before-event-send-callback)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다.
