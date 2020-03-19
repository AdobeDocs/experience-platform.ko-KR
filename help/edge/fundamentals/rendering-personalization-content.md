---
title: 맞춤형 컨텐츠 렌더링
seo-title: Adobe Experience Platform 웹 SDK 맞춤형 컨텐츠 렌더링
description: Experience Platform 웹 SDK를 사용하여 개인화된 콘텐츠를 렌더링하는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 개인화된 콘텐츠를 렌더링하는 방법 살펴보기
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (베타) 맞춤형 컨텐츠 렌더링

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

SDK는 이벤트를 서버에 보내고 이벤트에서 옵션으로 `viewStart` `true` 설정하면 개인화된 컨텐츠를 자동으로 렌더링합니다.

```javascript
alloy("event", {
  "viewStart": true,
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
});
```

개인화된 컨텐츠의 렌더링은 비동기식으로 이루어지므로 특정 컨텐츠가 페이지의 일부인 경우를 가정하지 마십시오.

## 깜박임 관리

개인화 콘텐츠를 렌더링할 때 SDK에서 깜박임이 없도록 해야 합니다. FOOC(Flash of Original Content)라고도 하는 Flicker는 테스트나 개인화 중에 대체 요소가 표시되기 전에 원본 컨텐츠가 잠깐 표시되는 경우입니다. SDK는 개인화 컨텐츠가 성공적으로 렌더링될 때까지 이러한 요소가 숨겨지도록 페이지의 요소에 CSS 스타일을 적용하려고 합니다.

깜박임 관리 기능에는 다음과 같은 몇 가지 단계가 있습니다.

1. 미리 숨기기
1. 사전 처리
1. 렌더링

### 미리 숨기기

사전 숨김 단계 동안 SDK는 `prehidingStyle` 구성 옵션을 사용하여 HTML 스타일 태그를 만들고 DOM에 추가하여 페이지의 큰 부분이 숨겨지도록 합니다. 페이지의 어떤 부분을 개인화할 것인지 잘 모를 경우 `prehidingStyle` `body { opacity: 0 !important }`로 설정하는 것이 좋습니다. 이렇게 하면 전체 페이지가 숨겨집니다. 그러나 Lighthouse, Web Page Tests 등과 같은 툴에서 보고한 페이지 렌더링 성능이 저하될 수 있습니다. 최상의 페이지 렌더링 성능을 얻으려면 개인화할 페이지의 `prehidingStyle` 부분을 포함하는 컨테이너 요소 목록으로 설정하는 것이 좋습니다.

아래 HTML 페이지와 같은 HTML 페이지가 있고 `bar` 및 `bazz` 컨테이너 요소만 개인화될 것이라고 가정할 경우:

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

그러면 `prehidingStyle` 그런 것으로 설정해야 `#bar, #bazz { opacity: 0 !important }`합니다.

### 사전 처리

SDK가 서버로부터 개인화된 콘텐츠를 수신하면 사전 처리 단계가 시작됩니다. 이 단계 동안 응답이 미리 처리되어 개인화된 컨텐츠를 포함해야 하는 요소가 숨겨지도록 합니다. 이러한 요소가 숨겨져 있으면 구성 옵션을 기반으로 만들어진 HTML 스타일 태그가 제거되고 HTML 본문 또는 숨겨진 컨테이너 요소가 표시됩니다. `prehidingStyle`

### 렌더링

모든 개인화 컨텐츠가 성공적으로 렌더링된 후 또는 오류가 발생한 경우, 이전에 숨겨진 모든 요소가 SDK에 의해 숨겨진 페이지에 없음을 확인하도록 표시됩니다.

## SDK가 비동기적으로 로드될 때 깜박임 관리

최상의 페이지 렌더링 성능을 얻으려면 항상 SDK를 비동기식으로 로드하는 것이 좋습니다. 그러나 개인화된 컨텐츠의 렌더링에는 몇 가지 의미가 있습니다. SDK 파섹 HTML 페이지의 SDK 앞에 사전 숨김 조각을 추가해야 합니다. 다음은 전체 본문을 숨기는 예제 조각입니다.

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

HTML 본문이나 컨테이너 요소가 장기간 숨겨지지 않도록 코드 조각은 `3000` 밀리초 후 조각을 기본적으로 제거하는 타이머를 사용합니다. 밀리초 `3000` 값은 최대 대기 시간입니다. 서버로부터의 응답이 더 빨리 수신되고 처리되면, HTML 스타일 태그는 가능한 빨리 제거됩니다.
