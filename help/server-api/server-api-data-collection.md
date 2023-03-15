---
title: 데이터 수집
description: Adobe Experience Platform Edge Network Server API가 수집된 데이터를 구조화하는 방법에 대해 알아봅니다.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---


# 데이터 수집

다음 [!DNL Server API] 는 두 가지 유형의 데이터 수집 끝점을 제공합니다.

* [대화형 데이터 수집 엔드포인트](interactive-data-collection.md)클라이언트가 서버에서 응답을 반환할 것으로 예상할 때 사용됩니다. 이러한 엔드포인트는 데이터 수집을 수행하는 동안 다른 Edge Network 서비스에서 콘텐츠를 반환할 수도 있습니다.
* [비대화형 이벤트 데이터 수집](non-interactive-data-collection.md)서버에서 응답이 필요하지 않을 때 사용됩니다. 이러한 끝점은 데이터 수집에만 사용됩니다.

## `Event` 오브젝트 {#event-object}

에서 수집한 데이터 [!DNL Server API] 은(는) 다음 구조로 되어 있습니다. `Event` 개체. 이 객체의 구조는 아래에 설명되어 있습니다.

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
| `xdm` | 오브젝트 | *필수 여부*. 데이터 세트 스키마에 해당하는 XDM 형식의 데이터가 포함된 JSON 개체입니다. |
| `data` | 오브젝트 | *선택 사항입니다*. Edge Network에서 XDM에 매핑할 수 있는 자유 형식 데이터가 포함된 JSON 개체입니다. |

