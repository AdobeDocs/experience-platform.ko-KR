---
title: Adobe Experience Platform 웹 SDK 명령 실행
description: Experience Platform 웹 SDK 명령을 실행하는 방법 알아보기
keywords: 명령 실행;commandName;Provides;getLibraryInfo;응답 개체;동의;
translation-type: tm+mt
source-git-commit: 308c10eb0d1f78dad2b8b6158f28d0384a65c78c
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---


# 명령 실행


기본 코드가 웹 페이지에 구현되면 SDK로 명령 실행을 시작할 수 있습니다. 명령을 실행하기 전에 외부 파일(`alloy.js`)이 서버에서 로드될 때까지 기다릴 필요가 없습니다. SDK의 로드가 완료되지 않은 경우 명령은 SDK에서 가능한 빨리 큐에 올라가 처리됩니다.

명령은 다음 구문을 사용하여 실행됩니다.

```javascript
alloy("commandName", options);
```

`commandName`은 SDK에 수행할 작업을 지시하지만 `options`은 명령에 전달할 매개 변수와 데이터입니다. 사용 가능한 옵션은 명령에 따라 다르므로 각 명령에 대한 자세한 내용은 설명서를 참조하십시오.

## 약속에 대한 메모

[약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) 은 SDK가 웹 페이지의 코드와 통신하는 방법에 대한 기본 사항입니다. 약속은 일반적인 프로그래밍 구조이며 이 SDK 또는 JavaScript에만 국한되지 않습니다. 약속은 약속이 생성될 때 알려지지 않은 값에 대한 대리자 역할을 합니다. 값이 알려지면 프로미션은 값으로 &quot;해결됨&quot;됩니다. 처리기 함수는 약속이 해결되거나 약속을 확인하는 과정에서 오류가 발생했을 때 알림을 받을 수 있도록 약속과 연결할 수 있습니다. 약속에 대한 자세한 내용은 [이 자습서](https://javascript.info/promise-basics) 또는 웹에 있는 다른 리소스를 참조하십시오.

## 성공 또는 실패 처리 {#handling-success-or-failure}

명령이 실행될 때마다 약속이 반환됩니다. 약속은 명령의 최종 완료를 나타냅니다. 아래 예에서 `then` 및 `catch` 메서드를 사용하여 명령이 성공했는지 또는 실패한 지를 확인할 수 있습니다.

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

명령 성공 시점을 아는 것이 중요하지 않은 경우 `then` 호출을 제거할 수 있습니다.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

마찬가지로 명령 실패 시간을 아는 것이 중요하지 않은 경우 `catch` 호출을 제거할 수 있습니다.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 응답 개체

명령에서 반환된 모든 약속은 `result` 객체로 확인됩니다. 결과 개체는 명령 및 사용자의 동의에 따라 데이터를 포함합니다. 예를 들어 라이브러리 정보는 다음 명령에서 결과 객체의 속성으로 전달됩니다.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(results.libraryInfo.version);
  });
```

### 동의

사용자가 특정 목적을 위해 동의하지 않은 경우 약속은 여전히 해결됩니다.그러나 응답 객체에는 사용자가 동의한 내용의 컨텍스트에서 제공할 수 있는 정보만 포함됩니다.
