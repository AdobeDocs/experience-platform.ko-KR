---
title: eventType
description: sendEvent 호출에 대한 이벤트 유형을 설정합니다.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

다음 `eventType` 속성을 사용하면 웹 SDK를 사용하여 전송하는 이벤트 유형을 정의할 수 있습니다. 이 필드는 궁극적으로 다음을 채웁니다. `xdm.eventType` 필드. Adobe에 보내는 이벤트 유형을 구분하려는 경우 유용합니다.

Adobe은 사용할 수 있는 사전 정의된 이벤트 유형을 제공합니다. 다음을 참조하십시오 [사용 가능한 값 `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) 사전 정의된 값의 전체 목록은 XDM 사용 안내서에서 참조하십시오. 원하는 경우 고유한 값을 사용할 수도 있습니다.

두 가지를 모두 설정하면 `type` 여기 및 `xdm.eventType` 다음에서 [`xdm`](xdm.md) 이 필드의 값이 우선합니다.

## 웹 SDK 태그 확장을 사용하여 이벤트 유형 구성

설정 **[!UICONTROL 유형]** 태그 규칙 작업 내의 드롭다운 필드입니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 이벤트 보내기]**.
1. 아래 드롭다운을 사용합니다. **[!UICONTROL 유형]** 필드를 입력하거나 고유한 값을 입력합니다.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 이벤트 유형 구성

설정 `eventType` 문자열 속성을 사용하여 `sendEvent` 명령입니다.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
