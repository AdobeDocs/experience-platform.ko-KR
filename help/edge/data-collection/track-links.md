---
title: Adobe Experience Platform Web SDK를 사용하여 링크 추적
description: Experience Platform Web SDK를 사용하여 Adobe Analytics에 링크 데이터를 전송하는 방법 알아보기
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;웹 상호 작용;페이지 보기;링크 추적;링크;링크 추적 링크;clickCollection;클릭 컬렉션;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 링크 추적

링크를 수동으로 설정하거나 추적할 수 있습니다. [자동으로](#automaticLinkTracking). 수동 추적은 아래 세부 사항을 추가하여 수행합니다. `web.webInteraction` 스키마의 일부입니다. 다음 세 가지 필수 변수가 있습니다.

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

버전 2.15.0부터 Web SDK는 `region` HTML 를 클릭합니다. 이렇게 하면 [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html) Adobe Analytics의 보고 기능.

링크 유형은 다음 세 값 중 하나일 수 있습니다.

* **`other`:** 사용자 지정 링크
* **`download`:** 다운로드 링크
* **`exit`:** 종료 링크

이 값은 다음과 같습니다 [자동으로 매핑됨](adobe-analytics/automatically-mapped-vars.md) 다음과 같은 경우 Adobe Analytics에 [구성됨](adobe-analytics/analytics-overview.md) 그러기 위해서.

## 자동 링크 추적 {#automaticLinkTracking}

기본적으로 Web SDK는 자격 있는 링크 태그를 캡처하고 레이블을 지정하며 클릭 수를 기록합니다. 클릭은 [캡처](https://www.w3.org/TR/uievents/#capture-phase) 문서에 첨부된 이벤트 리스너를 누릅니다.

다음 방법으로 자동 링크 추적을 비활성화할 수 있습니다. [구성](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) 웹 SDK.

```javascript
clickCollectionEnabled: false
```

### 링크 추적에 적합한 태그는 무엇입니까?{#qualifyingLinks}

앵커의 경우 자동 링크 추적이 수행됩니다. `A` 및 `AREA` 태그 사이에 코드를 삽입하지 마십시오. 그러나 이러한 태그는 첨부된 링크가 있을 경우 링크 추적에 고려되지 않습니다 `onclick` 핸들러입니다.

### 링크의 레이블은 어떻게 지정됩니까?{#labelingLinks}

앵커 태그에 다운로드 속성이 포함되어 있거나 링크가 인기 있는 파일 확장명으로 끝나는 경우 링크가 다운로드 링크로 레이블이 지정됩니다. 다운로드 링크 한정자는 다음과 같을 수 있습니다. [구성됨](../fundamentals/configuring-the-sdk.md) 정규 표현식:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

링크 대상 도메인이 현재 도메인과 다른 경우 링크는 종료 링크로 레이블이 지정됩니다 `window.location.hostname`.

다운로드 또는 종료 링크로서 적합하지 않은 링크는 &quot;기타&quot;로 레이블이 지정됩니다.

### 링크 추적 값은 어떻게 필터링할 수 있습니까?

자동 링크 추적으로 수집된 데이터는 다음을 제공하여 검사 및 필터링될 수 있습니다. [onBeforeEventSend 콜백 함수](../fundamentals/tracking-events.md#modifying-events-globally).

링크 추적 데이터 필터링은 Analytics 보고를 위한 데이터를 준비할 때 유용할 수 있습니다. 자동 링크 추적은 링크 이름과 링크 URL을 모두 캡처합니다. Analytics 보고서에서 링크 이름은 링크 URL보다 우선합니다. 링크 URL을 보고하려면 링크 이름을 제거해야 합니다. 다음 예제는 `onBeforeEventSend` 다운로드 링크의 링크 이름을 제거하는 함수:

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

Web SDK 버전 2.15.0부터 자동 링크 추적으로 수집된 데이터는 다음을 제공하여 검사, 증강 또는 필터링할 수 있습니다. [onBeforeLinkClickSend 콜백 함수](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

이 콜백 함수는 자동 링크 클릭 이벤트가 발생하는 경우에만 실행됩니다.

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

를 사용하여 링크 추적 이벤트를 필터링할 때 `onBeforeLinkClickSend` 명령, Adobe은 다음을 권장합니다. `false` 추적해서는 안 되는 링크 클릭의 경우. 다른 모든 응답을 수행하면 Web SDK는 데이터를 Edge Network로 전송합니다.


>[!NOTE]
>
>** 다음 두 경우 모두 `onBeforeEventSend` 및 `onBeforeLinkClickSend` 콜백 함수가 설정되면 Web SDK에서 `onBeforeLinkClickSend` 링크 클릭 상호 작용 이벤트를 필터링하고 확장하는 콜백 함수이며 그 뒤에는 `onBeforeEventSend` callback 함수.