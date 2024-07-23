---
title: 여러 웹 SDK 인스턴스 사용
description: 여러 Experience Platform 웹 SDK 속성과 상호 작용하는 방법을 알아봅니다.
keywords: 여러 속성
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 여러 웹 SDK 인스턴스 사용

동일한 페이지에서 두 개의 서로 다른 속성과 상호 작용하려는 경우가 있습니다. 이러한 사례는 다음과 같습니다.

* 인수되어 함께 웹 사이트를 통합하는 작업을 진행 중인 회사
* 여러 회사 간의 데이터 공유 관계
* 새로운 Adobe 솔루션을 테스트하는 고객으로서 기존 구현에 지장을 주지 않으려는 고객

SDK를 사용하면 기본 코드의 배열에 다른 이름을 추가하여 각 속성에 대해 별도의 인스턴스를 만들 수 있습니다. 다음 예제에서는 `titanium`과(와) `copper`의 두 이름을 제공합니다.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

따라서 스크립트는 SDK의 두 인스턴스를 만듭니다. 첫 번째 인스턴스와 상호 작용하기 위한 전역 함수의 이름은 `titanium`이고 두 번째 인스턴스와 상호 작용하기 위한 전역 함수의 이름은 `copper`입니다.

두 개의 별도 인스턴스를 생성하여 각각 다른 속성에 대해 구성할 수 있습니다. `titanium`과(와) 상호 작용하여 발생하는 모든 통신 또는 데이터 지속성은 `copper`에서 격리된 상태로 유지됩니다.

위의 예에서 각 인스턴스를 사용하여 명령을 실행할 수 있습니다.

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

동일한 인스턴스에서 다른 명령을 실행하기 전에 각 인스턴스에 대해 `configure` 명령을 실행해야 합니다.

>[!IMPORTANT]
>
>쿠키와의 충돌을 방지하려면 각 웹 SDK 인스턴스에 고유한 `datastreamId`과(와) 고유한 `orgId`이(가) 있어야 합니다.
