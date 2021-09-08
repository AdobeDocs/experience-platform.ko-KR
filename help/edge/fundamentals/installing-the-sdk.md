---
title: Adobe Experience Platform Web SDK 설치
description: Experience Platform 웹 SDK를 설치하는 방법을 알아봅니다.
keywords: 웹 sdk 설치;웹 sdk 설치;internet explorer;약속;npm 패키지
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f5d3c5911357d4b76e4d38564bf637e2549469d6
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 2%

---

# SDK 설치 {#installing-the-sdk}

Adobe Experience Platform Web SDK를 사용하는 세 가지 지원 방법이 있습니다.

1. Adobe Experience Platform Web SDK를 사용하는 기본 방법은 데이터 수집 UI를 사용하는 것입니다.
1. Adobe Experience Platform Web SDK는 CDN(Content Delivery Network)에서도 사용할 수 있습니다.
1. EcmaScript 5 및 EcmaScript 2015(ES6) 모듈을 내보내는 NPM 라이브러리를 사용합니다.

## 옵션 1: 태그 확장 설치

태그 확장에 대한 설명서는 [launch 설명서](../../tags/extensions/web/sdk/overview.md)를 참조하십시오.

## 옵션 2: 사전 빌드된 독립형 버전 설치

사전 빌드된 버전은 CDN에서 사용할 수 있습니다. 페이지에서 직접 CDN의 라이브러리를 참조하거나 자체 인프라에서 다운로드하여 호스팅할 수 있습니다. 축소된 및 축소 해제된 형식으로 사용할 수 있습니다. 축소 해제된 버전은 디버깅 목적에 유용합니다.

URL 구조: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js 또는 축소되지 않은 버전의 alloy.js입니다.

예:


* 축소: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* 축소 해제: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)


### 코드 추가 {#adding-the-code}

사전 빌드된 독립형 버전은 페이지에 직접 추가된 &quot;기본 코드&quot;가 필요합니다. 다음 &quot;기본 코드&quot;를 복사하여 HTML의 `<head>` 태그에 가능한 높게 붙여넣습니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

&quot;기본 코드&quot;는 `alloy`이라는 글로벌 함수를 만듭니다. 이 함수를 사용하여 SDK와 상호 작용합니다. 전역 함수에 다른 이름을 지정하려면 `alloy` 이름을 다음과 같이 변경합니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

이 예에서 전역 함수의 이름은 `alloy` 대신 `mycustomname` 로 변경됩니다.

>[!IMPORTANT]
>
>잠재적인 문제를 방지하려면 숫자가 아니며 `window`에 이미 있는 속성의 이름과 충돌하지 않는 하나 이상의 문자가 포함된 이름을 사용하십시오.

이 기본 코드는 전역 함수를 만드는 것 외에도 서버에 호스팅된 외부 파일 \(`alloy.js`\) 내에 포함된 추가 코드도 로드합니다. 기본적으로 이 코드는 웹 페이지의 성능을 최대한 향상시키기 위해 비동기식으로 로드됩니다. 권장되는 구현입니다.

### Internet Explorer 지원 {#support-internet-explore}

