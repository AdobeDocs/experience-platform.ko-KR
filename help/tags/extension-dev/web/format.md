---
title: 웹 확장의 라이브러리 모듈
description: Adobe Experience Platform에서 웹 확장용 라이브러리 모듈의 형식을 지정하는 방법을 알아봅니다.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 64%

---

# 웹 확장의 라이브러리 모듈

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../term-updates.md)을 참조하십시오.

>[!IMPORTANT]
>
>이 문서에서는 웹 확장에 대한 라이브러리 모듈 형식을 다룹니다. Edge 확장을 개발하는 경우 대신 [Edge 확장 모듈 형식 지정](../edge/format.md)에 대한 안내서를 참조하십시오.

라이브러리 모듈은 확장이 제공하는 재사용 가능한 코드의 일부이며, Adobe Experience Platform의 태그 런타임 라이브러리 내에 전달됩니다. 그런 다음 이 라이브러리는 클라이언트의 웹 사이트에서 실행됩니다. 예를 들어, `gesture` 이벤트 유형에는 클라이언트의 웹 사이트에서 실행되고 사용자 제스처를 감지하는 라이브러리 모듈이 있습니다.

라이브러리 모듈은 [CommonJS 모듈](http://wiki.commonjs.org/wiki/Modules/1.1.1)로 구성됩니다. CommonJS 모듈 내에서 사용할 수 있는 변수는 다음과 같습니다.

## [!DNL require]

액세스하기 위해서는 `require` 함수를 사용할 수 있습니다.

1. 태그로 제공되는 핵심 모듈입니다. 이러한 모듈은 `require('@adobe/reactor-name-of-module')`를 사용하여 액세스할 수 있습니다 . 자세한 내용은 사용 가능한 [핵심 모듈](./core.md)에 대한 문서를 참조하십시오.
1. 확장 내의 다른 모듈입니다. 확장의 모든 모듈은 상대 경로를 통해 액세스할 수 있습니다. 상대 경로는 `./` 또는 `../`로 시작해야 합니다 .

사용 예시:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## [!DNL module]

이름이 `module`인 자유 변수를 사용하여 모듈의 API를 내보낼 수 있습니다.

사용 예시:

```javascript
module.exports = function(…) { … }
```

## [!DNL exports]

이름이 `exports`인 자유 변수를 사용하여 모듈의 API를 내보낼 수 있습니다.

사용 예시:

```javascript
exports.sayHello = function(…) { … }
```

이는 `module.exports`의 대안이지만, 사용이 보다 제한적입니다. `exports` 사용 시 `module.exports`와 `exports` 사이의 차이점 및 관련 주의 사항을 더 잘 이해하려면 [node.js의 module.exports 및 내보내기 이해하기](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)를 참조하십시오 . 확실하지 않은 경우에는 `exports`가 아닌 `module.exports`를 사용하면 보다 편리한 작업이 가능합니다.

## 실행 및 캐싱

태그 런타임 라이브러리가 실행되면 모듈이 즉시 &quot;설치&quot;되고 해당 모듈은 캐시됩니다. 다음 모듈의 경우:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` 은 즉시 기록되지만,  `runs when necessary` 는 내보낸 함수를 태그 엔진에서 호출한 이후에만 기록됩니다. 특정 모듈의 용도는 필요하지 않지만, 함수를 내보내기 전에 필요한 설정을 수행하여 이 기능을 활용할 수 있습니다.
