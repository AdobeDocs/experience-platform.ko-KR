---
title: 웹 확장에 대한 작업 유형
description: 웹 속성에서 태그 확장에 대한 작업 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 54%

---

# 웹 확장을 위한 작업 유형

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../term-updates.md)을 참조하십시오.

작업 유형 라이브러리 모듈은 사전 정의된 작업을 수행하도록 설계되었습니다. 이 작업이 제공하는 기능은 사용자가 결정합니다. 비콘을 보내거나, 오퍼를 표시하거나, 방문에 대한 감사 메시지를 보내거나, 쿠키를 저장하거나, 지원 채팅을 여시겠습니까?

>[!IMPORTANT]
>
>이 문서에서는 웹 확장의 작업 유형을 다룹니다. Edge 확장을 개발하는 경우 [Edge 확장에 대한 작업 유형](../edge/action-types.md) 안내서를 대신 참조하십시오.
>
>또한 이 문서에서는 사용자가 라이브러리 모듈 및 태그 확장에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 소개 내용이 필요한 경우 이 안내서로 돌아가기 전에 [라이브러리 모듈 형식 지정](./format.md)에 대한 개요를 참조하십시오.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

예를 들어, Adobe Experience Platform 사용자가 메시지를 구성할 수 있도록 하기 위해 사용자가 설정 객체에 메시지를 입력하고 저장하도록 허용할 수 있습니다. 객체는 다음과 같습니다.

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

사용자 정의 메시지에서 작동하려면 모듈을 다음과 같이 변경해야 합니다.

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## 컨텍스트 기반 이벤트 데이터

그런 다음 규칙을 실행하는 이벤트에 대한 컨텍스트 정보가 포함된 두 번째 인수를 모듈에 전달해야 합니다. 이는 특정 경우에 유용할 수 있으며 다음과 같이 액세스할 수 있습니다.

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
