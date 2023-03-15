---
title: 타사 라이브러리 구현
description: Adobe Experience Platform 태그 확장 내에서 타사 라이브러리를 호스팅하는 다양한 방법에 대해 알아봅니다.
exl-id: d8eaf814-cce8-499d-9f02-b2ed3c5ee4d0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 68%

---

# 타사 라이브러리 구현

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../term-updates.md)를 참조하십시오.

Adobe Experience Platform에서 태그 확장의 주요 목적 중 하나는 기존 마케팅 기술(라이브러리)을 웹 사이트에 쉽게 구현할 수 있도록 하는 것입니다. 확장을 사용하면 웹 사이트의 HTML을 수동으로 편집하지 않고도 타사 컨텐츠 전달 네트워크(CDN)에서 제공하는 라이브러리를 구현할 수 있습니다.

확장 내에서 타사(공급업체) 라이브러리를 호스팅하는 방법이 몇 가지 있습니다. 이 문서에서는 각 솔루션의 장단점을 포함하여 다양한 구현 방법에 대한 개요를 제공합니다.

## 전제 조건

이 문서를 사용하려면 태그 내의 확장과 구성 방법을 비롯한 확장 작업에 대한 이해가 필요합니다. 다음을 참조하십시오. [확장 개발 개요](./overview.md) 추가 정보.

## 기본 코드 로드 프로세스

태그의 컨텍스트 밖에서 마케팅 기술이 일반적으로 웹 사이트에서 로드되는 방식을 이해하는 것이 중요합니다. 타사 라이브러리 공급업체는 라이브러리의 기능을 로드하기 위해 웹 사이트의 HTML 내에 포함되어야 하는 코드 조각(기본 코드라고 함)을 제공합니다.

일반적으로 마케팅 기술의 기본 코드는 사이트에서 로드할 때 다음 프로세스의 일부 변형을 실행합니다.

1. 공급업체 라이브러리와 상호 작용하는 데 사용할 수 있는 전역 함수를 설정합니다.
1. 공급업체 라이브러리를 로드합니다.
1. 구성 및 추적 목적으로 전역 함수에 대하여 큐에 대기한 초기 호출 시리즈를 만듭니다.

전역 함수가 처음 설정되면 라이브러리 로드가 완료되기 전에 함수를 호출할 수 있습니다. 수행하는 모든 호출은 기본 코드의 큐 대기 메커니즘에 추가된 다음 라이브러리가 로드되면 순차적 순서로 실행됩니다.

라이브러리 로드가 완료되면 전역 함수가 큐를 건너뛰고 대신 함수에 대한 향후 호출을 즉시 처리하는 새 함수로 대체됩니다.

### 기본 코드 예

다음 JavaScript는에 대한 축소되지 않은 기본 코드의 예입니다. [Pinterest 전환 태그](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?): 태그를 사용하여 다양한 구현 전략에 맞게 기본 코드가 어떻게 조정되는지 보여주기 위해 이 문서의 후반부에 참조됩니다.

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

