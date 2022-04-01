---
title: 대화형 데이터 수집
description: Adobe Experience Platform Edge Network Server API에서 대화형 데이터 수집을 수행하는 방법을 알아봅니다
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs interactive data collection
keywords: 데이터 수집;수집;experience platform edge network;api;대화형 데이터 수집
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 6%

---


# 대화형 데이터 수집

## 개요 {#overview}

대화형 데이터 수집 종단점은 단일 이벤트를 수신하며 클라이언트가 Adobe Experience Platform Edge Network 서버에서 응답을 반환해야 할 때 사용됩니다. 이러한 종단점은 데이터 수집을 수행하는 동안 다른 Experience Edge 서비스의 콘텐츠를 반환할 수도 있습니다.

서버 응답에 하나 이상이 포함됩니다 `Handle` 객체(아래 표시된 대로)

## API 호출 예

### API 형식 {#format}

```http
POST /ee/v2/interact
```

### 요청 {#request}

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
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
   }
}'
```

| 매개 변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 예. | 데이터 스트림 ID. |
| `requestId` | `String` | 아니요 | 내부 서버 요청과 상관 관계가 있는 클라이언트 임의 ID를 제공합니다. 아무 것도 제공되지 않으면 에지 네트워크에서 하나를 생성하여 응답으로 반환합니다. |

### 응답 {#response}

성공한 응답은 HTTP 상태를 반환합니다 `200 OK`, 하나 이상 사용 `Handle` 객체(데이터 스트림 구성에서 활성화된 실시간 에지 서비스에 따라 다름).

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
