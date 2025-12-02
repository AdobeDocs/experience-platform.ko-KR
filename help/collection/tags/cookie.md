---
title: 쿠키
description: 태그 속성에 대한 쿠키를 수동으로 작성, 편집 또는 삭제합니다.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---

# `cookie`

`_satellite.cookie` 개체에는 태그 규칙에서 참조할 수 있는 쿠키를 작성, 편집 또는 삭제할 수 있는 메서드가 포함되어 있습니다. 해당 라이브러리의 많은 핵심 기능을 포함하는 [`js-cookie`](https://github.com/js-cookie/js-cookie)의 부분 복사본입니다.

## `cookie.set()`

`set()` 메서드는 태그 속성이 참조할 수 있는 쿠키를 기록합니다.

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

다음 메서드 매개 변수를 사용할 수 있습니다.

| 이름 | 유형 | 필수 여부 | 설명 |
|---|---|---|---|
| **`name`** | `string` | 예 | 쿠키의 이름입니다. |
| **`value`** | `string` | 예 | 쿠키의 값 |
| **`attributes`** | `object` | 아니요 | 쿠키에 포함할 추가 속성입니다. |

`attributes` 개체는 다음 속성을 지원합니다.

| 속성 이름 | 유형 | 필수 여부 | 기본 | 설명 |
|---|---|---|---|---|
| **`expires`** | `number` 또는 [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | 아니요 | 브라우저 세션이 끝날 때 쿠키가 만료됨 | 쿠키가 만료될 일 수입니다. |
| **`path`** | `string` | 아니요 | 사이트 전체에 표시되는 쿠키 | 도메인에서 쿠키가 표시되는 위치입니다. |
| **`domain`** | `string` | 아니요 | 아래에 생성된 도메인에 표시되는 쿠키 | 쿠키가 표시되는 유효한 도메인(하위 도메인 포함 또는 제외). 도메인이 하위 도메인 없이 포함된 경우 해당 도메인 아래의 모든 하위 도메인에 쿠키가 표시됩니다. |
| **`secure`** | `boolean` | 아니요 | 속성 설정 없음 | 쿠키에 보안 프로토콜(`https://`)이 필요한지 여부를 결정합니다. 생략하면 보안 프로토콜 요구 사항이 없습니다. |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | 아니요 | 속성 설정 없음 | 쿠키의 [`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) 특성을 설정할 수 있습니다. `sameSite`을(를) `None`(으)로 설정하는 경우 `secure`도 `true`(으)로 설정해야 합니다. |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

이 메서드를 호출하면 원하는 쿠키가 작성되고 작성된 직렬화된 쿠키 문자열이 반환됩니다. 이 문자열은 주로 디버깅 또는 로깅 용도로 사용됩니다.

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>태그 개체의 이전 버전은 `_satellite.setCookie()`을(를) 사용했습니다. `setCookie()` 메서드는 `_satellite.cookie.set()`을(를) 위해 사용되지 않습니다.

## `cookie.get()`

`get()` 메서드가 쿠키 값을 반환합니다.

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| 이름 | 유형 | 필수 여부 | 설명 |
|---|---|---|---|
| **`name`** | `string` | 예 | 값을 검색할 쿠키 이름(대/소문자 구분). |

쿠키 이름이 있으면 는 쿠키 값을 반환합니다. 쿠키 이름이 없으면 `undefined`을(를) 반환합니다.

>[!TIP]
>
>태그 개체의 이전 버전은 `_satellite.getCookie()`을(를) 사용했습니다. `getCookie()` 메서드는 `_satellite.cookie.get()`을(를) 위해 사용되지 않습니다.

## `cookie.remove()`

`remove()` 메서드는 사용자가 설정한 쿠키를 삭제합니다.

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| 이름 | 유형 | 필수 여부 | 설명 |
|---|---|---|---|
| **`name`** | `string` | 예 | 제거할 쿠키 이름입니다. |
| **`attributes`** | `object` | 아니요 | 제거할 쿠키와 연관된 속성입니다. `path` 또는 `domain` 특성을 사용하여 쿠키를 설정하는 경우 쿠키를 제거할 때 동일한 특성을 포함하십시오. 이러한 속성을 포함하지 않으면 쿠키가 제거되지 않습니다. |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>태그 개체의 이전 버전은 `_satellite.removeCookie()`을(를) 사용했습니다. `removeCookie()` 메서드는 `_satellite.cookie.remove()`을(를) 위해 사용되지 않습니다.
