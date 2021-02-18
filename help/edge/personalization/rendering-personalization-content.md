---
title: Adobe Experience Platform 웹 SDK를 사용하여 개인화된 컨텐츠 렌더링
description: Adobe Experience Platform 웹 SDK를 사용하여 개인화된 컨텐츠를 렌더링하는 방법을 알아봅니다.
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decision;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# 개인화된 컨텐츠 렌더링

Adobe Experience Platform [!DNL Web SDK]은 Adobe Target을 포함하여 Adobe에서 개인화 솔루션 쿼리를 지원합니다. 개인화를 위한 두 가지 모드가 있습니다.자동으로 렌더링할 수 있는 컨텐츠 및 개발자가 렌더링해야 하는 컨텐츠 검색 또한 SDK는 [깜박임 관리](../personalization/manage-flicker.md)에 대한 기능을 제공합니다.

## 자동으로 컨텐츠 렌더링

이벤트를 서버에 보낼 때 SDK는 개인화된 컨텐츠를 자동으로 렌더링하고 이벤트의 옵션으로 `renderDecisions` `true`로 설정합니다.

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

개인화된 컨텐츠의 렌더링은 비동기 방식이므로 특정 컨텐츠가 페이지에 포함되는 경우를 가정하지 마십시오.

## 수동으로 컨텐츠 렌더링

`decisionScopes` 옵션을 지정하여 `sendEvent` 명령에서 약속으로 반환되는 결정 목록을 요청할 수 있습니다. 범위는 개인화 솔루션이 원하는 결정을 알 수 있도록 해주는 문자열입니다.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

그러면 결정 목록이 각 결정에 대해 JSON 개체로서 반환됩니다.

```json
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
> [!DNL Target]을(를) 사용하는 경우 범위는 서버에서 mBox가 됩니다. 이러한 범위는 개별적으로 수행하는 것이 아니라 모두 한 번에 요청됩니다. 글로벌 mbox는 항상 전송됩니다.

### 자동 컨텐츠 검색

자동 렌더링 가능 결정을 포함시키고 NOT이 합금을 자동으로 렌더링하도록 하려면 `renderDecisions`을(를) `false`로 설정하고 특수 범위 `__view__`을(를) 포함할 수 있습니다.`result.decisions`
