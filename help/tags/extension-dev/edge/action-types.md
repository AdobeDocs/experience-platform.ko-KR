---
title: Edge Extensions에 대한 작업 유형
description: Edge 속성에서 태그 확장에 대한 작업 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 42%

---

# Edge 확장의 작업 유형

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

태그 규칙에서 작업은 규칙 조건이 평가를 통과한 후에 수행되는 작업입니다. 작업 유형은 확장에 의해 제공되며, 해당 효과는 완전히 확장 작성자에 의해 정의됩니다.

예를 들어, 확장에서는 체크아웃 중에 어려움을 겪는 사용자를 돕기 위해 지원 채팅 대화 상자를 표시할 수 있는 &quot;지원 채팅 표시&quot; 작업 유형을 제공할 수 있습니다.

이 문서에서는 Adobe Experience Platform에서 Edge Extension에 대한 작업 유형을 정의하는 방법을 설명합니다.

>[!IMPORTANT]
>
>웹 확장을 개발하는 경우 [웹 확장에 대한 작업 유형](../web/action-types.md)에 대한 안내서를 대신 참조하십시오.
>
>또한 이 문서에서는 사용자가 라이브러리 모듈 및 Edge Extensions에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 소개 내용이 필요한 경우 이 안내서로 돌아가기 전에 [라이브러리 모듈 형식 지정](./format.md)에 대한 개요를 참조하십시오.

작업 유형은 일반적으로 다음과 같이 구성됩니다.

1. 사용자가 작업의 설정을 수정할 수 있는 Experience Platform UI 및 데이터 수집 UI 내에 표시되는 보기.
2. 설정을 해석하고 작업을 수행하기 위해 태그 런타임 라이브러리 내에 제공되는 라이브러리 모듈입니다.

예를 들어 일부 데이터를 타사 엔드포인트로 전달하는 모듈은 다음과 같을 수 있습니다.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

사용자가 종단점을 구성할 수 있도록 하고, 모듈 내의 설정 객체에 끝점의 입력 및 지속성을 허용하려면 객체는 다음과 비슷합니다.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

사용자 정의 종단점에서 작업하려면 모듈을 다음 예로 변경해야 합니다.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## 작업 결과

작업 모듈에서 반환된 결과는 무엇이든 될 수 있습니다. 이 작업에서 비동기 작업을 실행해야 하는 경우 해결한 후 원하는 결과를 반환하는 [promise](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise)를 반환할 수 있습니다.

작업 결과는 `context` 매개 변수(`context.arc.ruleStash`)를 통해 모든 모듈에서 사용할 수 있는 `ruleStash` 키 내에 저장됩니다. `ruleStash` [여기](./context.md#rulestash)에 대해 자세히 알아볼 수 있습니다.
