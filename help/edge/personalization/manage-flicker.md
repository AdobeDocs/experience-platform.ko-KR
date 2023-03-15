---
title: Adobe Experience Platform Web SDK를 사용하여 개인화된 경험에 대한 플리커 관리
description: Adobe Experience Platform Web SDK를 사용하여 사용자 경험에서 플리커를 관리하는 방법을 알아봅니다.
keywords: target;깜박임;사전 숨김;스타일 비동기화;비동기;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 플리커 관리

개인화 콘텐츠를 렌더링할 때 SDK에서 깜박임이 없는지 확인해야 합니다. FOOC(원본 컨텐츠 Flash)라고도 하는 플리커는 테스트/개인화 중에 대체 컨텐츠가 나타나기 전에 원본 컨텐츠가 잠깐 나타나는 것입니다. SDK는 페이지의 요소에 CSS 스타일을 적용하여 개인화 콘텐츠가 성공적으로 렌더링될 때까지 해당 요소를 숨기도록 합니다.

플리커 관리 기능에는 다음과 같은 몇 가지 단계가 있습니다.

1. 사전 숨김
1. 전처리
1. 렌더링

## 사전 숨김

사전 숨김 단계 동안 SDK는 `prehidingStyle` HTML 스타일 태그를 만든 후 DOM에 추가하여 페이지의 큰 부분이 숨겨지도록 하는 구성 옵션 개인화할 페이지 부분을 잘 모르는 경우 설정하는 것이 좋습니다. `prehidingStyle` 끝 `body { opacity: 0 !important }`. 이렇게 하면 전체 페이지가 숨겨집니다. 그러나 Lighthouse, 웹 페이지 테스트 등의 도구에서 보고하는 페이지 렌더링 성능이 더 나빠지는 단점이 있습니다. 최상의 페이지 렌더링 성능을 가지려면 을 설정하는 것이 좋습니다 `prehidingStyle` 로 나열된 컨테이너 요소 목록에서 개인화할 페이지의 부분을 포함합니다.

아래 페이지와 같은 HTML 페이지가 있고 해당 페이지만 알고 있다고 가정합니다. `bar` 및 `bazz` 컨테이너 요소는 항상 개인화됩니다.

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

그런 다음 `prehidingStyle` 다음과 같은 항목으로 설정해야 합니다. `#bar, #bazz { opacity: 0 !important }`.

## 전처리

전처리 단계는 SDK가 서버로부터 개인화된 콘텐츠를 받으면 시작됩니다. 이 단계에서는 응답을 전처리하여 개인화된 콘텐츠를 포함해야 하는 요소를 숨깁니다. 이러한 요소가 숨겨지면 를 기반으로 만들어진 HTML 스타일 태그가 `prehidingStyle` 구성 옵션이 제거되고 HTML 본문 또는 숨겨진 컨테이너 요소가 표시됩니다.

## 렌더링

모든 개인화 콘텐츠가 성공적으로 렌더링되거나 오류가 있는 경우 이전에 숨겨진 모든 요소가 표시되어 SDK에 의해 숨겨진 숨겨진 요소가 페이지에 없는지 확인합니다.

## SDK가 비동기적으로 로드될 때 깜박임 관리

항상 SDK를 비동기식으로 로드하여 최상의 페이지 렌더링 성능을 얻는 것이 좋습니다. 그러나 이는 개인화된 콘텐츠의 렌더링에 몇 가지 영향을 미칩니다. SDK가 비동기적으로 로드되면 코드 조각 사전 숨김을 사용해야 합니다. 코드 조각 사전 숨김은 HTML 페이지에서 SDK 앞에 추가해야 합니다. 다음은 전체 본문을 숨기는 예제 코드 조각입니다.

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

HTML 본문 또는 컨테이너 요소가 장기간 숨겨지지 않도록 코드 조각 사전 숨김은 기본적으로 다음 시간 이후에 코드 조각을 제거하는 타이머를 사용합니다 `3000` 밀리초. 다음 `3000` 밀리초는 최대 대기 시간입니다. 서버의 응답을 더 빨리 받고 처리한 경우 HTML 스타일 사전 숨김 태그가 가능한 한 빨리 제거됩니다.
