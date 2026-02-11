---
title: 웹 SDK JavaScript 라이브러리 설치
description: 독립 실행형 CDN 파일을 사용하여 웹 SDK 라이브러리를 참조합니다.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 웹 SDK JavaScript 라이브러리 설치

[웹 SDK 태그 확장](/help/tags/extensions/client/web-sdk/overview.md)을 사용하지 않도록 선택하는 경우 Adobe의 CDN에서 호스팅되는 독립 실행형 JavaScript 라이브러리를 참조하여 웹 SDK을 설치할 수 있습니다. 라이브러리를 직접 참조하거나 다운로드하여 자체 인프라에 호스팅할 수 있습니다. 축소된 전체 형식으로 사용할 수 있습니다.

웹 SDK 라이브러리는 다음 URL 구조를 사용하여 사용할 수 있습니다.

* **축소됨**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **전체**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

URL에 포함할 최신 버전은 [웹 SDK 릴리스 노트](../release-notes.md)를 참조하세요. 예를 들어 버전 2.19.1의 전체 버전에 대한 URL은 `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`입니다.

## 기본 코드 및 라이브러리 로더 추가

추가할 코드는 다음 두 개의 섹션으로 구성됩니다.

* **기본 코드**: 웹 SDK이 비동기적으로 로드되는 동안 명령을 대기시켜 부트스트래핑을 허용합니다. 자세한 내용은 [기본 코드](base-code.md)을 참조하세요. Adobe에서는 페이지를 로드하는 동안 웹 SDK 명령을 호출할 때 경쟁 조건을 방지하기 위해 라이브러리를 비동기적으로 로드할 때 기본 코드를 사용하는 것이 좋습니다.
* **라이브러리 로더**: 전체 JavaScript 라이브러리를 로드합니다.

웹 SDK을 호출할 수 있는 스크립트 앞에 `<head>` 태그에서 다음 코드 블록을 가능한 한 높게 추가합니다.

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

웹 SDK을 동기적으로 로드하려면 라이브러리를 로드할 때 `async` 특성을 제거할 수 있습니다. `async` 특성을 제거하면 브라우저가 라이브러리를 가져와서 실행하는 동안 HTML 구문 분석이 차단됩니다. 사용자에게 기본 콘텐츠를 표시하기 전에 이렇게 추가로 지연하는 것은 일반적으로 권장되지 않지만 조직의 필요에 따라 적절할 수 있습니다.