이 SDK에서는 비동기 작업 완료를 통신하는 방법인 약속을 사용합니다. SDK에서 사용하는 [Promise](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) 구현은 기본적으로 [!DNL Internet Explorer]를 제외한 모든 타겟 브라우저에서 지원됩니다. [!DNL Internet Explorer]에서 SDK를 사용하려면 `window.Promise` [polychild](https://remysharp.com/2010/10/08/what-is-a-polyfill)가 있어야 합니다.

이미 `window.Promise` 폴리칠이 있는지 확인하려면:

1. [!DNL Internet Explorer]에서 웹 사이트를 엽니다.
1. 브라우저의 디버깅 콘솔을 엽니다.
1. 콘솔에 `window.Promise` 을 입력한 다음 Enter 키를 누릅니다.

`undefined` 이외의 다른 항목이 나타나면 이미 `window.Promise`을(를) 입력했을 수 있습니다. `window.Promise`이(가) 폴리필인지를 확인하는 또 다른 방법은 위의 설치 지침을 완료한 후 웹 사이트를 로드한 것입니다. SDK에서 약속에 대한 내용을 언급하는 동안 오류가 발생하면 `window.Promise`을 채우지 않았을 수 있습니다.

`window.Promise`을(를) 채우도록 결정한 경우, 이전에 제공한 기본 코드 위에 다음 스크립트 태그를 포함하십시오.

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

이 태그는 `window.Promise` 이 유효한 Promise 구현인지 확인하는 스크립트를 로드합니다.

>[!NOTE]
>
>다른 Promise 구현을 로드하도록 선택하는 경우 `Promise.prototype.finally`을 지원하는지 확인하십시오.

### JavaScript 파일을 동기식으로 로드 {#loading-javascript-synchronously}

[코드](#adding-the-code)를 추가하는 것과 같이, 복사하여 웹 사이트의 HTML에 붙여넣은 기본 코드는 외부 파일을 로드합니다. 외부 파일에는 SDK의 핵심 기능이 포함되어 있습니다. 이 파일이 로드되는 동안 실행하려는 모든 명령은 큐에 있다가 파일이 로드된 후 처리됩니다. 파일을 비동기식으로 로드하는 것이 가장 강력한 설치 방법입니다.

그러나 특정 상황에서 파일을 동기식으로 \(이러한 상황에 대한 자세한 내용은 나중에 문서화됨\) 로드할 수 있습니다. 이렇게 하면 외부 파일이 로드되고 실행될 때까지 브라우저에서 나머지 HTML 문서를 구문 분석하고 렌더링할 수 없습니다. 기본 콘텐츠를 사용자에게 표시하기 전에 이러한 추가적인 지연은 일반적으로 좌절되지만, 상황에 따라 적절할 수 있습니다.

파일을 비동기식으로 로드하지 않고 동기식으로 로드하려면 아래 표시된 대로 두 번째 `script` 태그에서 `async` 속성을 제거합니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js"></script>
```

## 옵션 3: NPM 패키지 사용

Adobe Experience Platform Web SDK는 NPM 패키지도 사용할 수 있습니다. [](https://www.npmjs.com) NPM은 JavaScript용 패키지 관리자입니다. NPM 패키지를 설치하면 Adobe Experience Platform Web SDK JavaScript에 대한 빌드 프로세스를 제어할 수 있습니다. NPM 패키지는 브라우저에서 실행되어야 하는 EcmaScript 버전 5 모듈 또는 EcmaScript 버전 2015(ES6) 모듈을 표시합니다.

```bash
npm install @adobe/alloy
```

Adobe Experience Platform 웹 SDK의 NPM 패키지는 `createInstance` 함수를 노출합니다. 이 함수는 인스턴스를 만드는 데 사용됩니다. 함수에 전달되는 이름 옵션은 로그에 사용되는 접두사를 제어합니다. 다음은 패키지 사용의 예입니다.

### 패키지를 ECMAScript 2015(ES6) 모듈로 사용

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM 패키지는 CommonJS 모듈을 사용합니다. 따라서 bundler를 사용할 때는 번들러가 CommonJS 모듈을 지원하는지 확인합니다. [롤업](https://rollupjs.org)과 같은 일부 번들러는 CommonJS 지원을 제공하는 [플러그인](https://www.npmjs.com/package/@rollup/plugin-commonjs)이 필요합니다.

### 패키지를 ECMAScript 5 모듈로 사용

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Internet Explorer 지원

Adobe Experience Platform SDK에서는 비동기 작업 완료를 통신하는 방법인 약속을 사용합니다. SDK에서 사용하는 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 구현은 기본적으로 [!DNL Internet Explorer]를 제외한 모든 타겟 브라우저에서 지원됩니다. [!DNL Internet Explorer]에서 SDK를 사용하려면 `window.Promise` [polychild](https://remysharp.com/2010/10/08/what-is-a-polyfill)가 있어야 합니다.

약속 폴리채우기에 사용할 수 있는 하나의 라이브러리는 promise-polyfill입니다. NPM으로 설치하는 방법에 대한 자세한 내용은 [promise-polyfill 설명서](https://www.npmjs.com/package/promise-polyfill) 를 참조하십시오.

>[!NOTE]
>
>다른 Promise 구현을 로드하도록 선택하는 경우 `Promise.prototype.finally`을 지원하는지 확인하십시오.
