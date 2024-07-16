---
title: Adobe Target을 통한 Personalization
description: Server API를 사용하여 Adobe Target에서 생성된 개인화된 경험을 전달하고 렌더링하는 방법에 대해 알아봅니다.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# Adobe Target을 통한 Personalization

## 개요 {#overview}

Edge Network 서버 API는 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)의 도움을 받아 Adobe Target에서 만들어진 개인화된 경험을 전달하고 렌더링할 수 있습니다.

>[!IMPORTANT]
>
>[Target VEC(시각적 경험 작성기)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)를 통해 만들어진 Personalization 경험은 서버 API에서 완전히 지원되지 않습니다. 서버 API는 VEC에서 만든 활동을 **검색**&#x200B;할 수 있지만 서버 API는 VEC에서 만든 활동을 **렌더링**&#x200B;할 수 없습니다. VEC에서 만든 활동을 렌더링하려면 Web SDK 및 Edge Network 서버 API를 사용하여 [하이브리드 개인화](../web-sdk/personalization/hybrid-personalization.md)를 구현하십시오.

## 데이터 스트림 구성 {#configure-your-datastream}

Adobe Target과 함께 서버 API를 사용하려면 먼저 데이터 스트림 구성에서 Adobe Target 개인화를 활성화해야 합니다.

Adobe Target 사용 방법에 대한 자세한 내용은 [데이터 스트림에 서비스 추가 가이드](../datastreams/overview.md#adobe-target-settings)를 참조하십시오.

데이터 스트림을 구성할 때 [!DNL Property Token], [!DNL Target Environment ID] 및 [!DNL Target Third Party ID Namespace]에 대한 값을 제공할 수 있습니다(선택적).

Adobe Target이 선택된 상태에서 데이터 스트림 서비스 구성 화면을 표시하는 ![UI 이미지](assets/target-datastream.png)

## 사용자 지정 매개 변수 {#custom-parameters}

각 요청의 [!DNL XDM] 부분에 있는 대부분의 필드는 점 표기법으로 serialize된 다음 사용자 지정 또는 [!DNL mbox] 매개 변수로 Target에 전송됩니다.


### 예 {#custom-parameters-example}

다음 XDM 샘플이 제공됩니다.

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

Target에서 대상을 만들 때 다음 값을 사용자 지정 매개 변수로 사용할 수 있습니다.

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Target 프로필 업데이트 {#profile-update}

[!DNL Server API]에서 대상 프로필을 업데이트할 수 있습니다. Target 프로필을 업데이트하려면 프로필 데이터가 다음 형식의 요청의 `data` 부분으로 전달되었는지 확인하십시오.

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Target 활동 쿼리 {#querying-target-activities}

### 스키마 {#schemas}

요청의 쿼리 부분은 Target에서 반환되는 콘텐츠를 결정합니다. `personalization` 개체 아래에서 `schemas`은(는) Target에서 반환할 콘텐츠의 형식을 결정합니다.

어떤 종류의 오퍼를 검색할지 확실하지 않은 경우 Edge Network에 대한 개인화 쿼리에 4개의 스키마를 모두 포함해야 합니다.

* **HTML 기반 오퍼:**
https://ns.adobe.com/personalization/html-content-item
* **JSON 기반 오퍼:**
https://ns.adobe.com/personalization/json-content-item
* **리디렉션 오퍼 타깃팅**
https://ns.adobe.com/personalization/redirect-item
* **DOM 조작 오퍼 타깃팅**
https://ns.adobe.com/personalization/dom-action

### 결정 범위 {#decision-scopes}

적절한 콘텐츠를 반환하려면 Adobe Target [!DNL mbox] 이름이 `decisionScopes` 배열에 포함되어야 합니다.

#### 예 {#decision-scopes-example}

아래 예제에서는 `serverapimbox`(이)라는 Target 활동과 함께 네 가지 오퍼 형식을 모두 요청합니다.

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
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

적절한 Target 쿼리와 함께 전체 XDM 개체, 프로필 매개 변수를 포함하는 전체 요청이 아래에 요약되어 있습니다.

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
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### 응답 {#response}

Edge Network은 아래 응답과 유사한 응답을 반환합니다.

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
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
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

방문자가 Adobe Target에 전송된 데이터를 기반으로 개인화 활동을 사용할 수 있는 경우 관련 활동 콘텐츠가 `handle` 개체에서 검색됩니다. 여기서 유형은 `personalization:decisions`입니다.

`handle`에서도 다른 콘텐츠가 반환되는 경우가 있습니다. 다른 콘텐츠 유형은 Target 개인화와 관련이 없습니다. 방문자가 여러 활동을 수행할 수 있는 경우 각 활동은 배열에서 별도의 `personalization` 개체가 됩니다.

아래 표는 응답의 해당 부분에 대한 주요 요소를 설명합니다.

| 속성 | 설명 | 예 |
|---|---|---|
| `scope` | 제안된 오퍼의 원인이 되는 Target mbox 이름입니다. | `"scope": "serverapimbox"` |
| `items[].schema` | 제안된 오퍼와 연관된 콘텐츠의 스키마. 이는 개인화 활동을 만들 때 선택한 활동 유형과 관련이 있습니다. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | 오퍼 활동에 대한 고유 ID. 일반적으로 6자리 숫자입니다. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | 사용자 지정 오퍼 활동의 이름입니다. 이는 활동 만들기 단계 동안 제공됩니다. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | 개인화 경험에 대한 고유 ID. | `"experience.id": "0"` |
| `items[].meta.experience.name` | 개인화 경험의 고유 이름입니다. | `"experience.name": "Experience A"` |
| `items[].data.id` | 제안된 오퍼의 ID입니다. | `"id": "282484"` |
| `items[].data.format` | 제안된 오퍼와 연관된 콘텐츠의 형식입니다. | `"format: "application/json` |
| `items[].data.content` | 제안된 오퍼와 연관된 콘텐츠. 호출 애플리케이션의 콘텐츠 개인화에 사용됩니다. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## 서버측 개인화 샘플 애플리케이션 {#sample}

[이 URL](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side)에 있는 샘플 응용 프로그램은 Adobe Experience Platform을 사용하여 Adobe Target에서 개인화 콘텐츠를 가져오는 방법을 보여 줍니다. 웹 페이지는 반환된 개인화 콘텐츠에 따라 변경됩니다.

이 샘플은 [!DNL Web SDK]과(와) 같은 클라이언트측 라이브러리에 의존하여 개인화 콘텐츠를 가져오지 _않습니다_. 대신 Adobe Experience Platform API를 사용하여 개인화 콘텐츠를 가져옵니다. 그런 다음 반환된 개인화 컨텐츠를 기반으로 HTML 서버측을 생성합니다.
