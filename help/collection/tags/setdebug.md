---
title: setDebug()
description: 브라우저 콘솔을 통해 사이트에서 디버깅을 활성화합니다.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

`_satellite.setDebug()` 메서드를 사용하면 사이트에서 [디버깅](../use-cases/debugging.md)을 활성화하거나 비활성화할 수 있습니다. 이 메서드는 브라우저 콘솔에서 로컬로 실행하기 위한 것입니다. Adobe에서는 태그 규칙 내에서 이 메서드를 호출하지 않는 것이 좋습니다.

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**: [디버깅](../use-cases/debugging.md)을 사용하도록 설정합니다. 태그 라이브러리([`_satellite.logger`](logger.md) 포함)에서 생성된 메시지가 브라우저 콘솔에 표시됩니다.
* **`_satellite.setDebug(false);`**: 디버깅을 사용하지 않습니다. 태그 라이브러리에서 생성된 콘솔 메시지는 표시되지 않습니다.

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>JavaScript의 기본 `console.log()`(으)로 작성된 메시지는 DevTools가 열려 있는 모든 사용자에게 항상 표시됩니다. Adobe에서는 가능한 경우 [`_satellite.logger`](logger.md)을(를) 사용하는 것이 좋습니다.

## 디버그 모드 지속성

이 메서드를 호출할 때 디버그 모드에서는 다음 범위를 사용합니다.

* **브라우저 세션**: 디버그 모드가 페이지 로드 동안 지속됩니다. 브라우저 세션을 종료하거나 명시적으로 비활성화할 때까지 활성화된 상태로 유지됩니다.
* **원본 범위**: 디버그 모드는 동일한 사이트(도메인 + 포트 + 프로토콜)에서만 유지됩니다.
* **브라우저 프로필별**: 디버그 모드가 교차 프로필이 아닙니다.

다른 형식의 [디버깅](../use-cases/debugging.md)은(는) 브라우저 콘솔 메서드를 사용하여 디버그 모드에 영향을 주고 덮어쓸 수 있습니다.
