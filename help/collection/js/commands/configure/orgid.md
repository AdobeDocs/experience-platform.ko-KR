---
title: orgId
description: orgId 속성은 데이터가 전송되는 조직을 Adobe에 알려 주는 문자열입니다.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

`orgId` 속성은 데이터가 전송되는 조직을 Adobe에 알려 주는 문자열입니다. **이 속성은 웹 SDK을 사용하여 보낸 모든 데이터에 필요합니다.**

`orgID` 찾기

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. Adobe Experience Cloud 내의 어디에서나 **`[Ctrl]`** + **`[I]`**&#x200B;을(를) 누릅니다. [!UICONTROL User Data Debugger] 창이 열립니다.
1. **[!UICONTROL Copy]** 옆에 있는 ![&#x200B; &#x200B;](../../assets/copy.png)복사[!UICONTROL Current Org ID]를 클릭하거나 **[!UICONTROL Assigned Orgs]** 탭을 클릭하여 액세스할 수 있는 다른 조직 ID를 확인합니다.
1. 원하는 정보를 찾으면 **[!UICONTROL Close]**&#x200B;을(를) 클릭합니다.

조직 ID는 항상 24자의 영숫자 문자열이며, 항상 `@AdobeOrg`로 끝납니다.

`orgId` 명령을 실행할 때 `configure` 문자열을 설정합니다. 웹 SDK을 구성할 때 이 속성을 생략하면 웹 SDK에 콘솔 오류가 발생하고 데이터가 Adobe으로 전송되지 않습니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## 웹 SDK 태그 확장을 사용하여 조직 ID 설정

이 설정은 [SDK 인스턴스 구성 설정](/help/tags/extensions/client/web-sdk/configure/general.md)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다. 필드는 태그 속성이 작성된 조직을 기반으로 자동으로 채워집니다.
