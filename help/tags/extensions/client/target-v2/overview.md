---
title: Adobe Target v2 확장 개요
description: Adobe Experience Platform의 Adobe Target v2 태그 확장에 대해 알아봅니다.
exl-id: 8f491d67-86da-4e27-92bf-909cd6854be1
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 61%

---

# Adobe Target v2 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

이 확장을 사용하여 규칙을 작성할 때 사용할 수 있는 옵션에 대한 정보를 보려면 이 참조를 사용하십시오.

## Adobe Target v2 확장 구성

>[!IMPORTANT]
>
>Adobe Target 확장을 사용하려면 At.js 2.x가 필요합니다.

Adobe Target 확장이 아직 설치되지 않은 경우 속성을 연 다음, 를 선택합니다 **[!UICONTROL Extensions > Catalog]**&#x200B;를 클릭하고 Target 확장을 마우스로 가리킨 다음 을 선택합니다. **[!UICONTROL 설치]**.

확장을 구성하려면 Extensions 탭을 열고 확장을 마우스로 가리킨 다음 을 선택합니다 **[!UICONTROL 구성]**.

![](../../../images/targetv2config.png)

### at.js 설정

시간 초과를 제외한 모든 at.js 설정은 Target UI의 at.js 구성에서 자동으로 검색됩니다. 확장은 처음 추가될 때 Target UI에서 설정만 검색하므로, 추가 업데이트가 필요한 경우 UI에서 모든 설정을 관리해야 합니다.

다음 구성 옵션을 사용할 수 있습니다.

#### 클라이언트 코드

클라이언트 코드는 Target의 계정 식별자입니다. 이 코드는 거의 항상 기본값으로 유지해야 합니다. 데이터 요소를 사용하여 변경할 수 있습니다.

#### 조직 ID

이 ID는 구현을 Adobe Experience Cloud 계정에 연결합니다. 이 코드는 거의 항상 기본값으로 유지해야 합니다. 데이터 요소를 사용하여 변경할 수 있습니다.

#### 서버 도메인

서버 도메인은 Target 요청이 전송되는 도메인을 나타냅니다. 이 도메인은 거의 항상 기본값으로 유지해야 합니다.

#### GDPR Opt-In

활성화된 경우 Adobe Target은 동의 관리 전략을 지원하는 데 도움이 되는 옵트인 기능을 제공합니다. 선택 기능을 통해 고객이 Target 태그를 실행하는 방법과 시기를 제어할 수 있습니다.  Adobe 옵트인에 대한 자세한 내용은 [GDPR(개인 정보 및 일반 데이터 보호 규정)](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)을 참조하십시오.

#### Timeout (ms)

정의한 기간 내에 Target에서 응답을 받지 못하면 요청 시간이 초과되고 기본 콘텐츠가 표시됩니다. 방문자 세션 중에 추가 요청을 계속 시도합니다. 기본값은 3000ms이며, 이 값은 Target 사용자 인터페이스에 구성된 시간 초과와 다를 수 있습니다.

시간 초과 설정 작동 방식에 대한 자세한 내용은 [Adobe Target 도움말](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html)을 참조하십시오.

## Target 확장 작업 유형

이 섹션에서는 Target 확장에서 사용할 수 있는 작업 유형을 설명합니다.

Target 확장은 규칙의 Then 부분에서 다음 작업을 제공합니다.

### Target 로드

규칙 컨텍스트에서 Target을 로드하는 것이 적절할 수 있는 태그 규칙에 이 작업을 추가합니다. 이렇게 하면 at.js 라이브러리가 페이지에 로드됩니다. 대부분의 구현에서 사이트의 모든 페이지에 Target을 로드해야 합니다. 대상 로드 작업은 대상 호출 앞에 있는 경우에만 사용하는 것이 좋습니다. 그렇지 않으면 Analytics 호출이 지연되는 것과 같은 문제가 발생할 수 있습니다.

구성이 필요하지 않습니다.

### On-Device Decisioning을 사용하여 Target 로드

을 사용하여 Target을 로드하는 것이 적절할 수 있는 태그 규칙에 이 작업을 추가합니다. [on-device decisioning](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/on-device-decisioning/on-device-decisioning.html) 규칙 컨텍스트에서 활성화됩니다. 이렇게 하면 On-Device Decisioning이 활성화된 at.js 라이브러리가 페이지에 로드됩니다. 대부분의 구현에서 사이트의 모든 페이지에 Target을 로드해야 합니다. Adobe은 On-Device Decisioning에서 Target 로드 작업이 Target 호출 앞에 있는 경우에만 을 사용하는 것이 좋습니다. 그렇지 않으면 Analytics 호출이 지연되는 것과 같은 문제가 발생할 수 있습니다.

구성이 필요하지 않습니다.

### 모든 요청에 매개 변수 추가

이 작업 유형을 사용하면 모든 Target 요청에 매개 변수를 추가할 수 있습니다. Target 로드 작업을 먼저 사용해야 합니다.

1. 추가할 매개 변수의 이름과 값을 지정합니다.
1. 추가 아이콘을 선택하여 매개 변수를 더 추가합니다.

### 페이지 로드 요청에 매개 변수 추가

이 작업 유형을 사용하면 매개 변수를 페이지 로드 요청에 특별히 추가할 수 있습니다. Target 로드 작업을 먼저 사용해야 합니다.

1. 추가할 매개 변수의 이름과 값을 지정합니다.
1. 추가 아이콘을 선택하여 매개 변수를 더 추가합니다.

