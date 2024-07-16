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

`renderDecisions` 속성을 사용하면 웹 SDK에서 자동 렌더링에 적합한 개인화된 콘텐츠를 강제로 렌더링할 수 있습니다.

## 웹 SDK 태그 확장을 사용하여 개인화된 콘텐츠 렌더링

태그 규칙 동작 내에서 **[!UICONTROL 시각적 개인화 결정 렌더링]** 확인란을 선택합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 작업]에서 기존 작업을 선택하거나 작업을 만드십시오.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 이벤트 보내기]**(으)로 설정합니다.
1. [!UICONTROL Personalization] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL 시각적 개인화 결정 렌더링]** 확인란을 선택하십시오.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

## 웹 SDK JavaScript 라이브러리를 사용하여 개인화된 콘텐츠 렌더링

`sendEvent` 명령을 실행할 때 `renderDecisions` 부울을 설정합니다. 생략하면 이 속성은 기본적으로 `false`(으)로 설정됩니다. 개인화된 콘텐츠를 자동으로 렌더링하려면 이 속성을 `true`(으)로 설정하십시오.

>[!IMPORTANT]
>
>`renderDecisions` 속성이 [`documentUnloading`](documentunloading.md) 속성과 호환되지 않습니다. 두 속성을 동시에 `true`(으)로 설정하면 안 됩니다.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
