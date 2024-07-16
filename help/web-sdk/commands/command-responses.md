---
title: 명령 응답 처리
description: JavaScript 약속을 사용하여 명령의 응답을 처리합니다.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 명령 응답 처리

일부 웹 SDK 명령은 조직에 유용할 수 있는 데이터가 포함된 개체를 반환할 수 있습니다. 원하는 경우 해당 데이터로 수행할 작업을 선택할 수 있습니다. 명령 응답은 효과적으로 작동하기 위해 Edge Network 데이터가 필요하므로 제안 및 대상에 유용합니다.

명령 응답에서는 JavaScript [약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise)을(를) 사용하며, 약속이 만들어질 때 알 수 없는 값에 대해 프록시 역할을 합니다. 값이 알려지면 해당 값으로 약속이 &quot;해결됨&quot;이 됩니다.

## 웹 SDK 태그 확장을 사용하여 명령 응답 처리

규칙의 일부로 **[!UICONTROL 이벤트 보내기 완료]** 이벤트를 구독하는 규칙을 만듭니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 이벤트]에서 기존 이벤트를 선택하거나 이벤트를 만듭니다.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 이벤트 유형]을(를) **[!UICONTROL 이벤트 전송 완료]**(으)로 설정합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

그런 다음 **[!UICONTROL 제안 적용]** 또는 **[!UICONTROL 응답 적용]** 작업을 이 규칙에 포함할 수 있습니다.

1. 위에서 만들었거나 편집한 규칙을 볼 때 기존 작업을 선택하거나 작업을 만듭니다.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고, 원하는 동작에 따라 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 제안 적용]** 또는 **[!UICONTROL 응답 적용]**(으)로 설정합니다.
1. 작업의 원하는 필드를 설정한 다음 **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 명령 응답 처리

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

명령에서 반환된 모든 약속은 `result` 개체를 사용합니다. 예를 들어 [`getLibraryInfo`](getlibraryinfo.md) 명령을 사용하여 `result` 개체에서 라이브러리 정보를 가져올 수 있습니다.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

이 `result` 개체의 내용은 사용하는 명령과 사용자의 동의의 조합에 따라 다릅니다. 사용자가 특정 목적을 위해 동의를 하지 않은 경우, 응답 대상에는 사용자가 동의한 내용의 맥락에서 제공할 수 있는 정보만 포함되어 있다.
