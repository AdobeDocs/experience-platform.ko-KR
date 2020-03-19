---
title: 명령 실행
seo-title: Adobe Experience Platform 웹 SDK 명령 실행
description: Experience Platform 웹 SDK 명령을 실행하는 방법 학습
seo-description: Experience Platform 웹 SDK 명령을 실행하는 방법 학습
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (베타) 명령 실행

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

웹 페이지에 기본 코드가 구현된 후 SDK로 명령 실행을 시작할 수 있습니다. 명령을 실행하기 전에 외부 파일 \(`alloy.js`\)이 서버에서 로드될 때까지 기다릴 필요가 없습니다. SDK의 로드가 완료되지 않으면 SDK에서 가능한 한 빨리 명령을 큐에 넣고 처리합니다.

명령은 다음 구문을 사용하여 실행됩니다.

```javascript
alloy("commandName", options);
```

는 `commandName` SDK에 수행해야 하는 작업을 알려주며, 명령에 전달할 매개 변수와 데이터는 `options` 무엇입니까? 사용 가능한 옵션은 명령에 따라 다르므로 각 명령에 대한 자세한 내용은 설명서를 참조하십시오.

## 약속에 대한 메모

[SDK가](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 웹 페이지의 코드와 통신하는 방법에 대한 기본적인 약속은 약속은 일반적인 프로그래밍 구조이며 이 SDK 또는 JavaScript에 한정되지 않습니다. 약속은 약속이 생성될 때 알려지지 않은 값에 대한 대리인 역할을 합니다. 값이 알려지면 약속의 값이 &quot;해결됨&quot;입니다. 처리기 함수를 약속과 연결할 수 있으므로 약속이 해결되거나 약속을 확인하는 과정에서 오류가 발생했을 때 알림을 받을 수 있습니다. 약속에 대한 자세한 내용은 [이 자습서](https://javascript.info/promise-basics) 또는 웹에 있는 다른 리소스를 참조하십시오.

## 성공 또는 실패 처리

명령이 실행될 때마다 약속이 반환됩니다. 약속은 명령의 최종 완료를 나타냅니다. 아래 예제에서는 `then` 및 `catch` 메서드를 사용하여 명령이 성공했는지 실패했는지 확인할 수 있습니다.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

명령이 성공한 시점을 아는 것이 중요하지 않은 경우 `then` 호출을 제거할 수 있습니다.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

마찬가지로, 명령이 언제 실패하는지 아는 것이 중요하지 않은 경우 `catch` 호출을 제거할 수 있습니다.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## 오류 억제

약속이 거부되고 `catch` 호출을 추가하지 않은 경우 Adobe Experience Platform Web SDK에서 로깅을 활성화할지 여부와 관계없이 오류 &quot;버블 업&quot;이 브라우저의 개발자 콘솔에 기록됩니다. 이러한 문제가 발생하는 경우 SDK 구성에 설명된 `suppressErrors` 대로 `true` 구성 옵션을 [설정할 수 있습니다](configuring-the-sdk.md).
