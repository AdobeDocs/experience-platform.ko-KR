---
title: idMigrationEnabled
description: 웹 SDK에서 AMCV 쿠키를 읽을 수 있도록 합니다.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled` 속성을 사용하면 웹 SDK에서 이전 Adobe Experience Cloud 구현에서 설정한 AMCV 쿠키를 읽을 수 있습니다. 조직에서 구현을 웹 SDK으로 업그레이드하는 경우 이 설정을 사용하면 현재 Adobe Experience Cloud ID 서비스로 더 원활하게 전환할 수 있습니다. 이 설정은 웹 SDK으로 업그레이드할 때 고유 방문자 수가 급격히 증가하지 않도록 매우 중요합니다.

조직에서 새로운 웹 SDK 구현을 실행하는 경우 이 설정을 활성화해도 데이터 수집이나 방문자 식별에는 영향을 주지 않습니다. 모든 구현에 대해 이 기능을 활성화한 상태로 두는 단점이 없습니다.

`idMigrationEnabled` 명령을 실행할 때 `configure` 부울을 설정합니다. 웹 SDK을 구성할 때 이 속성을 생략하면 기본적으로 `true`이(가) 됩니다. 방문자 API에서 설정한 AMCV 쿠키를 읽는 기능을 비활성화하려면 이 속성을 설정합니다. 대부분의 조직에서는 이 속성을 설정할 필요가 없습니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## 웹 SDK 태그 확장을 사용하여 방문자 ID 마이그레이션 활성화

이러한 설정은 [ID 구성 설정](/help/tags/extensions/client/web-sdk/configure/identity.md)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다.
