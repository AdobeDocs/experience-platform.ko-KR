---
title: Adobe Experience Platform 웹 SDK 구성
description: 웹 SDK을 사용할 때 필요한 설정을 설정하려면 configure 명령을 사용하십시오.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Adobe Experience Platform 웹 SDK 구성

웹 SDK 구성은 **`configure`** 명령을 사용하여 수행됩니다. 이 명령은 [`sendEvent`](../sendevent/overview.md)과 같은 다른 웹 SDK 명령을 호출하기 전에 페이지를 로드할 때마다 필요합니다.

**[`datastreamId`](datastreamid.md) 및 [`orgId`](orgid.md) 속성이 필요합니다.** 다른 모든 속성은 조직의 구현 요구 사항에 따라 선택 사항입니다. 다음 예제는 사용 가능한 대부분의 속성을 사용하는 구성 객체를 보여 줍니다.

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
    filterClickDetails: function(content) {
      content.linkUrl = "https://example.com/current.html";
    },
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints", "oneTimeAnalyticsReferrer"],
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
  prehidingStyle: "#container { opacity: 0 !important }",
  conversation: {
    stickyConversationSession: false
  },
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
