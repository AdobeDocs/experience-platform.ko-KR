---
title: NPM 패키지를 사용하여 Web SDK 설치
description: NPM 패키지를 사용하여 Web SDK 라이브러리를 설치하고 참조합니다.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# NPM 패키지를 사용하여 Web SDK 설치

Adobe Experience Platform Web SDK는 [NPM 패키지](https://www.npmjs.com). NPM 패키지를 설치하면 Adobe Experience Platform Web SDK JavaScript 라이브러리에 대한 빌드 프로세스를 제어할 수 있습니다. NPM 패키지는 브라우저에서 실행되도록 지정된 EcmaScript 버전 5 모듈 또는 EcmaScript 버전 2015(ES6) 모듈을 노출합니다.

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK의 NPM 패키지는 `createInstance` 함수. 함수에 전달되는 이름 옵션은 로깅에 사용되는 접두사를 제어합니다. 다음은 패키지 사용의 예입니다.

## 패키지를 ECMAScript 2015(ES6) 모듈로 사용

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM 패키지는 CommonJS 모듈을 사용합니다. 따라서 번들러를 사용할 때는 번들러가 CommonJS 모듈을 지원하는지 확인하십시오. 다음과 같은 일부 번들러 [롤업](https://rollupjs.org), 필수 [플러그인](https://www.npmjs.com/package/@rollup/plugin-commonjs) CommonJS 지원을 제공합니다.

## 패키지를 ECMAScript 5 모듈로 사용

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
