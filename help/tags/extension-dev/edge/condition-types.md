---
title: Edge Extensions에 대한 조건 유형
description: Adobe Experience Platform에서 Edge Extension에 대한 조건 유형 라이브러리 모듈을 정의하는 방법을 알아봅니다.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 44%

---

# Edge 확장의 조건 유형

>[!NOTE]
>
> Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../term-updates.md)을 참조하십시오.

태그 규칙에서 조건은 이벤트가 발생한 후 평가됩니다. 규칙이 계속 처리되려면 모든 조건이 true를 반환해야 합니다. 조건 유형은 확장에 의해 제공되며, 어떤 조건이 true 또는 false인지를 평가하여 부울 값을 반환합니다.

예를 들어, 확장은 사용자가 CSS 선택기를 지정할 수 있는 &quot;뷰포트 포함&quot; 조건 유형을 제공할 수 있습니다. 조건이 클라이언트의 웹 사이트에서 평가되면, 확장은 CSS 선택기와 일치하는 요소를 찾아 해당 조건이 사용자의 뷰포트 내에 포함되어 있는지 여부를 반환할 수 있습니다.

이 문서에서는 Adobe Experience Platform에서 Edge Extension에 대한 조건 유형을 정의하는 방법을 설명합니다.

>[!IMPORTANT]
>
>웹 확장을 개발하는 경우 [웹 확장에 대한 조건 유형](../web/condition-types.md)에 대한 안내서를 대신 참조하십시오.
>
>또한 이 문서에서는 사용자가 라이브러리 모듈 및 Edge Extensions에 이러한 모듈을 통합하는 방법을 잘 알고 있다고 가정합니다. 소개 내용이 필요한 경우 이 안내서로 돌아가기 전에 [라이브러리 모듈 형식 지정](./format.md)에 대한 개요를 참조하십시오.

조건 유형은 일반적으로 다음과 같이 구성됩니다.

1. 사용자가 조건에 대한 설정을 수정할 수 있는 데이터 수집 UI 내에 표시되는 보기입니다.
2. 설정을 해석하고 조건을 평가하는 태그 런타임 라이브러리 내에 제공되는 라이브러리 모듈입니다.

예를 들어, 사용자가 호스트 `example.com`에 있는지 여부를 평가하려면 모듈이 다음과 같을 수 있습니다.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

호스트 이름을 입력하고 설정 객체에 저장하도록 사용자가 호스트 이름을 구성할 수 있도록 하려면 객체가 이 예제와 유사할 수 있습니다.

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
