---
title: prehidingStyle
description: 개인화된 콘텐츠를 깜박임 없이 로드할 수 있는 CSS 정의를 만듭니다.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

다음 `prehidingStyle` 속성을 사용하면 CSS 선택기를 정의하여 개인화된 콘텐츠가 로드될 때까지 숨길 수 있습니다. 이 속성은 깜박임을 방지하기 위해 동기식 웹 SDK 구현에서 유용합니다. Adobe은 [코드 조각 사전 숨김](../../personalization/manage-flicker.md) 비동기 Web SDK 구현의 경우.

이 속성에서 정의하는 CSS 선택기는 첫 번째 를 실행할 때 콘텐츠를 숨깁니다 [`sendEvent`](../sendevent/overview.md) 페이지의 명령입니다. 일반적으로 개인화된 컨텐츠를 포함하는 Adobe에서 응답을 받으면 컨텐츠는 표시되지 않습니다. 다음과 같은 경우에도 콘텐츠가 숨김 취소됩니다. `sendEvent` 명령이 실패하거나 시간이 초과됩니다.

두 가지를 모두 포함하는 경우 `prehidingStyle` 또한 구현에서 코드 조각 사전 숨김을 사용하는 경우에는 코드 조각 사전 숨김이 이 구성 속성보다 우선합니다.

## 웹 SDK 태그 확장을 사용하여 스타일 미리 숨기기

다음 항목 선택 **[!UICONTROL 사전 숨김 스타일 제공]** 단추 조건 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 개인화] 섹션을 선택한 다음 버튼을 선택합니다 **[!UICONTROL 사전 숨김 스타일 제공]**.
1. 이 버튼은 CSS 편집기가 있는 모달 창을 엽니다. 원하는 CSS 선택기와 선언 블록을 삽입한 다음 를 클릭합니다 **[!UICONTROL 저장]** 모달 창을 닫습니다.
1. 클릭 **[!UICONTROL 저장]** 확장 설정에서 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 스타일 미리 숨기기

설정 `prehidingStyle` 문자열을 실행할 때 `configure` 명령입니다. Web SDK를 구성할 때 이 속성을 생략하면 첫 번째 `sendEvent` 페이지의 명령입니다. 이 값을 동기적으로 로드된 라이브러리에 대해 원하는 CSS 선택기 및 선언 블록으로 설정합니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
