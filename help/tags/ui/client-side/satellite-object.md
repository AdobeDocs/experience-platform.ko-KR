---
title: 위성 개체 참조
description: 클라이언트측 _satellite 개체 및 태그를 사용하여 수행할 수 있는 다양한 기능에 대해 알아봅니다.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 42%

---

# 위성 개체 참조

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

이 문서는 클라이언트측의 참조 역할을 합니다 `_satellite` 개체 및 이 개체를 사용하여 수행할 수 있는 다양한 함수를 참조하십시오.

## `track`

**코드**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**예**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` 는 코어 태그 확장의 지정된 식별자로 구성된 직접 호출 이벤트 유형을 사용하여 모든 규칙을 실행합니다. 위의 예에서는 구성된 식별자가 `contact_submit`인 Direct Call 이벤트 유형을 사용하여 모든 규칙을 트리거합니다. 관련 정보가 들어 있는 선택적 개체도 전달됩니다. 세부 개체는 조건 또는 작업의 텍스트 필드 내에 `%event.detail%`을 입력하거나, 사용자 지정 코드 조건 또는 작업에서 코드 편집기 내에 `event.detail`을 입력하여 액세스할 수 있습니다.

## `getVar`

**코드**

```javascript
_satellite.getVar(name: string) => *
```

**예**

```javascript
var product = _satellite.getVar('product');
```

제공된 예에서 이름이 일치하는 데이터 요소가 있으면 데이터 요소의 값이 반환됩니다. 일치하는 데이터 요소가 없으면 `_satellite.setVar()`를 사용하여 이름이 일치하는 사용자 지정 변수를 이전에 설정했는지 확인합니다. 일치하는 사용자 지정 변수가 있으면 해당 값이 반환됩니다.

>[!NOTE]
>
>백분율(`%`) 구문을 통해 태그 구현에서 많은 양식 필드에 대한 변수를 참조할 수 있으므로 호출의 필요성을 줄일 수 있습니다 `_satellite.getVar()`. 예를 들어 `%product%` 은 제품 데이터 요소 또는 사용자 지정 변수의 값에 액세스합니다.

이벤트가 규칙을 트리거할 때 규칙의 해당 규칙을 전달할 수 있습니다 `event` 개체 `_satellite.getVar()` 다음과 같습니다.

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

**코드**

```javascript
_satellite.setVar(name: string, value: *)
```

**예**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` 지정된 이름과 값으로 사용자 지정 변수를 설정합니다. 변수 값은 나중에 `_satellite.getVar()`를 사용하여 액세스할 수 있습니다.

키가 변수 이름이고 값이 해당 변수 값인 개체를 전달하여 한 번에 여러 변수를 선택적으로 설정할 수 있습니다.

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**코드**

```javascript
_satellite.getVisitorId() => Object
```

**예**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

[!DNL Adobe Experience Cloud ID] 확장이 속성에 설치된 경우 이 메서드는 방문자 ID 인스턴스를 반환합니다. 자세한 내용은 [Experience Cloud ID 서비스 설명서](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ko-KR)를 참조하십시오.

## `logger`

**코드**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**예**

```javascript
_satellite.logger.error('No product ID found.');
```

다음 `logger` 개체를 사용하면 브라우저 콘솔에 메시지를 기록할 수 있습니다. 이 메시지는 사용자가 태그 디버깅을 활성화한 경우( `_satellite.setDebug(true)` 또는 적절한 브라우저 확장 사용)을 참조하십시오.

### 사용 중단 경고 로깅

```javascript
_satellite.logger.deprecation(message: string)
```

**예**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

이렇게 하면 브라우저 콘솔에 경고가 기록됩니다. 사용자가 태그 디버깅을 활성화하는지 여부를 나타내는 메시지가 표시됩니다.

## `cookie` {#cookie}

