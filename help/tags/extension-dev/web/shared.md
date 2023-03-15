---
title: 웹 확장의 공유 모듈
description: Adobe Experience Platform에서 웹 확장에 대한 공유 라이브러리 모듈을 정의하는 방법을 알아봅니다.
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 66%

---

# 웹 확장의 공유 모듈

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

공유 모듈은 다른 확장과 통신할 수 있는 메커니즘입니다. 예를 들어, 확장 A는 데이터를 비동기식으로 로드하여 확장 B에서 [약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise)을 통해 사용할 수 있도록 할 수 있습니다.

JavaScript 구현에서 모든 공유 모듈은 `turbine` 프리 변수에서 제공하는 [`getSharedModule`](../turbine.md#shared) 메서드를 사용하여 인스턴스화됩니다.

공유 모듈은 다른 확장 내에서 호출되지 않는 경우에도 태그 라이브러리에 포함됩니다. 라이브러리 크기를 불필요하게 증가시키지 않으려면 공유 모듈로 노출된 항목에 주의해야 합니다.

공유 모듈에는 보기 구성 요소가 없습니다.

고유한 태그 확장을 개발할 때 제공하려는 공유 모듈을 정의할 수 있습니다. 예를 들어, 사용자 ID를 비동기적으로 로드한 다음 약속을 통해 사용자 ID를 다른 확장과 공유하는 모듈을 만들 수 있습니다.

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

다음에서 [확장 매니페스트](../manifest.md), 이 공유 모듈의 이름을 입력해야 합니다. 이름을 `user-id-promise`로 지정하면, 다른 확장이 다음과 같이 이 공유 모듈에 액세스할 수 있습니다.

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

공유 모듈은 CommonJS 모듈에서 내보낼 수 있는 모든 항목(예: 함수, 객체, 문자열, 숫자 또는 부울)일 수 있습니다.
