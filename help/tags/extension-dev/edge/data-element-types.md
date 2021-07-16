---
title: Edge Extensions에 대한 데이터 요소 유형
description: edge 속성에서 태그 확장에 대한 데이터 요소 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 44%

---

# Edge 확장의 데이터 요소 유형

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../term-updates.md)을 참조하십시오.

데이터 요소 유형 라이브러리 모듈은 데이터 일부를 검색합니다. 모듈 작성자는 이 데이터 조각을 검색하는 방법을 결정합니다. 예를 들어, 데이터 요소 유형을 사용하여 Adobe Experience Platform 사용자가 XDM 레이어 또는 사용자 지정 데이터 레이어에서 데이터를 검색할 수 있도록 할 수 있습니까.

>[!IMPORTANT]
>
>이 문서에서는 Edge 확장의 데이터 요소 유형을 다룹니다. 웹 확장을 개발하는 경우 [웹 확장에 대한 데이터 요소 유형](../web/data-element-types.md)에 대한 안내서를 대신 참조하십시오.
>
>또한 이 문서에서는 사용자가 라이브러리 모듈 및 태그 확장에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 소개 내용이 필요한 경우 이 안내서로 돌아가기 전에 [라이브러리 모듈 형식 지정](./format.md)에 대한 개요를 참조하십시오.

사용자가 사용자 지정 데이터 레이어에서 데이터를 검색할 수 있도록 허용하려면 모듈이 이 예제와 같을 수 있습니다.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Adobe Experience Platform 사용자가 데이터 레이어에 대해 반환한 데이터를 구성할 수 있도록 하기 위해, 사용자가 키 이름을 입력한 다음 해당 이름을 `settings` 개체에 저장하도록 허용할 수 있습니다. 객체는 다음과 같을 수 있습니다.

```js
{
  keyName: "campaignId"
}
```

사용자 정의 로컬 저장소 항목 이름으로 작동하려면 모듈을 다음과 같이 변경해야 합니다.

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## 라이브러리 모듈 컨텍스트

모든 데이터 요소 모듈은 모듈이 호출될 때 제공되는 `context` 변수에 액세스할 수 있습니다. 자세한 내용은 [여기](./context.md)를 참조하십시오.