`_satellite.cookie` 는 쿠키를 읽고 쓰는 함수를 포함합니다. 타사 라이브러리 js-쿠키의 노출된 사본입니다. 이 라이브러리의 고급 사용에 대한 자세한 내용은 [js 쿠키 설명서](https://www.npmjs.com/package/js-cookie#basic-usage).

### 쿠키 설정 {#cookie-set}

쿠키를 설정하려면 `_satellite.cookie.set()`.

**코드**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>오래된 [`setCookie`](#setCookie) 쿠키를 설정하는 메서드에서 이 함수 호출에 대한 세 번째(선택 사항) 인수는 쿠키의 TTL(time-to-live)을 나타내는 정수입니다. 이 새 메서드에서는 &quot;attributes&quot; 개체가 대신 세 번째 인수로 수락됩니다. 새 메서드를 사용하여 쿠키에 대한 TTL을 설정하려면 다음을 제공해야 합니다 `expires` 속성 개체의 속성을 원하는 값으로 설정합니다. 이것은 아래 예제에 나와 있습니다.

**예**

다음 함수 호출은 1주 후에 만료되는 쿠키를 기록합니다.

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### 쿠키 검색 {#cookie-get}

쿠키를 검색하려면 `_satellite.cookie.get()`.

**코드**

```javascript
_satellite.cookie.get(name: string) => string
```

**예**

다음 함수 호출은 이전에 설정된 쿠키를 읽습니다.

```javascript
var product = _satellite.cookie.get('product');
```

### 쿠키 제거 {#cookie-remove}

쿠키를 제거하려면 `_satellite.cookie.remove()`.

**코드**

```javascript
_satellite.cookie.remove(name: string)
```

**예**

다음 함수 호출은 이전에 설정한 쿠키를 제거합니다.

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**코드**

```javascript
_satellite.buildInfo
```

이 개체에는 현재 태그 런타임 라이브러리 빌드에 대한 정보가 들어 있습니다. 개체에는 다음 속성이 포함되어 있습니다.

### `turbineVersion`

이렇게 하면 [터빈](https://www.npmjs.com/package/@adobe/reactor-turbine) 현재 라이브러리 내에서 사용되는 버전입니다.

### `turbineBuildDate`

컨테이너 내에 사용된 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 버전이 빌드된 ISO 8601 날짜입니다.

### `buildDate`

현재 라이브러리가 빌드된 ISO 8601 날짜입니다.

다음 예에서는 개체 값을 보여 줍니다.

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

이 개체에는 현재 태그 런타임 라이브러리가 배포되는 환경에 대한 정보가 들어 있습니다.

**코드**

```javascript
_satellite.environment
```

개체에는 다음 속성이 포함되어 있습니다.

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 환경의 ID입니다. |
| `stage` | 이 라이브러리가 빌드된 환경입니다. 가능한 값은 다음과 같습니다 `development`, `staging`, 및 `production`. |

## `notify`

>[!NOTE]
>
>이 메서드는 더 이상 사용되지 않습니다. 대신 `_satellite.logger.log()`를 사용하십시오.

**코드**

```javascript
_satellite.notify(message: string[, level: number])
```

**예**

```javascript
_satellite.notify('Hello world!');
```

`notify` 브라우저 콘솔에 메시지를 기록합니다. 이 메시지는 사용자가 태그 디버깅을 활성화한 경우( `_satellite.setDebug(true)` 또는 적절한 브라우저 확장 사용)을 참조하십시오.

기록되는 메시지의 스타일링 및 필터링에 영향을 주는 선택적 로깅 수준을 전달할 수 있습니다. 지원되는 수준은 다음과 같습니다.

3 - 정보 메시지.

4 - 경고 메시지.

5 - 오류 메시지.

로깅 수준을 제공하지 않거나 다른 수준 값을 전달하지 않으면 메시지가 일반 메시지로 기록됩니다.

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>이 메서드는 더 이상 사용되지 않습니다. 대신 [`_satellite.cookie.set()`](#cookie-set)를 사용하십시오.

**코드**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**예**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

사용자의 브라우저에서 쿠키를 설정합니다. 쿠키는 지정된 일 수 동안 지속됩니다.

## `readCookie`

>[!IMPORTANT]
>
>이 메서드는 더 이상 사용되지 않습니다. 대신 [`_satellite.cookie.get()`](#cookie-get)를 사용하십시오.

**코드**

```javascript
_satellite.readCookie(name: string) => string
```

**예**

```javascript
var product = _satellite.readCookie('product');
```

사용자의 브라우저에서 쿠키를 읽습니다.

## `removeCookie`

>[!NOTE]
>
>이 메서드는 더 이상 사용되지 않습니다. 대신 [`_satellite.cookie.remove()`](#cookie-remove)를 사용하십시오.

**코드**

```javascript
_satellite.removeCookie(name: string)
```

**예**

```javascript
_satellite.removeCookie('product');
```

사용자의 브라우저에서 쿠키가 제거됩니다.

## 디버깅 함수

다음 함수는 프로덕션 코드에서 액세스하면 안 됩니다. 이러한 함수는 디버깅 목적으로만 사용되며 필요에 따라 시간이 지나면서 변경됩니다.

### `container`

**코드**

```javascript
_satellite._container
```

**예**

>[!IMPORTANT]
>
>이 함수는 프로덕션 코드에서 액세스하면 안 됩니다. 이 함수는 디버깅 목적으로만 사용되며 필요에 따라 시간이 지나면서 변경됩니다.

### `monitor`

**코드**

```javascript
_satellite._monitors
```

**예**

>[!IMPORTANT]
>
>이 함수는 프로덕션 코드에서 액세스하면 안 됩니다. 이 함수는 디버깅 목적으로만 사용되며 필요에 따라 시간이 지나면서 변경됩니다.

**샘플**

태그 라이브러리를 실행하는 웹 페이지에서 HTML에 코드 조각을 추가합니다. 일반적으로 이 코드는 `<head>` 요소 앞에 `<script>` 태그 라이브러리를 로드하는 요소입니다. 이렇게 하면 모니터가 태그 라이브러리에서 발생하는 가장 빠른 시스템 이벤트를 포착할 수 있습니다. 예:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

첫 번째 스크립트 요소에서 태그 라이브러리가 아직 로드되지 않았으므로 초기 `_satellite` 개체를 만들고 배열이 `_satellite._monitors` 가 초기화되었습니다. 그러면 스크립트가 해당 배열에 모니터 개체를 추가합니다. 모니터 개체는 나중에 태그 라이브러리에 의해 호출되는 다음 메서드를 지정할 수 있습니다.

### `ruleTriggered`

이 함수는 이벤트가 규칙을 트리거한 후에 호출되지만, 규칙의 조건 및 작업이 처리되기 전에 호출됩니다. `ruleTriggered`에 전달된 이벤트 개체에는 트리거된 규칙에 대한 정보가 들어 있습니다.

### `ruleCompleted`

이 함수는 규칙이 완전히 처리된 후에 호출됩니다. 즉, 이벤트가 발생하고 모든 조건이 전달되고 모든 작업이 실행된 후에 호출됩니다. 에 전달된 이벤트 개체 `ruleCompleted` 완료된 규칙에 대한 정보를 포함합니다.

### `ruleConditionFailed`

이 함수는 규칙이 트리거되고 해당 조건 중 하나가 실패하면 호출됩니다. `ruleConditionFailed`에 전달된 이벤트 개체에는 트리거된 규칙과 실패한 조건에 대한 정보가 들어 있습니다.

`ruleTriggered`가 호출되면 `ruleCompleted` 또는 `ruleConditionFailed`가 곧 호출됩니다.

>[!NOTE]
>
> 모니터는 세 가지 메서드(`ruleTriggered`, `ruleCompleted`및 `ruleConditionFailed`)를 모두 지정하지 않아도 됩니다. Adobe Experience Platform의 태그는 모니터에서 제공한 모든 지원 메서드를 사용합니다.

### 모니터 테스트

위의 예에서는 모니터에 있는 세 가지 메서드를 모두 지정합니다. 메서드가 호출되면 모니터가 관련 정보를 기록합니다. 이를 테스트하려면 태그 라이브러리에서 두 가지 규칙을 설정합니다.

1. 브라우저가 [!DNL Chrome]인 경우에만 전달되는 클릭 이벤트와 브라우저 조건이 있는 규칙입니다.
1. 브라우저가 [!DNL Firefox]인 경우에만 전달되는 클릭 이벤트와 브라우저 조건이 있는 규칙입니다.

[!DNL Chrome]에서 페이지를 열고 브라우저 콘솔을 열고 페이지를 선택하면 콘솔에 다음과 같이 표시됩니다.

![](../../images/debug.png)

필요에 따라 이러한 핸들러에 추가 후크 또는 추가 정보를 추가할 수 있습니다.
