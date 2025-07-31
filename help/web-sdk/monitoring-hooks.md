---
title: Adobe Experience Platform Web SDK에 대한 후크 모니터링
description: Adobe Experience Platform Web SDK에서 제공하는 모니터링 후크를 사용하여 구현을 디버깅하고 웹 SDK 로그를 캡처하는 방법을 알아봅니다.
exl-id: 56633311-2f89-4024-8524-57d45c7d38f7
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---

# 웹 SDK에 대한 후크 모니터링

Adobe Experience Platform Web SDK에는 다양한 시스템 이벤트를 모니터링하는 데 사용할 수 있는 모니터링 후크가 포함되어 있습니다. 이러한 도구는 자체 디버깅 도구를 개발하고 Web SDK 로그를 캡처하는 데 유용합니다.

웹 SDK은 [디버깅](commands/configure/debugenabled.md)을 사용했는지 여부에 관계없이 모니터링 함수를 트리거합니다.

## `onInstanceCreated` {#onInstanceCreated}

이 콜백 함수는 새 웹 SDK 인스턴스를 성공적으로 만든 경우 트리거됩니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.instance` | 함수 | 웹 SDK 명령을 호출하는 데 사용되는 인스턴스 함수입니다. |

## `onInstanceConfigured` {#onInstanceConfigured}

이 콜백 함수는 [`configure`](commands/configure/overview.md) 명령이 정상적으로 확인될 때 웹 SDK에 의해 트리거됩니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.config` | 오브젝트 | 웹 SDK 인스턴스에 사용한 구성이 포함된 객체입니다. 모든 기본값이 추가된 상태로 [`configure`](commands/configure/overview.md) 명령에 전달되는 옵션입니다. |

## `onBeforeCommand` {#onBeforeCommand}

이 콜백 함수는 다른 명령이 실행되기 전에 웹 SDK에 의해 트리거됩니다. 이 함수를 사용하여 특정 명령의 구성 옵션을 검색할 수 있습니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.commandName` | 문자열 | 이 함수가 실행되기 전의 웹 SDK 명령 이름입니다. |
| `data.options` | 오브젝트 | 웹 SDK 명령에 전달된 옵션이 포함된 개체입니다. |

## `onCommandResolved` {#onCommandResolved}

이 콜백 함수는 명령 약속을 해결할 때 트리거됩니다. 이 함수를 사용하여 명령 옵션과 결과를 확인할 수 있습니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.commandName` | 문자열 | 실행된 웹 SDK 명령의 이름입니다. |
| `data.options` | 오브젝트 | 웹 SDK 명령에 전달된 옵션이 포함된 개체입니다. |
| `data.result` | 오브젝트 | 웹 SDK 명령의 결과를 포함하는 개체입니다. |

## `onCommandRejected` {#onCommandRejected}

이 콜백 함수는 명령 약속이 거부되기 전에 트리거되며 명령이 거부된 이유에 대한 정보를 포함합니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.commandName` | 문자열 | 실행된 웹 SDK 명령의 이름입니다. |
| `data.options` | 오브젝트 | 웹 SDK 명령에 전달된 옵션이 포함된 개체입니다. |
| `data.error` | 오브젝트 | 명령이 거부된 이유와 함께 브라우저의 네트워크 호출에서 반환된 오류 메시지가 포함된 개체(대부분의 경우 `fetch`)입니다. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

이 콜백 함수는 네트워크 요청이 실행되기 전에 트리거됩니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.requestId` | 문자열 | 디버깅을 활성화하기 위해 웹 SDK에서 생성한 `requestId`입니다. |
| `data.url` | 문자열 | 요청한 URL입니다. |
| `data.payload` | 오브젝트 | `POST` 메서드를 통해 JSON 형식으로 변환되고 요청 본문으로 전송되는 네트워크 요청 페이로드 개체입니다. |

## `onNetworkResponse` {#onNetworkResponse}

이 콜백 함수는 브라우저가 응답을 받을 때 트리거됩니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.requestId` | 문자열 | 디버깅을 활성화하기 위해 웹 SDK에서 생성한 `requestId`입니다. |
| `data.url` | 문자열 | 요청한 URL입니다. |
| `data.payload` | 오브젝트 | `POST` 메서드를 통해 JSON 형식으로 변환되고 요청 본문으로 전송되는 페이로드 개체입니다. |
| `data.body` | 문자열 | 문자열 형식의 응답 본문. |
| `data.parsedBody` | 오브젝트 | 구문 분석된 응답 본문을 포함하는 개체입니다. 응답 본문을 구문 분석하는 동안 오류가 발생하는 경우 이 매개 변수는 정의되지 않습니다. |
| `data.status` | 문자열 | 정수 형식의 응답 코드입니다. |
| `data.retriesAttempted` | 정수 | 요청을 보낼 때 시도된 재시도 횟수입니다. 0은 요청이 첫 번째 시도에서 성공했음을 의미합니다. |

## `onNetworkError` {#onNetworkError}

이 콜백 함수는 네트워크 요청이 실패할 때 트리거됩니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.requestId` | 문자열 | 디버깅을 활성화하기 위해 웹 SDK에서 생성한 `requestId`입니다. |
| `data.url` | 문자열 | 요청한 URL입니다. |
| `data.payload` | 오브젝트 | `POST` 메서드를 통해 JSON 형식으로 변환되고 요청 본문으로 전송되는 페이로드 개체입니다. |
| `data.error` | 오브젝트 | 명령이 거부된 이유와 함께 브라우저의 네트워크 호출에서 반환된 오류 메시지가 포함된 개체(대부분의 경우 `fetch`)입니다. |

