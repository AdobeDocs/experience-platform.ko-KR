---
title: 웹 확장에 대한 데이터 요소 유형
description: 웹 속성에서 태그 확장에 대한 데이터 요소 유형 라이브러리 모듈을 정의하는 방법에 대해 알아봅니다.
exl-id: 3aa79322-2237-492f-82ff-0ba4d4902f70
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 49%

---

# 웹 확장에 대한 데이터 요소 유형

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

데이터 수집 태그에서 데이터 요소는 기본적으로 페이지의 데이터 조각에 대한 별칭입니다. 이 데이터는 쿼리 문자열 매개 변수, 쿠키, DOM 요소 또는 기타 위치에서 찾을 수 있습니다. 데이터 요소는 규칙에서 참조하고 이러한 데이터 조각에 액세스하기 위해 추상적으로 사용할 수 있습니다.

데이터 요소 유형은 확장에서 제공하며 사용자가 특정 방식으로 데이터 조각에 액세스하도록 데이터 요소를 구성할 수 있습니다. 예를 들어, 확장은 사용자가 로컬 저장소 항목 이름을 지정할 수 있는 &quot;로컬 저장소 항목&quot; 데이터 요소 유형을 제공할 수 있습니다. 데이터 요소가 규칙에 의해 참조되면 확장은 데이터 요소를 구성할 때 사용자가 제공한 로컬 저장소 항목 이름을 사용하여 로컬 저장소 항목 값을 조회할 수 있습니다.

이 문서에서는 Adobe Experience Platform에서 웹 확장에 대한 데이터 요소 유형을 정의하는 방법을 다룹니다.

>[!IMPORTANT]
>
>Edge 확장을 개발하는 경우 대신 [Edge 확장에 대한 데이터 요소 유형](../edge/data-element-types.md)에 대한 안내서를 참조하십시오.
>
>이 문서에서는 또한 사용자가 라이브러리 모듈 및 웹 확장에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 소개 내용이 필요한 경우 이 안내서로 돌아가기 전에 [라이브러리 모듈 형식 지정](./format.md)에 대한 개요를 참조하십시오.

데이터 요소 유형은 일반적으로 다음과 같이 구성됩니다.

1. 사용자가 데이터 요소에 대한 설정을 수정할 수 있도록 하는 Experience Platform UI 및 데이터 수집 UI에 표시되는 [보기](./views.md).
2. 설정을 해석하고 데이터 조각을 검색하기 위해 태그 런타임 라이브러리 내에 전달되는 라이브러리 모듈입니다.

사용자가 이름이 `productName`인 로컬 저장소 항목에서 데이터를 검색할 수 있도록 허용하려는 상황을 생각해 보겠습니다 . 모듈은 다음과 같습니다.

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Adobe Experience Platform 사용자가 로컬 저장소 항목 이름을 구성할 수 있도록 하려면 사용자가 이름을 입력한 다음 해당 이름을 `settings` 개체에 저장하도록 허용할 수 있습니다. 객체는 다음과 같을 수 있습니다.

```js
{
  itemName: "campaignId"
}
```

사용자 정의 로컬 저장소 항목 이름으로 작동하려면 모듈을 다음과 같이 변경해야 합니다.

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## 기본값 지원

사용자는 모든 데이터 요소에 대해 기본값을 구성할 수 있습니다. 데이터 요소 라이브러리 모듈에서 `undefined` 또는 `null`의 값을 반환하면 데이터 요소에 대해 사용자가 구성한 기본값으로 자동으로 대체됩니다.

## 컨텍스트 기반 이벤트 데이터

규칙이 트리거된 결과로서 데이터 요소를 검색하는 경우(예: 데이터 요소가 규칙의 조건 및 작업에 사용됨) 규칙을 실행한 이벤트 관련 컨텍스트 정보가 포함된 두 번째 인수가 모듈에 전달됩니다. 이는 특정 경우에 유용할 수 있으며 다음과 같이 액세스할 수 있습니다.

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

`event` 객체에는 다음 속성이 포함되어야 합니다.

| 속성 | 설명 |
| --- | --- |
| `$type` | 마침표를 사용하여 연결된 확장 이름 및 이벤트 이름을 설명하는 문자열입니다. 예: `youtube.play`. |
| `$rule` | 현재 실행 중인 규칙에 대한 정보가 포함된 객체입니다. 객체에는 다음과 같은 하위 속성이 포함되어야 합니다.<ul><li>`id`: 현재 실행 중인 규칙의 ID입니다.</li><li>`name`: 현재 실행 중인 규칙의 이름입니다.</li></ul> |

규칙을 트리거하는 이벤트 유형을 제공하는 확장은 선택적으로 이 `event` 객체에 다른 유용한 정보를 추가할 수 있습니다.
