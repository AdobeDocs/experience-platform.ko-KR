---
title: 비대화형 데이터 수집
description: Adobe Experience Platform Edge Network Server API가 비대화형 데이터 수집을 수행하는 방법에 대해 알아봅니다.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---


# 비대화형 데이터 수집

## 개요 {#overview}

비대화형 이벤트 데이터 수집 엔드포인트는 여러 이벤트를 Experience Platform 데이터 세트 또는 다른 콘센트로 전송하는 데 사용됩니다.

최종 사용자 이벤트가 짧은 기간(예: 네트워크 연결이 없는 경우) 로컬 큐에 있는 경우 이벤트를 일괄 보내는 것이 좋습니다.

일괄 처리 이벤트는 반드시 동일한 최종 사용자에게 속하지 않아야 합니다. 즉, 이벤트는 이벤트 내에 서로 다른 ID를 보유할 수 있습니다 `identityMap` 개체.

## 비대화형 API 호출 예 {#example}

### API 형식 {#api-format}

```http
POST /ee/v2/collect
```

### 요청 {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
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

| 매개변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 예 | 데이터 수집 끝점에서 사용하는 데이터 스트림의 ID입니다. |
| `requestId` | `String` | 아니요 | 외부 요청 추적 ID를 제공합니다. 아무 것도 제공되지 않으면 Edge Network가 자동으로 생성한 후 응답 본문/헤더로 다시 반환합니다. |
| `silent` | `Boolean` | 아니요 | Edge Network가 `204 No Content` 페이로드가 비어 있거나 없는 응답입니다. 해당 HTTP 상태 코드 및 페이로드를 사용하여 심각한 오류가 보고됩니다. |

### 응답 {#response}

성공적인 응답은 다음 상태 중 하나를 반환하며 `requestID` 요청에 아무 것도 제공되지 않은 경우.

* `202 Accepted` 요청이 성공적으로 처리된 경우
* `204 No Content` 요청이 성공적으로 처리되고 `silent` 매개 변수가 로 설정되었습니다. `true`;
* `400 Bad Request` 요청이 제대로 구성되지 않은 경우(예: 필수 기본 id를 찾을 수 없음).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