### 페이지 로드 요청 실행

이 작업 유형을 사용하면 페이지가 로드될 때 Target이 요청을 실행할 수 있습니다. Target 로드 작업을 먼저 사용해야 합니다.

깜박임을 방지하기 위한 본문 숨기기와 본문 요소를 숨길 때 사용된 스타일을 활성화할지 여부를 지정해야 합니다. 다음 옵션을 사용할 수 있습니다.

* **Body Hiding:** 이 설정을 활성화하거나 비활성화할 수 있습니다. 기본값은 Enabled로, HTML BODY가 숨겨짐을 의미합니다.
* **Body Hidden Style:** 기본값은 body{opacity:0}입니다. 이 값은 body{display:none}과 같은 다른 값으로 변경될 수 있습니다.

자세한 내용은 [Target 온라인 도움말 설명서](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html)를 참조하십시오.

### 트리거 보기

보기 트리거 작업은 새 페이지를 로드할 때마다 또는 페이지의 구성 요소가 다시 렌더링될 때 호출할 수 있습니다. 단일 페이지 애플리케이션에 대해 트리거 보기를 구현해야 합니다.

1. 트리거해야 하는 보기 이름을 지정합니다.
1. Page 확인란을 선택하여 보기 트리거가 보고할 노출에 도움을 주는지 여부를 지정합니다. 보기가 다시 렌더링되고 보고할 노출에 도움을 주지 않는 구성 요소와 관련이 있는 경우 Page 확인란을 선택 취소합니다.

보기 트리거에 대한 자세한 내용은 [`triggerView()` 도움말 설명서](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/functions-overview/adobe-target-triggerview-atjs-2.html)를 참조하십시오.

## Adobe Target 기본 배포

Target 확장이 설치되면 하나 이상의 규칙을 만들어 적절하게 배포합니다. 먼저 Target 라이브러리(at.js)를 로드하고, 페이지 로드 요청에 사용할 매개 변수를 지정하고, 페이지 로드 요청을 실행해야 합니다.

이 기본 구현을 사용한 Target 규칙은 다음과 같습니다.

![](../../../images/targetv2deploy.png)

이 규칙을 저장한 후 동작을 테스트할 수 있도록 라이브러리에 추가하고 빌드/배포해야 합니다.

## 비동기 배포를 통한 Adobe Target 확장

태그를 비동기식으로 배포할 수 있습니다. Target을 통해 비동기식으로 태그 라이브러리를 로드하는 경우 Target도 비동기식으로 로드됩니다. 이 시나리오는 완벽하게 지원되지만, 처리해야 하는 한 가지 추가 고려 사항이 있습니다.

비동기 배포의 경우, Target 라이브러리가 완전히 로드되고 콘텐츠 교환이 수행되기 전에 페이지에서 기본 콘텐츠 렌더링을 완료할 수 있습니다. 이렇게 하면 Target에서 지정한 개인화된 콘텐츠로 대체되기 전에 기본 콘텐츠가 잠깐 나타나는 &quot;깜박임&quot;이라고 하는 것이 나타날 수 있습니다. 이러한 깜박임이 발생하지 않도록 하려면 콘텐츠 깜박임을 방지하기 위해 코드 조각 사전 숨김을 사용하여 태그 번들을 비동기식으로 로드하는 것이 좋습니다.

코드 조각 사전 숨김을 사용할 때는 몇 가지 주의해야 할 사항이 있습니다.

* 태그 헤더 포함 코드를 로드하기 전에 코드 조각을 추가해야 합니다.
* 이 코드는 태그로 관리할 수 없으므로 페이지에 직접 추가해야 합니다.
* 다음 중 가장 이른 이벤트가 발생하면 페이지가 표시됩니다.
   * 페이지 로드 응답을 받은 경우
   * 페이지 로드 요청이 시간 초과된 경우
   * 코드 조각 자체가 시간 초과된 경우
* 사전 숨김 기간을 최소화하기 위해 코드 조각 사전 숨김을 사용하는 모든 페이지에서 &quot;Fire Page Load Request&quot; 작업을 사용해야 합니다.
* Target에 사용하는 페이지 로드 규칙의 페이지 로드 요청 작업에서도 본문 숨기기가 활성화되어 있어야 합니다. 그렇지 않으면, 모든 페이지 로드는 시간 초과 기간 동안 숨겨진 상태로 유지됩니다.

코드 조각 사전 숨김은 다음과 같으며, 축소할 수 있습니다. 구성 가능한 옵션은 끝에 있습니다.

```js
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

기본적으로 이 코드 조각은 전체 HTML BODY를 사전에 숨깁니다. 경우에 따라 전체 페이지가 아닌 특정 HTML 요소만 사전에 숨길 수 있습니다. 이 작업은 스타일 매개 변수를 사용자 지정하여 수행할 수 있습니다. 페이지의 특정 영역만 사전에 숨기는 항목으로 바꿉니다.

예를 들어, ID별로 식별되는 두 개의 영역인 container-1 및 container-2가 있으면 이 스타일을 기본값 대신 다음과 같이 바꿀 수 있습니다.

```css
#container-1, #container-2 {opacity: 0 !important}
```

기본값:

```css
body {opacity: 0 !important}
```

기본적으로 코드 조각은 3000ms 또는 3초에 시간 초과됩니다. 이 값을 사용자 지정할 수 있습니다.
