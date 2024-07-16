---
title: CSP(콘텐츠 보안 정책) 지원
description: Adobe Experience Platform에서 웹 사이트를 태그와 통합할 때 CSP(콘텐츠 보안 정책) 제한을 처리하는 방법을 알아봅니다.
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 54%

---

# CSP(콘텐츠 보안 정책) 지원

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

CSP(콘텐츠 보안 정책)는 XSS(교차 사이트 스크립팅) 공격을 방지하는 보안 기능입니다. 이는 실제로는 알 수 없는 곳에서 가져온 것이지만 출처를 신뢰할 수 있는 것처럼 브라우저를 속여 악의적인 콘텐츠를 실행하게 할 때 발생합니다. CSP를 사용하면 사용자를 대신하여 브라우저가 스크립트가 실제로 신뢰할 수 있는 소스에서 오고 있는지 확인할 수 있습니다.

CSP는 서버 응답에 `Content-Security-Policy` HTTP 헤더를 추가하거나 구성된 `<meta>` 요소를 HTML 파일의 `<head>` 섹션에 추가하여 구현됩니다.

>[!NOTE]
>
> CSP에 대한 자세한 내용은 [MDN 웹 문서](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)를 참조하십시오.

Adobe Experience Platform의 태그는 웹 사이트에서 스크립트를 동적으로 로드하도록 설계된 태그 관리 시스템입니다. 기본 CSP는 잠재적인 보안 문제를 방지하기 위해 동적으로 로드되는 이러한 스크립트를 차단합니다. 이 문서에서는 태그에서 동적으로 로드되는 스크립트를 허용하도록 CSP를 구성하는 방법에 대한 지침을 제공합니다.

태그가 CSP와 작동하도록 하려면 극복해야 할 두 가지 주요 과제가 있습니다.

* **태그 라이브러리의 원본을 신뢰할 수 있어야 합니다.** 이 조건이 충족되지 않으면 태그 라이브러리 및 기타 필수 JavaScript 파일이 브라우저에 의해 차단되고 페이지에서 로드되지 않습니다.
* **인라인 스크립트를 허용해야 합니다.**&#x200B;이 조건이 충족되지 않으면 맞춤형 코드 규칙 작업이 페이지에서 차단되며 제대로 실행되지 않습니다.

보안이 강화되면 콘텐츠 작성자를 대신하여 더 많은 양의 작업이 필요합니다. 태그를 사용하고 CSP를 제 위치에 보유하려면 다른 스크립트를 안전한 것으로 잘못 표시하지 않고 두 문제를 모두 해결해야 합니다. 이 문서의 나머지 부분에서는 이 작업을 수행하는 방법에 대한 지침을 제공합니다.

## 태그를 신뢰할 수 있는 소스로 추가

CSP를 사용할 때는 `Content-Security-Policy` 헤더의 값에 신뢰할 수 있는 도메인을 포함해야 합니다. 태그에 제공해야 하는 값은 사용 중인 호스팅 유형에 따라 달라집니다.

### 자체 호스팅

라이브러리를 [자체 호스팅](../publishing/hosts/self-hosting-libraries.md)하고 있는 경우 빌드의 소스는 사용자의 도메인일 수 있습니다. 다음 구성을 사용하여 호스트 도메인을 안전한 소스로 지정할 수 있습니다.

**HTTP 헤더**

```http
Content-Security-Policy: script-src 'self'
```

**HTML `<meta>` 태그**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Adobe 관리 호스팅

[Adobe 관리 호스트](../publishing/hosts/managed-by-adobe-host.md)를 사용하는 경우 빌드를 `assets.adobedtm.com`에서 관리합니다. 이미 로드하는 스크립트를 중단하지 않도록 `self`을(를) 안전한 도메인으로 지정해야 하지만 안전한 항목으로 나열하려면 `assets.adobedtm.com`이(가) 필요하며 그렇지 않은 경우 태그 라이브러리가 페이지에 로드되지 않습니다. 이 경우 다음 구성을 사용해야 합니다.

