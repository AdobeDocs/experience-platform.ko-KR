---
title: Personalization 개요
description: Adobe Experience Platform Edge Network 서버 API를 사용하여 Adobe 개인화 솔루션에서 개인화된 콘텐츠를 검색하는 방법에 대해 알아봅니다.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: ae6c6d21b1eea900d01be3287827296071429d30
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 9%

---

# Personalization 개요

[!DNL Server API]을(를) 사용하면 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html), [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/ajo-home) 및 [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=ko)을(를) 포함하여 Adobe 개인화 솔루션에서 개인화된 콘텐츠를 검색할 수 있습니다.

또한 [!DNL Server API]은(는) [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 지정 개인화 연결](../destinations/catalog/personalization/custom-personalization.md)과(와) 같은 Adobe Experience Platform 개인화 대상을 통해 동일 페이지 및 다음 페이지 개인화 기능을 지원합니다. 동일 페이지 및 다음 페이지 개인화에 대한 Experience Platform을 구성하는 방법에 대해 알아보려면 [전용 안내서](../destinations/ui/activate-edge-personalization-destinations.md)를 참조하세요.

Server API를 사용하는 경우 개인화 엔진에서 제공하는 응답을 사이트의 콘텐츠를 렌더링하는 데 사용되는 논리와 통합해야 합니다. [Web SDK](../web-sdk/home.md)과(와) 달리 [!DNL Server API]에는 Adobe 개인화 솔루션에서 반환된 콘텐츠를 자동으로 적용하는 메커니즘이 없습니다.

## 용어 {#terminology}

Adobe 개인화 솔루션을 사용하기 전에 다음 개념을 이해해야 합니다.

* **오퍼**: 오퍼는 오퍼를 볼 자격이 있는 사람을 지정하는 규칙과 관련된 마케팅 메시지입니다.
* **결정**: 결정(이전 이름: 오퍼 활동)은 오퍼를 선택함을 알려줍니다.
* **스키마**: 결정의 스키마가 반환된 오퍼의 유형을 알려줍니다.
* **범위**: 결정 범위입니다.
   * Adobe Target에서 [!DNL mbox]입니다. [!DNL global mbox]은(는) `__view__` 범위입니다.
   * [!DNL Offer Decisioning]의 경우 offer decisioning 서비스에서 오퍼를 제안하는 데 사용할 활동 및 배치 ID가 포함된 JSON의 Base64 인코딩 문자열입니다.

## `query` 개체 {#query-object}

개인화된 콘텐츠를 검색하려면 요청 예제에 대한 명시적 요청 쿼리 개체가 필요합니다. 쿼리 개체의 형식은 다음과 같습니다.

```json
{
  "query": {
    "personalization": {
      "schemas": [
        "https://ns.adobe.com/personalization/html-content-item",
        "https://ns.adobe.com/personalization/json-content-item",
        "https://ns.adobe.com/personalization/redirect-item",
        "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes": [
        "alloyStore",
        "siteWide",
        "__view__",
        "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
      ],
      "surfaces": [
        "web://mywebpage.html/",
        "web://mywebpage.html/#sample-json-content"
      ]
    }
  }
}
```



| 속성 | 유형 | 필수/선택적 | 설명 |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Target 개인화에 필요합니다. offer decisioning에 선택 사항입니다. | 반환된 오퍼 유형을 선택하기 위해 결정에 사용된 스키마 목록. |
| `scopes` | `String[]` | 선택 사항입니다 | 결정 범위 목록. 요청당 최대 30개. |

## 핸들 개체 {#handle}

