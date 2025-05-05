---
title: Adobe Analytics 확장을 위한 공유 모듈
description: Adobe Experience Platform의 Adobe Analytics 태그 확장에서 제공하는 공유 라이브러리 모듈에 대해 알아봅니다.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 70%

---

# Adobe Analytics 확장을 위한 공유 모듈

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

[Adobe Analytics 확장](./overview.md)은 Experience 애플리케이션에 통합할 수 있는 서로 다른 두 개의 [공유 모듈](../../../extension-dev/web/shared.md)을 제공합니다. 이러한 모듈은 다음 섹션에 설명되어 있습니다.

## [!DNL get-tracker]

Adobe Analytics에서 비콘을 전송하기 전에 추적기 개체를 초기화해야 합니다. 초기화 프로세스는 추적기 개체를 만들면 발생하는 [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ko)를 로드한 후 시작합니다.

다음과 같이 `get-tracker` 공유 모듈을 사용하여 추적기 개체가 완전히 초기화된 후 추적기 개체에 액세스할 수 있습니다.

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Adobe Analytics 설치 여부 확인

Adobe Analytics이 확장과 동일한 태그 라이브러리에 설치되지 않았거나 포함되지 않았을 수 있습니다. 이러한 이유로 코드에서 이러한 경우인지 확인하고 적절하게 처리하는 것이 좋습니다. 다음 JavaScript는 이를 구현하는 방법의 예입니다.

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

`getTracker`이(가) `undefined`인 경우 Adobe Analytics 확장이 태그 라이브러리에 없습니다. Adobe Analytics가 설치되지 않은 경우 어떤 기능이 손실될 것인지를 정확하게 반영하도록 기록된 메시지를 사용자 지정할 수 있습니다.


## [!DNL augment-tracker]

추적기 개체가 초기화되면 프로세스의 다음 단계가 보완됩니다. 이 단계를 사용하면 변수가 Adobe Analytics 확장 구성에서 적용되기 전이나 비콘이 전송되기 전에 필요한 모든 것을 사용하여 확장에서 추적기를 늘릴 수 있습니다.

또한 확장 프로그램은 서버에서 데이터 또는 JavaScript를 가져오는 등의 비동기 작업을 수행하는 동안 추적기 초기화 프로세스를 일시 중지할 수 있습니다.

다음과 같이 `augment-tracker` 모듈을 구현할 수 있습니다.

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

추적기 초기화 프로세스의 확대 단계에 도달하면 `augmentTracker()`에 전달된 함수가 호출됩니다.

추적기를 확대하기 전에 비동기 작업을 완료해야 하는 경우 다음과 같이 함수에서 약속을 반환할 수 있습니다.

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

약속을 반환하면 약속이 해결될 때까지 추적기 초기화 프로세스를 일시 중지해야 한다는 메시지가 Adobe Analytics에 표시됩니다.

>[!WARNING]
>
>추적기 초기화 프로세스를 일시 중지하면 비콘이 전송되지 않아 데이터가 수집되지 않을 수 있으므로 주의하십시오(예를 들어, 사용자가 비콘이 전송되기 전에 페이지를 종료한 경우).
