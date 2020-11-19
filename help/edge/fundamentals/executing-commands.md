---
title: 명령 실행
seo-title: Adobe Experience Platform 웹 SDK 명령 실행
description: Experience Platform 웹 SDK 명령을 실행하는 방법 살펴보기
seo-description: Experience Platform 웹 SDK 명령을 실행하는 방법 살펴보기
keywords: Executing commands;commandName;Promises;getLibraryInfo;response objects;consent;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---


# 명령 실행

웹 페이지에 기본 코드가 구현되면 SDK로 명령 실행을 시작할 수 있습니다. 명령을 실행하기 전에 외부 파일(합금.js)이 서버에서 로드될 때까지 기다릴 필요가 없습니다. SDK의 로딩이 완료되지 않으면 SDK에서 가능한 한 빨리 명령을 큐에 넣고 처리합니다.

명령은 다음 구문을 사용하여 실행됩니다.

```javascript
alloy("commandName", options);
```

이 `commandName` 는 SDK에 수행해야 하는 작업을 알려주고, 명령에 전달할 매개 변수 및 데이터 `options` 는 무엇입니까? 사용 가능한 옵션은 명령에 따라 다르므로 각 명령에 대한 자세한 내용은 설명서를 참조하십시오.

## 약속에 대한 메모

[약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) 사항은 SDK가 웹 페이지의 코드와 통신하는 방법에 대한 기본 사항입니다. 약속은 일반적인 프로그래밍 구조로, 이 SDK 또는 JavaScript에만 국한되지 않습니다. 약속은 약속이 생성될 때 알려지지 않은 값에 대한 대리자 역할을 합니다. 값이 알려지면 약속의 값이 &quot;해결됨&quot;입니다. 처리기 함수를 약속과 연결할 수 있으므로 약속이 해결되거나 약속을 확인하는 과정에서 오류가 발생하면 알림을 받을 수 있습니다. 약속에 대한 자세한 내용은 [이 자습서](https://javascript.info/promise-basics) 또는 웹에 있는 다른 리소스를 참조하십시오.

## 성공 또는 실패 처리 {#handling-success-or-failure}

명령이 실행될 때마다 약속이 반환됩니다. 약속은 명령의 최종 완료를 나타냅니다. 아래 예에서, `then` 및 `catch` 메서드를 사용하여 명령이 성공했는지 실패했는지 확인할 수 있습니다.

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

명령이 언제 실행되는지 아는 것이 중요하지 않은 경우 `then` 호출을 제거할 수 있습니다.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

마찬가지로, 명령이 실패하는 시점을 아는 것이 중요하지 않은 경우 `catch` 호출을 제거할 수 있습니다.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 응답 개체

명령에서 반환된 모든 약속은 `result` 개체로 결정됩니다. 결과 개체에는 명령과 사용자의 동의에 따라 데이터가 포함됩니다. 예를 들어 라이브러리 정보는 다음 명령에 결과 개체의 속성으로 전달됩니다.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(results.libraryInfo.version);
  });
```

### 동의

사용자가 특정 목적을 위해 동의하지 않은 경우 약속은 여전히 해결됩니다.그러나 응답 개체에는 사용자가 동의한 내용 컨텍스트에서만 제공할 수 있는 정보만 포함됩니다.
