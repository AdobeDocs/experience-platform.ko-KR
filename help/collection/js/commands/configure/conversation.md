---
title: 대화
description: Brand Concierge 채팅 설정을 구성합니다.
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# `conversation`

>[!AVAILABILITY]
>
>웹 SDK용 Brand Concierge은 현재 **베타**&#x200B;에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

`conversation` 개체에 Brand Concierge 채팅 세션에 대한 구성 옵션이 포함되어 있습니다. 이 개체는 웹 SDK 버전 2.31.0 이상에서 지원됩니다.

## 속성

| 속성 | 유형 | 설명 |
| --- | --- | --- |
| **`collectSources`** | `boolean` | 웹 SDK이 `adobe_brand_concierge_source` 쿼리 문자열 매개 변수를 읽고 `xdm.channel.referringSource`에 포함하는지 여부를 결정합니다. 기본값은 `false`입니다. |
| **`stickyConversationSession`** | `boolean` | 웹 SDK이 페이지 로드 시 Brand Concierge 채팅 세션을 유지하기 위해 세션 쿠키를 설정하는지 여부를 결정합니다. 기본값은 `false`입니다. 생략하거나 `false`(으)로 설정하면 Brand Concierge 채팅은 페이지를 로드할 때마다 새 세션을 시작합니다. |

## 예

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## 웹 SDK 태그 확장을 사용하여 대화 설정 구성

이러한 설정은 [Brand Concierge 설정](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다.
