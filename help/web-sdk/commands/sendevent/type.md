---
title: eventType
description: sendEvent 호출에 대한 이벤트 유형을 설정합니다.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

`eventType` 속성을 사용하면 웹 SDK를 사용하여 보내는 이벤트 유형을 정의할 수 있습니다. 이 필드는 궁극적으로 `xdm.eventType` 필드를 채웁니다. Adobe에 보내는 이벤트 유형을 구분하려는 경우 유용합니다.

Adobe은 사용할 수 있는 사전 정의된 이벤트 유형을 제공합니다. 미리 정의된 값의 전체 목록은 XDM 사용 안내서의 `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)에 대해 사용 가능한 [값을 참조하십시오. 원하는 경우 고유한 값을 사용할 수도 있습니다.

여기에서 `type`을(를) 설정하고 [`xdm`](xdm.md) 개체에서 `xdm.eventType`을(를) 모두 설정하는 경우 이 필드의 값이 우선합니다.

## 웹 SDK 태그 확장을 사용하여 이벤트 유형 구성

태그 규칙 작업 내에서 **[!UICONTROL Type]** 드롭다운 필드를 설정합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 작업]에서 기존 작업을 선택하거나 작업을 만드십시오.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 이벤트 보내기]**(으)로 설정합니다.
1. **[!UICONTROL Type]** 필드 아래의 드롭다운을 사용하거나 고유한 값을 입력하십시오.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

## 웹 SDK JavaScript 라이브러리를 사용하여 이벤트 유형 구성

`sendEvent` 명령을 실행할 때 `eventType` 문자열 속성을 설정하십시오.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
