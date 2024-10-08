---
title: Adobe Analytics과 상호 작용
description: Edge Network 서버 API를 사용하여 Adobe Analytics과 상호 작용하는 방법을 알아봅니다.
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 5de1ec17b78c97be21c0d2afd6f0b119a6074b6f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Adobe Analytics과 상호 작용

## 개요 {#overview}

Adobe Analytics 데이터 수집은 XDM 데이터를 Adobe Analytics이 이해할 수 있는 형식으로 변환하여 작동합니다. 여러 XDM 필드가 Analytics 변수에 [자동으로 매핑](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html)됩니다. XDM 값을 이전 Analytics 변수에 수동으로 매핑할 수도 있습니다.

Adobe Analytics이 서버 API에서 데이터를 수신하도록 하려면 데이터 스트림 구성 페이지에 보고서 세트 ID를 입력하여 이벤트를 Adobe Analytics에 전달하도록 [데이터 스트림을 구성](../datastreams/overview.md#adobe-analytics-settings)해야 합니다.

![Adobe Analytics 데이터 스트림 구성](assets/analytics-datastream.png)

## Adobe Analytics과 상호 작용 {#interacting-analytics}

### API 형식 {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### 요청 {#request}

아래 샘플에는 `_experience.analytics` 필드 그룹에서 자동으로 매핑된 여러 값이 포함되어 있습니다. JSON 기반 데이터 계층도 포함됩니다. 이러한 데이터 계층은 자동으로 매핑될 수 없지만 [데이터 수집을 위한 데이터 준비](../datastreams/data-prep.md)를 사용하여 위에서 참조된 필드 그룹이 포함된 스키마에 이러한 값을 매핑할 수 있습니다.

사용자가 해당 필드에 매핑하는 모든 값은 API 요청에 포함된 것처럼 적절한 Analytics 값에 자동으로 매핑됩니다.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev",
               "name": "Home Page"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 3440,
               "viewportHeight": 1440
            }
         },
         "placeContext": {
            "localTime": "2022-03-22T22:45:21.193-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-23T04:45:21.193Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
      }
   },
   "data": {
      "page": {
         "pageInfo": {
            "pageName": "Promotions",
            "siteSection": "Home"
         },
         "promos": {
            "heroPromos": "purse,shoes,sunglasses"
         },
         "customVariables": {
            "testGroup": "orange/black theme"
         },
         "events": {
            "homePage": true
         },
         "products": [
            {
               "productSKU": "abc123",
               "productName": "shirt"
            }
         ]
      }
   }
}'
```

### 응답 {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
