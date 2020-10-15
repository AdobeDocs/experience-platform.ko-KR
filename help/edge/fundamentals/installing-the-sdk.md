---
title: Adobe Experience Platform 웹 SDK 설치
seo-title: SDK 설치 Adobe Experience Platform 웹 SDK
description: Experience Platform 웹 SDK 설치 방법 살펴보기
seo-description: Experience Platform 웹 SDK 설치 방법 살펴보기
keywords: web sdk installation;installing web sdk;internet explorer;promise;
translation-type: tm+mt
source-git-commit: 5ef902ef7f7717121744f7f0074c0aa17e5a9e9a
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---


# SDK 설치 {#installing-the-sdk}

Adobe Experience Platform 웹 SDK를 사용하는 가장 선호하는 방법은 [Adobe Experience Platform Launch을 이용하는 것입니다](http://launch.adobe.com/). Extension 카탈로그 `AEP Web SDK` 에서 Extension을 검색하고 설치한 다음 Extension을 구성합니다.

AEP 웹 SDK는 CDN에서 사용할 수도 있습니다. 이 파일을 참조하거나 다운로드하여 자체 인프라에서 호스팅할 수 있습니다. 축소 및 축소 버전이 아닌 버전으로 사용할 수 있습니다. 분류되지 않은 버전은 디버깅에 유용합니다.

URL 구조:https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR 합금.js를 참조하십시오.

예:

* 축소: [https://cdn1.adoberesources.net/alloy/2.1.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.1.0/alloy.min.js)
* 축소 해제: [https://cdn1.adoberesources.net/alloy/2.1.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.1.0/alloy.js)

## 코드 추가 {#adding-the-code}

Adobe Experience Platform 구현의 첫 번째 단계 [!DNL Web SDK] 는 HTML의 `<head>` 태그에 가능한 한 높은 곳에 다음 &quot;기본 코드&quot;를 복사하고 붙여넣는 것입니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.1.0/alloy.min.js" async></script>
```

기본 코드는 이름이 인 전역 함수를 만듭니다 `alloy`. 이 함수를 사용하여 SDK와 상호 작용합니다. 전역 함수 이름을 다른 이름으로 지정하려면 다음과 같이 `alloy` 이름을 변경할 수 있습니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.1.0/alloy.min.js" async></script>
```

이 예에서 전역 함수의 이름이 대신 `mycustomname`로 변경되었습니다 `alloy`.

>[!IMPORTANT]
>
>잠재적인 문제를 방지하려면 숫자가 아니고 이미 찾은 속성의 이름과 충돌하지 않는 하나 이상의 문자가 포함된 이름을 사용하십시오 `window`.

이 기본 코드는 전역 함수를 만드는 것 외에도 서버에서 호스팅되는 외부 파일 \(`alloy.js`\) 내에 포함된 추가 코드도 로드합니다. 기본적으로 이 코드는 웹 페이지의 성능을 가능한 한 빨리 유지하도록 비동기식으로 로드됩니다. 권장 구현입니다.

## Internet Explorer 지원 {#support-internet-explore}

이 SDK는 비동기 작업의 완료를 통신하는 방법인 약속 기능을 사용합니다. SDK에서 [사용하는 Promise](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) 구현은 기본적으로 모든 대상 브라우저에서 지원됩니다 [!DNL Internet Explorer]. 에서 SDK를 사용하려면 [!DNL Internet Explorer]폴리칠이 `window.Promise` 필요합니다 [](https://remysharp.com/2010/10/08/what-is-a-polyfill).

폴리칠이 이미 있는지 확인하려면 다음을 `window.Promise` 수행하십시오.

1. 웹 사이트를 엽니다 [!DNL Internet Explorer].
1. 브라우저의 디버깅 콘솔을 엽니다.
1. 콘솔 `window.Promise` 에 입력한 다음 Enter 키를 누릅니다.

다른 것 `undefined` 이 나타나면 이미 폴리칠이 되어 있을 수 있습니다 `window.Promise`. 웹 사이트 `window.Promise` 를 로드하여 폴리채우기 여부를 확인하는 또 다른 방법은 위의 설치 지침을 완료한 후에 찾아보는 것입니다. SDK에서 약속에 대한 내용을 언급하는 동안 오류가 발생하는 경우 완전히 채워지지 않을 수 있습니다 `window.Promise`.

다각형을 입력해야 한다고 결정한 경우 이전에 제공한 기본 코드 위에 다음 스크립트 태그 `window.Promise`를 포함하십시오.

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

이렇게 하면 유효한 Promise 구현이 되도록 스크립트 `window.Promise` 가 로드됩니다.

>[!NOTE]
>
>다른 Promise 구현을 로드하도록 선택하는 경우, 이 구현이 지원되는지 확인하십시오 `Promise.prototype.finally`.

## JavaScript 파일을 동기식으로 로드 {#loading-javascript-synchronously}

코드 추가 섹션에 설명된 [대로](#adding-the-code), 웹 사이트의 HTML에 복사하여 붙여넣은 기본 코드는 추가 코드를 포함하는 외부 파일을 로드합니다. 이 추가 코드에는 SDK의 핵심 기능이 포함되어 있습니다. 이 파일이 로드되는 동안 실행하려는 모든 명령이 큐에 올라가 파일이 로드된 후 처리됩니다. 가장 성능이 뛰어난 설치 방법입니다.

그러나 특정 상황에서 파일을 동기식으로 로드할 수도 있습니다(이러한 상황에 대한 자세한 내용은 나중에 문서로 기록됨\). 이렇게 하면 외부 파일이 로드되어 실행될 때까지 브라우저에서 나머지 HTML 문서를 구문 분석하여 렌더링되는 것을 차단합니다. 사용자에게 주요 컨텐츠를 표시하기 전에 이러한 추가 지연은 일반적으로 권장되지 않지만 상황에 따라 적절한 지연이 가능합니다.

파일을 비동기적으로 로드하지 않고 동기식으로 로드하려면 아래 표시된 것처럼 두 번째 `async` `script` 태그에서 속성을 제거합니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.1.0/alloy.min.js"></script>
```
