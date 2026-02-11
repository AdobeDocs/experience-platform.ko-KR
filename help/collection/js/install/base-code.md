---
title: 기본 코드
description: 데이터 수집 라이브러리가 비동기적으로 로드되는 동안 큐 명령(부트스트랩)입니다.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 기본 코드

기본 코드는 Adobe Experience Platform 웹 SDK이 비동기적으로 로드되는 동안 명령을 대기시켜 부트스트래핑을 활성화합니다. 기본 코드가 실행되면 경쟁 조건이나 라이브러리가 로드될 때의 타이밍 걱정 없이 [`configure`](../commands/configure/overview.md) 또는 [`sendEvent`](../commands/sendevent/overview.md) 같은 명령을 즉시 호출할 수 있습니다. 웹 SDK 로드가 완료되면 대기 중인 명령은 대기열에 추가된 순서와 동일한 순서로 실행됩니다.

명령은 큐에 있는 경우에도 약속을 반환합니다. 명령이 대기열에 있으면 웹 SDK 로드가 완료될 때 명령이 실행된 후 Promise가 해결되거나 거부됩니다. 웹 SDK 로드가 완료되지 않은 경우(예: 라이브러리 로드가 실패한 경우) 큐에 있는 약속은 보류 상태로 유지됩니다.

## 기본 코드 추가

웹 SDK을 호출할 수 있는 스크립트 앞에 `<head>` 태그에 가능한 한 높은 기본 코드를 배치합니다.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

기본 코드를 추가한 후 선택한 메서드([JavaScript 라이브러리 로더](library.md) 또는 [태그 포함 코드](/help/tags/extensions/client/web-sdk/getting-started.md))를 사용하여 웹 SDK을 로드합니다. 태그 기반 구현의 경우 기본 코드는 웹 SDK 태그 확장 2.34.0 이상에서 지원됩니다.

이 기본 코드는 다음 시나리오에서 필요한 **not**&#x200B;입니다.

* JavaScript 라이브러리를 동기적으로 로드하는 경우. 라이브러리를 가져오고 실행하는 동안 동기 로드 블록 구문 분석.
* 태그 확장을 사용하는 경우 웹 SDK에 대한 모든 호출은 태그 규칙 또는 작업 내에서 수행됩니다. 구현이 태그 라이브러리 외부의 웹 SDK을 참조하는 경우에만 기본 코드를 포함해야 합니다. 대부분의 태그 구현은 일반적으로 태그 라이브러리 외부에서 웹 SDK을 호출하지 않으므로 대부분의 태그 구현에는 기본 코드가 필요하지 않습니다.

## 예시

명령이 대기열에 추가되고 해결되는 타이밍을 이해하려면 이 코드 예제 내의 주석을 참조하십시오. 이 예는 JavaScript 라이브러리와 태그 확장 모두에 적용됩니다.

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## SDK 인스턴스 이름 바꾸기

기본 코드의 마지막 줄을 수정하여 호출하는 전역 함수의 이름을 바꿀 수 있습니다. 변경:

```js
(window,["alloy"]);
```

끝:

```js
(window,["ingot"]);
```

이 변경 사항으로 `ingot` 대신 `alloy`을(를) 사용하여 명령을 호출할 수 있습니다.

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## 여러 SDK 인스턴스

원할 경우 기본 코드를 사용하여 한 페이지에 두 개 이상의 SDK 인스턴스를 구성할 수 있습니다. 자세한 내용은 [여러 웹 SDK 인스턴스 사용](../../use-cases/multiple-instances.md)을 참조하십시오.
