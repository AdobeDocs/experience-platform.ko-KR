---
title: edgeBasePath
description: Adobe 서비스와 상호 작용하는 데 사용되는 끝점의 기본 경로입니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

다음 `edgeBasePath` 속성은 Adobe 서비스와 상호 작용할 때 대상 경로를 변경합니다. 대부분의 조직에서는 이 속성을 설정하거나 변경할 필요가 없습니다.

## 웹 SDK 태그 확장을 사용한 Edge 기본 경로

에 원하는 텍스트를 입력합니다. **[!UICONTROL 가장자리 기준 경로]** 텍스트 필드 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 고급 설정] 섹션에 원하는 값을 입력합니다. **[!UICONTROL 가장자리 기준 경로]** 텍스트 필드.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하는 Edge 기본 경로

설정 `edgeBasePath` 다음을 실행할 때 텍스트 필드 `configure` 명령입니다. 이 속성을 생략하면 기본값은 `ee`. Adobe은 대부분의 구성에서 이 속성을 생략하는 것을 권장합니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
