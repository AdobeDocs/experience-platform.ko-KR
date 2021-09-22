---
description: 서버 및 템플릿 사양은 일반적인 끝점 '/authoring/destination-server'를 통해 Adobe Experience Platform 대상 SDK에 구성할 수 있습니다.
title: 대상 SDK의 서버 및 템플릿 사양에 대한 구성 옵션
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 9%

---

# 서버 및 템플릿 사양에 대한 구성 옵션

## 개요 {#overview}

일반적인 종단점 `/authoring/destination-servers`을 통해 Adobe Experience Platform 대상 SDK에서 서버 및 템플릿 사양을 구성할 수 있습니다. 엔드포인트에서 수행할 수 있는 작업의 전체 목록은 [대상 API 엔드포인트 작업](./destination-server-api.md)을 참조하십시오.

## 예제 구성 {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## 서버 사양 {#server-specs}

![강조 표시된 서버 구성](./assets/server-configuration.png)

고객은 HTTP 내보내기를 통해 Adobe Experience Platform에서 대상에 데이터를 활성화할 수 있습니다. 서버 구성에는 메시지를 받는 서버(사용자 측 서버)에 대한 정보가 포함되어 있습니다.

이 프로세스는 대상 플랫폼에 일련의 HTTP 메시지로 사용자 데이터를 전달합니다. 아래 매개 변수는 HTTP 서버 사양 템플릿에서 가져옵니다.

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | *필수 여부.* Adobe에만 표시되는 서버의 친숙한 이름을 나타냅니다. 파트너 또는 고객은 이 이름을 볼 수 없습니다. 예 `Moviestar destination server`. |
| `destinationServerType` | 문자열 | *필수 여부.* `URL_BASED` 은 현재 사용 가능한 유일한 옵션입니다. |
| `templatingStrategy` | 문자열 | *필수 여부.* <ul><li>Adobe이 아래 `value` 필드에서 URL을 변환해야 하는 경우 `PEBBLE_V1` 을 사용합니다. 다음과 같은 종단점이 있는 경우 이 옵션을 사용합니다. `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Adobe 측에 변환이 필요하지 않으면 `NONE` 을 사용하십시오. 예를 들어 다음과 같은 종단점이 있습니다. `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 문자열 | *필수 여부.* Experience Platform이 연결해야 하는 API 엔드포인트의 주소를 입력합니다. |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## 템플릿 사양 {#template-specs}

![강조 표시된 템플릿 구성](./assets/template-configuration.png)

템플릿 사양을 사용하면 내보낸 메시지의 형식을 대상에 지정하는 방법을 구성할 수 있습니다. Adobe은 [Jinja](https://jinja.palletsprojects.com/en/2.11.x/)와 유사한 템플릿 언어를 사용하여 XDM 스키마에서 해당 필드를 대상에서 지원하는 형식으로 변환합니다. 변형에 대한 자세한 내용은 아래 링크를 참조하십시오.

* [메시지 포맷](./message-format.md)
* [ID, 속성 및 세그먼트 멤버십 변환에 템플릿 언어 사용 ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe은 메시지 변환 템플릿을 만들고 테스트하는 데 도움이 되는 [개발자 도구](./create-template.md)를 제공합니다.

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `httpMethod` | 문자열 | *필수 여부.* Adobe이 서버 호출에 사용할 메서드입니다. 옵션은 `GET`, `PUT`, `POST`, `DELETE`, `PATCH`입니다. |
| `templatingStrategy` | 문자열 | *필수 여부.*  `PEBBLE_V1`. |
| `value` | 문자열 | *필수 여부.* 이 문자열은 Platform 고객의 데이터를 서비스에 필요한 형식으로 변환하는 문자 이스케이프 처리 버전입니다. <br> 템플릿을 작성하는 방법에 대한 자세한 내용은 템플릿  [사용 섹션을 참조하십시오](./message-format.md#using-templating). <br> 문자 이스케이프에 대한 자세한 내용은  [RFC JSON 표준 섹션 7](https://tools.ietf.org/html/rfc8259#section-7)을 참조하십시오. <br> 단순 변환의 예는 프로필 속성( [Profile Attributestransformation)](./message-format.md#attributes) 을 참조하십시오. |
| `contentType` | 문자열 | *필수 여부.* 서버가 허용하는 컨텐츠 유형입니다. 이 값은 `application/json`일 가능성이 높습니다. |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
