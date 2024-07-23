---
title: downloadLinkQualifier
description: 자동 링크 추적이 다운로드 링크를 정규화하는 방법을 결정하는 데 도움이 됩니다.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

[`clickCollectionEnabled`](clickcollectionenabled.md)을(를) 사용하여 자동 링크 추적을 사용하도록 설정하는 경우 `downloadLinkQualifier` 속성은 다운로드 링크로 간주되는 URL의 기준을 결정하는 데 도움이 됩니다.

이 속성은 정규 표현식 문자열입니다. 클릭한 URL이 이 정규식과 일치하면 `xdm.web.webInteraction.type`이(가) `"download"`(으)로 설정됩니다. 또한 `download` HTML 특성이 포함된 경우 링크는 즉시 다운로드 링크로 분류됩니다. `clickCollectionEnabled`을(를) 사용하지 않으면 이 속성은 아무 작업도 하지 않습니다.

## 웹 SDK 태그 확장을 사용한 링크 한정자 다운로드

**[!UICONTROL 클릭 데이터 수집 사용]** 확인란을 활성화한 다음 [태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL 링크 한정자 다운로드]**&#x200B;에 원하는 텍스트를 입력합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 데이터 수집] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL 데이터 수집 사용]** 확인란을 선택합니다.
1. 활성화하면 **[!UICONTROL 다운로드 링크 한정자]** 텍스트 상자가 나타납니다. 원하는 값을 입력합니다. 정규 표현식을 테스트하고 기본값을 복원하는 데 사용할 수도 있습니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 링크 한정자 다운로드

`configure` 명령을 실행할 때 `downloadLinkQualifier` 문자열을 설정합니다. 이 등록 정보를 생략하면 기본값은 다음 값으로 설정됩니다.

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

다른 기준을 사용하여 다운로드 링크를 자격을 부여하려면 이 속성을 원하는 정규 표현식 값으로 설정합니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
