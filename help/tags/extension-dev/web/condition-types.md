---
title: 웹 확장에 대한 조건 유형
description: 웹 속성에서 태그 확장에 대한 조건 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 65%

---

# 웹 확장을 위한 조건 유형

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

규칙 컨텍스트에서 조건은 이벤트가 발생한 후 평가됩니다. 규칙이 계속 처리되려면 모든 조건이 true를 반환해야 합니다. 예외 사항은 사용자가 명시적으로 &quot;예외&quot; 버킷에 조건을 배치하는 경우로, 이때는 버킷 내의 모든 조건이 처리를 계속하기 위해서는 false를 반환해야 합니다.

예를 들어, 확장은 사용자가 CSS 선택기를 지정할 수 있는 &quot;뷰포트 포함&quot; 조건 유형을 제공할 수 있습니다. 조건이 클라이언트의 웹 사이트에서 평가되면, 확장은 CSS 선택기와 일치하는 요소를 찾아 해당 조건이 사용자의 뷰포트 내에 포함되어 있는지 여부를 반환할 수 있습니다.

이 문서에서는 Adobe Experience Platform에서 웹 확장에 대한 조건 유형을 정의하는 방법을 설명합니다.

>[!NOTE]
>
>Edge 확장을 개발하는 경우 [Edge 확장에 대한 조건 유형](../edge/condition-types.md)에 대한 안내서를 대신 참조하십시오.
>
>이 문서에서는 사용자가 라이브러리 모듈 및 웹 확장에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 소개 내용이 필요한 경우 이 안내서로 돌아가기 전에 [라이브러리 모듈 형식 지정](./format.md)에 대한 개요를 참조하십시오.

조건 유형은 일반적으로 다음과 같이 구성됩니다.

1. A [보기](./views.md) 사용자가 조건에 대한 설정을 수정할 수 있는 Experience Platform UI 및 데이터 수집 UI에 표시됩니다.
2. 설정을 해석하고 조건을 평가하는 태그 런타임 라이브러리 내에 제공되는 라이브러리 모듈입니다.

조건 유형 라이브러리 모듈에는 다음과 같은 하나의 목표가 있습니다. 사실인지 거짓인지를 평가합니다. 평가 대상은 사용자가 결정합니다.

예를 들어, 사용자가 `example.com` 호스트에 있는지 여부를 평가하려면 모듈이 다음과 같을 수 있습니다.

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

이제 Adobe Experience Platform 사용자가 호스트 이름을 구성할 수 있도록 하려는 상황을 고려해 보겠습니다. 사용자가 호스트 이름을 입력한 다음 설정 객체에 호스트 이름을 저장하도록 허용할 수 있습니다. 객체는 다음과 같을 수 있습니다.

```js
{
  "hostname": "example.com"
}
```

사용자 정의 호스트 이름에서 작동하려면 모듈을 다음과 같이 변경해야 합니다.

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## 컨텍스트 기반 이벤트 데이터

규칙을 실행한 이벤트와 관련된 컨텍스트 정보가 포함된 두 번째 인수가 모듈에 전달됩니다. 이는 특정 경우에 유용할 수 있으며 다음과 같이 액세스할 수 있습니다.

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
