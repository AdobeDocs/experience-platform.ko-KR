---
title: set디버그
description: 웹 SDK 디버그 설정을 활성화하거나 비활성화합니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

다음 `setDebug` 명령을 사용하면 웹 SDK에서 디버깅 모드를 시작하거나 종료할 수 있습니다. 에 사용할 수 있는 여러 옵션 중 하나입니다. [디버깅](../use-cases/debugging.md). Adobe은 개발 환경 내에서 또는 프로덕션 환경 내의 로컬 시스템에서 디버그 모드를 활성화하는 것을 권장합니다.

## 웹 SDK 태그 확장을 사용하여 디버그 설정

태그 확장은 UI 내에서 디버그 옵션을 전환하는 기능을 제공하지 않습니다. JavaScript 구문을 사용하여 사용자 지정 코드 편집기를 사용하거나, 사이트에 있는 동안 브라우저 콘솔 내에 JavaScript 코드를 입력할 수 있습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 디버그 설정

실행 `setDebug` 명령을 사용하여 웹 SDK의 구성된 인스턴스를 호출할 수 있습니다. 구성 객체의 유일한 옵션은 다음과 같습니다 `enabled`디버그 모드가 활성화되어 있는지 여부를 결정하는 부울입니다.

```js
alloy("setDebug", {"enabled": true});
```
