---
title: setVar()
description: getVar()를 사용하여 나중에 검색할 수 있는 값을 설정합니다.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# `setVar()`

`_satellite.setVar()` 메서드를 사용하면 나중에 [`_satellite.getVar()`](getvar.md)에서 참조할 수 있는 하나 이상의 사용자 지정 이름/값 쌍을 설정할 수 있습니다.

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>`getVar()` 메서드가 데이터 요소와 `setVar()`에서 설정한 값을 모두 검색할 수 있지만 이 두 엔터티 형식은 별개입니다. `setVar()`을(를) 사용하여 태그 UI에서 데이터 요소와 이름이 같은 값을 설정하면 덮어쓰지 않습니다.

## 지속성 및 범위

`setVar()`개의 값이 페이지 메모리에만 있습니다.

* **현재 페이지만**: 페이지가 언로드될 때까지 값이 유지됩니다. 단일 페이지 애플리케이션에서는 완전히 다시 로드하거나 덮어쓰기/지울 때까지 지속됩니다.
* **브라우저 저장소 없음**: 쿠키, 로컬 저장소 또는 세션 저장소에 아무 것도 기록되지 않습니다.

## `setVar()`을(를) 사용하여 설정된 값 참조

`getVar()`을(를) 사용하여 사용자 지정 코드에서 값을 검색할 수 있습니다.

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

데이터 요소 표기법을 지원하는 필드의 태그 UI에서 다음 변수를 참조할 수도 있습니다.

```text
%Ad location%
```

>[!NOTE]
>
>`setVar()`을(를) 사용하여 설정된 값이 데이터 요소와 동일한 이름을 사용하고 데이터 요소 표기법으로 해당 이름을 참조하는 경우 데이터 요소가 우선합니다.

## 예

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```
