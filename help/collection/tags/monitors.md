---
title: 모니터(_M)
description: 이벤트 리스너를 추가하여 태그 구현을 디버깅하십시오.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# `_monitors`

`_satellite._monitors` 개체를 사용하면 라이브러리에서 트리거된 규칙을 검색할 때 이벤트 리스너를 만들고 사용자 지정 코드를 실행할 수 있습니다. 주요 용도는 규칙이 올바르게 트리거되도록 구현 디버깅을 지원하는 것입니다.

>[!IMPORTANT]
>
>이 개체는 디버깅 목적으로만 사용됩니다. 프로덕션 논리를 이 오브젝트에 연결하지 마십시오. Adobe은 언제든지 이 개체 내의 속성 또는 이름을 변경할 수 있습니다.

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

다음 이벤트 유형을 수신할 수 있습니다.

## `ruleTriggered`

이 콜백 함수는 규칙의 조건 및 작업이 처리되기 전에 이벤트가 규칙을 트리거할 때 실행됩니다. 이 함수가 트리거되면 `ruleCompleted` 또는 `ruleConditionFailed`이(가) 바로 이후에 트리거됩니다(함께 수행할 수 없음).

## `ruleCompleted`

`ruleCompleted` 콜백 함수는 규칙의 조건 기준이 성공하고 모든 규칙의 작업이 실행될 때 `ruleTriggered` 이후에 실행됩니다.

## `ruleConditionFailed`

규칙 조건 중 하나 이상이 실패하면 `ruleConditionFailed` 이후에 `ruleTriggered` 콜백 함수가 실행됩니다.

## `Rule` 개체

각 콜백 함수는 규칙 자체에 대한 정보를 제공하는 `Rule` 개체를 노출합니다.

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| 이름 | 유형 | 설명 |
|---|---|---|
| **`id`** | `string` | 규칙의 고유 식별자입니다. |
| **`name`** | `string` | 규칙에 대한 알기 쉬운 이름. |
| **`events`** | `Event[]` | 규칙을 트리거하도록 구성한 이벤트 배열입니다. |
| **`conditions`** | `Condition[]` | 규칙을 트리거하기 위해 구성한 조건 배열입니다. |
| **`actions`** | `Action[]` | 규칙이 트리거될 때 실행되도록 구성한 작업의 배열입니다. |

## 예

태그 라이브러리 로더를 호출하기 전에 `<head>` 태그의 HTML에 다음 코드 조각을 추가하십시오.

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

페이지의 이 지점에서 태그 라이브러리가 아직 로드되지 않았으므로 초기 `_satellite` 개체가 만들어지고 `_satellite._monitors`의 배열이 초기화됩니다. 그런 다음 스크립트가 해당 배열에 모니터 개체를 추가합니다.

모니터를 사용할 때는 다음 팁을 고려하십시오.

* 태그 라이브러리가 로드되기 전에 후크가 만들어지기 때문에 이러한 디버그 메시지는 `console.log` 대신 [`_satellite.logger`](logger.md)을(를) 사용합니다.
* 코드 예제는 세 개의 콜백 함수를 모두 포함하지만 필수 필드는 아닙니다. 사이트에서 규칙을 디버깅할 때 원하는 후크만 포함할 수 있습니다.
* 동일한 이벤트에 대해서도 여러 모니터가 허용됩니다. 단일 이벤트에 대해 여러 모니터를 사용하는 경우 호출 순서가 보장되지 않습니다.
* 태그 라이브러리를 로드하기 전에 `_monitors`을(를) _전에_&#x200B;만드십시오. 라이브러리가 로드된 후 이러한 후크를 만들면 해당 시점부터 트리거되는 규칙만 캡처됩니다.
