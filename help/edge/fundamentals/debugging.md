---
title: 디버깅
seo-title: Adobe Experience Platform 웹 SDK 디버깅
description: Experience Platform 웹 SDK 디버깅 전환 방법 학습
seo-description: Experience Platform 웹 SDK 디버깅 전환 방법 학습
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (베타) 디버깅

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

디버깅이 활성화되면 SDK는 구현을 디버깅하고 SDK가 어떻게 작동하는지 이해하는 데 도움이 되는 메시지를 브라우저 콘솔로 출력합니다. 디버깅을 수행하면 구성된 스키마에 대해 수집되는 데이터에 대한 서버측 동기 유효성 검사가 발생합니다.

디버깅은 기본적으로 비활성화되지만 다음 세 가지 방법으로 전환할 수 있습니다.

* `configure` command
* `debug` command
* 쿼리 문자열 매개 변수가 포함된 랜딩 페이지 URL이 있는지 확인합니다

## 구성 명령을 사용하여 디버깅 전환

명령을 사용하여 SDK를 구성할 때 `configure` 옵션을 로 설정하여 디버깅을 `debugEnabled` 활성화합니다 `true`.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>따라서 개인 브라우저만이 아니라 웹 페이지의 모든 사용자에 대한 디버깅이 가능합니다.

## 디버그 명령으로 디버깅 전환

다음과 같이 별도의 `debug` 명령으로 디버깅을 전환할 수 있습니다.

```javascript
alloy("debug", {
  "enabled": true
});
```

웹 페이지의 코드를 변경하지 않으려는 경우 또는 웹 사이트의 모든 사용자에 대해 로깅 메시지를 생성하지 않으려는 경우 브라우저의 JavaScript 콘솔 내에서 언제든지 `debug` 명령을 실행할 수 있으므로 특히 유용합니다.

## 쿼리 문자열 매개 변수를 사용한 디버깅 전환

쿼리 문자열 매개 변수를 `alloy_debug` 다음과 `true` `false` 같이 설정하여 디버깅을 전환합니다.

```HTTP
http://example.com/?alloy_debug=true
```

웹 페이지의 코드를 변경하지 않거나 웹 사이트의 모든 사용자에 대해 로깅 메시지가 생성되지 않도록 하려는 경우 이 `debug` 명령은 브라우저 내에서 웹 페이지를 로드할 때 쿼리 문자열 매개 변수를 설정할 수 있으므로 특히 유용합니다.

## 우선 순위 및 기간

명령 또는 쿼리 문자열 매개 변수를 통해 디버깅을 설정하면 `debug` 명령에 설정된 모든 `debug` `configure` 옵션을 무시합니다. 이 두 경우 세션 동안 디버깅도 전환된 상태로 유지됩니다. 즉, debug 명령 또는 쿼리 문자열 매개 변수를 사용하여 디버깅을 활성화하면 다음 중 하나가 실행될 때까지 활성화됩니다.

* 세션 종료
* You run the `debug` command
* 쿼리 문자열 매개 변수를 다시 설정합니다
