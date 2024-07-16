---
title: Offer decisioning을 통한 Personalization
description: Server API를 사용하여 Offer decisioning을 통해 개인화된 경험을 전달하고 렌더링하는 방법에 대해 알아봅니다.
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---

# Offer decisioning을 통한 Personalization

## 개요 {#overview}

Edge Network 서버 API는 [Offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ko-KR)에서 관리되는 개인화된 경험을 웹 채널에 전달할 수 있습니다.

[!DNL Offer Decisioning]은(는) 활동 및 개인화 경험을 만들고, 활성화하고, 제공할 수 있는 비시각적 인터페이스를 지원합니다.

## 전제 조건 {#prerequisites}

[!DNL Offer Decisioning]을(를) 통한 Personalization에서는 통합을 구성하기 전에 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko-KR)에 액세스할 수 있어야 합니다.

## 데이터 스트림 구성 {#configure-your-datastream}

Server API를 Offer decisioning과 함께 사용하려면 먼저 데이터 스트림 구성에서 Adobe Experience Platform 개인화를 사용하도록 설정하고 **[!UICONTROL Offer decisioning]** 옵션을 사용하도록 설정해야 합니다.

offer decisioning 사용 방법에 대한 자세한 내용은 [데이터 스트림에 서비스 추가 가이드](../datastreams/overview.md#adobe-experience-platform-settings)를 참조하십시오.

![Offer decisioning이 선택된 데이터 스트림 서비스 구성 화면을 표시하는 UI 이미지](assets/aep-od-datastream.png)

## 대상자 만들기 {#audience-creation}

[!DNL Offer Decisioning]은(는) 대상 생성을 위해 Adobe Experience Platform 세분화 서비스를 사용합니다. [!DNL Segmentation Service] [여기](../segmentation/home.md)에 대한 설명서를 찾을 수 있습니다.

## 결정 범위 정의 {#creating-decision-scopes}

[!DNL Offer Decision Engine]은(는) [!DNL Offer Library]과(와) 함께 Adobe Experience Platform 데이터 및 [실시간 고객 프로필](../profile/home.md)을(를) 사용하여 적시에 적절한 고객과 채널에 오퍼를 제공합니다.

[!DNL Offer Decisioning Engine]에 대한 자세한 내용은 전용 [설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ko-KR)를 참조하세요.

[데이터 스트림을 구성](#configure-your-datastream)한 후에는 개인화 캠페인에 사용할 결정 범위를 정의해야 합니다.

[결정 범위](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes)은(는) 오퍼를 제안할 때 [!DNL Offer Decisioning Service]에서 사용할 활동 및 배치 ID가 포함된 Base64로 인코딩된 JSON 문자열입니다.

**결정 범위 JSON**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**결정 범위 Base64 인코딩 문자열**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

오퍼 및 컬렉션을 만든 후에는 [결정 범위](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes)를 정의해야 합니다.

Base64로 인코딩된 결정 범위를 복사합니다. 서버 API 요청의 `query` 개체에서 사용합니다.

![Offer decisioning UI를 표시하고 결정 범위를 강조 표시하는 UI 이미지입니다.](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## API 호출 예 {#api-example}

**API 형식**

```http
POST /ee/v2/interact
```

### 요청 {#request}

전체 XDM 개체, 데이터 개체 및 Offer decisioning 쿼리를 포함하는 전체 요청은 아래에 요약되어 있습니다.

>[!NOTE]
>
>`xdm` 및 `data` 개체는 선택 사항이며, 해당 개체에 필드를 사용하는 조건으로 세그먼트를 만든 경우에만 Offer decisioning에 필요합니다.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
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
                "version": "1.0",
                "environment": "serverapi"
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
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### 응답 {#response}

Edge Network은 아래 응답과 유사한 응답을 반환합니다.

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

방문자가 [!DNL Offer Decisioning]에 전송된 데이터를 기반으로 개인화 활동을 사용할 수 있는 경우 관련 활동 콘텐츠가 `handle` 개체에서 검색됩니다. 여기서 유형은 `personalization:decisions`입니다.

다른 콘텐트도 `handle` 개체 아래에 반환됩니다. 다른 콘텐츠 형식은 [!DNL Offer Decisioning] 개인화와 관련이 없습니다. 방문자가 여러 활동을 수행할 수 있는 경우 배열에 포함됩니다.

아래 표는 응답의 해당 부분에 대한 주요 요소를 설명합니다.

| 속성 | 설명 | 예 |
|---|---|---|
| `scope` | 반환된 제안된 오퍼와 연결된 결정 범위입니다. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 오퍼 활동에 대한 고유 ID. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 오퍼 배치에 대한 고유 ID. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 제안된 오퍼의 고유 ID. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 제안된 오퍼와 연관된 콘텐츠의 스키마. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 제안된 오퍼의 고유 ID. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 제안된 오퍼와 연관된 콘텐츠의 형식입니다. | `"format": "text/html"` |
| `language` | 제안된 오퍼의 콘텐츠와 연관된 언어의 배열입니다. | `"language": [ "en-US" ]` |
| `content` | 문자열 형식으로 제안된 오퍼와 연결된 콘텐츠. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 제안된 오퍼와 연결된 이미지 컨텐츠(URL 형식). | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 제안된 오퍼와 관련된 특성이 포함된 JSON 개체입니다. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
