---
title: 여러 속성을 사용한 인터랙션
seo-title: Adobe Experience Platform 웹 SDK 여러 속성을 사용한 인터랙션
description: 여러 Experience Platform 웹 SDK 속성과 상호 작용하는 방법 학습
seo-description: 여러 Experience Platform 웹 SDK 속성과 상호 작용하는 방법 학습
keywords: multiple properties;configure;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 1%

---


# 여러 속성을 사용한 인터랙션

동일한 페이지에서 두 개의 다른 속성과 상호 작용하려는 경우가 있습니다. 다음과 같은 보고서가 포함됩니다.

* 웹 사이트를 하나로 통합하기 위해 노력하고 있는 회사
* 여러 회사 간의 데이터 공유 관계
* 새로운 Adobe 솔루션을 테스트하고 있지만 기존 구현을 방해하지 않으려는 고객

SDK를 사용하면 기본 코드의 배열에 다른 이름을 추가하여 각 속성에 대해 별도의 인스턴스를 만들 수 있습니다. 다음 예에서는 두 개의 이름을 제공했습니다. `mycustomname1` 및 `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

따라서 스크립트에서 SDK의 두 인스턴스를 만듭니다. 첫 번째 인스턴스와 상호 작용하기 위한 전역 함수 이름 `mycustomname1` 이 지정되고 두 번째 인스턴스와 상호 작용하기 위한 전역 함수의 이름이 지정됩니다 `mycustomname2`.

두 개의 개별 인스턴스를 만들어 각각 다른 속성에 대해 구성할 수 있습니다. 상호 작용으로 발생하는 모든 통신 또는 데이터 지속성 `mycustomname1` 은 그 반대로 `mycustomname2` 분리됩니다.

위의 예에서 다음과 같이 각 인스턴스를 사용하여 명령을 실행할 수 있습니다.

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

동일한 인스턴스에서 다른 명령을 실행하기 전에 각 인스턴스에 대한 `configure` 명령을 실행해야 합니다.

## 제한

쿠키와 충돌하지 않도록 하기 위해 한 페이지 [!DNL Web SDK] 에 있는 한 개의 Adobe Experience Platform 인스턴스에만 특정 항목이 있을 수 있습니다 `edgeConfigId`.  유사하게, Adobe Experience Platform의 한 인스턴스만이 특정 [!DNL Web SDK] 을 가질 수 있습니다 `orgId`.
