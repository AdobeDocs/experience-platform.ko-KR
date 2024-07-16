---
title: 대화형 데이터 수집
description: Adobe Experience Platform Edge Network 서버 API에서 대화형 데이터 수집을 수행하는 방법에 대해 알아봅니다.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f8434746c4a023ec895d23a59e04fca4baecfc36
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---

# 대화형 데이터 수집

## 개요 {#overview}

대화형 데이터 수집 엔드포인트는 단일 이벤트를 수신하며, 클라이언트가 Adobe Experience Platform Edge Network 서버에서 응답이 반환될 것으로 예상할 때 사용됩니다. 이러한 엔드포인트는 데이터 수집을 수행하는 동안 다른 Edge Network 서비스에서 콘텐츠를 반환할 수도 있습니다.

>[!IMPORTANT]
>
>`/interact` 끝점은 주로 Experience Platform SDK에서 사용하도록 디자인되었습니다. 이 종단점은 추가 변경 사항이며 해당 동작은 예고 없이 발전할 수 있습니다. 예를 들어 나중에 응답 페이로드에 새 항목이 추가될 수 있습니다.

아래 표시된 대로 서버 응답에 하나 이상의 `Handle` 개체가 포함되어 있습니다.

## API 호출 예

### API 형식 {#format}

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

| 매개변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 예. | 데이터 스트림 ID입니다. |
| `requestId` | `String` | 아니요 | 내부 서버 요청의 상관 관계를 확인하기 위해 클라이언트 임의 ID를 제공합니다. 아무 것도 제공되지 않으면 Edge Network이 생성한 후 응답에 반환합니다. |

### 응답 {#response}

성공한 응답은 데이터 스트림 구성에서 활성화된 실시간 에지 서비스에 따라 하나 이상의 `Handle` 개체와 함께 HTTP 상태 `200 OK`을(를) 반환합니다.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
