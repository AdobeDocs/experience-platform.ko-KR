---
title: downloadLinkQualifier
description: 자동 링크 추적이 다운로드 링크를 정규화하는 방법을 결정하는 데 도움이 됩니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

다음을 사용하여 자동 링크 추적을 활성화하는 경우 [`clickCollectionEnabled`](clickcollectionenabled.md), `downloadLinkQualifier` 속성은 다운로드 링크로 간주되는 URL의 기준을 결정하는 데 도움이 됩니다.

이 속성은 정규 표현식 문자열입니다. 클릭한 URL이 이 정규 표현식과 일치하면 `xdm.web.webInteraction.type` 이(가) (으)로 설정됨 `"download"`. 또한 링크가 다음을 포함하는 경우 즉시 다운로드 링크로 분류됩니다. `download` HTML 특성입니다. If `clickCollectionEnabled` 이 활성화되지 않은 경우 이 속성은 아무 작업도 하지 않습니다.

## 웹 SDK 태그 확장을 사용한 링크 한정자 다운로드

활성화 **[!UICONTROL 클릭 데이터 수집 활성화]** 확인란을 선택한 다음 아래에 원하는 텍스트를 입력합니다. **[!UICONTROL 다운로드 링크 한정자]** 조건 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 데이터 수집] 섹션을 선택한 다음 확인란을 선택합니다 **[!UICONTROL 클릭 데이터 수집 활성화]**.
1. 활성화하면 **[!UICONTROL 다운로드 링크 한정자]** 텍스트 상자가 나타납니다. 원하는 값을 입력합니다. 정규 표현식을 테스트하고 기본값을 복원하는 데 사용할 수도 있습니다.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 링크 한정자 다운로드

설정 `downloadLinkQualifier` 문자열을 실행할 때 `configure` 명령입니다. 이 등록 정보를 생략하면 기본값은 다음 값으로 설정됩니다.

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

다른 기준을 사용하여 다운로드 링크를 자격을 부여하려면 이 속성을 원하는 정규 표현식 값으로 설정합니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
