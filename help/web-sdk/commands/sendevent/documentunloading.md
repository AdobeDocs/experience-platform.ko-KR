---
title: documentUnload
description: JavaScript sendBeacon API를 사용하여 데이터를 Adobe으로 전송합니다.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

다음 `documentUnloading` 속성을 사용하면 JavaScript [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) Adobe에 데이터를 보내는 방법. 일반적인 요청이 너무 오래 걸리는 경우 브라우저가 요청을 취소할 수 있습니다. 웹 SDK에 다음을 사용하도록 지시할 수 있습니다. `sendBeacon` 따라서 페이지에서 멀리 탐색한 후 요청이 백그라운드에서 실행됩니다. 데이터 요청을 언로드할 때 브라우저가 취소하지 않도록 하려면 이 속성을 활성화하십시오.

일부 브라우저에서는 전송할 수 있는 데이터 양에 64KB의 제한을 부과합니다. `sendBeacon` 한 번에. 페이로드가 너무 크기 때문에 브라우저가 이벤트를 거부하면 웹 SDK는 일반적인 전송 메서드를 사용하는 것으로 돌아갑니다.

## 웹 SDK 태그 확장을 사용하여 문서 언로드 구성

활성화 **[!UICONTROL 문서가 언로드됩니다.]** 확인란을 선택할 수 있습니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 이벤트 보내기]**.
1. 활성화 **[!UICONTROL 문서가 언로드됩니다.]** 의 확인란 [!UICONTROL 데이터] 섹션.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 문서 언로드 구성

설정 `documentUnloading` 를 실행할 때 부울 `sendEvent` 명령입니다. 기본값은 입니다 `false`. 이 속성을 다음으로 설정 `true` 을(를) 사용하려면 `sendBeacon` Adobe에 데이터를 보내는 방법.

>[!IMPORTANT]
>
>다음 `documentUnloading` 속성이 과(와) 호환되지 않음 [`renderDecisions`](renderdecisions.md) 속성. 두 속성을 모두 로 설정하면 안 됩니다. `true` 동시에.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
