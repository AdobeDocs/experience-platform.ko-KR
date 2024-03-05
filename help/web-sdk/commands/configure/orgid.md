---
title: orgId
description: orgId 속성은 데이터가 전송되는 조직을 Adobe에게 알려 주는 문자열입니다.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

다음 `orgId` 속성은 데이터가 전송되는 조직을 Adobe에게 알려 주는 문자열입니다. **이 속성은 웹 SDK를 사용하여 전송되는 모든 데이터에 필요합니다.**

를 찾으려면 `orgID`:

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. Adobe Experience Cloud 내 어디에서든 **`[Ctrl]`** + **`[I]`**. A [!UICONTROL 사용자 데이터 디버거] 창이 열립니다.
1. 클릭 **[!UICONTROL 복사]** ![복사](../../assets/copy.png) 다음 옆에 [!UICONTROL 현재 조직 ID]을 클릭하거나 **[!UICONTROL 할당된 조직]** 탭으로 이동하여 액세스할 수 있는 다른 조직 ID를 확인합니다.
1. 원하는 정보를 찾으면 **[!UICONTROL 닫기]**.

조직 ID는 항상 24자의 영숫자 문자열이며, 항상 로 끝납니다. `@AdobeOrg`.

## 구성 `orgID` Web SDK 태그 확장 사용

조직 ID를 입력합니다. **[!UICONTROL IMS 조직 ID]** 텍스트 필드 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 원하는 조직 ID를 [!UICONTROL IMS 조직 ID] 상단 근처에 있는 텍스트 필드.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 구성 `orgID` 웹 SDK JavaScript 라이브러리 사용

설정 `orgId` 문자열을 실행할 때 `configure` 명령입니다. 웹 SDK를 구성할 때 이 속성을 생략하면 웹 SDK에 콘솔 오류가 발생하고 데이터가 Adobe으로 전송되지 않습니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
