---
title: Adobe Experience Platform과 상호 작용
description: Edge Network Server API를 사용하여 Adobe Experience Platform과 상호 작용하는 방법을 알아봅니다
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: 데이터 수집; 콘센트 analytics; Adobe Experience Platform Edge Network api;aep
exl-id: c49e40b7-9653-40f1-9db5-8941b20de8a3
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---

# Adobe Experience Platform과 상호 작용

## 개요 {#overview}

Experience Platform 데이터 수집을 활성화하려면 먼저 [데이터 스트림 구성](../edge/datastreams/overview.md) 이벤트를 Experience Platform 데이터 세트에 전달하는 데 사용됩니다.

구성이 완료되면 데이터 스트림 구성에 `com_adobe_experience_platform`를 채울 수 있습니다.


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
