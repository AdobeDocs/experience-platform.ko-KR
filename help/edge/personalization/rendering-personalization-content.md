---
title: 맞춤형 컨텐츠 렌더링
seo-title: Adobe Experience Platform 웹 SDK 맞춤형 컨텐츠 렌더링
description: Experience Platform 웹 SDK를 사용하여 개인화된 컨텐츠를 렌더링하는 방법 학습
seo-description: Experience Platform 웹 SDK를 사용하여 개인화된 컨텐츠를 렌더링하는 방법 학습
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# 개인화 옵션 개요

Adobe Experience Platform은 Adobe Target을 비롯한 Adobe에서 개인화 솔루션 쿼리를 지원합니다. [!DNL Web SDK] 개인화 모드에는자동으로 렌더링될 수 있는 컨텐츠 및 개발자가 렌더링해야 하는 컨텐츠 검색 또한 SDK는 깜박임을 [관리하는 기능도 제공합니다](../personalization/manage-flicker.md).

## 컨텐츠 자동 렌더링

이벤트를 서버로 보내고 이벤트에서 옵션으로 설정하면 SDK에서 개인화된 컨텐츠 `renderDecisions` `true` 를 자동으로 렌더링합니다.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

개인화된 컨텐츠의 렌더링은 비동기 방식이므로 특정 컨텐츠가 페이지의 일부일 때는 추측하지 마십시오.

## 수동으로 컨텐츠 렌더링

옵션을 지정하여 명령에서 약속으로 반환되는 결정 목록을 `sendEvent` 요청할 수 `decisionScopes` 있습니다. 범위는 개인화 솔루션이 원하는 결정을 알 수 있도록 해주는 문자열입니다.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  })
```

그러면 결정 목록이 각 결정에 대해 JSON 개체로서 반환됩니다.

```javascript
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

>[!TIP]
>
> 사용하는 경우 범위 [!DNL Target]는 서버에서 mBox가 되며, 범위가 모두 개별적으로 요청되지 않고 한 번에 요청됩니다. 글로벌 mbox는 항상 전송됩니다.

### 자동 컨텐츠 검색

자동 렌더링 가능 결정 `result.decisions` 을 포함시키고 NOT이 합금 자동 렌더링을 제공하고자 하는 경우, 특별 범위를 설정하고 포함시킬 수 `renderDecisions` `false``__view__`있습니다.
