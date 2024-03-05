---
title: idMigrationEnabled
description: Web SDK가 AMCV 쿠키를 읽을 수 있도록 합니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

다음 `idMigrationEnabled` 속성을 사용하면 웹 SDK에서 이전 Adobe Experience Cloud 구현에서 설정한 AMCV 쿠키를 읽을 수 있습니다. 조직에서 구현을 웹 SDK로 업그레이드하는 경우 이 설정을 사용하면 현재 Adobe Experience Cloud ID 서비스로 더 원활하게 전환할 수 있습니다. 이 설정은 Web SDK로 업그레이드할 때 고유 방문자 수가 급격히 증가하지 않도록 매우 중요합니다.

조직에서 새로운 웹 SDK 구현을 실행하는 경우 이 설정을 활성화해도 데이터 수집 또는 방문자 식별에는 영향을 주지 않습니다. 모든 구현에 대해 이 기능을 활성화한 상태로 두는 단점이 없습니다.

## 웹 SDK 태그 확장을 사용하여 ID 마이그레이션 활성화

다음 항목 선택 **[!UICONTROL VisitorAPI에서 웹 SDK로 ECID 마이그레이션]** 다음과 같은 경우 확인란 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 를 찾습니다. [!UICONTROL 신원] 섹션을 선택한 다음 확인란을 선택합니다 **[!UICONTROL VisitorAPI에서 웹 SDK로 ECID 마이그레이션]**.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 ID 마이그레이션 활성화

설정 `idMigrationEnabled` 를 실행할 때 부울 `configure` 명령입니다. Web SDK를 구성할 때 이 속성을 생략하면 기본값이 로 설정됩니다. `true`. 방문자 API에서 설정한 AMCV 쿠키를 읽는 기능을 비활성화하려면 이 속성을 설정합니다. 대부분의 조직에서는 이 속성을 설정할 필요가 없습니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
