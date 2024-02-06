---
title: Adobe Experience Platform Web SDK 명령 실행
description: Experience Platform 웹 SDK 명령을 실행하는 방법에 대해 알아봅니다
keywords: 명령 실행;commandName;약속;getLibraryInfo;응답 개체;동의;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: ffc60e83285188bc5b0f6eb7a20fafee16d51d4d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 명령 실행


웹 페이지에 기본 코드가 구현되면 SDK를 사용하여 명령 실행을 시작할 수 있습니다. 외부 파일( )을 기다릴 필요가 없습니다.`alloy.js`)를 입력하여 명령을 실행하기 전에 서버에서 로드할 수 있습니다. SDK의 로드가 완료되지 않은 경우 명령은 가능한 한 빨리 SDK에서 대기 및 처리됩니다.

명령은 다음 구문을 사용하여 실행됩니다.

```javascript
alloy("commandName", options);
```

다음 `commandName` 은 SDK에 수행할 작업을 알려주고, `options` 는 명령에 전달할 매개 변수와 데이터입니다. 사용 가능한 옵션은 명령에 따라 다르므로 각 명령에 대한 자세한 내용은 설명서를 참조하십시오.

## 약속에 대한 메모

[약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise) 는 SDK가 웹 페이지의 코드와 통신하는 방법에 대한 기본 사항입니다. 약속은 일반적인 프로그래밍 구조이며 이 SDK 또는 JavaScript에만 해당되지 않습니다. 약속은 약속이 생성될 때 알 수 없는 값에 대한 대용물 역할을 합니다. 값이 알려지면 해당 값으로 약속이 &quot;해결됨&quot;이 됩니다. 처리기 함수를 약속과 연결할 수 있으므로 약속이 해결되었거나 약속을 해결하는 과정에서 오류가 발생한 경우 알림을 받을 수 있습니다. 약속에 대한 자세한 내용은 다음을 참조하십시오. [이 자습서](https://javascript.info/promise-basics) 또는 웹에 있는 다른 모든 리소스.

## 성공 또는 실패 처리 {#handling-success-or-failure}

명령이 실행될 때마다 약속이 반환됩니다. 약속은 명령의 최종 완료를 나타냅니다. 아래 예에서는 `then` 및 `catch` 명령이 성공했는지 또는 실패했는지 확인하는 메서드입니다.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "result" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

명령이 성공하는 시점을 아는 것이 중요하지 않은 경우 `then` 호출합니다.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

마찬가지로 명령 실패 시점을 아는 것이 중요하지 않은 경우 `catch` 호출합니다.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 응답 개체

명령에서 반환된 모든 약속은 `result` 개체. 명령 및 사용자의 동의에 따라 결과 개체에 데이터가 포함됩니다. 예를 들어 라이브러리 정보는 다음 명령에서 결과 개체의 속성으로 전달됩니다.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### 동의

사용자가 특정 목적을 위해 동의하지 않은 경우, 약속은 여전히 해결되지만, 응답 개체에는 사용자가 동의한 내용의 컨텍스트에서 제공할 수 있는 정보만 포함됩니다.