## `onBeforeLog` {#onBeforeLog}

이 콜백 함수는 웹 SDK이 콘솔에 모든 것을 기록하기 전에 트리거됩니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.componentName` | 문자열 | 로그 메시지를 생성한 구성 요소의 이름입니다. |
| `data.level` | 문자열 | 로깅 수준입니다. 지원되는 수준: `log`, `info`, `warn`, `error`. |
| `data.arguments` | 문자열 배열 | 로그 메시지의 인수. |


## `onContentRendering` {#onContentRendering}

이 콜백 함수는 다양한 렌더링 단계에서 `personalization` 구성 요소에 의해 트리거됩니다. 페이로드는 `status` 매개 변수에 따라 다를 수 있습니다. 함수 매개 변수에 대한 자세한 내용은 아래 샘플을 참조하십시오.

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.componentName` | 문자열 | 로그 메시지를 생성한 구성 요소의 이름입니다. |
| `data.payload` | 오브젝트 | `POST` 메서드를 통해 JSON 형식으로 변환되고 요청 본문으로 전송되는 페이로드 개체입니다. |
| `data.status` | 문자열 | `personalization` 구성 요소가 렌더링 상태를 웹 SDK에 알립니다.  지원되는 값: <ul><li>`rendering-started`: 웹 SDK에서 제안을 렌더링하려고 함을 나타냅니다. 웹 SDK에서 결정 범위 또는 보기를 렌더링하기 전에 `data` 개체에서 `personalization` 구성 요소와 범위 이름으로 렌더링하려는 제안을 볼 수 있습니다.</li><li>`no-offers`: 요청된 매개 변수에 대해 페이로드가 수신되지 않았음을 나타냅니다.</li> <li>`rendering-failed`: 웹 SDK에서 제안을 렌더링하지 못했음을 나타냅니다.</li><li>`rendering-succeeded`: 결정 범위에 대한 렌더링이 완료되었음을 나타냅니다.</li> <li>`rendering-redirect`: 웹 SDK에서 리디렉션 제안을 렌더링함을 나타냅니다.</li></ul> |

## `onContentHiding` {#onContentHiding}

이 콜백 함수는 사전 숨김 스타일이 적용되거나 제거될 때 트리거됩니다.

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|----------|
| `data.instanceName` | 문자열 | 웹 SDK 인스턴스가 저장된 전역 변수의 이름입니다. |
| `data.componentName` | 문자열 | 로그 메시지를 생성한 구성 요소의 이름입니다. |
| `data.status` | 문자열 | `personalization` 구성 요소가 렌더링 상태를 웹 SDK에 알립니다. 지원되는 값: <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## NPM 패키지를 사용할 때 모니터링 후크를 지정하는 방법 {#specify-monitoring-npm}

[NPM 패키지](install/npm.md)를 통해 웹 SDK을 사용하는 경우 아래와 같이 `createInstance` 함수에 모니터링 후크를 지정할 수 있습니다.

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## 예 {#example}

웹 SDK에서 전역 변수 `__alloyMonitors`에서 개체 배열을 찾습니다.

모든 Web SDK 이벤트를 캡처하려면 페이지에 Web SDK 코드가 로드되기 전에 모니터링 후크를 정의해야 합니다. 각 모니터링 메서드는 웹 SDK 이벤트를 캡처합니다.

페이지에 웹 SDK 코드 로드가 *후*&#x200B;인 모니터링 후크를 정의할 수 있지만 페이지 로드 전에 트리거된 모든 후크는 *캡처되지 않습니다*.

모니터링 후크 개체를 정의할 때 특수 논리를 정의할 메서드만 정의하면 됩니다.
예를 들어 `onContentRendering`에만 신경쓰는 경우 해당 메서드를 정의할 수 있습니다. 한 번에 모든 모니터링 후크를 사용할 필요는 없습니다.

여러 모니터링 후크 객체를 정의할 수 있습니다. 해당 이벤트가 트리거될 때 지정된 메서드가 있는 모든 개체가 호출됩니다.

>[!TIP]
>
>모든 모니터링 후크가 구현된 예제 페이지 아래를 참조하십시오.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
