---
title: CSP 구성
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Experience Platform 웹 SDK에 대한 CSP를 구성하는 방법을 알아봅니다
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: 구성;구성;SDK;Edge;Web SDK;구성;컨텍스트;웹;장치;환경;웹 SDK 설정;컨텐츠 보안 정책;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# CSP 구성

A [컨텐츠 보안 정책](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP)는 브라우저에서 사용할 수 있는 리소스를 제한하는 데 사용됩니다. CSP는 스크립트 및 스타일 리소스의 기능을 제한할 수도 있습니다. Adobe Experience Platform Web SDK는 CSP가 필요하지 않지만 CSP를 추가하면 공격 지표를 줄여 악의적인 공격을 방지할 수 있습니다.

CSP는 방법을 반영해야 합니다. [!DNL Platform Web SDK] 배포 및 구성됩니다. 다음 CSP는 SDK가 제대로 작동하는 데 필요한 변경 사항을 보여 줍니다. 특정 환경에 따라 추가 CSP 설정이 필요할 수 있습니다.

## 컨텐츠 보안 정책 예

다음 예는 CSP를 구성하는 방법을 보여줍니다.

### Edge 도메인에 대한 액세스 허용

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

위의 예에서, `EDGE-DOMAIN` 은 자사 도메인으로 교체해야 합니다. 자사 도메인이 [edgeDomain](configuring-the-sdk.md#edge-domain) 설정. 자사 도메인이 구성되지 않은 경우 `EDGE-DOMAIN` 을(를) (으)로 교체해야 합니다. `*.adobedc.net`. 다음을 사용하여 방문자 마이그레이션이 켜진 경우 [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), `connect-src` 지시문에는 `*.demdex.net`.

### NONCE를 사용하여 인라인 스크립트 및 스타일 요소 허용

[!DNL Platform Web SDK] 은 페이지 콘텐츠를 수정할 수 있으며 인라인 스크립트 및 스타일 태그를 만들려면 승인해야 합니다. 이를 위해 Adobe에서는 다음에 임시 항목을 사용하는 것이 좋습니다. [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP 지시문입니다. 임시 항목은 서버에서 생성한 암호학적으로 강력한 무작위 토큰으로, 각 고유 페이지 보기마다 한 번씩 생성됩니다.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

또한 CSP 임시값을 속성에 추가해야 합니다. [!DNL Platform Web SDK] [기본 코드](installing-the-sdk.md#adding-the-code) 스크립트 태그를 사용하는 경우입니다. [!DNL Platform Web SDK] 그런 다음 페이지에 인라인 스크립트 또는 스타일 태그를 추가할 때 해당 임시 항목을 사용합니다.

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

임시 항목을 사용하지 않는 경우 다른 옵션은 를 추가하는 것입니다 `unsafe-inline` (으)로 `script-src` 및 `style-src` CSP 지침:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe **아님** 추천 지정 `unsafe-inline` 를 사용하면 페이지에서 스크립트를 실행할 수 있어 CSP의 이점을 제한할 수 있습니다.