**HTTP 헤더**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>` 태그**


태그 라이브러리를 [비동기적으로](./asynchronous-deployment.md)로드해야 하는 중요한 전제 조건이 있습니다. 태그 라이브러리의 동기식 로드와 작동하지 않습니다(결과: 제대로 실행되지 않는 콘솔 오류 및 규칙).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

이미 로드하는 스크립트가 계속 작동하도록 `self`을 안전한 도메인으로 지정해야 하고 `assets.adobedtm.com` 또한 안전한 항목으로 나열해야 하며 그렇지 않은 경우 라이브러리 빌드가 페이지에 로드되지 않습니다.

## 인라인 스크립트

CSP는 기본적으로 인라인 스크립트를 허용하지 않으므로 이를 허용하려면 수동으로 구성해야 합니다. 인라인 스크립트를 허용하는 두 가지 옵션이 있습니다.

* [임시 허용(양호한 보안)](#nonce)
* [모든 인라인 스크립트 허용(최소 보안)](#unsafe-inline)

>[!NOTE]
>
>CSP 사양은 해시를 사용하는 세 번째 옵션에 대한 세부 사항이 있지만 이 접근 방식은 태그와 같은 태그 관리 시스템에 적합하지 않습니다. Platform의 태그에 해시를 사용하는 제한 사항에 대한 자세한 내용은 [SRI(Subresource Integrity) 안내서](./sri.md)를 참조하십시오.

### 임시 허용 {#nonce}

이 방법에는 암호화 임시값을 생성하여 사이트의 모든 인라인 스크립트와 CSP에 추가하는 작업이 포함됩니다. 브라우저에서 임시값을 포함하는 인라인 스크립트를 로드하라는 지침을 받으면 임시값을 CSP 헤더에 포함된 값과 비교합니다. 일치하는 경우 스크립트가 로드됩니다. 이 임시 항목은 새 페이지를 로드할 때마다 변경해야 합니다.

>[!IMPORTANT]
>
>이 방법을 사용하려면 빌드를 비동기식으로 로드해야 합니다. 빌드를 동기식으로 로드할 때는 작동하지 않으므로 콘솔 오류가 발생하고 규칙이 제대로 실행되지 않습니다. 자세한 내용은 [비동기 배포](./asynchronous-deployment.md) 안내서를 참조하십시오.

아래 예는 Adobe 관리 호스트에 대한 CSP 구성에 임시값을 추가하는 방법을 보여줍니다. 자체 호스팅을 사용하는 경우 `assets.adobedtm.com`을 제외할 수 있습니다.

**HTTP 헤더**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**HTML `<meta>` 태그**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

헤더 또는 HTML 태그를 구성한 후에는 인라인 스크립트를 로드할 때 임시값을 찾을 위치를 태그에 알려주어야 합니다. 스크립트를 로드할 때 태그가 임시 항목을 사용하려면 다음을 수행해야 합니다.

1. 데이터 레이어 내에서 임시 항목이 있는 위치를 참조하는 데이터 요소를 만듭니다.
1. Core Extension을 구성하고 사용한 데이터 요소를 지정합니다.
1. 데이터 요소 및 Core Extension 변경 사항을 게시합니다.

>[!NOTE]
>
>위의 프로세스에서는 사용자 지정 코드의 수행이 아닌 사용자 지정 코드의 로딩만 처리합니다. 인라인 스크립트에 CSP와 호환되지 않는 사용자 지정 코드가 있는 경우 CSP를 우선 사용합니다. 예를 들어 사용자 지정 코드를 사용하여 인라인 스크립트를 DOM에 추가하여 로드하는 경우 태그에서 임시 항목을 추가할 수 없으므로 특정 사용자 지정 코드 작업이 예상대로 작동하지 않습니다.

### 모든 인라인 스크립트 허용 {#unsafe-inline}

임시 항목을 사용하는 것이 도움이 되지 않는 경우, CSP에서 모든 인라인 스크립트를 허용하도록 구성할 수 있습니다. 이 옵션은 가장 안전하지 않은 옵션이지만 구현 및 유지 관리도 더 쉽습니다.

다음 예는 CSP 헤더에서 모든 인라인 스크립트를 허용하는 방법을 보여줍니다.

#### 자체 호스팅

자체 호스팅을 사용하는 경우 다음 구성을 사용하십시오.

**HTTP 헤더**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**HTML `<meta>` 태그**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Adobe 관리 호스팅

Adobe 관리 호스팅을 사용하는 경우 다음 구성을 사용하십시오.

**HTTP 헤더**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**HTML `<meta>` 태그**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## 다음 단계

이 문서를 읽은 후에는 태그 라이브러리 파일 및 인라인 스크립트를 수락하도록 CSP 헤더를 구성하는 방법을 이해할 수 있어야 합니다.

추가 보안 조치로서 SRI(Subresource Integrity)를 사용하여 가져온 라이브러리 빌드의 유효성을 확인할 수도 있습니다. 그러나 이 기능은 태그와 같은 태그 관리 시스템과 함께 사용할 때 몇 가지 주요 제한 사항이 있습니다. 자세한 내용은 [Platform의 SRI 호환성](./sri.md)에 대한 안내서를 참조하십시오.
