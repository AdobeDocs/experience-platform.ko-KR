---
title: orgId
description: orgId 속성은 데이터가 전송되는 조직을 Adobe에게 알려 주는 문자열입니다.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

`orgId` 속성은 데이터를 보낼 조직을 Adobe에게 알려 주는 문자열입니다. **이 속성은 웹 SDK를 사용하여 보낸 모든 데이터에 필요합니다.**

`orgID` 찾기

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. Adobe Experience Cloud 내의 어디에서나 **`[Ctrl]`** + **`[I]`**&#x200B;을(를) 누릅니다. [!UICONTROL 사용자 데이터 디버거] 창이 열립니다.
1. [!UICONTROL 현재 조직 ID] 옆에 있는 **[!UICONTROL 복사]** ![복사](../../assets/copy.png)를 클릭하거나 **[!UICONTROL 할당된 조직]** 탭을 클릭하여 액세스할 수 있는 다른 조직 ID를 확인합니다.
1. 원하는 정보를 모두 찾으면 **[!UICONTROL 닫기]**&#x200B;를 클릭합니다.

조직 ID는 항상 24자의 영숫자 문자열이며, 항상 `@AdobeOrg`로 끝납니다.

## 웹 SDK 태그 확장을 사용하여 `orgID` 구성

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL IMS 조직 ID]** 텍스트 필드에 조직 ID를 입력하십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. 원하는 조직 ID를 맨 위의 [!UICONTROL IMS 조직 ID] 텍스트 필드에 입력합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 `orgID` 구성

`configure` 명령을 실행할 때 `orgId` 문자열을 설정합니다. 웹 SDK를 구성할 때 이 속성을 생략하면 웹 SDK에 콘솔 오류가 발생하고 데이터가 Adobe으로 전송되지 않습니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
