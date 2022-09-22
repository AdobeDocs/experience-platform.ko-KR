---
title: 웹 확장에 대한 이벤트 유형
description: Adobe Experience Platform에서 웹 확장에 대한 이벤트 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 30%

---

# 웹 확장에 대한 이벤트 유형

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

태그 규칙에서 이벤트는 규칙을 실행하기 위해 발생해야 하는 활동입니다. 예를 들어, 웹 확장은 특정 마우스 또는 터치 동작의 발생을 감시하는 &quot;제스처&quot; 이벤트 유형을 제공할 수 있습니다. 제스처가 발생하면 이벤트 논리에서 규칙을 실행하게 됩니다.

이벤트 유형 라이브러리 모듈은 활동이 발생하는 시점을 감지한 다음 함수를 호출하여 관련 규칙을 실행하도록 설계되었습니다. 감지되는 이벤트는 사용자 지정할 수 있습니다. 예를 들어, 는 사용자가 특정 제스처를 취하거나 빠르게 스크롤하거나 다른 사용자와 상호 작용하는 시점을 감지할 수 있습니다.

이 문서에서는 Adobe Experience Platform에서 웹 확장에 대한 이벤트 유형을 정의하는 방법을 설명합니다.

>[!NOTE]
>
>이 문서에서는 사용자가 라이브러리 모듈 및 웹 확장에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 이 안내서로 돌아가기 전에 구현의 입문 부분을 보려면 [라이브러리 모듈 형식 지정](./format.md) 개요를 참조하십시오.

이벤트 유형은 확장에 의해 정의되며 일반적으로 다음과 같이 구성됩니다.

1. A [보기](./views.md) 사용자가 이벤트의 설정을 수정할 수 있는 데이터 수집 UI 내에 표시됩니다.
2. 설정을 해석하고 특정 활동이 수행되는지를 감시하는, 태그 런타임 라이브러리 내에 제공되는 라이브러리 모듈입니다.

`module.exports` 둘 다 수락 `settings` 및 `trigger` 매개 변수. 이를 통해 이벤트 유형의 사용자 지정을 사용할 수 있습니다.

```js
module.exports = function(settings, trigger) { … };
```

| 매개 변수 | 설명 |
| --- | --- |
| `settings` | 이벤트 유형의 보기에서 사용자가 구성한 설정을 포함하는 객체입니다. 개발자는 이 객체에 대한 입력을 완벽하게 제어할 수 있습니다. |
| `trigger` | 규칙이 실행될 때마다 모듈이 호출해야 하는 함수입니다. 일대일 관계는 `settings` 개체, `trigger` 함수 및 규칙을 포함할 수 있습니다. 즉, 하나의 규칙에 대해 받은 트리거 함수를 다른 규칙을 실행하는 데 사용할 수 없습니다. |

>[!NOTE]
>
>내보낸 함수는 이벤트 유형을 사용하도록 구성된 각 규칙에 대해 한 번 호출됩니다.

예를 들어 5초 동안의 활동을 사용하여 5초 후 활동이 수행되고 규칙이 실행됩니다. 모듈은 이 예제와 비슷합니다.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Adobe Experience Platform 사용자가 지속 시간을 구성할 수 있도록 하려면 설정 객체에 지속 시간을 입력하고 저장하는 옵션이 필요합니다. 객체는 다음과 같을 수 있습니다.

```js
{
  "duration": 25000
}
```

사용자 정의 지속 시간에 대해 작업하려면 모듈을 업데이트하여 이를 포함해야 합니다.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## 컨텍스트 기반 이벤트 데이터 전달

