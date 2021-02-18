---
title: Adobe Experience Platform 웹 SDK 설치
description: Experience Platform 웹 SDK를 설치하는 방법을 알아봅니다.
keywords: 웹 sdk 설치;웹 sdk 설치;internet explorer;promise;web sdk 설치;web sdk 설치;internet explorer;promise;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---


# SDK {#installing-the-sdk} 설치

Adobe Experience Platform 웹 SDK를 사용하는 가장 선호하는 방법은 [Adobe Experience Platform Launch](http://launch.adobe.com/)을 이용하는 것입니다. 확장 카탈로그에서 `AEP Web SDK`을 검색하여 설치한 다음 확장을 구성합니다.

Adobe Experience Platform 웹 SDK는 CDN에서 사용할 수도 있습니다. 이 파일을 참조하거나 다운로드하여 자체 인프라에서 호스팅할 수 있습니다. 축소된 버전 및 간소화되지 않은 버전으로 사용할 수 있습니다. 간소화되지 않은 버전은 디버깅에 유용합니다.

URL 구조:https://cdn1.adoberesources.net/alloy/[버전]/alloy.min.js OR 합금.js를 다운로드하지 않은 버전의 경우

예:

* 축소:[https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* 축소 해제:[https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## {#adding-the-code} 코드 추가

Adobe Experience Platform [!DNL Web SDK]을(를) 구현하는 첫 번째 단계는 HTML의 `<head>` 태그에 가능한 한 높은 값으로 다음 &quot;기본 코드&quot;를 복사하여 붙여 넣는 것입니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

기본 코드는 `alloy`이라는 전역 함수를 만듭니다. 이 함수를 사용하여 SDK와 상호 작용합니다. 전역 함수의 이름을 다른 이름으로 지정하려면 다음과 같이 `alloy` 이름을 변경할 수 있습니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

이 예에서 전역 함수의 이름이 `alloy` 대신 `mycustomname`으로 변경되었습니다.

>[!IMPORTANT]
>
>잠재적인 문제를 방지하려면 숫자가 아닌 하나 이상의 문자가 포함된 이름을 사용하십시오. 이 이름은 `window`에 이미 있는 속성의 이름과 충돌하지 않습니다.

이 기본 코드는 글로벌 함수를 만드는 것 외에도 서버에 호스팅된 외부 파일 \(`alloy.js`\) 내에 포함된 추가 코드도 로드합니다. 기본적으로 이 코드는 웹 페이지의 성능을 가능한 한 빨리 제공하도록 비동기적으로 로드됩니다. 권장 구현입니다.

## Internet Explorer 지원 {#support-internet-explore}

이 SDK에서는 비동기 작업의 완료를 통신하는 방법인 약속 기능을 사용합니다. SDK에서 사용하는 [Promise](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) 구현은 기본적으로 [!DNL Internet Explorer]를 제외한 모든 대상 브라우저에서 지원됩니다. [!DNL Internet Explorer]에서 SDK를 사용하려면 `window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)가 있어야 합니다.

이미 `window.Promise`개의 폴리칠이 있는지 확인하려면:

1. [!DNL Internet Explorer]에서 웹 사이트를 엽니다.
1. 브라우저의 디버깅 콘솔을 엽니다.
1. 콘솔에 `window.Promise`을 입력한 다음 Enter 키를 누릅니다.

`undefined` 이외의 다른 항목이 나타나면 이미 폴린으로 채워진 `window.Promise`이(가) 있을 수 있습니다. 위의 설치 지침을 완료한 후 웹 사이트를 로드하여 `window.Promise`이(가) 폴리칠되었는지 확인하는 또 다른 방법입니다. SDK에서 약속에 대한 내용을 언급하는 동안 오류가 발생하는 경우, `window.Promise`을(를) 채우지 않았을 수 있습니다.

`window.Promise`을(를) 다각도로 채우도록 결정한 경우 이전에 제공된 기본 코드 위에 다음 스크립트 태그를 포함하십시오.

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

이렇게 하면 `window.Promise`이(가) 유효한 Promise 구현인지 확인하는 스크립트가 로드됩니다.

>[!NOTE]
>
>다른 Promise 구현을 로드하도록 선택하는 경우 `Promise.prototype.finally`을(를) 지원하는지 확인하십시오.

## JavaScript 파일을 동기적으로 {#loading-javascript-synchronously} 로드

[코드 추가](#adding-the-code)에 설명된 대로, 복사해서 웹 사이트의 HTML에 붙여 넣은 기본 코드는 추가 코드가 있는 외부 파일을 로드합니다. 이 추가 코드에는 SDK의 핵심 기능이 포함되어 있습니다. 이 파일을 로드하는 동안 실행하려는 명령은 큐에 올라가 파일을 로드한 후 처리됩니다. 가장 성능이 뛰어난 설치 방법입니다.

그러나 특정 상황에서 파일을 동기식으로 로드할 수도 있습니다(이러한 상황에 대한 자세한 내용은 나중에 문서화됩니다\). 이렇게 하면 외부 파일을 로드하여 실행할 때까지 브라우저에서 나머지 HTML 문서를 구문 분석하여 렌더링되지 않습니다. 사용자에게 기본 컨텐츠를 표시하기 전에 이러한 추가 지연은 일반적으로 거절되지만 상황에 따라 적절할 수 있습니다.

파일을 비동기적으로 로드하는 대신 동기식으로 로드하려면 아래 표시된 것처럼 두 번째 `script` 태그에서 `async` 속성을 제거합니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```
