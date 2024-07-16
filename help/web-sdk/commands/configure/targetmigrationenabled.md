---
title: target마이그레이션 활성화됨
description: Web SDK에서 Adobe Target 쿠키를 읽고 쓸 수 있도록 허용합니다.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

`targetMigrationEnabled` 속성은 Web SDK가 Adobe Target 1.x 및 2.x 라이브러리에서 사용하는 mbox 및 mboxEdgeCluster 쿠키를 읽고 쓸 수 있는 부울입니다. 이 옵션을 사용하면 이전 Adobe Target 구현을 사용하는 페이지와 웹 SDK를 사용하는 페이지 간에 방문자 프로필을 유지할 수 있습니다.

## Web SDK 태그 확장을 사용하여 at.js에서 Target 마이그레이션 활성화

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL Target을 at.js에서 Web SDK로 마이그레이션]** 확인란을 선택하십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL Personalization] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL at.js에서 Web SDK로 Target 마이그레이션]** 확인란을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 at.js에서 Target 마이그레이션 활성화

`configure` 명령을 실행할 때 `targetMigrationEnabled` 부울을 설정합니다. Web SDK를 구성할 때 이 속성을 생략하면 기본적으로 `false`(으)로 설정됩니다. Adobe Target 1.x 또는 2.x 라이브러리를 계속 사용하는 페이지가 있는 경우 이 값을 `true`(으)로 설정하십시오.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
