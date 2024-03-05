---
title: 디버깅 메서드
description: Web SDK에서 디버깅 기능을 전환하는 방법에 대해 알아봅니다.
keywords: 웹 sdk 디버깅;디버깅;구성;구성 명령;디버그 명령;edgeConfigId;setDebug;debugEnabled;디버그;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 디버깅 메서드

디버깅이 활성화되면 Web SDK는 구현 디버깅에 도움이 될 수 있는 메시지를 브라우저 콘솔에 출력합니다. 디버깅은 SDK가 설정한 규칙 및 데이터 요소에 따라 작동하는 방식을 이해하려 할 때 유용합니다.

디버깅은 기본적으로 비활성화되어 있지만 네 가지 방법으로 전환할 수 있습니다. 이러한 메서드를 조합하여 사용하면 개발 워크플로에서 가장 편리한 디버깅을 활성화하거나 비활성화할 수 있습니다.

## 사용 `debugEnabled` 다음에서 `configure` 명령

설정 `debugEnabled` 확장을 구성할 때 부울을 true로 설정합니다. 이 옵션은 사이트의 페이지를 방문하는 모든 사람에게 디버깅을 사용할 수 있으므로 일반적으로 개발 환경에 사용됩니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

다음을 참조하십시오 [`debugEnabled`](../commands/configure/debugenabled.md) 추가 정보.

## 사용 `setDebug` 명령

위의 부울과 유사하게, 이 명령은 페이지의 모든 방문자에 대해 디버깅을 활성화합니다.

```js
alloy("setDebug", {"enabled": true});
```

다음을 참조하십시오. [`setDebug`](../commands/setdebug.md) 명령 을 참조하십시오.

## 쿼리 문자열 매개 변수 설정

쿼리 문자열을 추가하여 디버깅을 활성화할 수 있습니다 `?alloy_debug=true` 를 입력합니다. 예:

`http://example.com/?alloy_debug=true`

이 메서드는 로컬 컴퓨터에만 적용되므로 모든 사용자에 대해 디버깅을 활성화하지 않고 프로덕션 웹 사이트를 디버깅할 수 있습니다. 이러한 방식으로 디버깅을 활성화하면 나머지 탐색 세션에 대해 또는 비활성화할 때까지 계속 유지됩니다.

## Adobe Experience Platform Debugger 사용

Adobe Experience Platform Debugger은 웹 페이지를 검사하고 Experience Cloud 제품 구현을 디버깅하는 데 도움이 되는 강력한 도구입니다. AEP 웹 SDK 섹션의 구성 탭에서 디버깅을 활성화할 수 있습니다.

![디버거 활성화](../assets/enable-debugging.png)

다음을 참조하십시오 [Adobe Experience Platform Debugger 개요](/help/debugger/home.md) 추가 정보.
