---
title: onBeforeLinkClickSend
description: 링크 추적 데이터가 전송되기 바로 전에 실행되는 콜백입니다.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>이 콜백은 더 이상 사용되지 않습니다. 대신 [`filterClickDetails`](clickcollection.md)을(를) 사용합니다.

`onBeforeLinkClickSend` 콜백을 사용하면 해당 데이터가 Adobe으로 전송되기 바로 전에 전송한 링크 추적 데이터를 변경할 수 있는 JavaScript 함수를 등록할 수 있습니다. 이 콜백을 사용하면 요소를 추가, 편집 또는 제거하는 기능을 포함하여 `xdm` 또는 `data` 개체를 조작할 수 있습니다. 감지된 클라이언트측 보트 트래픽과 같이 조건부로 데이터 전송을 모두 취소할 수도 있습니다. 웹 SDK 2.15.0 이상에서 지원됩니다.

이 콜백은 [`clickCollectionEnabled`](clickcollectionenabled.md)이(가) 활성화되어 있고 [`filterClickDetails`](clickcollection.md)에 등록된 함수가 없는 경우에만 실행됩니다. `clickCollectionEnabled`이(가) 비활성화되어 있거나 `filterClickDetails`에 등록된 함수가 포함되어 있는 경우 이 콜백은 실행되지 않습니다. `onBeforeEventSend`과(와) `onBeforeLinkClickSend`이(가) 모두 등록된 함수를 포함하는 경우 `onBeforeLinkClickSend`이(가) 먼저 실행됩니다.

>[!WARNING]
>
>이 콜백에서는 사용자 지정 코드를 사용할 수 있습니다. 콜백에 포함하는 코드에서 catch되지 않은 예외가 발생하면 이벤트 처리가 중지됩니다. 데이터가 Adobe으로 전송되지 않습니다.

## Web SDK 태그 확장을 사용하여 링크 클릭 전 콜백 구성 {#tag-extension}

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL 링크 전 이벤트 전송 콜백 코드 제공]** 단추를 선택합니다. 이 단추를 누르면 원하는 코드를 삽입할 수 있는 모달 창이 열립니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 데이터 수집] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL 데이터 수집 사용]** 확인란을 선택합니다.
1. **[!UICONTROL 링크 클릭 전 이벤트 전송 콜백 코드 제공]** 단추를 선택합니다.
1. 이 단추는 코드 편집기가 있는 모달 창을 엽니다. 원하는 코드를 삽입한 다음 **[!UICONTROL 저장]**&#x200B;을 클릭하여 모달 창을 닫습니다.
1. 확장 설정에서 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

코드 편집기 내에서 다음 변수에 액세스할 수 있습니다.

* **`content.clickedElement`**: 클릭한 DOM 요소입니다.
* **`content.xdm`**: 이벤트에 대한 XDM 페이로드입니다.
* **`content.data`**: 이벤트에 대한 데이터 개체 페이로드입니다.
* **`return true`**: 현재 변수 값이 있는 콜백을 즉시 종료합니다. 등록된 함수가 포함된 경우 `onBeforeEventSend` 콜백이 실행됩니다.
* **`return false`**: 콜백을 즉시 종료하고 Adobe에 데이터 전송을 중단합니다. `onBeforeEventSend` 콜백이 실행되지 않습니다.

`content`의 외부에서 정의된 모든 변수를 사용할 수 있지만, Adobe으로 전송되는 페이로드에는 포함되지 않습니다.

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

[`onBeforeEventSend`](onbeforeeventsend.md)과(와) 마찬가지로 `return true`하여 함수를 즉시 완료하거나 `return false`하여 Adobe에 대한 데이터 전송을 중단할 수 있습니다. `onBeforeEventSend`과(와) `onBeforeLinkClickSend`에 모두 등록된 함수가 들어 있는 경우 `onBeforeLinkClickSend`에서 데이터 전송을 중단하면 `onBeforeEventSend` 함수가 실행되지 않습니다.

## Web SDK JavaScript 라이브러리를 사용하여 링크 클릭 전 콜백 구성 {#library}

`configure` 명령을 실행할 때 `onBeforeLinkClickSend` 콜백을 등록합니다. 인라인 함수 내에서 매개 변수 변수를 변경하여 `content` 변수 이름을 원하는 값으로 변경할 수 있습니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

인라인 함수 대신 자체 함수를 등록할 수도 있습니다.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
