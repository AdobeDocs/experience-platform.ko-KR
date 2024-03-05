---
title: target마이그레이션 활성화됨
description: Web SDK에서 Adobe Target 쿠키를 읽고 쓸 수 있도록 허용합니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

다음 `targetMigrationEnabled` 속성은 Web SDK가 Adobe Target 1.x 및 2.x 라이브러리에서 사용하는 mbox 및 mboxEdgeCluster 쿠키를 읽고 쓸 수 있도록 하는 부울입니다. 이 옵션을 사용하면 이전 Adobe Target 구현을 사용하는 페이지와 웹 SDK를 사용하는 페이지 간에 방문자 프로필을 유지할 수 있습니다.

## Web SDK 태그 확장을 사용하여 at.js에서 Target 마이그레이션 활성화

다음 항목 선택 **[!UICONTROL Target을 at.js에서 Web SDK로 마이그레이션]** 다음과 같은 경우 확인란 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 개인화] 섹션을 선택한 다음 확인란을 선택합니다 **[!UICONTROL Target을 at.js에서 Web SDK로 마이그레이션]**.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 at.js에서 Target 마이그레이션 활성화

설정 `targetMigrationEnabled` 를 실행할 때 부울 `configure` 명령입니다. Web SDK를 구성할 때 이 속성을 생략하면 기본값이 로 설정됩니다. `false`. 이 값을 다음으로 설정 `true` 일부 페이지에서 여전히 Adobe Target 1.x 또는 2.x 라이브러리를 사용하고 있는 경우.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
