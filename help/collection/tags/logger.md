---
title: logger
description: 디버깅할 때 브라우저 콘솔에 정보를 출력합니다.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# `logger`

`_satellite.logger` 개체에는 [디버깅](../use-cases/debugging.md)을 사용하도록 설정할 때 브라우저 콘솔에 진단 또는 정보 메시지를 출력할 수 있는 메서드가 있습니다. 디버깅이 활성화되어 있지 않으면 모든 `logger` 메서드 호출이 아무 작업도 수행하지 않습니다.

이러한 메서드를 사용하면 개발자, 기술 마케터 및 테스터가 태그 속성 내에 있는 트리거와 시기를 쉽게 확인할 수 있습니다. 이러한 콘솔 메시지는 디버깅이 활성화된 경우에만 표시되므로 사이트 방문자의 브라우저 콘솔에 영향을 주지 않고 프로덕션에 `logger`개의 메시지를 남길 수 있습니다.

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>태그 개체의 이전 버전은 `_satellite.notify()`을(를) 사용했습니다. `notify()` 함수는 `_satellite.logger`을(를) 위해 더 이상 사용되지 않습니다.

## 메서드에서 사용할 수 있습니다

디버깅이 활성화되면 모든 `_satellite.logger` 메서드가 해당 JavaScript `console.*` 메서드로 전달됩니다. 대부분의 `console` 인수 또는 개체는 `_satellite.logger`을(를) 사용하여 지원됩니다.

| 메서드 | 발송 대상 | 권장 사용 |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | 자세한 진단 유틸리티를 사용하십시오. 일부 브라우저에서는 자세한 정보를 기록해야 자세한 정보를 확인할 수 있습니다. |
| `_satellite.logger.log()` | `console.log()` | 일반 메시지. |
| `_satellite.logger.info()` | `console.info()` | 높은 수준의 정보 제공 이벤트. |
| `_satellite.logger.warn()` | `console.warn()` | 복구할 수 있는 문제 콘솔 항목은 노란색으로 강조 표시됩니다. |
| `_satellite.logger.error()` | `console.error()` | 실패. 콘솔 항목은 빨간색으로 강조 표시됩니다. Adobe에서는 스택에 `error` 개체를 사용하는 것이 좋습니다. |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## 콘솔 출력

라이브러리는 모든 콘솔 출력 메시지에 다음을 추가합니다.

* **🚀**: 태그 구현에서 비롯된 콘솔 메시지를 쉽게 검색할 수 있도록 지원합니다.
* **\[Origin\]**: 로그가 시작된 규칙, 작업, 확장 또는 데이터 요소 이름입니다. 구현 외부의 로거 메서드를 호출하는 경우(브라우저 콘솔을 통해) `[Custom Script]`이(가) 사용됩니다.
* **메시지 출력**: 메서드를 호출할 때 메시지 출력이 포함되었습니다.

>[!NOTE]
>
>로거가 `%c` 접두사를 적용하므로 `%s`, `%d` 및 `🚀 [Origin]`과(와) 같은 브라우저 서식 토큰이 적용되지 않습니다.
