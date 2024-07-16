---
title: set디버그
description: 웹 SDK 디버그 설정을 활성화하거나 비활성화합니다.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

`setDebug` 명령을 사용하면 Web SDK에서 디버깅 모드를 시작하거나 종료할 수 있습니다. [디버깅](../use-cases/debugging.md)에 사용할 수 있는 여러 옵션 중 하나입니다. Adobe은 개발 환경 내에서 또는 프로덕션 환경 내의 로컬 시스템에서 디버그 모드를 활성화하는 것을 권장합니다.

## 웹 SDK 태그 확장을 사용하여 디버그 설정

태그 확장은 UI 내에서 디버그 옵션을 전환하는 기능을 제공하지 않습니다. JavaScript 구문을 사용하여 사용자 지정 코드 편집기를 사용하거나, 사이트에 있는 동안 브라우저 콘솔 내에 JavaScript 코드를 입력할 수 있습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 디버그 설정

웹 SDK의 구성된 인스턴스를 호출할 때 `setDebug` 명령을 실행합니다. 구성 개체에 있는 유일한 옵션은 디버그 모드가 사용되는지 여부를 결정하는 부울인 `enabled`입니다.

```js
alloy("setDebug", {"enabled": true});
```
