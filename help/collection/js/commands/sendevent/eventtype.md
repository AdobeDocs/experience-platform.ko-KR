---
title: eventType
description: sendEvent 호출에 대한 이벤트 유형을 설정합니다.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

`eventType` 속성을 사용하면 웹 SDK을 사용하여 보내는 이벤트 유형을 정의할 수 있습니다. 이 필드는 궁극적으로 `xdm.eventType` 필드를 채웁니다. Adobe으로 보내는 이벤트 유형을 구분하려는 경우 유용합니다.

Adobe에서는 사용할 수 있는 사전 정의된 이벤트 유형을 제공합니다. 미리 정의된 값의 전체 목록은 XDM 사용 안내서의 [에 대해 사용 가능한 `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)값을 참조하십시오. 원하는 경우 고유한 값을 사용할 수도 있습니다.

여기에서 `type`을(를) 설정하고 `xdm.eventType` 개체에서 [`xdm`](xdm.md)을(를) 모두 설정하는 경우 이 필드의 값이 우선합니다.

`eventType` 명령을 실행할 때 `sendEvent` 문자열 속성을 설정하십시오.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## 웹 SDK 태그 확장을 사용한 이벤트 유형

&#39;[**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields)&#39; 작업을 구성할 때 이 속성에 해당하는 웹 SDK 태그 확장은 [!UICONTROL Send event] 드롭다운 메뉴입니다.