개인화 솔루션에서 검색된 개인화된 콘텐츠는 페이로드에 대해 다음과 같은 형식의 `personalization:decisions` 핸들에 표시됩니다.

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| 속성 | 유형 | 설명 |
| --- | --- | --- |
| `payload.id` | 문자열 | 결정 ID. |
| `payload.scope` | 문자열 | 제안된 오퍼의 원인이 되는 결정 범위입니다. |
| `payload.scopeDetails.decisionProvider` | 문자열 | Adobe Target을 사용할 때 `TGT`(으)로 설정합니다. |
| `payload.scopeDetails.activity.id` | 문자열 | 오퍼 활동에 대한 고유 ID. |
| `payload.scopeDetails.experience.id` | 문자열 | 오퍼 배치에 대한 고유 ID. |
| `items[].id` | 문자열 | 오퍼 배치에 대한 고유 ID. |
| `items[].data.id` | 문자열 | 제안된 오퍼의 ID입니다. |
| `items[].data.schema` | 문자열 | 제안된 오퍼와 연관된 콘텐츠의 스키마. |
| `items[].data.format` | 문자열 | 제안된 오퍼와 연관된 콘텐츠의 형식입니다. |
| `items[].data.language` | 문자열 | 제안된 오퍼의 콘텐츠와 연관된 언어의 배열입니다. |
| `items[].data.content` | 문자열 | 문자열 형식으로 제안된 오퍼와 연결된 콘텐츠. |
| `items[].data.selector` | 문자열 | DOM 작업 오퍼에 대한 대상 DOM 요소를 식별하는 데 사용되는 HTML 선택기. |
| `items[].data.prehidingSelector` | 문자열 | DOM 작업 오퍼를 처리하는 동안 숨길 DOM 요소를 식별하는 데 사용되는 HTML 선택기입니다. |
| `items[].data.deliveryUrl` | 문자열 | 제안된 오퍼와 연결된 이미지 컨텐츠(URL 형식). |
| `items[].data.characteristics` | 문자열 | JSON 오브젝트 형식으로 제안된 오퍼와 연관된 특성입니다. |

## 샘플 API 호출 {#sample-call}

**API 형식**

```http
POST /ee/v2/interact
```

### 요청 {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| 매개변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `configId` | 문자열 | 예 | 데이터 스트림 ID입니다. |
| `requestId` | 문자열 | 아니요 | 외부 요청 추적 ID를 제공합니다. 아무 것도 제공되지 않으면 Edge Network이 자동으로 생성한 후 응답 본문/헤더로 다시 반환합니다. |

### 응답 {#response}

데이터 스트림 구성에서 활성화된 Edge Services에 따라 `200 OK` 상태와 하나 이상의 `Handle` 개체를 반환합니다.

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## 알림 {#notifications}

프리페치된 콘텐츠 또는 보기가 최종 사용자에게 방문되거나 렌더링될 때 알림을 실행해야 합니다. 올바른 범위에 대해 알림을 실행하려면 각 범위에 대해 해당 `id`을(를) 추적해야 합니다.

보고를 올바르게 반영하려면 해당 범위에 대해 올바른 `id`이(가) 있는 알림을 실행해야 합니다.

**API 형식**

```http
POST /ee/v2/collect
```

### 요청 {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| 매개변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 예 | 데이터 수집 끝점에서 사용하는 데이터 스트림의 ID입니다. |
| `requestId` | `String` | 아니요 | 외부 외부 요청 추적 ID. 아무 것도 제공되지 않으면 Edge Network이 자동으로 생성한 후 응답 본문/헤더로 다시 반환합니다. |
| `silent` | `Boolean` | 아니요 | Edge Network이 빈 페이로드와 함께 `204 No Content` 응답을 반환해야 하는지 여부를 나타내는 선택적 부울 매개 변수입니다. 해당 HTTP 상태 코드 및 페이로드를 사용하여 심각한 오류가 보고됩니다. |

### 응답 {#notifications-response}

성공적인 응답은 다음 상태 중 하나를 반환하며, 요청에 아무 것도 제공되지 않은 경우 `requestID`을(를) 반환합니다.

* 요청이 성공적으로 처리된 경우 `202 Accepted`;
* 요청이 성공적으로 처리되고 `silent` 매개 변수가 `true`(으)로 설정된 경우 `204 No Content`;
* `400 Bad Request` 요청이 제대로 형성되지 않은 경우(예: 필수 기본 id를 찾을 수 없음).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
