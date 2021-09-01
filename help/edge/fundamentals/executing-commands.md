---
title: Adobe Experience Platform Web SDK 명령 실행
description: Experience Platform 웹 SDK 명령을 실행하는 방법을 알아봅니다
keywords: 명령 실행;commandName;약속;getLibraryInfo;응답 개체;동의;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: ca3ee230d510dfb9de400b6f573a612ec33c8f7a
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# 명령 실행


웹 페이지에 기본 코드가 구현되면 SDK로 명령 실행을 시작할 수 있습니다. 명령을 실행하기 전에 외부 파일(`alloy.js`)이 서버에서 로드될 때까지 기다릴 필요가 없습니다. SDK 로드가 완료되지 않으면 명령은 가능한 한 빨리 SDK에서 큐에 올라가 처리합니다.

명령은 다음 구문을 사용하여 실행됩니다.

```javascript
alloy("commandName", options);
```

`commandName`은 SDK에 수행할 작업을 지시하고, `options`는 명령에 전달할 매개 변수와 데이터입니다. 사용 가능한 옵션은 명령에 따라 다르므로 각 명령에 대한 자세한 내용은 설명서를 참조하십시오.

## 약속에 대한 메모

[](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) Promises는 SDK가 웹 페이지의 코드와 통신하는 방법에 근본적입니다. 약속은 일반적인 프로그래밍 구조이며 이 SDK나 JavaScript에만 국한되지 않습니다. 약속은 약속이 만들어질 때 알 수 없는 값에 대한 프록시 역할을 합니다. 값이 알려지면 약속이 값으로 &quot;해결됨&quot;됩니다. 핸들러 함수는 약속과 연결될 수 있으므로 약속이 해결될 때 또는 약속을 확인하는 과정에서 오류가 발생했을 때 알림을 받을 수 있습니다. 약속에 대해 자세히 알아보려면 [이 자습서](https://javascript.info/promise-basics) 또는 웹의 다른 리소스를 참조하십시오.

## 성공 또는 실패 처리 {#handling-success-or-failure}

명령이 실행될 때마다 약속이 반환됩니다. 이 약속은 명령의 최종 완료를 나타냅니다. 아래 예제에서는 `then` 및 `catch` 메서드를 사용하여 명령의 성공 또는 실패 시점을 결정할 수 있습니다.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

명령 성공 시점을 알 필요가 없는 경우에는 `then` 호출을 제거할 수 있습니다.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

마찬가지로, 명령이 언제 실패하는지 알 필요가 없는 경우 `catch` 호출을 제거할 수 있습니다.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 응답 개체

명령에서 반환된 모든 약속은 `result` 개체로 해결됩니다. 결과 개체에는 명령과 사용자의 동의에 따라 데이터가 포함됩니다. 예를 들어 라이브러리 정보는 다음 명령에 결과 개체의 속성으로 전달됩니다.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
  });
```

### 동의

사용자가 특정 목적에 대해 동의하지 않은 경우 약속이 계속 해결됩니다. 그러나 응답 객체에는 사용자가 동의한 내용에 대한 컨텍스트에서만 제공할 수 있는 정보가 포함됩니다.
