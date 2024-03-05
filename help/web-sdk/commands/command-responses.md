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

명령 응답은 JavaScript를 사용합니다. [약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise)를 사용하여 약속을 만들 때 알 수 없는 값의 프록시 역할을 합니다. 값이 알려지면 해당 값으로 약속이 &quot;해결됨&quot;이 됩니다.

## 웹 SDK 태그 확장을 사용하여 명령 응답 처리

다음을 구독하는 규칙 만들기 **[!UICONTROL 이벤트 전송 완료]** 이벤트를 규칙의 일부로 사용합니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 이벤트]를 클릭하고 기존 이벤트를 선택하거나 이벤트를 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 이벤트 유형] 끝 **[!UICONTROL 이벤트 전송 완료]**.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

그런 다음 작업을 포함할 수 있습니다 **[!UICONTROL 제안 적용]** 또는 **[!UICONTROL 응답 적용]** 이 규칙을 따릅니다.

1. 위에서 만들었거나 편집한 규칙을 볼 때 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 제안 적용]** 또는 **[!UICONTROL 응답 적용]**&#x200B;원하는 동작에 따라 다릅니다.
1. 작업의 원하는 필드를 설정한 다음 을(를) 클릭합니다 **[!UICONTROL 변경 내용 유지]**.

## 웹 SDK JavaScript 라이브러리를 사용하여 명령 응답 처리

사용 `then` 및 `catch` 명령이 성공하거나 실패하는 경우를 결정하는 메서드입니다. 다음 중 하나를 생략할 수 있습니다 `then` 또는 `catch` 그 목적이 구현에 중요하지 않은 경우

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

명령에서 반환된 모든 약속은 `result` 개체. 예를 들어 다음 위치에서 라이브러리 정보를 가져올 수 있습니다. `result` 을 사용하는 개체 [`getLibraryInfo`](getlibraryinfo.md) 명령:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

이에 대한 내용 `result` 객체는 사용하는 명령과 사용자의 동의의 조합에 따라 다릅니다. 사용자가 특정 목적을 위해 동의를 하지 않은 경우, 응답 대상에는 사용자가 동의한 내용의 맥락에서 제공할 수 있는 정보만 포함되어 있다.
