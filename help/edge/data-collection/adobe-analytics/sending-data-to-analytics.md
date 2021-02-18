---
title: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Analytics으로 데이터 보내기
description: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Analytics으로 데이터를 전송하는 방법에 대해 알아봅니다.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;페이지 보기;링크 추적;링크;추적 링크;클릭 컬렉션;클릭 컬렉션;adobe analytics;sendEvent;s.tl();webPageDetails;webInteraction;webInteraction;페이지 보기;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Adobe Analytics으로 데이터 보내기

이전에는 페이지 보기와 링크(예: `s.t(), s.tl()`)를 구분하는 다른 기능이 있었지만 웹 SDK에는 `sendEvent` 명령만 있습니다. 이벤트와 함께 전송하는 데이터는 이벤트 보기가 페이지 보기인지 링크인지를 결정합니다. [링크 추적에 대해 자세히 알아보십시오](../track-links.md).

## 페이지 보기 보내기

`web.webPageDetails.pageViews.value=1` 변수를 설정하여 페이지 보기를 지정할 수 있습니다.

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

Analytics는 이 변수가 설정되어 있지 않더라도 페이지 보기를 기술적으로 기록하지만, 데이터에서 명시적인 페이지 보기를 기록하고 향후 구현을 입증하기 위해 이 변수를 설정하는 것이 좋습니다.
