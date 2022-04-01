---
title: Adobe Analytics과 상호 작용
description: Edge Network Server API를 사용하여 Adobe Analytics과 상호 작용하는 방법을 알아봅니다
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Analytics
keywords: 데이터 수집; 콘센트 analytics; Adobe Experience Platform Edge Network api;analytics
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---


# Adobe Analytics과 상호 작용

## 개요 {#overview}

Adobe Analytics 데이터 수집은 XDM 데이터를 Adobe Analytics에서 이해할 수 있는 형식으로 변환하여 작동합니다. 여러 XDM 필드는 다음과 같습니다 [자동 매핑](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) Analytics 변수로 이동합니다.

다음을 수행할 수도 있습니다 [수동으로 XDM 값 매핑](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) 이전 Analytics 변수에 할당하는 방법을 보여줍니다.

Adobe Analytics이 서버 API에서 데이터를 수신하도록 하려면 다음을 수행해야 합니다 [데이터 스트림 구성](../edge/fundamentals/datastreams.md#adobe-analytics-settings) 이벤트를 Adobe Analytics에 전달하려면 데이터 스트림 구성 페이지에 보고서 세트 ID를 입력합니다.

![Adobe Analytics 데이터 스트림 구성](assets/analytics-datastream.png)

## Adobe Analytics과 상호 작용 {#interacting-analytics}

### API 형식 {#format}

```http
POST https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}
```

### 요청 {#request}

아래 샘플에는 `_experience.analytics` 필드 그룹. 또한 JSON 기반 데이터 레이어도 포함되어 있습니다. 이러한 데이터 레이어는 자동으로 매핑할 수 없지만 [데이터 수집을 위한 데이터 준비](../edge/fundamentals/datastreams.md#data-prep) 이러한 값을 위에 참조된 필드 그룹을 포함하는 스키마에 매핑하려면,

사용자가 해당 필드에 매핑하는 모든 값은 API 요청에 포함된 것처럼 해당 Analytics 값에 자동으로 매핑됩니다.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
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
