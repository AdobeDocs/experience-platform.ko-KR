---
title: Edge 확장의 라이브러리 모듈
description: Edge 속성에서 태그 확장에 대한 라이브러리 모듈 형식을 지정합니다.
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 68%

---

# Edge 확장의 라이브러리 모듈

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

>[!IMPORTANT]
>
>이 문서에서는 Edge 확장의 라이브러리 모듈 형식을 다룹니다. 웹 확장을 개발하는 경우 [웹 확장 모듈 형식 지정](../web/format.md)에 대한 안내서를 대신 참조하십시오.

라이브러리 모듈은 Adobe Experience Platform의 태그 런타임 라이브러리(Edge 노드에서 실행되는 라이브러리) 내에서 전달되는 확장에서 제공하는 재사용 가능한 코드의 일부입니다. 예를 들어, `sendBeacon` 작업 유형에는 Edge 노드에서 실행하고 비콘을 전송하는 라이브러리 모듈이 있습니다.

라이브러리 모듈은 [CommonJS 모듈](https://nodejs.org/api/modules.html#modules-commonjs-modules)로 구성됩니다. CommonJS 모듈 내에서 사용할 수 있는 변수는 다음과 같습니다.

## [!DNL require]

`require` 함수를 사용하여 확장 내의 모듈에 액세스할 수 있습니다. 확장의 모든 모듈은 상대 경로를 통해 액세스할 수 있습니다. 상대 경로는 `./` 또는 `../`로 시작해야 합니다 .

사용 예시:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

이름이 `module`인 자유 변수를 사용하여 모듈의 API를 내보낼 수 있습니다.

사용 예시:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

이름이 `exports`인 자유 변수를 사용하여 모듈의 API를 내보낼 수 있습니다.

사용 예시:

```js
exports.sayHello = (…) => { … }
```

이는 `module.exports`의 대안이지만, 사용이 보다 제한적입니다. `exports` 사용 시 `module.exports`와 `exports` 사이의 차이점 및 관련 주의 사항을 더 잘 이해하려면 [node.js의 module.exports 및 내보내기 이해하기](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)를 참조하십시오 . 확실하지 않은 경우에는 `exports`가 아닌 `module.exports`를 사용하면 보다 편리한 작업이 가능합니다.

## 서버측 모듈 서명

확장에서 제공하는 모든 모듈 유형(데이터 요소, 조건 또는 작업)은 동일한 매개 변수를 사용하여 호출됩니다. [context](./context.md).

```js
exports.sayHello = (context) => { … }
```
