---
title: prehidingStyle
description: 개인화된 콘텐츠를 깜박임 없이 로드할 수 있는 CSS 정의를 만듭니다.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

`prehidingStyle` 속성을 사용하면 CSS 선택기를 정의하여 개인화된 콘텐츠가 로드될 때까지 숨길 수 있습니다. 이 속성은 깜박임을 방지하기 위해 동기식 웹 SDK 구현에서 유용합니다. Adobe 비동기 웹 SDK 구현을 위해 [코드 조각 사전 숨김](../../personalization/manage-flicker.md)을 사용하는 것이 좋습니다.

이 속성에서 정의하는 CSS 선택기는 페이지에서 첫 번째 [`sendEvent`](../sendevent/overview.md) 명령을 실행할 때 콘텐츠를 숨깁니다. 일반적으로 개인화된 컨텐츠를 포함하는 Adobe에서 응답을 받으면 컨텐츠는 표시되지 않습니다. `sendEvent` 명령이 실패하거나 시간이 초과되면 콘텐츠도 숨김 취소됩니다.

구현에 `prehidingStyle`과(와) 코드 조각 사전 숨김을 모두 포함하는 경우 코드 조각 사전 숨김이 이 구성 속성보다 우선합니다.

## 웹 SDK 태그 확장을 사용하여 스타일 미리 숨기기

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL 스타일 미리 숨기기 제공]** 단추를 선택합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL Personalization] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL 미리 숨기는 스타일 제공]** 단추를 선택합니다.
1. 이 버튼은 CSS 편집기가 있는 모달 창을 엽니다. 원하는 CSS 선택기와 선언 블록을 삽입한 다음 **[!UICONTROL 저장]**&#x200B;을 클릭하여 모달 창을 닫습니다.
1. 확장 설정에서 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 스타일 미리 숨기기

`configure` 명령을 실행할 때 `prehidingStyle` 문자열을 설정합니다. Web SDK를 구성할 때 이 속성을 생략하면 페이지에서 첫 번째 `sendEvent` 명령을 실행할 때 아무것도 숨겨지지 않습니다. 이 값을 동기적으로 로드된 라이브러리에 대해 원하는 CSS 선택기 및 선언 블록으로 설정합니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```
