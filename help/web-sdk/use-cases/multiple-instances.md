---
title: 여러 웹 SDK 인스턴스 사용
description: 여러 Experience Platform 웹 SDK 속성과 상호 작용하는 방법을 알아봅니다.
keywords: 여러 속성;구성;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 여러 웹 SDK 인스턴스 사용

동일한 페이지에서 두 개의 서로 다른 속성과 상호 작용하려는 경우가 있습니다. 이러한 사례는 다음과 같습니다.

* 인수되어 함께 웹 사이트를 통합하는 작업을 진행 중인 회사
* 여러 회사 간의 데이터 공유 관계
* 새로운 Adobe 솔루션을 테스트하는 고객으로서 기존 구현에 지장을 주지 않으려는 고객

SDK를 사용하면 기본 코드의 배열에 다른 이름을 추가하여 각 속성에 대해 별도의 인스턴스를 만들 수 있습니다. 다음 예제에서는 두 가지 이름을 제공합니다. `titanium` 및 `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

따라서 스크립트는 SDK의 두 인스턴스를 만듭니다. 첫 번째 인스턴스와 상호 작용하기 위한 전역 함수 이름은 입니다 `titanium` 두 번째 인스턴스와 상호 작용하기 위한 전역 함수 이름은 다음과 같습니다 `copper`.

두 개의 별도 인스턴스를 생성하여 각각 다른 속성에 대해 구성할 수 있습니다. 과의 상호 작용으로 인해 발생하는 모든 통신 또는 데이터 지속성 `titanium` 에서 격리됩니다. `copper`.

위의 예에서 각 인스턴스를 사용하여 명령을 실행할 수 있습니다.

```javascript
titanium("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  "data": {
    "key": "value"
  }
});

copper("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

다음을 실행하십시오. `configure` 동일한 인스턴스에서 다른 명령을 실행하기 전에 각 인스턴스에 대한 명령입니다.

>[!IMPORTANT]
>
>쿠키와의 충돌을 방지하려면 각 웹 SDK 인스턴스가 고유한 이름을 가져야 합니다 `edgeConfigId` 및 고유한 `orgId`.