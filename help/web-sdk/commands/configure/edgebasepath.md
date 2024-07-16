---
title: edgeBasePath
description: Adobe 서비스와 상호 작용하는 데 사용되는 끝점의 기본 경로입니다.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

`edgeBasePath` 속성은 Adobe 서비스와 상호 작용할 때 대상 경로를 변경합니다. 대부분의 조직에서는 이 속성을 설정하거나 변경할 필요가 없습니다.

## 웹 SDK 태그 확장을 사용한 Edge 기본 경로

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL Edge 기본 경로]** 텍스트 필드에 원하는 텍스트를 입력합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 고급 설정] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL Edge 기본 경로]** 텍스트 필드에 원하는 값을 입력합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하는 Edge 기본 경로

`configure` 명령을 실행할 때 `edgeBasePath` 텍스트 필드를 설정하십시오. 이 속성을 생략하면 기본값은 `ee`입니다. Adobe은 대부분의 구성에서 이 속성을 생략하는 것을 권장합니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
