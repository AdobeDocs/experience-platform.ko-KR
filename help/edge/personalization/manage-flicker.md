---
title: Adobe Experience Platform 웹 SDK를 사용하여 개인화된 경험을 위한 깜박임 관리
description: Adobe Experience Platform 웹 SDK를 사용하여 사용자 경험의 깜박임을 관리하는 방법을 알아봅니다.
keywords: target;flicker;prehingStyle;비동기적;비동기
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 깜박임 관리

개인화 콘텐츠를 렌더링할 때 SDK는 깜박임이 없도록 해야 합니다. FOOC(원본 컨텐츠의 Flash)이라고도 하는 깜박임은 테스트/개인화 도중 대체 요소가 표시되기 전에 원본 컨텐츠가 잠시 표시되는 경우입니다. SDK는 개인화 컨텐츠가 성공적으로 렌더링될 때까지 해당 요소가 숨겨지도록 페이지 요소에 CSS 스타일을 적용하려고 합니다.

깜박임 관리 기능에는 다음과 같은 몇 가지 단계가 있습니다.

1. 미리 숨기기
1. 사전 처리
1. 렌더링

## 미리 숨기기

사전 숨김 단계 동안 SDK는 `prehidingStyle` 구성 옵션을 사용하여 HTML 스타일 태그를 만들고 DOM에 추가하여 페이지의 큰 부분이 숨겨지도록 합니다. 페이지 중 어떤 부분을 개인화할 것인지 확실하지 않은 경우 `prehidingStyle`을 `body { opacity: 0 !important }`로 설정하는 것이 좋습니다. 이렇게 하면 전체 페이지가 숨겨집니다. 하지만 이러한 단점으로 인해 Lighthouse, 웹 페이지 테스트 등과 같은 툴에서 보고한 페이지 렌더링 성능이 더 나빠질 수 있습니다. 최상의 페이지 렌더링 성능을 유지하려면 `prehidingStyle`을(를) 개인화할 페이지의 일부가 포함된 컨테이너 요소 목록으로 설정하는 것이 좋습니다.

아래와 같은 HTML 페이지가 있고 `bar` 및 `bazz` 컨테이너 요소만 개인화됩니다.

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

그런 다음 `prehidingStyle`을(를) `#bar, #bazz { opacity: 0 !important }`과 같은 것으로 설정해야 합니다.

## 사전 처리

SDK가 서버로부터 개인화된 컨텐츠를 수신하면 사전 처리 단계가 시작됩니다. 이 단계 동안 응답이 사전 처리되어 개인화된 컨텐츠를 포함해야 하는 요소가 숨겨지도록 합니다. 이러한 요소가 숨겨진 후 `prehidingStyle` 구성 옵션을 기반으로 만들어진 HTML 스타일 태그가 제거되고 HTML 본문 또는 숨겨진 컨테이너 요소가 표시됩니다.

## 렌더링

모든 개인화 컨텐츠가 성공적으로 렌더링된 후 또는 오류가 발생한 경우, 이전에 숨겨진 모든 요소가 SDK에 의해 숨겨진 요소가 페이지에 없음을 확인하도록 표시됩니다.

## SDK가 비동기적으로 로드될 때 깜박임 관리

최상의 페이지 렌더링 성능을 얻으려면 항상 SDK를 비동기적으로 로드하는 것이 좋습니다. 그러나 개인화된 컨텐츠의 렌더링에는 몇 가지 의미가 있습니다. SDK가 비동기적으로 로드되면 사전 숨김 조각을 사용해야 합니다. 사전 숨김 조각을 HTML 페이지에서 SDK 앞에 추가해야 합니다. 다음은 전체 본문을 숨기는 예제 조각입니다.

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

HTML 본문이나 컨테이너 요소가 장기간 숨겨지지 않도록 하기 위해 코드 조각은 기본적으로 `3000` 밀리초 이후에 조각을 제거하는 타이머를 사용합니다. `3000` 밀리초는 최대 대기 시간입니다. 서버의 응답을 더 빨리 받고 처리한 경우, HTML 스타일 태그는 가능한 빨리 제거됩니다.
