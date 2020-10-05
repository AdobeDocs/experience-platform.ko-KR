---
title: Adobe Analytics의 페이지 및 링크 추적
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Analytics에 대한 링크 추적
description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 보내는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 보내는 방법 살펴보기
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 8840e00ec3aa28d43c371b793da4a4b9bfc8d259
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Adobe Analytics으로 데이터 보내기

반면에 과거에는 페이지 보기와 링크(예: `s.t(), s.tl()`)를 구별하기 위해 다른 기능이 있었지만 웹 SDK에서는 명령만 `sendEvent` 있습니다. 이벤트와 함께 전송하는 데이터는 페이지 보기여야 하는지 아니면 링크여야 하는지를 결정합니다.

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

이 변수가 설정되어 있지 않더라도 분석은 기술적으로 페이지 보기를 기록하지만, 데이터에서 명시적인 페이지 보기를 기록하고 향후 구현을 증명하려는 경우 이 변수를 설정하는 것이 좋습니다.

## 추적 링크

링크는 수동으로 설정하거나 [자동으로](#automaticLinkTracking)추적할 수 있습니다. 수동 추적은 스키마의 부분 아래에 세부 사항을 추가하여 `web.webInteraction` 수행됩니다. 세 가지 필수 변수가 있습니다. `web.webInteraction.name`, `web.webInteraction.type` and `web.webInteraction.linkClicks.value`.

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
  }
});
```

링크 유형은 다음 세 가지 값 중 하나일 수 있습니다.

* **`other`:** 사용자 지정 링크
* **`download`:** 다운로드 링크
* **`exit`:** 종료 링크

### 자동 링크 추적 {#automaticLinkTracking}

기본적으로 웹 SDK는 [적격한](#labelingLinks)링크 태그를 캡처하고 레이블 [및](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) 레코드를 [](#qualifyingLinks) 만듭니다. 문서에 첨부된 [캡처](https://www.w3.org/TR/uievents/#capture-phase) 클릭 이벤트 리스너를 통해 클릭 수가 캡처됩니다.

웹 SDK를 [구성하여](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) 자동 링크 추적을 비활성화할 수 있습니다.

```javascript
clickCollectionEnabled: false
```

#### 어떤 태그가 링크 추적에 적합합니까?{#qualifyingLinks}

앵커 `A` 및 `AREA` 태그에 대해 자동 링크 추적이 수행됩니다. 하지만 이러한 태그에는 연결된 처리기가 있는 경우 링크 추적에 포함되지 `onclick` 않습니다.

#### 링크 레이블은 어떻게 지정됩니까?{#labelingLinks}

앵커 태그에 다운로드 속성이 포함되거나 링크가 인기 있는 파일 확장자로 끝나는 경우 링크는 다운로드 링크로 레이블이 지정됩니다. 다운로드 링크 한정자는 [정규 표현식으로 구성할](../../fundamentals/configuring-the-sdk.md) 수 있습니다.

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

링크 대상 도메인이 현재 도메인과 다른 경우 링크는 종료 링크로 레이블이 지정됩니다 `window.location.hostname`.

다운로드 또는 종료 링크로 적합하지 않은 링크는 &quot;other&quot;로 레이블이 지정됩니다.
