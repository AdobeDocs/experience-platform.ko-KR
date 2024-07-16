---
title: idMigrationEnabled
description: Web SDK가 AMCV 쿠키를 읽을 수 있도록 합니다.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled` 속성을 사용하면 Web SDK에서 이전 Adobe Experience Cloud 구현에서 설정한 AMCV 쿠키를 읽을 수 있습니다. 조직에서 구현을 웹 SDK로 업그레이드하는 경우 이 설정을 사용하면 현재 Adobe Experience Cloud ID 서비스로 더 원활하게 전환할 수 있습니다. 이 설정은 Web SDK로 업그레이드할 때 고유 방문자 수가 급격히 증가하지 않도록 매우 중요합니다.

조직에서 새로운 웹 SDK 구현을 실행하는 경우 이 설정을 활성화해도 데이터 수집 또는 방문자 식별에는 영향을 주지 않습니다. 모든 구현에 대해 이 기능을 활성화한 상태로 두는 단점이 없습니다.

## 웹 SDK 태그 확장을 사용하여 ID 마이그레이션 활성화

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL VisitorAPI에서 웹 SDK로 ECID 마이그레이션]** 확인란을 선택합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL ID] 섹션을 찾은 다음 **[!UICONTROL VisitorAPI에서 웹 SDK로 ECID 마이그레이션]** 확인란을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 ID 마이그레이션 활성화

`configure` 명령을 실행할 때 `idMigrationEnabled` 부울을 설정합니다. Web SDK를 구성할 때 이 속성을 생략하면 기본적으로 `true`(으)로 설정됩니다. 방문자 API에서 설정한 AMCV 쿠키를 읽는 기능을 비활성화하려면 이 속성을 설정합니다. 대부분의 조직에서는 이 속성을 설정할 필요가 없습니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
