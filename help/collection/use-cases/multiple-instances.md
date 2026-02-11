---
title: 여러 웹 SDK 인스턴스 사용
description: 여러 Experience Platform 웹 SDK 속성과 상호 작용하는 방법을 알아봅니다.
keywords: 여러 속성
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 여러 웹 SDK 인스턴스 사용

동일한 페이지에서 두 개의 서로 다른 속성과 상호 작용하려는 경우가 있습니다. 가능한 시나리오는 다음과 같습니다.

* 인수되어 함께 웹 사이트를 통합하는 작업을 진행 중인 회사
* 여러 회사 간의 데이터 공유 관계
* 새로운 Adobe 솔루션을 테스트하는 고객으로서 기존 구현에 지장을 주지 않으려는 고객

SDK을 사용하면 [기본 코드](../js/install/base-code.md)의 배열에 다른 이름을 추가하여 각 속성에 대해 별도의 인스턴스를 만들 수 있습니다. 다음 예제에서는 `titanium`과(와) `copper`의 두 이름을 제공합니다.

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

그 결과, 스크립트는 라이브러리가 초기화될 때 두 개의 SDK 인스턴스가 되는 두 개의 전역 함수(위의 예에서 `titanium` 및 `copper`)를 만듭니다. 각 인스턴스는 자체 구성 및 상태를 유지합니다. `titanium`을(를) 사용하는 모든 명령은 `copper`에서 격리됩니다.

>[!TIP]
>
>태그와 함께 기본 코드를 사용하는 경우 태그 확장을 구성할 때 설정한 모든 인스턴스 이름이 모든 [SDK 인스턴스 이름](/help/tags/extensions/client/web-sdk/configure/general.md)과 일치하는지 확인하십시오.

`titanium` 및 `copper`을(를) 웹 SDK 인스턴스로 지정한 명명 패턴 예제에 따라 명령을 독립적으로 실행할 수 있습니다.

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

동일한 인스턴스에서 다른 명령을 실행하기 전에 각 인스턴스에 대해 [`configure`](../js/commands/configure/overview.md) 명령을 실행해야 합니다.

>[!IMPORTANT]
>
>쿠키와의 충돌을 방지하려면 각 웹 SDK 인스턴스에 고유한 `datastreamId`과(와) 고유한 `orgId`이(가) 있어야 합니다.
