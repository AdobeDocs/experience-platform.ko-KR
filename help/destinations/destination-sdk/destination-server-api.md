---
description: 이 페이지에서는 '/authoring/destination-server' API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. 대상에 대한 서버 및 템플릿 사양은 일반적인 끝점 '/authoring/destination-servers'를 통해 Adobe Experience Platform 대상 SDK에 구성할 수 있습니다.
title: 대상 서버 끝점 API 작업
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 4%

---

# 대상 서버 끝점 API 작업

>[!IMPORTANT]
>
>**API 엔드포인트**:  `platform.adobe.io/data/core/activation/authoring/destination-servers`

이 페이지에서는 `/authoring/destination-servers` API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. 대상에 대한 서버 및 템플릿 사양은 공통 끝점 `/authoring/destination-servers`을 통해 Adobe Experience Platform 대상 SDK에 구성할 수 있습니다. 이 끝점에서 제공하는 기능에 대한 설명은 [서버 및 템플릿 사양](./server-and-template-configuration.md)을 참조하십시오.

## 대상 서버 API 작업 시작 {#get-started}

계속하기 전에 필요한 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보가 필요하면 [시작 안내서](./getting-started.md)를 검토하십시오.

## 대상 서버에 대한 구성 만들기 {#create}

`/authoring/destination-servers` 종단점에 대한 POST 요청을 수행하여 새 대상 서버 구성을 만들 수 있습니다.

**API 형식**


```http
POST /authoring/destination-servers
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 서버 구성을 만듭니다. 아래 페이로드에는 `/authoring/destination-servers` 종단점에서 허용하는 모든 매개 변수가 포함되어 있습니다. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
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

| 매개 변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `name` | 문자열 | Adobe에만 표시되는 서버의 친숙한 이름을 나타냅니다. 파트너 또는 고객은 이 이름을 볼 수 없습니다. 예 `Moviestar destination server`. |
| `destinationServerType` | 문자열 | `URL_BASED` 은 현재 사용 가능한 유일한 옵션입니다. |
| `urlBasedDestination.url.templatingStrategy` | 문자열 | <ul><li>Adobe이 아래 `value` 필드에서 URL을 변환해야 하는 경우 `PEBBLE_V1` 을 사용합니다. 다음과 같은 종단점이 있는 경우 이 옵션을 사용합니다. `https://api.moviestar.com/data/{{endpoint.region}}/items` </li><li> Adobe 측에 변환이 필요하지 않으면 `NONE` 을 사용하십시오. 예를 들어 다음과 같은 종단점이 있습니다. `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 문자열 | Experience Platform이 연결해야 하는 API 엔드포인트의 주소를 입력합니다. |
| `urlBasedDestination.maxUsersPerRequest` | 정수 | Adobe은 내보낸 여러 프로필을 단일 HTTP 호출로 집계할 수 있습니다. 하나의 HTTP 호출에서 엔드포인트가 수신할 최대 프로필 수를 지정합니다. 이는 최상의 노력 집계에 해당합니다. 예를 들어 값 100을 지정하는 경우 Adobe은 호출 시 100보다 작은 수의 프로필을 전송할 수 있습니다. <br> 서버가 요청당 여러 사용자를 허용하지 않는 경우 이 값을 1로 설정하십시오. |
| `urlBasedDestination.splitUserById` | 부울 | 대상에 대한 호출이 ID로 분할되어야 하는 경우 이 플래그를 사용합니다. 서버가 특정 네임스페이스에 대해 호출당 하나의 ID만 수락하는 경우 이 플래그를 `true`로 설정하십시오. |
| `httpTemplate.httpMethod` | 문자열 | Adobe이 서버 호출에 사용할 메서드입니다. 옵션은 `GET`, `PUT`, `POST`, `DELETE`, `PATCH`입니다. |
| `httpTemplate.requestBody.templatingStrategy` | 문자열 |  `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | 문자열 | 이 문자열은 Platform 고객의 데이터를 서비스에 필요한 형식으로 변환하는 문자 이스케이프 처리 버전입니다. <br> <ul><li> 템플릿을 작성하는 방법에 대한 자세한 내용은 [템플릿 사용 섹션](./message-format.md#using-templating)을 참조하십시오. </li><li> 문자 이스케이프에 대한 자세한 내용은 [RFC JSON 표준, 7](https://tools.ietf.org/html/rfc8259#section-7) 섹션을 참조하십시오. </li><li> 단순 변환의 예는 [프로필 속성](./message-format.md#attributes) 변형을 참조하십시오. </li></ul> |
| `httpTemplate.contentType` | 문자열 | 서버가 허용하는 컨텐츠 유형입니다. 이 값은 `application/json`일 가능성이 높습니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

## 대상 서버 구성 나열 {#retrieve-list}

`/authoring/destination-servers` 종단점에 GET 요청을 수행하여 IMS 조직에 대한 모든 대상 서버 구성 목록을 검색할 수 있습니다.

**API 형식**


```http
GET /authoring/destination-servers
```

**요청**

다음 요청은 IMS 조직 및 샌드박스 구성을 기반으로 액세스 권한이 있는 대상 서버 구성 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 사용한 IMS 조직 ID 및 샌드박스 이름을 기반으로 액세스 권한이 있는 대상 서버 구성 목록과 함께 HTTP 상태 200을 반환합니다. 하나의 `instanceId` 은 하나의 대상 서버에 대한 템플릿에 해당합니다. 간결성을 위해 응답이 잘립니다.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
    
```

## 기존 대상 서버 구성 업데이트 {#update}

`/authoring/destination-servers` 종단점에 PUT 요청을 만들고 업데이트할 대상 서버 구성의 인스턴스 ID를 제공하여 기존 대상 서버 구성을 업데이트할 수 있습니다. 호출 본문에서 업데이트된 대상 서버 구성을 제공합니다.

**API 형식**


```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 대상 서버 구성의 ID입니다. |

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 기존 대상 서버 구성을 업데이트합니다.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
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





## 특정 대상 서버 구성 검색 {#get}

`/authoring/destination-servers` 종단점에 GET 요청을 하고 업데이트할 대상 서버 구성의 인스턴스 ID를 제공하여 특정 대상 서버 구성에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**


```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 검색할 대상 서버 구성의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
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


## 특정 대상 서버 구성 삭제 {#delete}

`/authoring/destination-servers` 종단점에 DELETE 요청을 하고 요청 경로에서 삭제하려는 대상 서버 구성의 ID를 제공하여 지정된 대상 서버 구성을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 삭제할 대상 서버 구성의 `id` |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 빈 HTTP 응답과 함께 HTTP 상태 200을 반환합니다.

## API 오류 처리

대상 SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 및 [요청 헤더 오류](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)를 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 `/authoring/destination-servers` API 종단점을 사용하여 대상 서버와 템플릿을 구성하는 방법을 알 수 있습니다. [대상 SDK를 사용하여 대상](./configure-destination-instructions.md)을 구성하는 방법을 읽어 이 단계가 대상 구성 프로세스에 맞는 위치를 파악합니다.
