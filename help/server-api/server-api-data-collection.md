---
title: 데이터 수집
description: Adobe Experience Platform Edge Network Server API가 수집된 데이터를 구성하는 방법을 알아봅니다
seo-description: Learn how the Adobe Experience Platform Edge Network Server API structures the collected data
keywords: 데이터 수집;수집;Adobe Experience Platform Edge Network;api;구조
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 4%

---


# 데이터 수집

다음 [!DNL Server API] 에서는 두 가지 유형의 데이터 수집 끝점을 제공합니다.

* [대화형 데이터 수집 끝점](interactive-data-collection.md): 클라이언트가 서버에서 응답을 반환해야 할 때 사용됩니다. 이러한 종단점은 데이터 수집을 수행하는 동안 다른 Edge 네트워크 서비스의 콘텐츠를 반환할 수도 있습니다.
* [비대화형 이벤트 데이터 수집](non-interactive-data-collection.md): 서버에서 응답이 필요하지 않을 때 사용됩니다. 이러한 종단점은 데이터 수집에만 사용됩니다.

## `Event` 개체 {#event-object}

에 의해 수집된 데이터 [!DNL Server API] 는 `Event` 개체. 이 객체의 구조는 아래에 설명되어 있습니다.

```json
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
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| 속성 | 유형 | 설명 |
| --- | --- | --- |
| `xdm` | 개체 | *필수 여부*. 데이터 세트 스키마에 해당하는 XDM 형식의 데이터가 포함된 JSON 개체. |
| `data` | 개체 | *선택 사항입니다*. Edge Network에서 XDM에 매핑할 수 있는 자유 양식 데이터가 포함된 JSON 개체입니다. |

