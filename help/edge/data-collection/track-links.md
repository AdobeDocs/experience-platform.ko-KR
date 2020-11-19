---
title: Adobe Analytics와의 링크 추적
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Analytics에 대한 링크 추적
description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 보내는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 보내는 방법 살펴보기
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# 링크 추적

링크는 수동으로 설정하거나 [자동으로](#automaticLinkTracking)추적할 수 있습니다. 수동 추적은 스키마의 부분 아래에 세부 사항을 추가하여 `web.webInteraction` 수행됩니다. 세 가지 필수 변수가 있습니다.

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

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

## 자동 링크 추적 {#automaticLinkTracking}

기본적으로 웹 SDK는 적격한 링크 태그에 대한 클릭 수를 캡처하고 레이블을 표시하며 기록합니다. 문서에 첨부된 [캡처](https://www.w3.org/TR/uievents/#capture-phase) 클릭 이벤트 리스너를 통해 클릭 수가 캡처됩니다.

웹 SDK를 [구성하여](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) 자동 링크 추적을 비활성화할 수 있습니다.

```javascript
clickCollectionEnabled: false
```

### 어떤 태그가 링크 추적에 적합합니까?{#qualifyingLinks}

앵커 `A` 및 `AREA` 태그에 대해 자동 링크 추적이 수행됩니다. 하지만 이러한 태그에는 연결된 처리기가 있는 경우 링크 추적에 포함되지 `onclick` 않습니다.

### 링크 레이블은 어떻게 지정됩니까?{#labelingLinks}

앵커 태그에 다운로드 속성이 포함되거나 링크가 인기 있는 파일 확장자로 끝나는 경우 링크는 다운로드 링크로 레이블이 지정됩니다. 다운로드 링크 한정자는 [정규 표현식으로 구성할](../fundamentals/configuring-the-sdk.md) 수 있습니다.

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

링크 대상 도메인이 현재 도메인과 다른 경우 링크는 종료 링크로 레이블이 지정됩니다 `window.location.hostname`.

다운로드 또는 종료 링크로 적합하지 않은 링크는 &quot;other&quot;로 레이블이 지정됩니다.
