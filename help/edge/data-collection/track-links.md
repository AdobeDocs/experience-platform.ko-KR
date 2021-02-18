---
title: Adobe Experience Platform 웹 SDK를 사용하여 링크 추적
description: Experience Platform 웹 SDK를 사용하여 링크 데이터를 Adobe Analytics으로 전송하는 방법 살펴보기
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;페이지 보기;링크 추적;링크;추적 링크;클릭 컬렉션;클릭 컬렉션;adobe analytics;sendEvent;s.tl();webPageDetails;webInteraction;webInteraction;페이지 보기;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# 링크 추적

링크는 수동으로 설정하거나 [자동으로](#automaticLinkTracking)추적할 수 있습니다. 수동 추적은 스키마의 `web.webInteraction` 부분 아래에 세부 정보를 추가하여 수행합니다. 다음 3개의 필수 변수가 있습니다.

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

링크 유형은 다음 3개 값 중 하나일 수 있습니다.

* **`other`:** 사용자 지정 링크
* **`download`다운로드** 링크
* **`exit`:** 종료 링크

## 자동 링크 추적 {#automaticLinkTracking}

기본적으로 웹 SDK는 적격한 링크 태그에 대한 클릭 수를 캡처하고 레이블을 표시하며 기록합니다. 클릭 수는 문서에 첨부된 [capture](https://www.w3.org/TR/uievents/#capture-phase) 클릭 이벤트 리스너를 사용하여 캡처됩니다.

웹 SDK를 [구성](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled)하면 자동 링크 추적을 비활성화할 수 있습니다.

```javascript
clickCollectionEnabled: false
```

### 어떤 태그가 링크 추적에 적합합니까?{#qualifyingLinks}

앵커 `A` 및 `AREA` 태그에 대해 자동 링크 추적이 수행됩니다. 그러나 이러한 태그에는 연결된 `onclick` 핸들러가 있으면 링크 추적에 포함되지 않습니다.

### 링크 레이블은 어떻게 됩니까?{#labelingLinks}

앵커 태그에 다운로드 속성이 포함되거나 링크가 많이 사용되는 파일 확장자로 끝나는 경우 링크가 다운로드 링크로 레이블이 지정됩니다. 다운로드 링크 한정자는 정규 표현식으로 [구성된](../fundamentals/configuring-the-sdk.md)일 수 있습니다.

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

링크 대상 도메인이 현재 `window.location.hostname`과(와) 다른 경우 링크는 종료 링크로 레이블이 지정됩니다.

다운로드 또는 종료 링크로 적합하지 않은 링크는 &quot;기타&quot;로 레이블이 지정됩니다.
