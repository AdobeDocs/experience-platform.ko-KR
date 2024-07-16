---
title: documentUnload
description: JavaScript sendBeacon API를 사용하여 Adobe으로 데이터를 전송합니다.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

`documentUnloading` 속성을 사용하면 JavaScript의 [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) 메서드를 사용하여 데이터를 Adobe으로 보낼 수 있습니다. 일반적인 요청이 너무 오래 걸리는 경우 브라우저가 요청을 취소할 수 있습니다. 웹 SDK에 `sendBeacon`을(를) 사용하도록 지정하여 페이지에서 멀어진 후 요청이 백그라운드에서 실행되도록 할 수 있습니다. 데이터 요청을 언로드할 때 브라우저가 취소하지 않도록 하려면 이 속성을 활성화하십시오.

일부 브라우저에서는 한 번에 `sendBeacon`을(를) 사용하여 전송할 수 있는 데이터 양에 64KB의 제한을 적용합니다. 페이로드가 너무 크기 때문에 브라우저가 이벤트를 거부하면 웹 SDK는 일반적인 전송 메서드를 사용하는 것으로 돌아갑니다.

## 웹 SDK 태그 확장을 사용하여 문서 언로드 구성

태그 규칙의 동작 내에서 **[!UICONTROL 문서가 언로드됨]** 확인란을 사용하도록 설정합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 작업]에서 기존 작업을 선택하거나 작업을 만드십시오.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 이벤트 보내기]**(으)로 설정합니다.
1. [!UICONTROL 데이터] 섹션에서 **[!UICONTROL 문서가 언로드]** 확인란을 사용하도록 설정합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

## 웹 SDK JavaScript 라이브러리를 사용하여 문서 언로드 구성

`sendEvent` 명령을 실행할 때 `documentUnloading` 부울을 설정합니다. 기본값은 `false`입니다. `sendBeacon` 메서드를 사용하여 데이터를 Adobe으로 보내려면 이 속성을 `true`(으)로 설정하십시오.

>[!IMPORTANT]
>
>`documentUnloading` 속성이 [`renderDecisions`](renderdecisions.md) 속성과 호환되지 않습니다. 두 속성을 동시에 `true`(으)로 설정하면 안 됩니다.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
