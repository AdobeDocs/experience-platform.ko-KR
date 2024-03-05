---
title: debugEnable
description: 코드를 사용하여 Web SDK에서 디버깅 기능을 활성화합니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

다음 `debugEnabled` 속성을 사용하면 웹 SDK 코드를 사용하여 디버깅을 활성화하거나 비활성화할 수 있습니다. 를 활성화하는 사용 가능한 방법 중 하나입니다 [디버깅](../../use-cases/debugging.md). 항상 디버깅을 활성화하려는 경우 웹 사이트 개발 중에 구현 내에서 디버깅을 활성화하면 다른 방법보다 편리할 수 있습니다. 이 디버깅 방법은 모든 방문자에 대해 활성화하므로 프로덕션 페이지에는 권장되지 않습니다.

다음을 참조하십시오. [디버깅](../../use-cases/debugging.md) 디버깅을 활성화하는 더 많은 방법에 대해서는 사용 사례 페이지를 참조하십시오.

## 웹 SDK 태그 확장을 사용하여 디버깅 활성화

Web SDK 태그 확장을 기본적으로 사용하여 사용할 수 있는 디버깅 옵션은 없습니다. 사용 [대체 디버깅 방법](../../use-cases/debugging.md).

## 웹 SDK JavaScript 라이브러리를 사용하여 디버깅 활성화

설정 `debugEnabled` 부울 변환 `true` 를 실행할 때 `configure` 명령입니다. SDK를 구성할 때 이 속성을 생략하면 기본값이 로 설정됩니다. `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
