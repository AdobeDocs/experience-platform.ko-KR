---
title: Adobe Experience Platform Web SDK를 사용하여 Adobe Analytics에 데이터 전송
description: Adobe Experience Platform Web SDK를 사용하여 Adobe Analytics에 데이터를 전송하는 방법에 대해 알아봅니다.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;웹 상호 작용;페이지 보기;링크 추적;링크;링크 추적 링크;clickCollection;클릭 컬렉션;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Adobe Analytics에 데이터 보내기

반면에 과거에는 페이지 보기와 링크를 구분하는 함수가 달랐습니다(예: `s.t(), s.tl()`) 웹 SDK에는 `sendEvent` 명령입니다. 이벤트와 함께 보내는 데이터는 해당 데이터가 페이지 보기여야 하는지 링크여야 하는지 여부를 결정합니다. [링크 추적에 대해 자세히 알아보기](../track-links.md).

## 페이지 보기 보내기

다음을 설정하여 페이지 보기를 지정할 수 있습니다. `web.webPageDetails.pageViews.value=1` 변수를 채우는 방법에 따라 페이지를 순서대로 표시합니다.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

Analytics는 이 변수가 설정되지 않았더라도 기술적으로 페이지 보기를 기록하지만, 데이터 및 향후 구현 증명에서 페이지 보기를 명시적으로 기록하려면 이 변수를 설정하는 것이 좋습니다.
