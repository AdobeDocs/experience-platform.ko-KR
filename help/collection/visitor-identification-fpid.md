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

[!DNL First-party IDs] (`FPIDs`)는 고객이 생성, 관리 및 저장하는 장치 ID입니다. 이를 통해 고객은 사용자 장치 식별을 제어할 수 있습니다. 보내기 `FPIDs`Edge Network는 새 브랜드를 생성하지 않습니다 `ECID` 를 포함해야 합니다.

다음 `FPID` 는 API 요청 본문에 `identityMap` 또는 쿠키로 전송할 수 있습니다.

An `FPID` 결정적으로 `ECID` 에지 네트워크에서 `FPID` id는 Experience Cloud 솔루션과 완벽하게 호환됩니다. 가져오기 `ECID` 특정 `FPID` 항상 동일한 결과를 산출하므로 사용자에게 일관된 경험이 제공됩니다.

다음 `ECID` 이 방법을 통해 검색할 수 있음 `identity.fetch` 쿼리:

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

를 모두 포함하는 요청의 경우 `FPID` 그리고 `ECID`, `ECID` 요청에 이미 있는 경우, `FPID`. 즉, 에지 네트워크는 `ECID` 이미 제공되고 있습니다. `FPID` 은 무시됩니다. 새로운 `ECID` 는 `FPID` 자체 제공됩니다.

장치 ID와 관련하여 `server` 데이터 세트는 다음 경우에 사용해야 합니다 `FPID` 를 장치 ID로 설정합니다. 기타 ID(예: `EMAIL`)도 요청 본문 내에 제공할 수 있지만, Edge Network에서는 기본 ID를 명시적으로 제공해야 합니다. 기본 ID는 프로필 데이터가 저장되는 기본 ID입니다.

>[!NOTE]
>
>각각 요청 본문 내에 명시적으로 설정된 기본 ID가 없는 요청은 실패합니다.

다음 `identityMap` 필드 그룹에 대해 올바른 형식 지정 `server` 데이터 스트림 요청:

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

다음 `identityMap` 필드 그룹에서는 `server` 데이터 스트림 요청:

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

이 경우 에지 네트워크에서 반환한 오류 응답은 다음과 유사합니다.

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

## 방문자 식별 `FPID`

를 통해 사용자 식별 `FPID`, `FPID` Edge Network에 요청하기 전에 쿠키가 전송되었습니다. 다음 `FPID` 는 쿠키나 의 일부로 전달할 수 있습니다 `identityMap` 요청 본문에.

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

## 요청 대상 `FPID` 전달 `identityMap` 필드

아래 예제는 [!DNL FPID] 로서의 `identityMap` 매개 변수.

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
