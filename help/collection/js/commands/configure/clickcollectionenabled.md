---
title: 클릭콜렉션활성화됨
description: 링크 클릭 데이터가 자동으로 수집되는지 여부를 결정하도록 웹 SDK을 구성하는 방법을 알아봅니다.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: 4d251ff7323e83ac5c47b5817f81e8fde64cb7d9
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `clickCollectionEnabled`

`clickCollectionEnabled` 속성은 웹 SDK에서 자동으로 링크 데이터를 수집하는지 여부를 결정하는 부울입니다. 이 변수를 설정하지 않으면 기본값은 `true`입니다. 즉, 기본적으로 링크 추적 데이터가 자동으로 수집됩니다. 링크 데이터를 수동으로 추적하려는 경우 이 속성을 `false`(으)로 설정하는 것이 좋습니다.

`clickCollectionEnabled`이(가) 활성화되면 다음 XDM 요소가 자동으로 데이터로 채워집니다.

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

이 부울을 활성화하면 기본적으로 내부 링크, 다운로드 링크 및 종료 링크가 모두 자동으로 추적됩니다. Adobe 자동 링크 추적을 추가로 제어하려면 [`clickCollection`](clickcollection.md) 개체를 사용하는 것이 좋습니다.

## 자동 링크 추적 논리

웹 SDK은 `<a>` 특성이 없는 경우 `<area>` 및 `onClick` HTML 요소에 대한 모든 클릭 수를 추적합니다. 문서에 연결된 [capture](https://www.w3.org/TR/uievents/#capture-phase) 클릭 이벤트 수신기로 클릭 수를 캡처합니다. 유효한 링크를 클릭하면 다음 논리가 순서대로 실행됩니다.

1. 링크가 [`downloadLinkQualifier`](downloadlinkqualifier.md)의 값을 기반으로 하는 기준과 일치하거나 링크에 `download` HTML 특성이 포함되어 있는 경우 `xdm.web.webInteraction.type`이(가) `"download"`(`clickCollection.downloadLinkEnabled`이(가) 활성화된 경우)로 설정됩니다.
1. 링크 대상 도메인이 현재 `window.location.hostname`과(와) 다른 경우 `xdm.web.webInteraction.type`이(가) `"exit"`(활성화된 경우)으로 설정됩니다.`clickCollection.exitLinkEnabled`
1. 링크가 `"download"` 또는 `"exit"`에 적합하지 않으면 `xdm.web.webInteraction.type`이(가) `"other"`(으)로 설정됩니다.

모든 경우에 `xdm.web.webInteraction.name`은(는) 클릭한 요소와 그 하위 항목을 다음 순서로 비어 있지 않은 첫 번째 값에 대해 확인합니다.

1. `innerText`(`textContent`(으)로 대체)
1. 지원되는 하위 텍스트 노드에서 `nodeValue` 연결됨
1. `alt` 특성
1. `title` 특성
1. `<input value="...">` 특성
1. `<img src="...">` 특성
1. `aria-label` 특성
1. `name` 특성
1. 빈 문자열

`xdm.web.webInteraction.URL` 필드가 링크 대상 URL로 설정되어 있습니다. 링크 이름도 URL로 설정하려면 `filterClickDetails` 개체에서 `clickCollection` 콜백을 사용하여 이 XDM 필드를 재정의할 수 있습니다.

## 구현

`clickCollectionEnabled` 명령을 실행할 때 `configure` 부울을 설정합니다. 웹 SDK을 구성할 때 이 속성을 생략하면 기본적으로 `true`이(가) 됩니다. `false` 및 `xdm.web.webInteraction.type`을(를) 수동으로 설정하려면 이 값을 `xdm.web.webInteraction.value`(으)로 설정하십시오.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```

## 열려 있는 [!DNL Shadow DOM] 요소 지원

웹 SDK은 **열린 Shadow DOM** 요소 내에 있는 링크에 대한 자동 클릭 추적을 지원합니다.

많은 최신 웹 사이트는 [웹 구성 요소](https://developer.mozilla.org/en-US/docs/Web/Web_Components)를 사용하여 재사용 가능한 캡슐화된 사용자 인터페이스 요소를 만듭니다. 이러한 구성 요소는 [**Shadow DOM**](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM)이라는 기술을 사용하여 내부 구조와 스타일을 나머지 페이지와 구분합니다.

Shadow DOM에는 두 가지 유형이 있습니다.

* **섀도 DOM 열기:** 내부 구조는 페이지에서 실행 중인 JavaScript에 액세스할 수 있습니다. 다른 스크립트는 구성 요소의 콘텐츠와 상호 작용하거나 검사할 수 있습니다.
* **닫힌 섀도 DOM:** 내부 구조가 구성 요소 외부의 JavaScript에 숨겨져 있으므로 추적이나 조작을 위해 액세스할 수 없습니다.

웹 SDK은 기본 문서의 링크에 대한 클릭과 마찬가지로 `<a>`섀도 DOM 열기`<area>` 내의 **및** 요소에 대한 클릭을 자동으로 추적합니다. 이 추적을 사용하면 열려 있는 [!DNL Shadow DOM]을(를) 사용하는 웹 구성 요소 내의 링크 클릭이 분석 데이터에 포함됩니다. 구성 요소 외부에서 작동하는 JavaScript 코드에서 내부 구조가 숨겨져 있으므로 **닫힌 섀도 DOM** 내부의 클릭은 추적되지 않습니다.

## 웹 SDK 태그 확장에 대한 클릭 컬렉션 활성화 또는 비활성화

태그를 사용하여 이러한 작업을 수행하는 방법에 대해 알아보려면 웹 SDK 확장 설명서의 [데이터 수집 구성 설정](/help/tags/extensions/client/web-sdk/configure/data-collection.md)을 참조하십시오.
