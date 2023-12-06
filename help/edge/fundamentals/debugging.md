---
title: Adobe Experience Platform Web SDK에서 디버깅
description: Experience Platform Web SDK에서 디버깅 기능을 전환하는 방법에 대해 알아봅니다.
keywords: 웹 sdk 디버깅;디버깅;구성;구성 명령;디버그 명령;edgeConfigId;setDebug;debugEnabled;디버그;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# 디버깅

디버깅이 활성화되면 SDK는 브라우저 콘솔에 메시지를 출력합니다. 이 메시지는 구현을 디버깅하고 SDK의 작동 방식을 이해하는 데 도움이 될 수 있습니다.

디버깅은 기본적으로 비활성화되어 있지만 네 가지 방법으로 전환할 수 있습니다.

* `configure` 명령
* `setDebug` 명령
* 쿼리 문자열 매개 변수
* Adobe Experience Platform Debugger에서 디버깅 활성화 켜기/끄기 Adobe Experience Platform은 웹 페이지를 검사하고 Experience Cloud 제품과 관련된 구현 문제를 디버깅하는 데 도움이 되는 강력한 도구입니다. Adobe Experience Platform Debugger은 두 가지 모두로 사용할 수 있습니다. [크롬](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 및 [Firefox](https://addons.mozilla.org/ko-KR/firefox/addon/adobe-experience-platform-dbg/) 확장명. AEP 웹 SDK 섹션의 구성 탭에서 디버깅을 활성화할 수 있습니다.

![구성 화면을 보여주는 Experience Platform 디버거 UI 이미지입니다.](../assets/enable-debugging.png)

## Configure 명령을 사용하여 디버깅 전환

를 사용하여 SDK를 구성할 때 `configure` 명령, 다음을 설정하여 디버깅 사용 `debugEnabled` 옵션 대상 `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>이렇게 하면 개인 브라우저가 아닌 웹 페이지의 모든 사용자에 대해 디버깅이 가능합니다.

## Debug 명령을 사용하여 디버깅 전환

별도의 디버깅 사용 `debug` 다음과 같은 명령:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

웹 페이지에서 코드를 변경하지 않으려는 경우 또는 웹 사이트의 모든 사용자에 대해 로깅 메시지를 생성하지 않으려는 경우 다음을 실행할 수 있으므로 특히 유용합니다. `debug` 언제든지 브라우저의 JavaScript 콘솔 내의 명령을 실행할 수 있습니다.

## 쿼리 문자열 매개 변수로 디버깅 전환

다음을 설정하여 디버깅 전환 `alloy_debug` 쿼리 문자열 매개 변수 `true` 또는 `false` 다음과 같이:

```HTTP
http://example.com/?alloy_debug=true
```

와 유사 `debug` 명령: 웹 페이지에서 코드를 변경하지 않으려는 경우 또는 웹 사이트의 모든 사용자에 대해 로깅 메시지를 생성하지 않으려는 경우 브라우저 내에서 웹 페이지를 로드할 때 쿼리 문자열 매개 변수를 설정할 수 있으므로 특히 유용합니다.

## 우선 순위 및 기간

를 통해 디버깅을 설정하는 경우 `debug` 명령 또는 쿼리 문자열 매개 변수에서 `debug` 에 설정된 옵션 `configure` 명령입니다. 이 두 경우 디버깅도 세션 기간 동안 켜진 상태로 유지됩니다. 즉, debug 명령 또는 쿼리 문자열 매개 변수를 사용하여 디버깅을 활성화하면 다음 중 하나가 될 때까지 활성화가 유지됩니다.

* 세션의 끝
* 다음을 실행합니다. `debug` 명령
* 쿼리 문자열 매개 변수를 다시 설정했습니다.

## 라이브러리 정보 검색 중

종종 웹 사이트에 로드한 라이브러리 뒤에 있는 일부 세부 정보에 액세스하는 데 유용합니다. 이렇게 하려면 다음을 실행합니다. `getLibraryInfo` 다음과 같은 명령:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

현재, 는 `libraryInfo` 개체에는 다음 속성이 포함되어 있습니다.

* `version`: 로드된 라이브러리의 버전입니다. 예를 들어 로드되는 라이브러리 버전이 1.0.0인 경우 값은 다음과 같습니다. `1.0.0`. 라이브러리가 태그 확장(&quot;AEP Web SDK&quot;라고 함) 내에서 실행될 때 버전은 라이브러리 버전이며 태그 확장 버전은 &quot;+&quot; 기호로 연결됩니다. 예를 들어, 라이브러리 버전이 1.0.0이고 태그 확장 버전이 1.2.0인 경우 값은 다음과 같습니다. `1.0.0+1.2.0`.
* `commands`: 로드된 라이브러리에서 지원하는 모든 사용 가능한 명령입니다.
* `configs`: 로드된 라이브러리의 모든 현재 구성입니다.
