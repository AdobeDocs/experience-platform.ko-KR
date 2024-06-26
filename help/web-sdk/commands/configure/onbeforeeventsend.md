---
title: onBeforeEventSend
description: 데이터가 전송되기 바로 전에 실행되는 콜백입니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# `onBeforeEventSend`

다음 `onBeforeEventSend` 콜백을 사용하면 데이터가 Adobe으로 전송되기 바로 전에 전송하는 데이터를 변경할 수 있는 JavaScript 함수를 등록할 수 있습니다. 이 콜백을 사용하면 `xdm` 또는 `data` 요소를 추가, 편집 또는 제거하는 기능이 포함된 개체입니다. 감지된 클라이언트측 보트 트래픽과 같이 조건부로 데이터 전송을 모두 취소할 수도 있습니다.

>[!WARNING]
>
>이 콜백에서는 사용자 지정 코드를 사용할 수 있습니다. 콜백에 포함하는 코드에서 catch되지 않은 예외가 발생하면 이벤트 처리가 중지됩니다. 데이터가 Adobe으로 전송되지 않습니다.

## Web SDK 태그 확장을 사용하여 이벤트 전송 전 콜백

다음 항목 선택 **[!UICONTROL 이벤트 전송 콜백 코드 전에 를 제공합니다.]** 단추 조건 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 이 단추를 누르면 원하는 코드를 삽입할 수 있는 모달 창이 열립니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 데이터 수집] 섹션을 선택한 다음 버튼을 선택합니다 **[!UICONTROL 이벤트 전송 콜백 코드 전에 를 제공합니다.]**.
1. 이 단추는 코드 편집기가 있는 모달 창을 엽니다. 원하는 코드를 삽입한 다음 **[!UICONTROL 저장]** 모달 창을 닫습니다.
1. 클릭 **[!UICONTROL 저장]** 확장 설정에서 변경 사항을 게시합니다.

코드 편집기 내에서 요소를 추가, 편집 또는 제거할 수 있습니다 `content` 개체. 이 개체에는 Adobe으로 전송된 페이로드가 포함되어 있습니다. 을(를) 정의할 필요가 없습니다. `content` 함수 내에 코드를 가져오거나 래핑합니다. 의 외부에 정의된 모든 변수 `content` 을 사용할 수 있지만 Adobe으로 전송되는 페이로드에는 포함되지 않습니다.

>[!TIP]
>
>개체 `content.xdm` 및 `content.data` 은 항상 이 컨텍스트에서 정의되므로 이 변수가 있는지 확인할 필요가 없습니다. 이러한 개체 내의 일부 변수는 구현 및 데이터 계층에 따라 다릅니다. Adobe은 JavaScript 오류를 방지하기 위해 이러한 객체 내에 정의되지 않은 값을 확인하는 것을 권장합니다.

예를 들어 다음을 원하는 경우:

* XDM 요소 추가 `xdm.commerce.order.purchaseID`
* 모든 문자 강제 적용 `xdm.marketing.trackingCode` 소문자로
* `xdm.environment.operatingSystemVersion` 삭제
* 이벤트 유형이 링크 클릭인 경우 아래 코드에 관계없이 데이터를 즉시 전송합니다
* 보트가 감지되면 Adobe에 데이터 보내기 취소

모달 창 내에서 이와 동등한 코드는 다음과 같습니다.

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

>[!NOTE]
>
>반환 방지 `false` 페이지의 첫 번째 이벤트에서 참조할 수 있습니다. 반환 `false` 첫 번째 이벤트에서는 개인화에 부정적인 영향을 줄 수 있습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 이벤트 전송 전 콜백

등록 `onBeforeEventSend` 다음을 실행할 때 콜백 `configure` 명령입니다. 다음을 변경할 수 있습니다. `content` variable name 을 인라인 함수 내에서 매개 변수 변수를 변경하여 원하는 값으로 지정합니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```
