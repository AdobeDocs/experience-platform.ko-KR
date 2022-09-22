---
title: Edge Extensions에 대한 데이터 요소 유형
description: edge 속성에서 태그 확장에 대한 데이터 요소 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 31%

---

# Edge 확장의 데이터 요소 유형

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

태그에서 데이터 요소는 서버에서 받은 이벤트 내에서 해당 데이터가 발견되는 위치에 관계없이 웹 또는 모바일 페이지의 데이터 조각에 대한 별칭입니다. 데이터 요소는 규칙에서 참조하고 이러한 데이터 조각에 액세스하기 위해 추상적으로 사용할 수 있습니다. 향후에 데이터 위치가 변경되면(예: 값을 포함하는 이벤트 키 변경), 단일 데이터 요소를 재구성할 수 있으며 해당 데이터 요소를 참조하는 모든 규칙은 변경되지 않습니다.

데이터 요소 유형은 확장에 의해 제공되며 확장 작성자는 이 데이터를 검색하는 방법을 결정합니다. 예를 들어, 데이터 요소 유형을 사용하여 Adobe Experience Platform 사용자가 XDM 레이어 또는 사용자 지정 데이터 레이어에서 데이터를 검색할 수 있도록 할 수 있습니까.

이 문서에서는 Adobe Experience Platform에서 Edge 확장의 데이터 요소 유형을 정의하는 방법을 설명합니다.

>[!IMPORTANT]
>
>웹 확장을 개발하는 경우 다음 안내서를 참조하십시오. [웹 확장에 대한 데이터 요소 유형](../web/data-element-types.md) 을 가리키도록 업데이트하는 것이 좋습니다.
>
>또한 이 문서에서는 사용자가 라이브러리 모듈 및 Edge Extensions에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 소개 내용이 필요한 경우 이 안내서로 돌아가기 전에 [라이브러리 모듈 형식 지정](./format.md)에 대한 개요를 참조하십시오.

일반적으로 데이터 요소 유형은 다음과 같이 구성됩니다.

1. 사용자가 데이터 요소의 설정을 수정할 수 있는 데이터 수집 UI 내에 표시되는 보기.
2. 설정을 해석하고 데이터 조각을 검색하기 위해 태그 런타임 라이브러리 내에 제공되는 라이브러리 모듈입니다.

사용자가 사용자 지정 데이터 레이어에서 데이터를 검색할 수 있도록 허용하려면 모듈이 이 예제와 같을 수 있습니다.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Adobe Experience Platform 사용자가 데이터 계층에 대해 반환한 데이터를 구성할 수 있도록 하기 위해 사용자가 키 이름을 입력한 다음 해당 이름을 `settings` 개체. 객체는 다음과 같을 수 있습니다.

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
