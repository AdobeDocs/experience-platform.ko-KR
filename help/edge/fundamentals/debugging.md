---
title: 디버깅
seo-title: Adobe Experience Platform 웹 SDK 디버깅
description: Experience Platform 웹 SDK 디버깅 전환 방법 살펴보기
seo-description: Experience Platform 웹 SDK 디버깅 전환 방법 살펴보기
keywords: debugging web sdk;debugging;configure;configure command;debug command;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: f63c897dd1a8a8ad9ef7ac025bf05b22265ea95a
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 1%

---


# 디버깅

디버깅이 활성화되면 SDK는 구현을 디버깅하고 SDK가 어떻게 작동하는지 이해하는 데 도움이 되는 메시지를 브라우저 콘솔로 출력합니다. 디버깅을 수행하면 구성된 스키마에 대해 수집되는 데이터의 서버측 동기 유효성 검사가 발생합니다.

디버깅은 기본적으로 비활성화되지만 다음 세 가지 방법으로 전환할 수 있습니다.

* `configure` command
* `setDebug` command
* 쿼리 문자열 매개 변수가 포함된 랜딩 페이지 URL이 있는지 확인합니다

## 구성 명령을 사용하여 디버깅 전환

명령을 사용하여 SDK를 구성할 때 `configure` 옵션을 로 설정하여 디버깅을 `debugEnabled` 활성화합니다 `true`.

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

다음과 같이 별도의 명령으로 디버깅을 `debug` 전환합니다.

```javascript
alloy("setDebug", {
  "enabled": true
});
```

웹 페이지의 코드를 변경하지 않거나 웹 사이트의 모든 사용자에 대해 로깅 메시지가 생성되는 것을 원치 않는 경우, 이는 브라우저의 JavaScript 콘솔 내에서 언제든지 명령을 실행할 수 있기 때문에 특히 유용합니다. `debug`

## 쿼리 문자열 매개 변수를 사용한 디버깅 전환

쿼리 문자열 매개 변수를 다음과 같이 `alloy_debug` 또는 `true` `false` 설정하여 디버깅을 전환합니다.

```HTTP
http://example.com/?alloy_debug=true
```

이 `debug` 명령과 유사하게, 웹 페이지의 코드를 변경하지 않거나 웹 사이트의 모든 사용자에 대해 로깅 메시지가 생성되는 것을 원치 않는 경우, 브라우저 내의 웹 페이지를 로드할 때 쿼리 문자열 매개 변수를 설정할 수 있으므로 특히 유용합니다.

## 우선 순위 및 기간

명령 또는 쿼리 문자열 매개 변수를 통해 디버깅을 설정하면 `debug` 명령에 설정된 모든 `debug` 옵션을 `configure` 무시합니다. 이러한 두 경우 세션 동안 디버깅도 계속 켜져 있습니다. 즉, 디버그 명령이나 쿼리 문자열 매개 변수를 사용하여 디버깅을 활성화하면 다음 중 하나가 실행되기 전까지 활성화됩니다.

* 세션 종료
* 명령을 `debug` 실행합니다
* 쿼리 문자열 매개 변수를 다시 설정합니다

## 라이브러리 정보 검색 중

웹 사이트에 로드한 라이브러리 이면의 일부 세부 정보에 액세스하는 것은 종종 유용합니다. 이렇게 하려면 다음과 같이 `getLibraryInfo` 명령을 실행합니다.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

현재 제공된 개체에는 다음 속성이 `libraryInfo` 포함되어 있습니다.

* `version` 로드된 라이브러리의 버전입니다. 예를 들어 로드되는 라이브러리 버전이 1.0.0이면 값이 됩니다 `1.0.0`.
