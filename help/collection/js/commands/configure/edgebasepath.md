---
title: edgeBasePath
description: Adobe 서비스와 상호 작용하는 데 사용되는 끝점의 기본 경로입니다.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

`edgeBasePath` 속성은 Adobe 서비스와 상호 작용할 때 대상 경로를 변경합니다. 데이터 수집을 위한 알파 또는 베타 프로그램에 참여하는 경우, Adobe에서 이 변수를 변경하도록 요청할 수 있습니다. 대부분의 조직에서는 이 속성을 설정하거나 변경할 필요가 없습니다.

`edgeBasePath` 명령을 실행할 때 `configure` 텍스트 필드를 설정하십시오. 이 속성을 생략하면 기본값은 `ee`입니다. Adobe에서는 대부분의 구성에서 이 속성을 생략하는 것이 좋습니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## 웹 SDK 태그 확장을 사용한 Edge 기본 경로

태그 확장을 구성할 때 이 필드에 해당하는 웹 SDK 태그 확장은 [고급 구성 설정](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md)에 있습니다.
