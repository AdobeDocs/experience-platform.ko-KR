---
title: Adobe Analytics의 페이지 및 링크 추적
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Analytics에 대한 링크 추적
description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 보내는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 보내는 방법 살펴보기
translation-type: tm+mt
source-git-commit: ab73e4d793cf39c29ddca385487bf027002db883
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Adobe Analytics으로 데이터 보내기

이전에는 페이지 보기와 링크(예: `s.t(), s.tl()`)를 구분하기 위해 서로 다른 기능이 있었지만 웹 SDK에서는 명령만 `sendEvent` 있습니다. 이벤트와 함께 전송하는 데이터는 페이지 보기여야 하는지 아니면 링크여야 하는지를 결정합니다.

## 페이지 보기 보내기

변수를 설정하여 페이지 보기를 지정할 수 `web.webPageDetails.pageViews.value=1` 있습니다.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

이 변수가 설정되어 있지 않더라도 분석은 페이지 보기를 기술적으로 기록하는 반면, 데이터에서 명시적인 페이지 보기를 기록하고 향후 구현을 가능하게 하려면 이 변수를 설정하는 것이 좋습니다.

## 추적 링크

스키마의 부분 아래에 세부 사항을 추가하여 링크를 설정할 수 `web.webInteraction` 있습니다. 세 가지 필수 변수가 있습니다. `web.webInteraction.name`, `web.webInteraction.type` and `web.webInteraction.linkClicks.value`.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
    }
  }
});
```

링크 유형은 다음 세 가지 값 중 하나일 수 있습니다.

* **`other`:** 사용자 지정 링크
* **`download`:** 다운로드 링크(라이브러리에 의해 자동으로 추적 가능)
* **`exit`:** 종료 링크

### 자동 링크 추적

웹 SDK는 [clickCollection을 활성화하여 모든 링크 클릭을 자동으로 추적할 수 있습니다](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled).

다운로드 링크는 널리 사용되는 파일 유형에 따라 자동으로 검색됩니다. 다운로드가 분류되는 방식에 대한 로직은 구성할 수 있습니다.
