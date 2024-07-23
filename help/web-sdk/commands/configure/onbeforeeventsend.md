---
title: onBeforeEventSend
description: 데이터가 Adobe으로 전송되기 바로 전에 전송하는 데이터를 변경할 수 있는 JavaScript 함수를 등록하도록 Web SDK를 구성하는 방법에 대해 알아봅니다.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# `onBeforeEventSend`

`onBeforeEventSend` 콜백을 사용하면 데이터가 Adobe으로 전송되기 바로 전에 전송하는 데이터를 변경할 수 있는 JavaScript 함수를 등록할 수 있습니다. 이 콜백을 사용하면 요소를 추가, 편집 또는 제거하는 기능을 포함하여 `xdm` 또는 `data` 개체를 조작할 수 있습니다. 감지된 클라이언트측 보트 트래픽과 같이 조건부로 데이터 전송을 모두 취소할 수도 있습니다.

>[!WARNING]
>
>이 콜백에서는 사용자 지정 코드를 사용할 수 있습니다. 콜백에 포함하는 코드에서 catch되지 않은 예외가 발생하면 이벤트 처리가 중지됩니다. 데이터가 Adobe으로 전송되지 않습니다.

## Web SDK 태그 확장을 사용하여 이벤트 전송 전 콜백 구성 {#tag-extension}

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL 이벤트 전송 전 콜백 코드 제공]** 단추를 선택합니다. 이 단추를 누르면 원하는 코드를 삽입할 수 있는 모달 창이 열립니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 데이터 수집] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL 이벤트 전송 콜백 코드 전에 제공]** 단추를 선택합니다.
1. 이 단추는 코드 편집기가 있는 모달 창을 엽니다. 원하는 코드를 삽입한 다음 **[!UICONTROL 저장]**&#x200B;을 클릭하여 모달 창을 닫습니다.
1. 확장 설정에서 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

코드 편집기 내에서 다음 변수에 액세스할 수 있습니다.

* **`content.xdm`**: 이벤트에 대한 [XDM](../sendevent/xdm.md) 페이로드입니다.
* **`content.data`**: 이벤트에 대한 [data](../sendevent/data.md) 개체 페이로드입니다.
* **`return true`**: 콜백을 즉시 종료하고 `content` 개체의 현재 값으로 Adobe에 데이터를 보냅니다.
* **`return false`**: 콜백을 즉시 종료하고 Adobe에 데이터 전송을 중단합니다.

`content`의 외부에서 정의된 모든 변수를 사용할 수 있지만, Adobe으로 전송되는 페이로드에는 포함되지 않습니다.

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>페이지의 첫 번째 이벤트에서 `false`을(를) 반환하지 마십시오. 첫 번째 이벤트에서 `false`을(를) 반환하면 개인화에 부정적인 영향을 줄 수 있습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 이벤트 전송 전 콜백을 구성합니다. {#library}

`configure` 명령을 실행할 때 `onBeforeEventSend` 콜백을 등록합니다. 인라인 함수 내에서 매개 변수 변수를 변경하여 `content` 변수 이름을 원하는 값으로 변경할 수 있습니다.

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
