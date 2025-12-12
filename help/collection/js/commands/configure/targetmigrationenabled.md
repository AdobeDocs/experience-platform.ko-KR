---
title: target마이그레이션 활성화됨
description: 웹 SDK에서 Adobe Target 쿠키를 읽고 쓸 수 있도록 허용합니다.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 051374def898d3797711525c5343e0a8454970a2
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# `targetMigrationEnabled`

`targetMigrationEnabled` 속성은 웹 SDK에서 Adobe Target 1.x 및 2.x 라이브러리가 사용하는 [`mbox` 및 `mboxEdgeCluster` 쿠키](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)를 읽고 쓸 수 있도록 하는 부울입니다. 이 옵션을 사용하면 이전 Adobe Target 구현을 사용하는 페이지와 웹 SDK을 사용하는 페이지 간에 방문자 프로필을 유지할 수 있습니다.

`targetMigrationEnabled` 명령을 실행할 때 `configure` 부울을 설정합니다. 웹 SDK을 구성할 때 이 속성을 생략하면 기본적으로 `false`이(가) 됩니다. Adobe Target 1.x 또는 2.x 라이브러리를 계속 사용하는 페이지가 있는 경우 이 값을 `true`(으)로 설정하십시오.

이 속성을 사용할 때는 Adobe Target 구현 내에서 [`overrideMboxEdgeServer`의 ](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver)`targetGlobalSettings()`도 사용하도록 설정해야 합니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## 웹 SDK 태그 확장을 사용하여 Target 마이그레이션 활성화

이 설정은 [Personalization 구성 설정](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다.
