---
title: 일반 javascript를 사용하여 빠른 시작
seo-title: 'Adobe Experience Platform 웹 SDK 빠른 시작 '
description: Experience Platform 웹 SDK를 사용하여 데이터를 수집하는 빠른 시작 가이드
seo-description: Experience Platform 웹 SDK를 사용하여 데이터를 수집하는 빠른 시작 가이드
keywords: 1st-party domain;CNAME;schema;create schema;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;install sdk;install web sdk;configure;configure web sdk;
translation-type: tm+mt
source-git-commit: f178da80d0902f76868986426600f3da426cf24d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 5%

---


# Adobe Experience Platform 웹 SDK JavaScript 빠른 시작 안내서

이 가이드는 Adobe Experience Platform 웹 SDK를 설정하는 다양한 방법을 안내합니다. 이 기능을 사용하려면에 있어야 허용 목록에 추가하다 합니다. 대기 목록에 오르고자 하는 경우 공인 소프트웨어 관리자(CSM)에게 문의하십시오.

- 자사 도메인(CNAME)이 [활성화되어 있어야](https://docs.adobe.com/content/help/ko-KR/core-services/interface/ec-cookies/cookies-first-party.html) 합니다. 이미 Analytics용 CNAME이 있는 경우 이 CNAME을 사용해야 합니다. 개발 테스트에서는 CNAME이 없어도 되지만 프로덕션으로 이동하려면 먼저 테스트가 필요합니다.
- Adobe Experience Platform에 대한 자격 부여  플랫폼을 구매하지 않은 경우, Adobe은 SDK와 함께 제한된 방식으로 사용할 수 있도록 Experience Platform 데이터 서비스 재단을 추가 비용 없이 제공합니다.
- 최신 버전의 방문자 ID 서비스를 사용하십시오.

## 스키마 준비

XDM으로 데이터를 [!DNL Experience Platform Edge Network] 가져옵니다. XDM은 스키마를 정의할 수 있는 데이터 형식입니다. 스키마는 데이터 형식을 [!DNL Edge Network] 예상하는 방법을 정의합니다. 데이터를 전송하려면 스키마를 정의해야 합니다.

- [스키마 만들기](../../xdm/tutorials/create-schema-ui.md)
- 만든 스키마에 Adobe Experience Platform [!DNL Web SDK] 믹싱 추가

다음 비디오는 데이터에 대한 스키마, 데이터 집합 및 스트리밍 소스 커넥터를 만드는 데 도움이 되도록 [!DNL Web SDK] 만들어졌습니다.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## 구성 ID 만들기

태그 관리 기능을 사용하지 않더라도 Adobe 론치의 [가장자리 구성 도구를](../fundamentals/edge-configuration.md) 사용하여 구성 ID를 만들 수 있습니다. 이렇게 하면 사용자가 데이터를 다양한 솔루션 [!DNL Edge Network] 으로 보낼 수 있습니다. 각 옵션을 찾는 방법에 대한 자세한 내용은 [에지 구성 도구](../fundamentals/edge-configuration.md) 페이지를 참조하십시오.

>[!NOTE]
>
>이 기능을 사용하려면 조직에서 허용 목록에 있어야 합니다. 허용 목록을 사용하려면 CSM에 문의하십시오.

## SDK 설치

SDK를 설치하려면 HTML의 `<head>` 태그에 가능한 한 높은 곳에 다음 &quot;기본 코드&quot;를 복사하여 붙여 넣습니다.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.1.0/alloy.min.js" async></script>
```

다른 옵션에 대한 자세한 내용은 SDK [설치를 참조하십시오](../fundamentals/installing-the-sdk.md).

## SDK 구성

다음으로 SDK에 구성을 제공합니다. 이 작업은 `configure` 명령을 사용하여 수행됩니다. 이 명령은 각 페이지에서 호출되는 첫 번째 명령이어야 합니다.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

여기에서 조직 ID뿐만 아니라 위에서 만든 구성 ID도 제공합니다. 필수 필드는 두 개뿐입니다. 그러나 다른 [구성 옵션도](../fundamentals/configuring-the-sdk.md)많습니다.

## 이벤트 보내기

구성 명령을 호출하면 이벤트 추적을 시작할 수 있습니다.

```javascript
alloy("sendEvent", {});
```

일반적으로 일부 데이터와 함께 이벤트를 전송합니다. 이렇게 XDM 데이터를 전송할 수 있습니다. 보내는 데이터는 XDM에서 만든 스키마에 있어야 합니다.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

이벤트를 추적하는 방법에 대한 자세한 내용은 이벤트 [추적을 참조하십시오](../fundamentals/tracking-events.md).

## 다음 단계

데이터를 이동한 후 다음을 수행할 수 있습니다.

- [스키마 구축](https://docs.adobe.com/content/help/ko-KR/experience-platform/xdm/schema/composition.html)
- [디버깅에 대한 자세한 내용](../fundamentals/debugging.md)
- 경험 [개인화](../fundamentals/rendering-personalization-content.md)
- 여러 솔루션으로 데이터 전송 방법 살펴보기
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
