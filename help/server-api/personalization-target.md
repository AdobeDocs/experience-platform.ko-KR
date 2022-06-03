---
title: Adobe Target을 통한 개인화
description: 서버 API를 사용하여 Adobe Target에서 만든 개인화된 경험을 제공하고 렌더링하는 방법을 알아봅니다
keywords: 개인화; 서버 api; Adobe Experience Platform Edge Network; 개인화 검색;target;adobe target
source-git-commit: 59cb43007c4a7ff125738c21064381cf833063b2
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---


# Adobe Target을 통한 개인화

## 개요 {#overview}

에지 네트워크 서버 API는 Adobe Target에서 만든 개인화된 경험을 제공하고 렌더링할 수 있습니다. [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>를 통해 생성된 개인화 경험 [Target VEC(시각적 경험 작성기)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 는 서버 API에서 지원되지 않습니다.

## 데이터 스트림 구성 {#configure-your-datastream}

Adobe Target과 함께 서버 API를 사용하려면 먼저 데이터 스트림 구성에서 Adobe Target 개인화를 활성화해야 합니다.

자세한 내용은 [데이터 스트림에 서비스 추가 안내서](../edge/datastreams/overview.md#adobe-target-settings)를 참조하십시오.

데이터 스트림을 구성할 때 다음에 값을 제공할 수 있습니다(선택 사항) [!DNL Property Token], [!DNL Target Environment ID], 및 [!DNL Target Third Party ID Namespace].

![Adobe Target이 선택된 상태로 데이터 스트림 서비스 구성 화면을 보여주는 UI 이미지](assets/target-datastream.png)

다음 중 하나를 선택할 수 있습니다 [!DNL Analytics Logging] 옵션:

* **[!DNL Server Side]**: 에 대한 기본 옵션입니다 [[!DNL A4T]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html). 이 옵션을 선택하면 개인화 컨텐츠가 Target에 의해 반환될 때마다 관련 내용이 표시됩니다 [!DNL A4T] 데이터는 Target 개인화 엔진의 응답을 기반으로 Analytics로 자동으로 전송됩니다.
* **[!DNL Client Side]**: 이 옵션을 선택하면 개인화 컨텐츠가 Target에 의해 반환될 때마다 관련 내용이 표시됩니다 [!DNL A4T] 데이터가 호출 애플리케이션에 반환됩니다. Analytics에 이 데이터를 기록하려는 경우에는 다음에 대한 후속 호출 시 이 데이터가 보고되는지 확인해야 합니다 [!DNL Analytics].

   >[!IMPORTANT]
   >
   >선택 외에 **[!UICONTROL 고객측]** Target 구성에서 Edge Network에서 를 반환하려면 Analytics도 비활성화해야 합니다. [!DNL A4T] 응답으로 정보를 다시 가져옵니다.


## 사용자 지정 매개 변수 {#custom-parameters}

의 대부분의 필드 [!DNL XDM] 각 요청의 일부가 점 표기법으로 직렬화된 다음 사용자 지정 또는 Target으로 전송됩니다 [!DNL mbox] 매개 변수.


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

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Target 프로필 업데이트 {#profile-update}

다음 [!DNL Server API] Target 프로필에 대한 업데이트를 허용합니다. Target 프로필을 업데이트하려면 프로필 데이터가 `data` 요청의 일부: 다음 형식으로

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

요청의 쿼리 부분은 Target이 반환하는 콘텐츠를 결정합니다. 아래에 `personalization` 개체, `schemas` Target에서 반환할 컨텐츠 유형을 결정합니다.

검색할 오퍼의 종류를 잘 모르는 경우 개인화 쿼리에 4개의 스키마를 모두 Edge Network에 포함해야 합니다.

* **HTML 기반 오퍼:**
https://ns.adobe.com/personalization/html-content-item
* **JSON 기반 오퍼:**
https://ns.adobe.com/personalization/json-content-item
* **Target 리디렉션 오퍼**
https://ns.adobe.com/personalization/redirect-item
* **Target DOM 조작 오퍼**
https://ns.adobe.com/personalization/dom-action

### 결정 범위 {#decision-scopes}

Adobe Target [!DNL mbox] 이름은 `decisionScopes` 적절한 컨텐츠를 반환하기 위한 배열입니다.

#### 예 {#decision-scopes-example}

아래 예에서는 네 개의 오퍼 유형이 모두 요청되며, 여기에는 `serverapimbox`.

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

적절한 Target 쿼리와 함께 전체 XDM 개체, 프로필 매개 변수를 포함하는 전체 요청은 아래에 요약되어 있습니다.

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

에지 네트워크는 아래 응답과 유사한 응답을 반환합니다.

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

방문자가 Adobe Target에 전송된 데이터를 기반으로 개인화 활동에 자격이 되는 경우 관련 활동 콘텐츠는 `handle` 객체, 여기서 유형은 `personalization:decisions`.

다른 콘텐츠는 경우에 따라 `handle` 또한. 다른 컨텐츠 유형은 Target 개인화와 관련이 없습니다. 방문자가 여러 활동에 대해 자격이 있는 경우 각 활동은 별개입니다 `personalization` 개체의 이름을 지정합니다.

아래 표는 응답의 해당 부분에 대한 주요 요소를 설명합니다.

| 속성 | 설명 | 예 |
|---|---|---|
| `scope` | 제안된 오퍼를 초래한 Target mbox 이름입니다. | `"scope": "serverapimbox"` |
| `items[].schema` | 제안된 오퍼와 연결된 컨텐츠의 스키마. 이는 개인화 활동을 만들 때 선택한 활동 유형과 관련이 있습니다. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | 오퍼 활동의 고유 ID입니다. 일반적으로 6자리 숫자입니다. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | 사용자가 지정한 오퍼 활동의 이름입니다. 이 기능은 활동 생성 단계 중에 제공됩니다. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | 개인화 경험의 고유 ID입니다. | `"experience.id": "0"` |
| `items[].meta.experience.name` | 개인화 경험의 고유 이름입니다. | `"experience.name": "Experience A"` |
| `items[].data.id` | 제안된 오퍼의 ID입니다. | `"id": "282484"` |
| `items[].data.format` | 제안된 오퍼와 연관된 컨텐츠의 형식입니다. | `"format: "application/json` |
| `items[].data.content` | 제안된 오퍼와 연관된 컨텐츠. 호출 애플리케이션의 콘텐츠를 개인화하는 데 사용됩니다. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |
