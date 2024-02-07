---
title: 비동기 배포
description: 웹 사이트에 Adobe Experience Platform 태그 라이브러리를 비동기적으로 배포하는 방법을 알아봅니다.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 59%

---

# 비동기 배포 {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="비동기 배포"
>abstract="이 옵션이 활성화되어 브라우저가 이 스크립트 태그를 구문 분석하면 JavaScript 파일 로드를 시작하지만, 라이브러리가 로드되고 실행될 때까지 기다리지 않고 나머지 문서를 계속 구문 분석하고 렌더링해야 한다는 것을 나타냅니다. 이로써 웹 페이지 성능을 높일 수 있지만 특정 규칙이 실행되는 방식에 중요한 영향을 미칠 수 있습니다. 자세한 내용은 이 문서를 참조하십시오."

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

제품에 필요한 JavaScript 라이브러리의 성능과 비차단 배포는 Adobe Experience Cloud 사용자에게 점점 더 중요해지고 있습니다. 다음과 같은 도구 [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) 는 사용자가 사이트에서 Adobe 라이브러리를 배포하는 방식을 변경할 것을 권장합니다. 이 문서에서는 비동기 방식으로 Adobe JavaScript 라이브러리를 사용하는 방법을 설명합니다.

## 동기와 비동기

### 동기식 배포

종종 라이브러리는 페이지의 `<head>` 태그에서 동기적으로 로드됩니다. 예:

```markup
<script src="example.js"></script>
```

기본적으로 브라우저는 문서를 구문 분석하여 이 라인에 도달한 다음 서버에서 JavaScript 파일을 가져오기 시작합니다. 브라우저는 파일이 반환될 때까지 기다렸다가 JavaScript 파일을 구문 분석하고 실행합니다. 마지막으로 HTML 문서의 나머지 부분을 계속 구문 분석합니다.

파서가 표시된 콘텐츠를 렌더링하기 전에 `<script>` 태그가 나타나면 콘텐츠 표시가 지연됩니다. 로드되는 JavaScript 파일이 사용자에게 콘텐츠를 표시하는 데 반드시 필요하지 않으면 방문자가 콘텐츠를 기다리도록 요구하지 않아도 됩니다. 라이브러리가 클수록 지연 시간이 길어집니다. 이러한 이유로, [!DNL Google PageSpeed] 또는 [!DNL Lighthouse]와 같은 웹 사이트 성능 벤치마크 도구는 동기적으로 로드된 스크립트에 종종 플래그를 지정합니다.

관리할 태그가 많을 경우 태그 관리 라이브러리는 빠르게 늘어날 수 있습니다.

### 비동기 배포

를 추가하여 모든 라이브러리를 비동기식으로 로드할 수 있습니다. `async` 속성 `<script>` 태그에 가깝게 배치하십시오. 예:

```markup
<script src="example.js" async></script>
```

이는 브라우저가 이 스크립트 태그를 구문 분석하면 JavaScript 파일 로드를 시작해야 하지만, 라이브러리가 로드되고 실행될 때까지 기다리지 않고 나머지 문서를 계속 구문 분석하고 렌더링해야 한다는 것을 나타냅니다.

## 비동기 배포에 대한 고려 사항

위에서 설명한 바와 같이, 동기 배포의 경우, 브라우저는 Adobe Experience Platform 태그 라이브러리가 로드되고 실행되는 동안 페이지 구문 분석 및 렌더링을 일시 중지합니다. 반면 비동기 배포에서는 라이브러리가 로드되는 동안 브라우저가 계속해서 페이지를 구문 분석하고 렌더링합니다. 페이지 구문 분석 및 렌더링과 관련하여 태그 라이브러리 로드가 완료될 수 있는 경우의 가변성을 고려해야 합니다.

