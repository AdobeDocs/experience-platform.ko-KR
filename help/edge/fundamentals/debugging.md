---
title: Adobe Experience Platform Web SDK에서 디버깅
description: Experience Platform 웹 SDK에서 디버깅 기능을 전환하는 방법을 알아봅니다.
keywords: 웹 sdk 디버깅;디버깅;구성;명령 구성;디버그 명령;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# 디버깅

디버깅이 활성화되면 SDK는 메시지를 브라우저 콘솔에 출력하며 구현을 디버깅하고 SDK가 작동하는 방식을 이해하는 데 도움이 됩니다.

디버깅은 기본적으로 비활성화되지만 다음 네 가지 방법으로 전환할 수 있습니다.

* `configure` 명령
* `setDebug` 명령
* 쿼리 문자열 매개 변수가 포함된 랜딩 페이지 URL이 있는지 확인합니다
* Adobe Experience Platform Debugger에서 디버깅 활성화 켜짐. Adobe Experience Platform은 웹 페이지를 검사하고 Experience Cloud 제품에 대한 구현 문제를 디버깅하는 데 도움이 되는 강력한 도구입니다. Adobe Experience Platform Debugger는 모두 [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 및 [Firefox](https://addons.mozilla.org/ko-KR/firefox/addon/adobe-experience-platform-dbg/) 확장. AEP 웹 SDK 섹션의 구성 탭에서 디버깅을 활성화할 수 있습니다.

![](../assets/enable-debugging.png)

## Configure 명령을 사용하여 디버깅 전환

를 사용하여 SDK를 구성할 때 `configure` 명령, 다음을 설정하여 디버깅 활성화 `debugEnabled` 옵션 `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>따라서 개인 브라우저만이 아니라 웹 페이지의 모든 사용자에 대해 디버깅을 사용할 수 있습니다.

## Debug 명령을 사용하여 디버깅 전환

별도의 `debug` 다음과 같이 명령을 수행합니다.

```javascript
alloy("setDebug", {
  "enabled": true
});
```

웹 페이지의 코드를 변경하지 않으려는 경우 또는 웹 사이트의 모든 사용자에 대해 로깅 메시지를 생성하지 않으려는 경우 `debug` 명령을 클릭합니다.

## 쿼리 문자열 매개 변수를 사용하여 디버깅 전환

를 설정하여 디버깅 전환 `alloy_debug` 쿼리 문자열 매개 변수 `true` 또는 `false` 아래와 같이 변경하는 것을 의미합니다.

```HTTP
http://example.com/?alloy_debug=true
```

와 비슷합니다 `debug` 명령을 사용하면 웹 페이지의 코드를 변경하지 않으려는 경우 또는 웹 사이트의 모든 사용자에 대해 로깅 메시지를 생성하지 않으려는 경우 브라우저 내에서 웹 페이지를 로드할 때 쿼리 문자열 매개 변수를 설정할 수 있으므로 특히 유용합니다.

## 우선 순위 및 기간

를 통해 디버깅을 설정할 때 `debug` 명령 또는 쿼리 문자열 매개 변수는 모든 `debug` 에 설정된 옵션 `configure` 명령. 이 두 경우 디버깅도 세션 기간 동안 전환된 상태로 유지됩니다. 즉, 디버그 명령이나 쿼리 문자열 매개 변수를 사용하여 디버깅을 활성화하면 다음 중 하나를 수행할 때까지 활성화됩니다.

* 세션의 끝
* 을(를) 실행합니다. `debug` 명령
* 쿼리 문자열 매개 변수를 다시 설정합니다

## 라이브러리 정보 검색

종종 웹 사이트에 로드한 라이브러리 이면의 일부 세부 정보에 액세스하는 데 유용합니다. 이렇게 하려면 를 실행합니다. `getLibraryInfo` 다음과 같이 명령을 수행합니다.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

현재 제공된 `libraryInfo` 객체에는 다음 속성이 포함됩니다.

* `version`: 로드된 라이브러리의 버전입니다. 예를 들어 로드되는 라이브러리 버전이 1.0.0이면 값은 다음과 같습니다 `1.0.0`. 라이브러리가 태그 확장(&quot;AEP 웹 SDK&quot;라고 함) 내에서 실행되면 버전은 라이브러리 버전이고, 태그 확장 버전은 &quot;+&quot; 기호로 연결됩니다. 예를 들어 라이브러리 버전이 1.0.0이고 태그 확장 버전이 1.2.0인 경우 값은 다음과 같습니다. `1.0.0+1.2.0`.
* `commands`: 이는 로드된 라이브러리에서 지원하는 모든 사용 가능한 명령입니다.
* `configs`: 이는 로드된 라이브러리에 있는 모든 현재 구성입니다.
