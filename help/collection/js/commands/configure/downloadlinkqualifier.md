---
title: downloadLinkQualifier
description: 자동 링크 추적이 다운로드 링크를 정규화하는 방법을 결정하는 데 도움이 됩니다.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

[`clickCollectionEnabled`](clickcollectionenabled.md)을(를) 사용하여 자동 링크 추적을 사용하도록 설정하는 경우 `downloadLinkQualifier` 속성은 다운로드 링크로 간주되는 URL의 기준을 결정하는 데 도움이 됩니다.

이 속성은 정규 표현식 문자열입니다. 클릭한 URL이 이 정규식과 일치하면 `xdm.web.webInteraction.type`이(가) `"download"`(으)로 설정됩니다. 또한 `download` HTML 특성이 포함된 경우 링크는 즉시 다운로드 링크로 분류됩니다. `clickCollectionEnabled`을(를) 사용하지 않으면 이 속성은 아무 작업도 하지 않습니다.

`downloadLinkQualifier` 명령을 실행할 때 `configure` 문자열을 설정합니다. 이 등록 정보를 생략하면 기본값은 다음 값으로 설정됩니다.

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

다른 기준을 사용하여 다운로드 링크를 자격을 부여하려면 이 속성을 원하는 정규 표현식 값으로 설정합니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## 웹 SDK 태그 확장을 사용하여 링크 한정자 다운로드

태그 확장을 구성할 때 이 필드에 해당하는 웹 SDK 태그 확장은 [데이터 수집 구성 설정](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier)에 있습니다.
