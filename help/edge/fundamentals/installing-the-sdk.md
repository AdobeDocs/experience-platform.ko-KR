---
title: Adobe Experience Platform 웹 SDK 설치
seo-title: SDK 설치 Adobe Experience Platform 웹 SDK
description: Experience Platform 웹 SDK 설치 방법 살펴보기
seo-description: Experience Platform 웹 SDK 설치 방법 살펴보기
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (베타) SDK 설치

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform Web SDK를 구현하는 첫 번째 단계는 다음 &quot;기본 코드&quot;를 복사하여 HTML의 `<head>` 태그에 최대한 붙여넣는 것입니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js" async></script>
```

기본 코드는 이름이 `alloy`지정된 전역 함수를 만듭니다. 이 함수를 사용하여 SDK와 상호 작용합니다. 전역 함수의 이름을 다른 이름으로 지정하려면 다음과 같이 `alloy` 이름을 변경할 수 있습니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="alloy.js" async></script>
```

이 예에서 전역 함수의 이름이 `mycustomname`대신 `alloy`바뀝니다.

>[!IMPORTANT]
>잠재적인 문제를 방지하려면 숫자가 아닌 하나 이상의 문자가 포함된 이름을 사용하고 이미 에 있는 속성의 이름과 충돌하지 않습니다 `window`.

이 기본 코드는 전역 함수를 만드는 것 외에도 서버에 호스트된 외부 파일 \(`alloy.js`\) 내에 포함된 추가 코드를 로드합니다. 기본적으로 이 코드는 웹 페이지가 가능한 한 성능이 향상되도록 하기 위해 비동기식으로 로드됩니다. 권장 구현입니다.

## Internet Explorer 지원

이 SDK는 비동기 작업의 완료를 통신하는 방법인 약속을 사용합니다. SDK [에서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 사용하는 Promise 구현은 기본적으로 Internet Explorer를 제외한 모든 대상 브라우저에서 지원됩니다. Internet Explorer에서 SDK를 사용하려면 `window.Promise` 다각형을 [작성해야](https://remysharp.com/2010/10/08/what-is-a-polyfill)합니다.

이미 폴리칠이 `window.Promise` 되었는지 확인하려면:

1. Internet Explorer에서 웹 사이트를 엽니다.
1. 브라우저의 디버깅 콘솔을 엽니다.
1. 콘솔에 `window.Promise` 입력한 다음 Enter 키를 누릅니다.

다른 `undefined` 것이 나타나면 이미 폴리칠을 한 것 `window.Promise`같습니다. 다중 `window.Promise` 채우기 여부를 확인하는 또 다른 방법은 위의 설치 지침을 완료한 후 웹 사이트를 로드하는 것입니다. SDK에서 약속에 대한 내용을 언급하는 동안 오류가 발생하는 경우 내용이 채워지지 않았을 수 `window.Promise`있습니다.

다각형을 채우기로 결정한 경우 이전에 제공한 기본 코드 위에 다음 스크립트 태그를 `window.Promise`포함하십시오.

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

이렇게 하면 올바른 Promise 구현이 `window.Promise` 되도록 하는 스크립트가 로드됩니다.

## JavaScript 파일을 동기식으로 로드

앞에서 설명한 바와 같이, 복사해서 웹 사이트의 HTML에 붙여 넣은 기본 코드는 추가 코드가 있는 외부 파일을 로드합니다. 이 추가 코드에는 SDK의 핵심 기능이 포함되어 있습니다. 이 파일이 로드되는 동안 실행하려는 모든 명령이 큐에 올라가 파일이 로드된 후 처리됩니다. 가장 성능이 뛰어난 설치 방법입니다.

그러나 특정 상황에서 파일을 동기식으로 로드할 수도 있습니다(이러한 상황에 대한 자세한 내용은 나중에 문서화됩니다\). 이렇게 하면 외부 파일이 로드되어 실행될 때까지 브라우저에서 나머지 HTML 문서를 구문 분석하여 렌더링되지 않습니다. 사용자에게 주요 컨텐츠를 표시하기 전에 이러한 추가 지연은 일반적으로 권장되지 않지만 상황에 따라 적절할 수 있습니다.

파일을 비동기적으로 로드하지 않고 동기식으로 로드하려면 아래 표시된 것처럼 두 번째 `async` `script` 태그에서 속성을 제거합니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js"></script>
```
