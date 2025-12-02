---
title: getVar()
description: setVar()를 사용하여 데이터 요소 값 또는 값 집합을 반환합니다.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# `getVar()`

`_satellite.getVar()` 메서드가 [Data 요소](/help/tags/ui/managing-resources/data-elements.md)의 현재 값 또는 [`_satellite.setVar()`](setvar.md)을(를) 사용하여 설정된 값을 반환합니다. 데이터 요소와 `setVar()` 값이 같은 이름을 공유하는 경우 데이터 요소가 우선합니다. 아직 존재하지 않는 문자열 식별자를 호출하는 경우 메서드는 `undefined`을(를) 반환합니다. 평가는 동기식입니다.

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

반환 값과 유형은 참조하는 데이터 요소 유형에 따라 다릅니다. 예를 들어 문자열 변수를 검색하는 `getVar()`을(를) 호출하는 경우 반환된 형식은 `string`입니다. 웹 SDK 변수 데이터 요소를 반환하는 `getVar()`을(를) 호출하는 경우 반환된 형식은 해당 변수에 설정된 모든 속성을 포함하는 `object`입니다.

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## 사용 가능한 필드

`getVar()` 메서드는 두 개의 인수를 지원합니다. 대부분의 사용 사례에서는 두 번째 선택적 인수를 포함하지 않습니다.

| 이름 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| **`name`** | `string` | 예 | 검색할 데이터 요소 이름입니다. 데이터 요소 이름은 대소문자를 구분합니다. |
| **`event`** | `object` | 아니요 | 트리거 규칙의 이벤트 컨텍스트. [사용자 지정 코드](/help/tags/ui/managing-resources/data-elements.md#custom-code) 또는 사용자 지정 확장을 사용하는 데이터 요소의 고급 사용 사례에서만 사용됩니다. 규칙이 이벤트(예: 클릭, 양식 제출 또는 사용자 지정 JavaScript 발송)에 의해 트리거되면 관련 이벤트 개체가 여기에 포함됩니다. 데이터 요소는 이 정보를 사용하여 클릭한 요소의 세부 사항이나 사용자 지정 이벤트의 속성과 같은 컨텍스트 값을 반환할 수 있습니다. |
