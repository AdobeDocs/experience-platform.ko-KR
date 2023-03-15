---
title: FPID를 통한 방문자 식별
description: FPID를 사용하여 서버 API를 통해 방문자를 일관되게 식별하는 방법을 알아봅니다
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: 에지 네트워크;게이트웨이;api;방문자;식별;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# FPID를 통한 방문자 식별

[!DNL First-party IDs] (`FPIDs`)는 고객이 생성, 관리 및 저장하는 장치 ID입니다. 이를 통해 고객은 사용자 장치를 식별할 수 있습니다. 전송 `FPIDs`, Edge Network는 완전히 새로운 기능을 생성하지 않습니다 `ECID` 를 포함하지 않는 요청에 대해 사용됩니다.

다음 `FPID` 의 일부로 API 요청 본문에 포함될 수 있습니다. `identityMap` 또는 쿠키로 전송할 수 있습니다.

An `FPID` 를 결정적으로 로 변환할 수 있습니다. `ECID` Edge Network에서 `FPID` id는 Experience Cloud 솔루션과 완전히 호환됩니다. 가져오기 `ECID` 특정에서 `FPID` 항상 동일한 결과를 산출하므로 사용자는 일관된 경험을 갖게 됩니다.

다음 `ECID` 가져온 이러한 방법은 를 통해 검색할 수 있습니다. `identity.fetch` 쿼리:

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

다음을 모두 포함하는 요청의 경우 `FPID` 및 `ECID`, `ECID` 요청에 이미 있는 이(가) 생성가능한에서 우선합니다. `FPID`. 즉, Edge Network는 `ECID` 및 이(가) 이미 제공됨 `FPID` 은(는) 무시됩니다. 새 항목 `ECID` 다음 경우에만 생성됩니다. `FPID` 은 자체적으로 제공됩니다.

장치 ID 측면에서 `server` 데이터 스트림은 다음을 사용해야 합니다. `FPID` 디바이스 ID로. 기타 ID(예: `EMAIL`)는 요청 본문 내에서 제공할 수도 있지만 Edge Network에서는 기본 ID를 명시적으로 제공해야 합니다. 기본 ID는 프로필 데이터가 저장될 기본 ID입니다.

>[!NOTE]
>
>ID가 없고 각각 요청 본문 내에 기본 ID가 명시적으로 설정되지 않은 요청은 실패합니다.

다음 `identityMap` 필드 그룹이 다음에 대해 올바르게 구성되었습니다. `server` 데이터 스트림 요청:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

다음 `identityMap` 필드 그룹에 을 설정하면 오류 응답이 발생합니다. `server` 데이터 스트림 요청:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

이 경우 Edge Network에서 반환하는 오류 응답은 다음과 비슷합니다.

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## 을 사용한 방문자 식별 `FPID`

다음을 통해 사용자를 식별하려면 `FPID`, 다음을 확인합니다. `FPID` edge 네트워크에 대한 모든 요청 전에 쿠키가 전송되었습니다. 다음 `FPID` 를 쿠키에 포함하거나 의 일부로 전달할 수 있습니다. `identityMap` 를 입력합니다.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
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
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## 다음을 포함한 요청 `FPID` 다음으로 전달됨 `identityMap` 필드

아래 예제는 [!DNL FPID] as a `identityMap` 매개 변수.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
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
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
