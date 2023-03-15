---
title: 웹 확장에 대한 이벤트 유형
description: Adobe Experience Platform에서 웹 확장에 대한 이벤트 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 30%

---

# 웹 확장에 대한 이벤트 유형

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

태그 규칙에서 이벤트는 규칙이 실행되기 위해 발생해야 하는 활동입니다. 예를 들어 웹 확장은 특정 마우스 또는 터치 제스처가 발생하는지 감시하는 &quot;제스처&quot; 이벤트 유형을 제공할 수 있습니다. 제스처가 발생하면 이벤트 논리에서 규칙을 실행하게 됩니다.

이벤트 유형 라이브러리 모듈은 활동이 발생하는 시기를 감지한 다음 함수를 호출하여 관련 규칙을 실행하도록 설계되었습니다. 검색 중인 이벤트는 사용자 지정할 수 있습니다. 예를 들어 은 사용자가 특정 제스처를 취하거나 빠르게 스크롤하거나 어떤 대상과 상호 작용하는 시기를 감지할 수 있습니다.

이 문서에서는 Adobe Experience Platform에서 웹 확장에 대한 이벤트 유형을 정의하는 방법을 다룹니다.

>[!NOTE]
>
>이 문서에서는 사용자가 라이브러리 모듈 및 웹 확장에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 이 안내서로 돌아가기 전에 구현의 입문 부분을 보려면 [라이브러리 모듈 형식 지정](./format.md) 개요를 참조하십시오.

이벤트 유형은 확장에 의해 정의되며 일반적으로 다음과 같이 구성됩니다.

1. A [보기](./views.md) Experience Platform UI 및 사용자가 이벤트에 대한 설정을 수정할 수 있는 데이터 수집 UI에 표시됩니다.
2. 설정을 해석하고 특정 활동이 수행되는지 감시하기 위해 태그 런타임 라이브러리 내에 전달되는 라이브러리 모듈입니다.

`module.exports` 다음 두 가지를 모두 수락 `settings` 및 `trigger` 매개 변수. 이렇게 하면 이벤트 유형을 사용자 지정할 수 있습니다.

```js
module.exports = function(settings, trigger) { … };
```

| 매개 변수 | 설명 |
| --- | --- |
| `settings` | 이벤트 유형의 보기에서 사용자가 구성한 설정을 포함하는 객체입니다. 개발자는 이 객체에 대한 입력을 완벽하게 제어할 수 있습니다. |
| `trigger` | 규칙이 실행될 때마다 모듈이 호출해야 하는 함수입니다. 에는 일대일 관계가 있습니다. `settings` 개체, a `trigger` 함수 및 규칙 즉, 한 규칙에 대해 받은 트리거 함수를 다른 규칙을 실행하는 데 사용할 수 없습니다. |

>[!NOTE]
>
>내보낸 함수는 이벤트 유형을 사용하도록 구성된 각 규칙에 대해 한 번 호출됩니다.

예를 들어 5초 경과 활동을 사용하면 5초 경과 후 활동이 수행되며 규칙이 실행됩니다. 모듈은 이 예제와 유사합니다.

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

규칙이 트리거되면 발생한 이벤트에 대한 추가 세부 정보를 제공하는 것이 유용한 경우가 있습니다. 이러한 정보는 규칙을 생성하는 사용자가 특정 동작을 달성하는 데 유용할 수 있습니다. 예를 들어, 마케터가 사용자가 화면을 스와이프할 때마다 분석 비콘이 전송되는 규칙을 만들려고 하는 경우. 확장은 다음을 제공해야 합니다. `swipe` 마케터가 이 이벤트 유형을 사용하여 적절한 규칙을 트리거할 수 있도록 이벤트 유형입니다. 마케터가 비콘에서 스와이프가 발생한 각도를 포함한다고 가정할 경우 추가 정보를 제공하지 않으면 이 작업을 수행하기 어렵습니다. 발생한 이벤트에 대한 추가 정보를 제공하려면 `trigger` 함수를 호출할 때 객체를 전달합니다. 예:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

그러면 마케팅 담당자는 텍스트 필드에 값을 지정하여 분석 비콘에서 이 `%event.swipeAngle%` 값을 사용할 수 있습니다. 또한, 다른 컨텍스트(예: 사용자 지정 코드 작업 등) 내에서도 `event.swipeAngle`에 액세스할 수 있습니다. 동일한 방식으로 마케터에게 유용할 수 있는 다른 유형의 선택적 이벤트 정보를 포함할 수 있다.

### [!DNL nativeEvent]

이벤트 유형이 기본 이벤트를 기반으로 하는 경우(예: 확장에서 `click` 이벤트 유형)을 설정하는 것이 좋습니다 `nativeEvent` 속성을 다음과 같이 지정합니다.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

이 기능은 마케팅 담당자가 커서 좌표와 같은 기본 이벤트의 모든 정보에 액세스하려고 할 때 유용합니다.

### [!DNL element]

요소와 발생한 이벤트 간에 강력한 관계가 있는 경우에는 를 설정하는 것이 좋습니다. `element` 속성을 요소의 DOM 노드에 추가합니다. 예를 들어 확장이 `click` 이벤트 유형이 이고, 마케팅 담당자가 구성할 수 있도록 허용하여 다음 ID가 있는 요소만 규칙이 실행되도록 합니다. `herobanner` 이(가) 선택되어 있습니다. 이 경우 사용자가 히어로 배너를 선택하면 를 호출하는 것이 좋습니다 `trigger` 및 설정 `element` 히어로 배너의 DOM 노드로 이동합니다.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 규칙 순서 준수

태그는 사용자에게 규칙 순서를 지정하는 기능을 제공합니다. 예를 들어, 사용자가 방향 변경 이벤트 유형을 사용하고 규칙이 실행되는 순서를 사용자 지정하는 두 개의 규칙을 만들 수 있습니다. Adobe Experience Platform 사용자가 다음 순서 값을 지정한다고 가정: `2` 규칙 A의 방향 변경 이벤트 및 순서 값 `1` 규칙 B의 방향 변경 이벤트에 사용됩니다. 이는 모바일 장치에서 방향이 변경되면 규칙 B가 규칙 A보다 먼저 실행되어야 함을 나타냅니다(하위 값이 있는 규칙이 먼저 실행되어야 함).

앞에서 설명한 바와 같이, 이 이벤트 모듈에서 내보낸 함수는 이벤트 유형을 사용하도록 구성된 각 규칙에 대해 한 번 호출됩니다. 내보낸 함수가 호출될 때마다 특정 규칙에 연결된 고유한 `trigger` 함수가 전달됩니다. 방금 설명한 시나리오에서 내보낸 함수는 `trigger` 규칙 B에 연결된 후 다시 a로 연결된 함수 `trigger` 규칙 A에 연결된 함수. 사용자가 규칙 A보다 낮은 순서 값을 제공했기 때문에 규칙 B가 우선합니다. 라이브러리 모듈에서 방향 변경을 감지하면 를 호출해야 합니다. `trigger` 라이브러리 모듈에 제공된 순서와 동일한 순서로 함수가 채워집니다.

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
