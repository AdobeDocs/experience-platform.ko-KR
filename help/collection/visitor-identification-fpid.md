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

[!DNL First-party IDs](`FPIDs`)은(는) 고객이 생성, 관리 및 저장하는 장치 ID입니다. 이를 통해 고객은 사용자 장치를 식별할 수 있습니다. `FPIDs`을(를) 보냄으로써, Edge Network은 새 `ECID`을(를) 포함하지 않는 요청에 대해 생성하지 않습니다.

`FPID`은(는) `identityMap`의 일부로 API 요청 본문에 포함되거나 쿠키로 전송될 수 있습니다.

`FPID`은(는) Edge Network이 `ECID`(으)로 결정적으로 변환할 수 있으므로 `FPID` ID는 Experience Cloud 솔루션과 완전히 호환됩니다. 특정 `FPID`에서 `ECID`을(를) 가져오면 항상 동일한 결과가 생성되므로 사용자는 일관된 경험을 갖게 됩니다.

이 방법으로 얻은 `ECID`은(는) `identity.fetch` 쿼리를 통해 검색할 수 있습니다.

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

`FPID`과(와) `ECID`이(가) 모두 포함된 요청의 경우, 요청에 이미 있는 `ECID`이(가) `FPID`에서 생성할 수 있는 요청보다 우선합니다. 즉, Edge Network이 이미 제공된 `ECID`을(를) 사용하고 `FPID`은(는) 무시됩니다. 새 `ECID`은(는) `FPID`이(가) 단독으로 제공되는 경우에만 생성됩니다.

장치 ID 측면에서 `server` 데이터 스트림은 `FPID`을(를) 장치 ID로 사용해야 합니다. 다른 ID(즉, `EMAIL`)도 요청 본문 내에 제공할 수 있지만, Edge Network을 사용하려면 기본 ID를 명시적으로 제공해야 합니다. 기본 ID는 프로필 데이터가 저장될 기본 ID입니다.

>[!NOTE]
>
>ID가 없고 각각 요청 본문 내에 기본 ID가 명시적으로 설정되지 않은 요청은 실패합니다.

`server` 데이터 스트림 요청에 대해 다음 `identityMap` 필드 그룹이 올바르게 구성되었습니다.

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

`server` 데이터 스트림 요청에서 설정할 때 다음 `identityMap` 필드 그룹으로 인해 오류 응답이 발생합니다.

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

이 경우 Edge Network이 반환하는 오류 응답은 다음과 비슷합니다.

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

## `FPID`을(를) 사용한 방문자 식별

`FPID`을(를) 통해 Edge Network을 식별하려면 사용자에게 요청하기 전에 `FPID` 쿠키가 전송되었는지 확인하십시오. `FPID`은(는) 쿠키를 통해 또는 요청 본문에서 `identityMap`의 일부로 전달될 수 있습니다.

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

## `FPID`이(가) 있는 요청이 `identityMap` 필드로 전달됨

다음 예제에서는 [!DNL FPID]을(를) `identityMap` 매개 변수로 전달합니다.

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
