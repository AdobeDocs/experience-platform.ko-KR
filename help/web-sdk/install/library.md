---
title: JavaScript 라이브러리를 사용하여 웹 SDK 설치
description: 독립 실행형 CDN 파일을 사용하여 웹 SDK 라이브러리를 참조합니다.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# JavaScript 라이브러리를 사용하여 웹 SDK 설치

를 사용하지 않고 웹 SDK를 설치할 수 있는 대안 [태그 확장 사용](extension.md) 는 CDN에서 호스팅되는 JavaScript 라이브러리를 참조합니다. 라이브러리를 직접 참조하거나 다운로드하여 자체 인프라에 호스팅할 수 있습니다. 축소된 전체 형식으로 사용할 수 있습니다.

웹 SDK 라이브러리는 다음 URL 구조를 사용하여 사용할 수 있습니다.

* **축소됨**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **전체**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

다음을 참조하십시오. [릴리스 정보](../release-notes.md) 를 사용하십시오. 예를 들어 버전 2.19.1의 전체 버전에 대한 URL은 입니다. `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## 코드 추가

다음 코드 블록을 `<head>` HTML 태그:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

이 코드는 비동기적으로 `alloy` 웹 SDK 명령을 호출할 수 있는 개체입니다. 웹 SDK를 동기적으로 로드하려면 다음을 제거할 수 있습니다. `async` 코드 블록의 마지막 행에 있는 특성입니다. 제거 `async` 속성은 라이브러리가 로드되고 실행될 때까지 브라우저에 의해 나머지 HTML 문서가 구문 분석되고 렌더링되지 않도록 차단합니다. 사용자에게 기본 콘텐츠를 표시하기 전에 이렇게 추가로 지연하는 것은 일반적으로 권장되지 않지만 조직의 필요에 따라 적절할 수 있습니다.
