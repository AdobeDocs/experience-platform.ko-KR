---
title: 비대화형 데이터 수집
description: Adobe Experience Platform Edge Network Server API에서 비대화형 데이터 수집을 수행하는 방법을 알아봅니다
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs non-interactive data collection
keywords: 데이터 수집;수집;adobe experience platform edge network;api;비대화형 데이터 수집
source-git-commit: 3bb73e5798d8fcdb6bb8bdcb796e8df6a1bd8805
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 4%

---


# 비대화형 데이터 수집

## 개요 {#overview}

비대화형 이벤트 데이터 수집 끝점은 여러 이벤트를 Experience Platform 데이터 세트 또는 다른 콘센트에 보내는 데 사용됩니다.

최종 사용자 이벤트가 짧은 시간 동안(예: 네트워크 연결이 없는 경우)에 로컬로 대기할 때 일괄적으로 이벤트를 전송하는 것이 좋습니다.

일괄 처리 이벤트가 반드시 동일한 최종 사용자에게 속할 필요는 없습니다. 즉, 이벤트가 해당 이벤트 내에 서로 다른 ID를 보유할 수 있습니다 `identityMap` 개체.


<!-- However, when an `ECID` identity is sent via a cookie or metadata (in Edge Network accepted format), the Edge Network will read it and associate it with each event in the batch.

Each event should include the corresponding `XDM` content that needs to be collected.

>[!NOTE]
>
>[Experience Edge Identity Protocol](visitor-identification.md#experience-edge-identity-protocol) (`ECID` generation) is not applicable for data collection requests, meaning that events sent to this API should already have at least one identity associated to them. For server datastreams (calls to `server.adobedc.net`), the API requires that each event contains an identity **explicitly set as primary**. For device datastreams, the Edge Network will attempt to set the `ECID` as primary, when it is present, and no other primary identity is explicitly set.

-->

## 비대화형 API 호출 예 {#example}

### API 형식 {#api-format}

```http
POST /ee/v2/collect
```

### 요청 {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webpagedetails.pageViews",
            "web": {
               "webPageDetails": {
                  "URL": "https://alloystore.dev/",
                  "name": "home-demo-Home Page"
               }
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         },
         "data": {
            "prop1": "custom value"
         }
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| 매개 변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 예 | 데이터 수집 끝점에서 사용하는 데이터 스트림의 ID입니다. |
| `requestId` | `String` | 아니요 | 외부 요청 추적 ID를 제공합니다. 제공된 항목이 없으면 Edge Network에서 사용자를 위해 하나를 생성하고 응답 본문/헤더에 다시 반환합니다. |
| `silent` | `Boolean` | 아니요 | Edge Network가 `204 No Content` 응답이 비어 있는지 여부. 중요한 오류는 해당 HTTP 상태 코드 및 페이로드를 사용하여 보고됩니다. |


### 응답 {#response}

성공적인 응답은 다음 상태 중 하나를 반환하고 `requestID` 요청에 아무 것도 제공되지 않은 경우.

* `202 Accepted` 요청이 성공적으로 처리된 시기;
* `204 No Content` 요청이 성공적으로 처리되고 `silent` 매개 변수가 `true`;
* `400 Bad Request` 요청이 제대로 구성되지 않은 경우(예: 필수 기본 ID를 찾을 수 없음)

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
