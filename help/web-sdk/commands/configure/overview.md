---
title: Adobe Experience Platform 웹 SDK 구성
description: 웹 SDK를 사용할 때 필요한 설정을 설정하려면 configure 명령을 사용하십시오.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Adobe Experience Platform 웹 SDK 구성

`configure` 명령을 사용하여 웹 SDK를 구성합니다. 웹 SDK 구성은 라이브러리 또는 태그 확장을 사용할 때마다 반드시 수행해야 하는 중요한 필수 단계입니다.

## 태그 확장을 사용하여 웹 SDK 구성 {#configure-tag-extension}

태그 확장을 통해 웹 SDK를 구성하려면 아래 단계를 따르십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. 모든 구성 옵션에 대한 자세한 내용을 보려면 [웹 SDK 태그 확장 구성 페이지](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)로 이동하십시오.

이러한 구성 설정은 확장을 사용하여 데이터를 Adobe으로 전송할 때마다 설정됩니다.

## JavaScript 라이브러리를 사용하여 웹 SDK 구성 {#configure-js}

`configure` 명령을 실행합니다. 이 명령은 [`sendEvent`](../sendevent/overview.md)과 같은 다른 웹 SDK 명령을 호출하기 전에 필요합니다.

[`datastreamId`](datastreamid.md) 및 [`orgId`](orgid.md) 속성이 필요합니다. 다른 모든 속성은 조직의 구현 요구 사항에 따라 선택 사항입니다.

지원되는 각 명령에 대한 자세한 내용은 이 사용 안내서의 목차를 참조하십시오.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
