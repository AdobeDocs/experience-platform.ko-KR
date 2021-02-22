---
title: CSP 구성
seo-title: Adobe Experience Platform 웹 SDK용 CSP 구성
description: Experience Platform 웹 SDK용 CSP를 구성하는 방법 알아보기
seo-description: Experience Platform 웹 SDK용 CSP를 구성하는 방법 알아보기
keywords: 구성;구성;SDK;edge;웹 SDK;구성;컨텍스트;웹;장치;환경;웹 sdk 설정;컨텐트 보안 정책;configuration;SDK;edge;web SDK;configure;context;web;device;environment;web sdk settings;content security policy
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---


# CSP 구성

[CSP(Content Security Policy](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Headers/Content-Security-Policy))는 브라우저에서 사용할 수 있는 리소스를 제한하는 데 사용됩니다. CSP는 스크립트 및 스타일 리소스의 기능을 제한할 수도 있습니다. Adobe Experience Platform 웹 SDK는 CSP가 필요하지 않지만 CSP를 추가하면 공격 대상이 줄어들어 악성 공격이 발생할 수 있습니다.

CSP는 [!DNL Platform Web SDK]의 배포 및 구성 방법을 반영해야 합니다. 다음 CSP는 SDK가 제대로 작동하는 데 필요한 변경 사항을 보여줍니다. 특정 환경에 따라 추가 CSP 설정이 필요할 수 있습니다.

## 컨텐츠 보안 정책 예

다음 예는 CSP를 구성하는 방법을 보여줍니다.

### Edge 도메인에 대한 액세스 허용

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

위의 예에서 `EDGE-DOMAIN`은(는) 퍼스트 파티 도메인으로 바꿔야 합니다. 퍼스트 파티 도메인은 [edgeDomain](configuring-the-sdk.md#edge-domain) 설정에 대해 구성됩니다. 퍼스트 파티 도메인을 구성하지 않은 경우 `EDGE-DOMAIN`을(를) `*.adobedc.net`으로 교체해야 합니다. 방문자 마이그레이션이 [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled)을(를) 사용하여 설정된 경우 `connect-src` 지시문에도 `*.demdex.net`이(가) 포함되어야 합니다.

### NONCE를 사용하여 인라인 스크립트 및 스타일 요소 허용

[!DNL Platform Web SDK] 페이지 컨텐츠를 수정할 수 있으며 인라인 스크립트 및 스타일 태그를 만들려면 승인을 받아야 합니다. 이를 수행하려면 [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP 지시문에 nonce를 사용하는 것이 좋습니다. nonce는 고유한 각 페이지 보기마다 한 번씩 생성되는 암호화된 강력한 임의 토큰입니다.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

또한 CSP nonce를 [!DNL Platform Web SDK] [기본 코드](installing-the-sdk.md#adding-the-code) 스크립트 태그에 속성으로 추가해야 합니다. [!DNL Platform Web SDK] 그런 다음 인라인 스크립트 또는 스타일 태그를 페이지에 추가할 때 해당 nonce를 사용합니다.

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

nonce를 사용하지 않는 경우 다른 옵션은 `script-src` 및 `style-src` CSP 지시어에 `unsafe-inline`을 추가하는 것입니다.

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>CSP의 혜택을 제한하는 페이지에서 모든 스크립트를 실행할 수 있기 때문에 Adobe은 **을 지정하는 것이 권장되지 않습니다**.`unsafe-inline`