규칙이 트리거되면 발생한 이벤트에 대한 추가 세부 사항을 제공하는 것이 종종 유용합니다. 이러한 정보는 규칙을 생성하는 사용자가 특정 동작을 달성하는 데 유용할 수 있습니다. 예를 들어 사용자가 화면을 스와이프할 때마다 분석 비콘이 전송되는 규칙을 마케팅 담당자가 생성하고 싶은 경우, 확장은 `swipe` 마케터가 이 이벤트 유형을 사용하여 적절한 규칙을 트리거할 수 있도록 이벤트 유형입니다. 마케터가 비콘에서 스와이프가 발생한 각도를 포함하려면 추가 정보를 제공하지 않으면 이 작업을 수행하기 어려울 수 있습니다. 발생한 이벤트에 대한 추가 정보를 제공하려면 `trigger` 함수를 호출할 때 객체를 전달합니다. 예:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

그러면 마케팅 담당자는 텍스트 필드에 값을 지정하여 분석 비콘에서 이 `%event.swipeAngle%` 값을 사용할 수 있습니다. 또한, 다른 컨텍스트(예: 사용자 지정 코드 작업 등) 내에서도 `event.swipeAngle`에 액세스할 수 있습니다. 마케팅 담당자에게 동일한 방식으로 유용할 수 있는 다른 유형의 선택적 이벤트 정보를 포함할 수 있습니다.

### [!DNL nativeEvent]

이벤트 유형이 기본 이벤트를 기반으로 하는 경우(예: 확장에서 `click` 이벤트 유형), `nativeEvent` 속성은 다음과 같습니다.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

이 기능은 마케팅 담당자가 커서 좌표와 같은 기본 이벤트의 모든 정보에 액세스하려고 할 때 유용합니다.

### [!DNL element]

요소와 발생한 이벤트 간에 강력한 관계가 있는 경우에는 `element` 속성을 요소의 DOM 노드에 추가합니다. 예를 들어 확장에서 다음을 제공하는 경우 `click` 이벤트 유형 및 마케팅 담당자가 구성할 수 있도록 허용하여 의 ID가 있는 요소만 실행되도록 합니다 `herobanner` 이 선택되어 있습니다. 이 경우 사용자가 히어로 배너를 선택하면 를 호출하는 것이 좋습니다 `trigger` 및 설정 `element` 히어로 배너의 DOM 노드에 추가합니다.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 규칙 순서 준수

태그는 사용자에게 규칙 순서를 지정하는 기능을 제공합니다. 예를 들어, 사용자가 방향 변경 이벤트 유형을 사용하고 규칙이 실행되는 순서를 지정하기 위해 두 개의 규칙을 만들 수 있습니다. Adobe Experience Platform 사용자가 순서 값을 `2` 규칙 A의 방향 변경 이벤트에 대한 값과 `1` 를 입력합니다. 이는 모바일 장치에서 방향이 변경되면 규칙 B가 규칙 A 전에 실행해야 함을 나타냅니다(순서 값이 낮은 규칙이 먼저 실행됨).

앞에서 설명한 바와 같이, 이 이벤트 모듈에서 내보낸 함수는 이벤트 유형을 사용하도록 구성된 각 규칙에 대해 한 번 호출됩니다. 내보낸 함수가 호출될 때마다 특정 규칙에 연결된 고유한 `trigger` 함수가 전달됩니다. 방금 설명한 시나리오에서 내보낸 함수는 `trigger` 규칙 B에 연결된 후 다시 `trigger` 규칙 A에 연결된 함수를 사용합니다. 사용자가 규칙 A보다 낮은 순서 값을 제공했기 때문에 규칙 B가 우선합니다. 라이브러리 모듈에서 방향 변경을 감지하면 다음을 호출하는 것이 중요합니다 `trigger` 함수는 라이브러리 모듈에 제공된 것과 동일한 순서로 제공됩니다.

아래 예제 코드에서는 방향 변경이 감지되면 트리거 함수가 내보낸 함수에 제공된 순서와 동일한 순서로 호출됩니다.

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

이를 통해 사용자가 지정한 순서가 유지될 수 있습니다.

잘못된 구현은 트리거 함수를 다른 순서로 호출하는 것입니다.

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

기본 프로그래밍 방식에서는 일반적으로 적절한 순서가 유지되지만, 의미를 이해하고 그에 따라 개발하는 것이 중요합니다.
