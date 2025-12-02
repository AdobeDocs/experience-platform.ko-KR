---
title: track()
description: 직접 호출 규칙을 트리거합니다.
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# `track()`

`_satellite.track()` 메서드를 사용하면 [직접 호출 규칙](/help/tags/extensions/client/core/overview.md#direct-call-event)을 트리거할 수 있습니다.

>[!IMPORTANT]
>
>Adobe은 `_satellite.track()`을(를) **레거시 구현 메서드**&#x200B;로 간주합니다. 여전히 완전히 지원되지만, Adobe에서는 새 구현에 권장되는 접근 방식인 [Adobe 클라이언트 데이터 레이어](/help/tags/extensions/client/client-data-layer/overview.md)와 같은 최신 구현 방법을 사용할 것을 강력히 권장합니다.
>
>사이트에서 `_satellite.track()`을(를) 사용하도록 선택한 경우 **모든 호출을 보호**&#x200B;하여 사이트가 태그 라이브러리에 단단히 연결되지 않도록 합니다. 보호되지 않는 경우 나중에 태그 속성을 제거하면 `_satellite` 개체에 대한 모든 참조에서 오류가 발생합니다.

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

태그 UI에 구성된 식별자를 사용하여 `_satellite.track()`을(를) 호출하면 해당 규칙이 즉시 트리거됩니다. 이 메서드를 호출하면 규칙 이벤트로만 작동합니다. 규칙의 조건은 규칙 작업을 실행하기 전에 계속 적용됩니다. 여러 직접 호출 규칙이 동일한 식별자를 사용할 수 있으므로 단일 `_satellite.track()` 호출을 사용하여 이러한 모든 규칙을 한 번에 트리거할 수 있습니다. 트리거된 각 규칙은 여러 규칙이 동일한 식별자를 공유하더라도 작업을 수행하기 전에 자체 조건을 확인합니다.

## 사용 가능한 필드

`_satellite.track()` 메서드는 두 개의 인수를 지원합니다.

| 이름 | 유형 | 필수 여부 | 설명 |
|---|---|---|---|
| **`identifier`** | `string` | 예 | 직접 호출 규칙 식별자. 태그 UI에서 규칙을 구성할 때 이 식별자를 설정합니다. |
| **`detail`** | `unknown` | 아니요 | 원하는 정보가 포함된 선택적 페이로드입니다. 규칙을 구성할 때 `event.detail`(사용자 지정 코드) 또는 `%event.detail%`(데이터 요소 표기법을 지원하는 텍스트 필드)을 사용하여 페이로드에 액세스할 수 있습니다. |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
