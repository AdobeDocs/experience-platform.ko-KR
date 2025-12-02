---
title: documentUnload
description: JavaScript sendBeacon API를 사용하여 Adobe으로 데이터를 전송합니다.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

`documentUnloading` 속성을 사용하면 JavaScript의 [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) 메서드를 사용하여 Adobe으로 데이터를 보낼 수 있습니다. 일반적인 요청이 너무 오래 걸리는 경우 브라우저가 요청을 취소할 수 있습니다. 웹 SDK에 `sendBeacon`을(를) 사용하도록 요청하면 페이지에서 멀어진 후 요청이 백그라운드에서 실행됩니다. 데이터 요청을 언로드할 때 브라우저가 취소하지 않도록 하려면 이 속성을 활성화하십시오.

일부 브라우저에서는 한 번에 `sendBeacon`을(를) 사용하여 전송할 수 있는 데이터 양에 64KB의 제한을 적용합니다. 페이로드가 너무 크기 때문에 브라우저가 이벤트를 거부하면 웹 SDK은 일반적인 전송 메서드를 사용하는 것으로 돌아갑니다. 주어진 브라우저에서 더 큰 페이로드를 허용하더라도 Adobe 데이터 수집 서버는 페이로드를 64KB까지 잘라냅니다.

`documentUnloading` 명령을 실행할 때 `sendEvent` 부울을 설정합니다. 기본값은 `false`입니다. `true` 메서드를 사용하여 Adobe으로 데이터를 전송하려면 이 속성을 `sendBeacon`(으)로 설정하십시오.

>[!IMPORTANT]
>
>`documentUnloading` 속성이 [`renderDecisions`](renderdecisions.md) 속성과 호환되지 않습니다. 두 속성을 동시에 `true`(으)로 설정하지 마십시오.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## 웹 SDK 태그 확장을 사용하여 문서 언로드

**[!UICONTROL Document will unload]** 확인란은 웹 SDK 태그 확장을 사용할 때 [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) 작업을 구성할 때 사용할 수 있습니다.
