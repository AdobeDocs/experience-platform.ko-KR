---
title: onBeforeLinkClickSend
description: 링크 추적 데이터가 전송되기 바로 전에 실행되는 콜백입니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

다음 `onBeforeLinkClickSend` callback을 사용하면 Adobe으로 데이터가 전송되기 바로 전에 전송하는 링크 추적 데이터를 변경할 수 있는 JavaScript 함수를 등록할 수 있습니다. 이 콜백을 사용하면 `xdm` 또는 `data` 요소를 추가, 편집 또는 제거하는 기능이 포함된 개체입니다. 감지된 클라이언트측 보트 트래픽과 같이 조건부로 데이터 전송을 모두 취소할 수도 있습니다. 웹 SDK 2.15.0 이상에서 지원됩니다.

이 콜백은 다음과 같은 경우에만 실행됩니다. [`clickCollectionEnabled`](clickcollectionenabled.md) 이(가) 활성화되었습니다. If `clickCollectionEnabled` 이(가) 비활성화되어 있으면 이 콜백은 실행되지 않습니다. 둘 다인 경우 `onBeforeEventSend` 및 `onBeforeLinkClickSend` 등록된 함수 포함, `onBeforeLinkClickSend` 함수가 먼저 실행됩니다. 한 번 `onBeforeLinkClickSend` 함수가 종료되면 `onBeforeEventSend` 그런 다음 함수가 실행됩니다.

>[!WARNING]
>
>이 콜백에서는 사용자 지정 코드를 사용할 수 있습니다. 콜백에 포함하는 코드에서 catch되지 않은 예외가 발생하면 이벤트 처리가 중지됩니다. 데이터가 Adobe으로 전송되지 않습니다.

## 링크 전 클릭 Web SDK 태그 확장을 사용하여 콜백 보내기

다음 항목 선택 **[!UICONTROL 링크 클릭 전 이벤트 콜백 코드 제공]** 단추 조건 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 이 단추를 누르면 원하는 코드를 삽입할 수 있는 모달 창이 열립니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 데이터 수집] 섹션을 선택한 다음 확인란을 선택합니다 **[!UICONTROL 클릭 데이터 수집 활성화]**.
1. 레이블이 지정된 단추 선택 **[!UICONTROL 링크 클릭 전 이벤트 콜백 코드 제공]**.
1. 이 단추는 코드 편집기가 있는 모달 창을 엽니다. 원하는 코드를 삽입한 다음 **[!UICONTROL 저장]** 모달 창을 닫습니다.
1. 클릭 **[!UICONTROL 저장]** 확장 설정에서 변경 사항을 게시합니다.

코드 편집기 내에서 요소를 추가, 편집 또는 제거할 수 있습니다 `content` 개체. 이 개체에는 Adobe으로 전송된 페이로드가 포함되어 있습니다. 을(를) 정의할 필요가 없습니다. `content` 함수 내에 코드를 가져오거나 래핑합니다. 의 외부에 정의된 모든 변수 `content` 을 사용할 수 있지만 Adobe으로 전송되는 페이로드에는 포함되지 않습니다.

>[!TIP]
>
>개체 `content.xdm`, `content.data`, 및 `content.clickedElement` 은 항상 이 컨텍스트에서 정의되므로 이 변수가 있는지 확인할 필요가 없습니다. 이러한 개체 내의 일부 변수는 구현 및 데이터 계층에 따라 다릅니다. Adobe은 JavaScript 오류를 방지하기 위해 이러한 객체 내에 정의되지 않은 값을 확인하는 것을 권장합니다.

예를 들어 다음 작업을 수행하려고 한다고 가정해 보겠습니다.

* 현재 페이지 URL 수정
* Adobe Analytics eVar에서 클릭한 요소 캡처
* 링크 유형을 &quot;기타&quot;에서 &quot;다운로드&quot;로 변경

모달 창 내에서 이와 동등한 코드는 다음과 같습니다.

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

과 비슷하게 [`onBeforeEventSend`](onbeforeeventsend.md), 다음을 수행할 수 있습니다. `return true` 함수를 즉시 완료하거나 `return false` 데이터 전송을 즉시 취소합니다. 에서 데이터 전송을 취소하는 경우 `onBeforeLinkClickSend` 두 경우 모두 `onBeforeEventSend` 및 `onBeforeLinkClickSend` 등록된 함수 포함, `onBeforeEventSend` 함수가 실행되지 않습니다.

## 링크 전 클릭 Web SDK JavaScript 라이브러리를 사용하여 콜백 보내기

등록 `onBeforeLinkClickSend` 다음을 실행할 때 콜백 `configure` 명령입니다. 다음을 변경할 수 있습니다. `content` variable name 을 인라인 함수 내에서 매개 변수 변수를 변경하여 원하는 값으로 지정합니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to immediately complete the function
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": lastChanceLinkLogic
});    
```
