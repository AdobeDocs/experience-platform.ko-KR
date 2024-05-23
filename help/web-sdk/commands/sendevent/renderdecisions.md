---
title: renderDecisions
description: 자동 렌더링에 적합한 개인화된 콘텐츠를 렌더링합니다.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

다음 `renderDecisions` 속성을 사용하면 웹 SDK에서 자동 렌더링에 적합한 개인화된 콘텐츠를 강제로 렌더링할 수 있습니다.

## 웹 SDK 태그 확장을 사용하여 개인화된 콘텐츠 렌더링

다음 항목 선택 **[!UICONTROL 시각적 개인화 결정 렌더링]** 확인란을 선택할 수 있습니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 이벤트 보내기]**.
1. 아래로 스크롤하여 [!UICONTROL 개인화] 섹션을 선택한 다음 **[!UICONTROL 시각적 개인화 결정 렌더링]** 확인란.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 개인화된 콘텐츠 렌더링

설정 `renderDecisions` 를 실행할 때 부울 `sendEvent` 명령입니다. 생략하면 이 속성의 기본값은 `false`. 이 속성을 다음으로 설정 `true` 개인화된 콘텐츠를 자동으로 렌더링하려는 경우.

>[!IMPORTANT]
>
>다음 `renderDecisions` 속성이 과(와) 호환되지 않음 [`documentUnloading`](documentunloading.md) 속성. 두 속성을 모두 로 설정하면 안 됩니다. `true` 동시에.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
