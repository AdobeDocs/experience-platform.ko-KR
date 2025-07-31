---
title: JavaScript 라이브러리를 사용하여 웹 SDK 설치
description: 독립 실행형 CDN 파일을 사용하여 웹 SDK 라이브러리를 참조합니다.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# JavaScript 라이브러리를 사용하여 웹 SDK 설치

[태그 확장](extension.md)을 사용하지 않고 웹 SDK을 설치하는 다른 방법은 CDN에서 호스팅되는 JavaScript 라이브러리를 참조하는 것입니다. 라이브러리를 직접 참조하거나 다운로드하여 자체 인프라에 호스팅할 수 있습니다. 축소된 전체 형식으로 사용할 수 있습니다.

웹 SDK 라이브러리는 다음 URL 구조를 사용하여 사용할 수 있습니다.

* **축소됨**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **전체**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

URL에 포함할 최신 버전은 [릴리스 정보](../release-notes.md)를 참조하세요. 예를 들어 버전 2.19.1의 전체 버전에 대한 URL은 `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`입니다.

## 코드 추가

다음 코드 블록을 HTML의 `<head>` 태그에 가능한 한 많이 추가합니다.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

이 코드는 모든 웹 SDK 명령을 호출할 수 있는 `alloy` 개체를 비동기적으로 만듭니다. 웹 SDK을 동기적으로 로드하려면 코드 블록의 마지막 줄에서 `async` 특성을 제거할 수 있습니다. `async` 특성을 제거하면 라이브러리가 로드되고 실행될 때까지 브라우저에 의해 나머지 HTML 문서가 구문 분석되고 렌더링되지 않습니다. 사용자에게 기본 콘텐츠를 표시하기 전에 이렇게 추가로 지연하는 것은 일반적으로 권장되지 않지만 조직의 필요에 따라 적절할 수 있습니다.
