---
title: Adobe Experience Platform Web SDK 설치
description: Experience Platform Web SDK를 설치하는 방법을 알아봅니다.
keywords: web sdk 설치;web sdk 설치;internet explorer;promise;npm 패키지
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: e0fc9708edec3b36bed9925f12fca9db8b477262
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 2%

---

# SDK 설치 {#installing-the-sdk}

Adobe Experience Platform Web SDK를 사용하는 세 가지 지원되는 방법은 다음과 같습니다.

1. Adobe Experience Platform Web SDK를 사용하는 기본 방법은 데이터 수집 UI 또는 Experience Platform UI를 사용하는 것입니다.
1. Adobe Experience Platform Web SDK는 CDN(콘텐츠 전달 네트워크)에서도 사용할 수 있습니다.
1. EcmaScript 5 및 EcmaScript 2015(ES6) 모듈을 내보내는 NPM 라이브러리를 사용합니다.

## 옵션 1: 태그 확장 설치

태그 확장에 대한 설명서는 [태그 설명서](../../tags/extensions/client/sdk/overview.md)

## 옵션 2: 미리 빌드된 독립 실행형 버전 설치

사전 빌드된 버전은 CDN에서 사용할 수 있습니다. 페이지에서 직접 CDN의 라이브러리를 참조하거나, 자체 인프라에서 다운로드하여 호스팅할 수 있습니다. 축소 및 축소 해제된 형식으로 사용할 수 있습니다. 축소되지 않은 버전은 디버깅에 유용합니다.

URL 구조: https://cdn1.adoberesources.net/alloy/[버전]축소되지 않은 버전의 /alloy.min.js 또는 alloy.js입니다.

예:


* 축소됨: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js)
* 축소 취소: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js)


### 코드 추가 {#adding-the-code}

사전 빌드된 독립 실행형 버전에는 페이지에 직접 추가된 &quot;기본 코드&quot;가 필요합니다. 다음 &quot;기본 코드&quot;를 복사해 최대한 높게 붙여 넣습니다. `<head>` HTML 태그:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

&quot;기본 코드&quot;는 라는 전역 함수를 만듭니다. `alloy`. 이 함수를 사용하여 SDK와 상호 작용합니다. 전역 함수의 이름을 다른 이름으로 지정하려면 `alloy` 이름을 다음과 같이 지정합니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

이 예에서는 전역 함수의 이름이 바뀝니다 `mycustomname`, 대신 `alloy`.

>[!IMPORTANT]
>
>잠재적인 문제를 방지하려면 숫자가 아니고 이미 발견된 속성 이름과 충돌하지 않는 문자가 하나 이상 포함된 이름을 사용하십시오. `window`.

이 기본 코드는 전역 함수를 만드는 것 외에도 외부 파일 \(`alloy.js`\) 서버에 호스팅됩니다. 기본적으로 이 코드는 비동기적으로 로드되어 웹 페이지가 가능한 한 성능을 유지할 수 있도록 합니다. 권장되는 구현입니다.

### Internet Explorer 지원 {#support-internet-explore}