먼저, 태그 라이브러리는 페이지 하단이 구문 분석되고 실행되기 전이나 후에 로드를 완료할 수 있으므로 더 이상 을 호출해서는 안 됩니다. `_satellite.pageBottom()` 페이지 코드(`_satellite` 는 라이브러리가 로드될 때까지 사용할 수 없습니다. 이에 대해서는 다음에서 설명합니다. [비동기적으로 태그 포함 코드 로드](#loading-the-tags-embed-code-asynchronously).

둘째, 태그 라이브러리는 다음 이전 또는 이후에 로드를 완료할 수 있습니다. [`DOMContentLoaded`](https://developer.mozilla.org/ko-KR/docs/Web/Events/DOMContentLoaded) 브라우저 이벤트(DOM 준비)가 발생했습니다.

이 두 가지 사항 때문에 [라이브러리가 로드됨](../../extensions/client/core/overview.md#library-loaded-page-top), [페이지 하단](../../extensions/client/core/overview.md#page-bottom), [DOM 지원](../../extensions/client/core/overview.md#page-bottom), 및 [Window Loaded](../../extensions/client/core/overview.md#window-loaded) 태그 라이브러리를 비동기적으로 로드할 때 코어 확장의 이벤트 유형입니다.

태그 속성에 다음 네 가지 규칙이 포함되어 있는 경우

* 규칙 A: Library Loaded 이벤트 유형 사용
* 규칙 B: Page Bottom 이벤트 유형 사용
* 규칙 C: DOM Ready 이벤트 유형 사용
* 규칙 D: Window Loaded 이벤트 유형 사용

태그 라이브러리 로드가 언제 완료되었는지에 관계없이 모든 규칙은 항상 다음 순서로 실행됩니다.

규칙 A → 규칙 B → 규칙 C → 규칙 D

이 순서가 항상 적용되지만, 일부 규칙은 태그 라이브러리 로드가 완료되면 즉시 실행될 수도 있고, 다른 규칙은 나중에 실행될 수도 있습니다. 태그 라이브러리 로드가 완료되면 다음 작업이 수행됩니다.

1. 규칙 A가 즉시 실행됩니다.
1. `DOMContentLoaded` 브라우저 이벤트(DOM Ready)가 이미 발생한 경우 규칙 B와 규칙 C가 즉시 실행됩니다. 그렇지 않으면 나중에 [`DOMContentLoaded`](https://developer.mozilla.org/ko-KR/docs/Web/Events/DOMContentLoaded) 브라우저 이벤트가 발생할 때 규칙 B와 규칙 C가 실행됩니다.
1. [`load`](https://developer.mozilla.org/ko-KR/docs/Web/Events/load) 브라우저 이벤트(Window Loaded)가 이미 발생한 경우 규칙 D가 바로 실행됩니다. 그렇지 않은 경우에는 나중에 [`load`](https://developer.mozilla.org/ko-KR/docs/Web/Events/load) 브라우저 이벤트가 발생할 때 규칙 D가 실행됩니다. 지침에 따라 태그 라이브러리를 설치한 경우에는 태그 라이브러리를 참고하십시오 *항상* 다음 작업 전 로드 완료 [`load`](https://developer.mozilla.org/ko-KR/docs/Web/Events/load) 브라우저 이벤트가 발생합니다.

이러한 원칙을 자신의 웹 사이트에 적용할 때 다음 사항을 고려하십시오.

* **Library Loaded 이벤트 유형을 사용하는 규칙은 데이터 계층이 완전히 로드되기 전에 실행될 수 있습니다.**&#x200B;이로 인해 페이지에서 아직 데이터를 사용할 수 없으므로 누락된 데이터로 규칙 작업이 실행될 수 있습니다. 이러한 유형의 문제는 규칙 구성을 수정하여 완화할 수 있습니다. 예를 들어 Library Loaded 이벤트 유형으로 트리거되는 규칙 대신, 데이터 계층이 로드를 완료하는 즉시 페이지 코드에 의해 트리거되는 Custom Event 또는 Direct Call 이벤트 유형을 사용할 수 있습니다.
* **Page Bottom 이벤트 유형은 특히 라이브러리가 비동기적으로 로드될 때 값을 제공하지 않습니다.**&#x200B;대신 로드된 Library Loaded, DOM Ready, Window Loaded 또는 기타 이벤트 유형을 고려하십시오.

순서가 맞지 않는 상황이 발생하는 경우 해결해야 하는 몇 가지 시간 문제가 있을 수 있습니다. 정확한 타이밍을 요구하는 배포에 이벤트 리스너와 Custom Event 또는 Direct Call 이벤트 유형을 사용해야 구현을 보다 강력하고 일관되게 만들 수 있습니다.

## 비동기적으로 태그 포함 코드 로드

태그는 를 구성할 때 포함 코드를 만들 때 비동기 로드를 켜는 토글 기능을 제공합니다. [환경](../publishing/environments.md). 비동기 로드를 직접 구성할 수도 있습니다.

1. 비동기 속성을 `<script>` 태그에 추가하여 스크립트를 비동기적으로 로드합니다.

   태그 포함 코드의 경우 다음 스크립트를

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   아래와 같이 변경하는 것을 의미합니다.

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. 이전에 태그 하단에 추가했을 수 있는 코드를 제거합니다.

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   이 코드는 브라우저 파서가 페이지 하단에 도달했음을 Platform에 알려줍니다. 이 시간 전에 태그가 로드 및 실행되지 않을 수 있으므로 를 호출하십시오. `_satellite.pageBottom()` 이로 인해 오류가 발생하고 Page Bottom 이벤트 유형이 예상대로 작동하지 않을 수 있습니다.
