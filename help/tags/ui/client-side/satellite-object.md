---
title: 태그 위성 개체 참조
description: 클라이언트측 _satellite 개체 및 Adobe Experience Platform에서 수행할 수 있는 다양한 기능에 대해 알아봅니다.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 48%

---

# Adobe Experience Platform 태그 위성 개체 참조

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../term-updates.md)을 참조하십시오.

이 문서는 클라이언트측 `_satellite` 개체 및 이 개체를 사용하여 수행할 수 있는 다양한 기능에 대한 참조 역할을 합니다.

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

데이터 수집 사용자 인터페이스의 여러 양식 필드에서 `%%` 구문을 사용하여 변수를 참조할 수 있으므로 `_satellite.getVar()` 호출을 줄일 수 있습니다. 예를 들어 %product%를 사용하면 제품 데이터 요소 또는 사용자 지정 변수의 값에 액세스합니다.

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

[!DNL Adobe Experience Cloud ID] 확장이 속성에 설치된 경우 이 메서드는 방문자 ID 인스턴스를 반환합니다. 자세한 내용은 [Experience Cloud ID 서비스 설명서](https://forums.adobe.com/external-link.jspa?url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fko_KR%2Fmcvid%2F)를 참조하십시오.

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

`logger` 개체를 사용하면 메시지를 브라우저 콘솔에 기록할 수 있습니다. 이 메시지는 사용자가 태그 디버깅을 활성화한 경우( `_satellite.setDebug(true)` 호출 또는 적절한 브라우저 확장 사용)에만 표시됩니다.

### 로깅 사용 중단 경고

```javascript
_satellite.logger.deprecation(message: string)
```

**예**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

이렇게 하면 브라우저 콘솔에 경고가 기록됩니다. 사용자가 태그 디버깅을 활성화하는지 여부를 나타내는 메시지가 표시됩니다.

## `cookie`

**코드**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

```javascript
_satellite.cookie.get(name: string) => string
```

```javascript
_satellite.cookie.remove(name: string)
```

**예**

```javascript
// Writing a cookie that expires in one week.
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

```javascript
// Reading a previously set cookie.
var product = _satellite.cookie.get('product');
```

```javascript
// Removing a previously set cookie.
_satellite.cookie.remove('product');
```

이것은 쿠키를 읽고 쓰는 유틸리티입니다. 타사 라이브러리 js-쿠키의 노출된 사본입니다. 고급 사용법은 [js-cookie 사용 설명서](https://www.npmjs.com/package/js-cookie#basic-usage)(외부 링크)를 참조하십시오.

## `buildInfo`

**코드**

```javascript
_satellite.buildInfo
```

이 개체에는 현재 태그 런타임 라이브러리 빌드에 대한 정보가 들어 있습니다. 개체에는 다음 속성이 포함되어 있습니다.

### `turbineVersion`

이 옵션은 현재 라이브러리 내에서 사용되는 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 버전을 제공합니다.

### `turbineBuildDate`

컨테이너 내에 사용된 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 버전이 빌드된 ISO 8601 날짜입니다.

### `buildDate`

현재 라이브러리가 빌드된 ISO 8601 날짜입니다.

### `environment`

이 라이브러리가 빌드된 환경입니다. 가능한 값은 다음과 같습니다.

* development
* staging
* production

다음 예에서는 개체 값을 보여 줍니다.

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

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

`notify` 브라우저 콘솔에 메시지를 기록합니다. 이 메시지는 사용자가 태그 디버깅을 활성화한 경우( `_satellite.setDebug(true)` 호출 또는 적절한 브라우저 확장 사용)에만 표시됩니다.

기록되는 메시지의 스타일링 및 필터링에 영향을 주는 선택적 로깅 수준을 전달할 수 있습니다. 지원되는 수준은 다음과 같습니다.

3 - 정보 메시지.

4 - 경고 메시지.

5 - 오류 메시지.

로깅 수준을 제공하지 않거나 다른 수준 값을 전달하지 않으면 메시지가 일반 메시지로 기록됩니다.

## `setCookie`

>[!NOTE]
>
>이 메서드는 더 이상 사용되지 않습니다. 대신 `_satellite.cookie.set()`를 사용하십시오.

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

>[!NOTE]
>
>이 메서드는 더 이상 사용되지 않습니다. 대신 `_satellite.cookie.get()`를 사용하십시오.

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
>이 메서드는 더 이상 사용되지 않습니다. 대신 `_satellite.cookie.remove()`를 사용하십시오.

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

태그 라이브러리를 실행하는 웹 페이지에서 HTML에 코드 조각을 추가합니다. 일반적으로 이 코드는 태그 라이브러리를 로드하는 `<script>` 요소 앞에 있는 `<head>` 요소에 삽입됩니다. 이렇게 하면 모니터가 태그 라이브러리에서 발생하는 가장 빠른 시스템 이벤트를 포착할 수 있습니다. 예:

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

첫 번째 스크립트 요소에서 태그 라이브러리가 아직 로드되지 않았으므로 초기 `_satellite` 개체가 생성되고 `_satellite._monitors`에서 배열이 초기화됩니다. 그러면 스크립트가 해당 배열에 모니터 개체를 추가합니다. 모니터 개체는 나중에 태그 라이브러리에 의해 호출되는 다음 메서드를 지정할 수 있습니다.

### `ruleTriggered`

이 함수는 이벤트가 규칙을 트리거한 후에 호출되지만, 규칙의 조건 및 작업이 처리되기 전에 호출됩니다. `ruleTriggered`에 전달된 이벤트 개체에는 트리거된 규칙에 대한 정보가 들어 있습니다.

### `ruleCompleted`

이 함수는 규칙이 완전히 처리된 후에 호출됩니다. 즉, 이벤트가 발생하고 모든 조건이 전달되고 모든 작업이 실행된 후에 호출됩니다. `ruleCompleted`에 전달된 이벤트 개체에는 완료된 규칙에 대한 정보가 들어 있습니다.

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