이 SDK는 비동기 작업의 완료를 통신하는 방법인 약속을 사용합니다. 다음 [약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) sdk에서 사용하는 구현은 을 제외한 모든 target 브라우저에서 기본적으로 지원됩니다. [!DNL Internet Explorer]. 에서 SDK를 사용하려면 [!DNL Internet Explorer], 다음을 수행해야 합니다. `window.Promise` [다량 충전됨](https://remysharp.com/2010/10/08/what-is-a-polyfill).

다음을 이미 가지고 있는지 확인 `window.Promise` 폴리필됨:

1. 에서 웹 사이트 열기 [!DNL Internet Explorer].
1. 브라우저의 디버깅 콘솔을 엽니다.
1. 유형 `window.Promise` 콘솔로 이동한 다음 Enter 키를 누릅니다.

다음 이외의 다른 항목일 경우 `undefined` 이(가) 나타나면 이미 폴리필했을 수 있습니다. `window.Promise`. 다음을 확인할 수 있는 다른 방법: `window.Promise` 는 위의 설치 지침을 완료한 후 웹 사이트를 로드하여 polyfilled입니다. SDK에서 약속에 대해 언급하는 동안 오류가 발생하면 채워지지 않았을 수 있습니다 `window.Promise`.

폴리필을 결정했다면 다음을 수행합니다 `window.Promise`는 이전에 제공된 기본 코드 위에 다음 스크립트 태그를 포함합니다.

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

이 태그는 다음을 확인하는 스크립트를 로드합니다 `window.Promise` 는 유효한 Promise 구현입니다.

>[!NOTE]
>
>다른 Promise 구현을 로드하도록 선택하는 경우 다음을 지원하는지 확인하십시오. `Promise.prototype.finally`.

### 동기적으로 JavaScript 파일 로드 {#loading-javascript-synchronously}

섹션에 설명된 대로 [코드 추가](#adding-the-code)를 사용하여 복사하고 웹 사이트의 HTML에 붙여넣은 기본 코드는 외부 파일을 로드합니다. 외부 파일에는 SDK의 핵심 기능이 포함되어 있습니다. 이 파일이 로드되는 동안 실행하려는 모든 명령은 큐에 있다가 파일이 로드된 후 처리됩니다. 파일을 비동기식으로 로드하는 것이 가장 성능이 좋은 설치 방법입니다.

그러나 특정 상황에서는 파일을 동기식으로 로드할 수 있습니다. \(이러한 상황에 대한 자세한 내용은 나중에 문서화됩니다\). 이렇게 하면 외부 파일이 로드되고 실행될 때까지 나머지 HTML 문서가 브라우저에 의해 구문 분석되고 렌더링되지 않습니다. 사용자에게 기본 콘텐츠를 표시하기 전에 이렇게 추가로 지연하는 것은 일반적으로 권장되지 않지만 상황에 따라 적절할 수 있습니다.

파일을 비동기식으로 로드하지 않고 동기식으로 로드하려면 `async` 속성(초) `script` 태그는 아래와 같습니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>
```

## 옵션 3: NPM 패키지 사용

Adobe Experience Platform Web SDK는 NPM 패키지로 사용할 수도 있습니다. [NPM](https://www.npmjs.com) 는 JavaScript용 패키지 관리자입니다. NPM 패키지를 설치하면 Adobe Experience Platform Web SDK JavaScript에 대한 빌드 프로세스를 제어할 수 있습니다. NPM 패키지는 브라우저에서 실행되도록 지정된 EcmaScript 버전 5 모듈 또는 EcmaScript 버전 2015(ES6) 모듈을 노출합니다.

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK의 NPM 패키지는 `createInstance` 함수. 이 함수는 인스턴스를 만드는 데 사용합니다. 함수에 전달되는 이름 옵션은 로깅에 사용되는 접두사를 제어합니다. 다음은 패키지 사용의 예입니다.

### 패키지를 ECMAScript 2015(ES6) 모듈로 사용

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM 패키지는 CommonJS 모듈을 사용합니다. 따라서 번들러를 사용할 때는 번들러가 CommonJS 모듈을 지원하는지 확인하십시오. 다음과 같은 일부 번들러 [롤업](https://rollupjs.org), 필수 [플러그인](https://www.npmjs.com/package/@rollup/plugin-commonjs) CommonJS 지원을 제공합니다.

### 패키지를 ECMAScript 5 모듈로 사용

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Internet Explorer 지원

Adobe Experience Platform SDK는 비동기 작업의 완료를 통신하는 방법인 약속을 사용합니다. 다음 [약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) sdk에서 사용하는 구현은 을 제외한 모든 target 브라우저에서 기본적으로 지원됩니다. [!DNL Internet Explorer]. 에서 SDK를 사용하려면 [!DNL Internet Explorer], 다음을 수행해야 합니다. `window.Promise` [다량 충전됨](https://remysharp.com/2010/10/08/what-is-a-polyfill).

폴리필을 약속하는 데 사용할 수 있는 라이브러리 중 하나는 약속 폴리필입니다. 다음을 참조하십시오. [promise-polyfill 설명서](https://www.npmjs.com/package/promise-polyfill) 를 참조하십시오.

>[!NOTE]
>
>다른 Promise 구현을 로드하도록 선택하는 경우 다음을 지원하는지 확인하십시오. `Promise.prototype.finally`.
