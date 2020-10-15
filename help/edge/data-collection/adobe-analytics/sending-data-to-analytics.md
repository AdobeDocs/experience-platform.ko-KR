---
title: Adobe Analytics의 페이지 및 링크 추적
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Analytics에 대한 링크 추적
description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 보내는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 보내는 방법 살펴보기
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 9e1ad05285b27a9fc8b56db903609add3fef144e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Adobe Analytics으로 데이터 보내기

반면에 과거에는 페이지 보기와 링크(예: `s.t(), s.tl()`)를 구별하기 위해 다른 기능이 있었지만 웹 SDK에서는 명령만 `sendEvent` 있습니다. 이벤트와 함께 전송하는 데이터는 페이지 보기여야 하는지 아니면 링크여야 하는지를 결정합니다. [링크 추적에 대한 자세한 내용](../track-links.md)

## 페이지 보기 보내기

변수를 설정하여 페이지 보기를 지정할 수 `web.webPageDetails.pageViews.value=1` 있습니다.

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

Analytics는 이 변수가 설정되어 있지 않더라도 페이지 보기를 기술적으로 기록하지만, 데이터에서 명시적인 페이지 보기를 기록하고 구현을 나중에 증명하려는 경우 이 변수를 설정하는 것이 좋습니다.
