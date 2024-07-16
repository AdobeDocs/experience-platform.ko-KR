---
title: Edge 확장에 대한 조건 유형
description: Adobe Experience Platform에서 Edge 확장에 대한 조건 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 38%

---

# Edge 확장의 조건 유형

>[!NOTE]
>
> Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

태그 규칙에서 조건은 이벤트가 발생한 후 평가됩니다. 규칙이 계속 처리되려면 모든 조건이 true를 반환해야 합니다. 조건 유형은 확장에서 제공되며 true 또는 false인지를 평가하여 부울 값을 반환합니다.

예를 들어, 확장은 사용자가 CSS 선택기를 지정할 수 있는 &quot;뷰포트 포함&quot; 조건 유형을 제공할 수 있습니다. 조건이 클라이언트의 웹 사이트에서 평가되면, 확장은 CSS 선택기와 일치하는 요소를 찾아 해당 조건이 사용자의 뷰포트 내에 포함되어 있는지 여부를 반환할 수 있습니다.

이 문서에서는 Adobe Experience Platform에서 Edge 확장에 대한 조건 유형을 정의하는 방법을 다룹니다.

>[!IMPORTANT]
>
>웹 확장을 개발하는 경우 [웹 확장에 대한 조건 유형](../web/condition-types.md)에 대한 안내서를 대신 참조하십시오.
>
>이 문서에서는 또한 사용자가 라이브러리 모듈 및 Edge 확장에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 소개 내용이 필요한 경우 이 안내서로 돌아가기 전에 [라이브러리 모듈 형식 지정](./format.md)에 대한 개요를 참조하십시오.

조건 유형은 일반적으로 다음과 같이 구성됩니다.

1. 사용자가 조건에 대한 설정을 수정할 수 있도록 하는 Experience Platform UI 및 데이터 수집 UI 내에 표시되는 보기.
2. 설정을 해석하고 조건을 평가하기 위해 태그 런타임 라이브러리 내에서 전달되는 라이브러리 모듈입니다.

예를 들어 사용자가 `example.com` 호스트에 있는지 여부를 평가하려면 모듈이 다음과 같을 수 있습니다.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

사용자가 호스트 이름을 입력할 수 있도록 호스트 이름을 구성할 수 있게 하고 설정 객체에 저장하려면 객체가 이 예제와 유사할 수 있습니다.

```js
{
  "hostname": "example.com"
}
```

사용자 정의 호스트 이름에서 작동하려면 모듈을 다음과 같이 변경해야 합니다.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## 조건 결과

조건 모듈에서 반환된 결과는 다음 중 하나일 수 있습니다.

1. 부울 값(`true` 또는 `false`).
1. 해결 시 부울 값을 반환하는 [약속](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Promise)

## 라이브러리 모듈 컨텍스트

모든 조건 모듈은 모듈을 호출할 때 제공되는 `context` 변수에 액세스할 수 있습니다. 자세한 내용은 [여기](./context.md)를 참조하십시오.
