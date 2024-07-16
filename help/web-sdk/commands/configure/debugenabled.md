---
title: debugEnable
description: 코드를 사용하여 Web SDK에서 디버깅 기능을 활성화합니다.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

`debugEnabled` 속성을 사용하면 웹 SDK 코드를 사용하여 디버깅을 활성화하거나 비활성화할 수 있습니다. 이 방법은 [디버깅](../../use-cases/debugging.md)을 사용하도록 설정하는 방법 중 하나입니다. 항상 디버깅을 활성화하려는 경우 웹 사이트 개발 중에 구현 내에서 디버깅을 활성화하면 다른 방법보다 편리할 수 있습니다. 이 디버깅 방법은 모든 방문자에 대해 활성화하므로 프로덕션 페이지에는 권장되지 않습니다.

디버깅을 사용할 수 있는 자세한 방법은 [디버깅](../../use-cases/debugging.md) 사용 사례 페이지를 참조하세요.

## 웹 SDK 태그 확장을 사용하여 디버깅 활성화

Web SDK 태그 확장을 기본적으로 사용하여 사용할 수 있는 디버깅 옵션은 없습니다. [대체 디버깅 메서드](../../use-cases/debugging.md)를 사용하십시오.

## 웹 SDK JavaScript 라이브러리를 사용하여 디버깅 사용

`configure` 명령을 실행할 때 `debugEnabled` 부울을 `true`(으)로 설정하십시오. SDK를 구성할 때 이 속성을 생략하면 기본값은 `false`입니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
