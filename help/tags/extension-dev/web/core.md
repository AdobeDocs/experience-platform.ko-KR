---
title: 웹 확장을 위한 핵심 라이브러리 모듈
description: 웹 확장 내에서 사용할 수 있는 핵심 라이브러리 모듈에 대해 알아봅니다.
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 82%

---

# 웹 확장을 위한 핵심 라이브러리 모듈

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

이 문서에서는 웹 확장 내에서 사용할 수 있는 핵심 라이브러리 모듈 목록을 제공합니다. `require('@adobe/{MODULE}')`를 사용하여 이러한 모듈에 액세스할 수 있습니다. 여기서 `{MODULE}`은 핵심 모듈의 이름입니다.

## [!DNL reactor-object-assign]

`reactor-object-assign`은 소스 객체의 속성을 대상 객체로 복사하여 기본 [`Object.assign`](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 메서드를 모방합니다.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

`reactor-cookie` 객체는 쿠키를 읽고 쓰는 유틸리티입니다. 자세한 내용은 [js-cookie npm 패키지](https://www.npmjs.com/package/js-cookie)를 참조하십시오.

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document`는 [`Document`](https://developer.mozilla.org/ko-KR/docs/Web/API/Document) 객체를 나타냅니다. 이러한 기능은 [`inject-loader`](https://www.npmjs.com/package/inject-loader) 등의 유틸리티를 사용하여 테스트 시 샘플 `document` 객체를 주입할 수 있으므로 모듈을 테스트할 때 유용할 수 있습니다 .

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string`은 [쿼리 문자열](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search)의 구문 분석 및 직렬화를 위한 유틸리티입니다.

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

이 유틸리티에는 다음과 같은 메서드가 있습니다.

* `queryString.parse({STRING})`: 쿼리 문자열을 객체로 구문 분석합니다. 쿼리 문자열에서 선행 `?`, `#` 및 `&` 문자는 무시됩니다.
* `queryString.stringify({OBJECT})`: 객체를 쿼리 문자열로 문자열 변환합니다.

### [!DNL reactor-load-script]

`reactor-load-script`는 URL이 지정된 경우 스크립트를 로드하는 함수입니다. 스크립트 태그가 생성되고 문서의 `head` 노드 내에 배치됩니다. 스크립트 로드 또는 성공 시점을 판단하기 위해 사용할 수 있는 [약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise)이 반환됩니다.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise`는 ECMAScript 6에서 [Promise API](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) 네이티브를 모방하는 생성자입니다. 네이티브 Promise API를 사용할 수 있으면, 대신 해당 API가 반환됩니다.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window`는 [`Window`](https://developer.mozilla.org/ko-KR/docs/Web/API/Window) 객체를 나타냅니다. 이러한 기능은 [`inject-loader`](https://www.npmjs.com/package/inject-loader) 등의 유틸리티를 사용하여 테스트 시 샘플 `Window` 객체를 주입할 수 있으므로 모듈을 테스트할 때 유용할 수 있습니다 .

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
