---
title: Adobe Experience Platform 웹 SDK의 디버깅
description: Experience Platform 웹 SDK의 디버깅 기능을 토글하는 방법을 알아봅니다.
keywords: 웹 sdk 디버깅;디버깅;구성;구성 명령;디버그 명령;EdgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: 0f671a967a67761e0cfef6fa0d022e3c3790c2d8
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 디버깅

디버깅이 활성화되면 SDK는 구현을 디버깅하고 SDK가 어떻게 작동하는지 이해하는 데 도움이 되는 메시지를 브라우저 콘솔에 출력합니다. 디버깅을 수행하면 구성된 스키마에 대해 수집되는 데이터의 서버측 동기 유효성 검사가 수행됩니다.

디버깅은 기본적으로 비활성화되지만 다음 3가지 방법으로 전환할 수 있습니다.

* `configure` command
* `setDebug` command
* 쿼리 문자열 매개 변수가 포함된 랜딩 페이지 URL이 있는지 확인합니다

## 구성 명령을 사용하여 디버깅 전환

`configure` 명령을 사용하여 SDK를 구성할 때 `debugEnabled` 옵션을 `true`로 설정하여 디버깅을 활성화합니다.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>따라서 개인 브라우저만이 아니라 웹 페이지의 모든 사용자에 대한 디버깅이 가능합니다.

## 디버그 명령을 사용하여 디버깅 전환

다음과 같이 별도의 `debug` 명령으로 디버깅을 전환합니다.

```javascript
alloy("setDebug", {
  "enabled": true
});
```

웹 페이지의 코드를 변경하지 않으려는 경우 또는 웹 사이트의 모든 사용자에 대해 로깅 메시지를 표시하지 않으려는 경우, 브라우저의 JavaScript 콘솔 내에서 언제든지 `debug` 명령을 실행할 수 있으므로 특히 유용합니다.

## 쿼리 문자열 매개 변수로 디버깅 전환

다음과 같이 `alloy_debug` 쿼리 문자열 매개 변수를 `true` 또는 `false`로 설정하여 디버깅을 전환합니다.

```HTTP
http://example.com/?alloy_debug=true
```

`debug` 명령과 유사하게, 웹 페이지의 코드를 변경하지 않으려는 경우 또는 웹 사이트의 모든 사용자에 대해 로깅 메시지를 표시하지 않으려는 경우 브라우저 내의 웹 페이지를 로드할 때 쿼리 문자열 매개 변수를 설정할 수 있으므로 특히 유용합니다.

## 우선 순위 및 기간

디버깅이 `debug` 명령 또는 쿼리 문자열 매개 변수를 통해 설정되면 `configure` 명령에 설정된 `debug` 옵션을 무시합니다. 이 두 경우 세션 동안 디버깅도 계속 켜져 있습니다. 즉, 디버그 명령이나 쿼리 문자열 매개 변수를 사용하여 디버깅을 활성화하면 다음 중 하나가 실행되기 전까지 활성화됩니다.

* 세션의 종료
* `debug` 명령을 실행합니다.
* 쿼리 문자열 매개 변수를 다시 설정합니다.

## 라이브러리 정보 검색 중

웹 사이트에 로드한 라이브러리의 세부 정보 중 일부를 액세스하는 데 도움이 되는 경우가 많습니다. 이렇게 하려면 다음과 같이 `getLibraryInfo` 명령을 실행합니다.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

현재 제공된 `libraryInfo` 개체에는 다음 속성이 포함되어 있습니다.

* `version` 로드된 라이브러리의 버전입니다. 예를 들어, 로드되는 라이브러리 버전이 1.0.0인 경우 값은 `1.0.0`입니다. 라이브러리가 Adobe Experience Platform Launch 확장 프로그램(&quot;AEP Web SDK&quot;)에서 실행될 때 버전은 라이브러리 버전이고 Platform launch 확장 버전은 &quot;+&quot; 기호로 연결됩니다. 예를 들어 라이브러리 버전이 1.0.0이고 Platform launch 확장 버전이 1.2.0인 경우 값은 `1.0.0+1.2.0`입니다.