요약하면, 위의 기본 코드는 라이브러리(`window.pintrk`)와 상호 작용할 전역 함수를 만드는 [즉시 호출된 함수 표현식(IFE)](https://developer.mozilla.org/ko-KR/docs/Glossary/IIFE)을 제공합니다. 또한 `scriptURL` 변수에는 라이브러리가 있는 `https://s.pinimg.com/ct/core.js` 값을 할당합니다. 앞에서 설명한 대로 라이브러리를 로드하기 전에 호출되는 모든 함수는 라이브러리를 사용할 수 있게 되면 차례로 실행되는 큐(`window.pintrk.queue`)에 푸시됩니다.

기본 코드의 다음 부분은 사이트에서 라이브러리가 로드되는 방식을 이해하는 데 가장 관련이 있습니다.

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

이 기본 코드는 스크립트 요소를 만들고 비동기적으로 로드하도록 설정하며 `src` URL을 `https://s.pinimg.com/ct/core.js`로 설정합니다. 그런 다음 문서에 이미 있는 첫 번째 스크립트 요소 앞에 스크립트 요소를 삽입하여 문서에 스크립트 요소를 추가합니다.

## 태그 구현 옵션

아래 섹션에서는 이전에 예제로 표시된 Pinterest 기본 코드를 사용하여 확장에서 공급업체 라이브러리를 로드할 수 있는 다양한 방법을 보여줍니다. 이러한 각 예제는 다음을 만드는 과정을 포함합니다 [웹 확장에 대한 작업 유형](./web/action-types.md) 웹 사이트에 라이브러리가 로드됩니다.

>[!NOTE]
>
>아래 예제에서는 데모용으로 작업 유형을 사용하지만 사이트에서 태그 라이브러리를 로드하는 모든 함수에 동일한 원칙을 적용할 수 있습니다.


다음 방법을 설명합니다.

- [타사 라이브러리 구현](#implementing-third-party-libraries)
   - [전제 조건](#prerequisites)
   - [기본 코드 로드 프로세스](#base-code-loading-process)
      - [기본 코드 예](#base-code-example)
   - [태그 구현 옵션](#tags-implementation-options)
      - [공급업체 호스트 에서 런타임에 로드{#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [태그 라이브러리 호스트에서 런타임에 로드](#load-at-runtime-from-the-tag-library-host)
      - [라이브러리를 직접 포함](#embed-the-library-directly)
   - [다음 단계](#next-steps)

### 공급업체 호스트 에서 런타임에 로드 {#vendor-host}

공급업체 라이브러리 호스팅에 가장 일반적인 방법은 공급업체의 CDN을 사용하는 것입니다. 대부분의 공급업체 라이브러리에 사용하는 기본 코드가 공급업체의 CDN에서 라이브러리를 로드하도록 이미 구성되었으므로 동일한 위치에서 라이브러리를 로드하도록 확장을 설정할 수 있습니다.

CDN의 파일에 대한 모든 업데이트는 확장에 의해 자동으로 로드되므로 이 방법은 일반적으로 유지 관리가 가장 쉽습니다.

이 메서드를 사용하면 전체 기본 코드를 다음과 같은 작업 유형에 바로 붙여넣을 수 있습니다.

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

선택적으로, 이 구현을 리팩터링하는 추가 단계를 수행할 수 있습니다. 변수 `scriptElement` 및 `firstScriptElement`의 범위가 이제 내보낸 함수로 지정되었기 때문에 이러한 변수가 전역 변형이 될 위험이 없어 IIFE를 제거할 수 있습니다.

또한 태그는 몇 가지 기능을 제공합니다 [핵심 모듈](./web/core.md) 모든 확장에서 사용할 수 있는 유틸리티입니다. 특히 `@adobe/reactor-load-script` 모듈은 스크립트 요소를 만들어 문서에 추가하여 원격 위치에서 스크립트를 로드합니다. 스크립트 로드 프로세스에 이 모듈을 사용하면 작업 코드를 더 세부적으로 재평가할 수 있습니다.

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### 태그 라이브러리 호스트에서 런타임에 로드

라이브러리 호스팅에 공급업체 CDN을 사용하면 몇 가지 위험이 발생합니다. CDN이 실패하거나, 파일을 언제든 중요한 버그로 업데이트하거나, 파일을 다양한 목적으로 훼손할 수 있습니다.

이러한 문제를 해결하기 위해 공급업체 라이브러리를 확장 내에 별도의 파일로 포함할 수 있습니다. 그런 다음 기본 태그 라이브러리와 함께 파일이 호스팅되도록 확장을 구성할 수 있습니다. 런타임 시 확장 프로그램은 기본 라이브러리를 웹 사이트로 전달한 동일한 서버의 공급업체 라이브러리를 로드합니다.

>[!IMPORTANT]
>
>경우에 따라 공급업체 라이브러리는 Pinterest 공급업체 라이브러리의 경우와 마찬가지로 타사 서버의 추가 코드를 로드할 수 있습니다. 이러한 경우 공급업체 라이브러리를 확장과 번들로 묶으면 모든 위험 관련 문제를 완전히 해결할 수 없습니다.

이를 구현하려면 먼저 공급업체 라이브러리를 시스템에 다운로드해야 합니다. Pinterest의 경우 공급업체 라이브러리는 [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js)에 있습니다. 파일을 다운로드한 후에는 확장 프로젝트 내에 파일을 배치해야 합니다. 아래 예에서 파일 이름은 `pinterest.js`이고 프로젝트 디렉토리의 `vendor` 폴더 내에 있습니다.

라이브러리 파일이 프로젝트에 있으면 를 업데이트해야 합니다. [확장 매니페스트](./manifest.md) (`extension.json`)를 클릭하여 공급업체 라이브러리가 기본 태그 라이브러리와 함께 제공되어야 함을 나타냅니다. 이 작업은 `hostedLibFiles` 배열 내에 라이브러리 파일에 대한 경로를 추가하여 수행합니다.

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

마지막으로, 주 라이브러리를 호스트하는 동일한 서버에서 공급업체 라이브러리를 로드하려면 작업 코드를 구성해야 합니다. 다음 예제는 [이전 섹션](#vendor-host)에 작성된 작업 코드를 시작점으로 사용합니다. [터빈 개체](./turbine.md)를 사용하면 다음과 같이 공급업체 파일의 파일 이름을(경로 없이) 전달해야 합니다.

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

이 방법을 사용할 때는 라이브러리가 CDN에서 업데이트될 때마다 다운로드한 공급업체 파일을 수동으로 업데이트하고 변경 사항을 새 버전의 확장에 릴리스해야 합니다.

### 라이브러리를 직접 포함

라이브러리 코드를 작업 코드 자체에 직접 포함시켜 공급업체 라이브러리를 완전히 로드할 필요가 없으므로 효율적으로 기본 태그 라이브러리의 일부로 사용할 수 있습니다. 이 방법을 사용하면 기본 라이브러리의 크기가 증가하지만 별도의 파일을 검색하기 위해 추가 HTTP 요청을 수행할 필요가 없습니다.

[이전 섹션](#vendor-host)에 내장된 작업 코드를 시작점으로 사용하여 스크립트가 로드되는 라인을 스크립트 자체의 내용으로 바꿀 수 있습니다.

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## 다음 단계

이 문서에서는 태그 확장에서 타사 라이브러리를 호스팅하는 다양한 방법에 대한 개요를 제공합니다. 제공된 예는 라이브러리에 중점을 두었지만 이러한 기술은 확장에서 활용할 수 있는 모든 코드에 적용됩니다.

작업 유형, 확장 매니페스트, 핵심 모듈 및 터빈 개체를 포함하여 확장 기능을 구성하기 위한 도구에 대한 자세한 내용은 이 안내서 전체에 연결된 설명서를 참조하십시오.
