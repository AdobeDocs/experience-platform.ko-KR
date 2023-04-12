---
description: 이 페이지에서는 '/authoring/audience-templates' API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 설명합니다.
title: 대상 메타데이터 끝점 API 작업
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 4%

---

# 대상 메타데이터 끝점 API 작업

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

이 페이지에서는 를 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/audience-templates` API 엔드포인트. 이 끝점을 사용할 시기에 대한 설명은 다음을 참조하십시오. [대상 메타데이터 관리](./audience-metadata-management.md).

## 대상 템플릿 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](./getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 새 대상 템플릿 만들기 {#create}

에 POST 요청을 만들어 새 대상 템플릿을 만들 수 있습니다 `/authoring/audience-templates` 엔드포인트.

**API 형식**

```http
POST /authoring/audience-templates
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새로운 대상 메타데이터 템플릿을 만듭니다. 아래 페이로드에는 `/authoring/audience-templates` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| 속성 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `name` | 문자열 | 대상에 대한 대상 메타데이터 템플릿의 이름입니다. 이 이름은 Experience Platform 사용자 인터페이스의 모든 파트너별 오류 메시지에 나타나고 다음에 구문 분석된 오류 메시지가 표시됩니다. `metadataTemplate.create.errorSchemaMap`. |
| `url` | 문자열 | 플랫폼에서 대상/세그먼트를 만들거나, 업데이트하거나, 삭제하거나, 확인하는 데 사용되는 API의 URL과 끝점입니다. 두 가지 업계 예는 다음과 같습니다. `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 및 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | 문자열 | 엔드포인트에서 대상의 세그먼트/대상을 프로그래밍 방식으로 만들기, 업데이트, 삭제 또는 확인하는 데 사용되는 방법입니다. 예: `POST`, `PUT`, `DELETE` |
| `headers.header` | 문자열 | API 호출에 추가해야 하는 HTTP 헤더를 지정합니다. 예, `"Content-Type"` |
| `headers.value` | 문자열 | API 호출에 추가해야 하는 HTTP 헤더의 값을 지정합니다. 예, `"application/x-www-form-urlencoded"` |
| `requestBody` | 문자열 | API로 전송해야 하는 메시지 본문의 콘텐츠를 지정합니다. 에 추가해야 하는 매개 변수 `requestBody` 개체는 API에서 허용하는 필드에 따라 다릅니다. 예를 보려면 [첫 번째 템플릿 예](./audience-metadata-management.md#example-1) 을 참조하십시오. |
| `responseFields.name` | 문자열 | API가 호출될 때 반환하는 응답 필드를 지정합니다. 예를 보려면 [템플릿 예](./audience-metadata-management.md#examples) 을 참조하십시오. |
| `responseFields.value` | 문자열 | API가 호출될 때 반환하는 응답 필드의 값을 지정합니다. |
| `responseErrorFields.name` | 문자열 | API가 호출될 때 반환하는 응답 필드를 지정합니다. 예를 보려면 [ 템플릿 예](./audience-metadata-management.md#examples) 을 참조하십시오. |
| `responseErrorFields.value` | 문자열 | 대상의 API 호출 응답에서 반환되는 오류 메시지를 구문 분석합니다. 이러한 오류 메시지는 Experience Platform 사용자 인터페이스의 사용자에게 표시됩니다. |
| `validations.field` | 문자열 | 대상에 API 호출을 수행하기 전에 모든 필드에 대한 유효성 검사를 실행해야 하는지 여부를 나타냅니다. 예를 들어 `{{validations.accountId}}` 을 입력하여 사용자의 계정 ID를 확인합니다. |
| `validations.regex` | 문자열 | 유효성 검사가 전달되도록 필드를 구성하는 방법을 나타냅니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 새로 만든 대상 템플릿에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

## 대상 템플릿 업데이트 {#update}

에 PUT 요청을 만들어 기존 대상 템플릿을 업데이트할 수 있습니다. `/authoring/audience-templates` 업데이트하려는 대상 템플릿의 인스턴스 ID를 제공하고 끝점입니다. 호출 본문에서 업데이트된 템플릿을 제공합니다.

**API 형식**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 대상 메타데이터 템플릿의 ID입니다. |

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 기존 대상 메타데이터 템플릿을 업데이트합니다.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```

## 대상 템플릿 목록 검색 {#retrieve-list}

에 GET 요청을 만들어 조직에 대한 모든 대상 템플릿 목록을 검색할 수 있습니다 `/authoring/audience-templates` 엔드포인트.

**API 형식**


```http
GET /authoring/audience-templates
```

**요청**

다음 요청은 조직 및 샌드박스 구성을 기반으로 액세스 권한이 있는 대상 템플릿 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 사용한 조직 ID 및 샌드박스 이름을 기반으로 액세스 권한이 있는 대상 메타데이터 템플릿 목록과 함께 HTTP 상태 200을 반환합니다. 1개 `instanceId` 는 한 대상에 대한 템플릿에 해당합니다. 간결성을 위해 응답이 잘립니다.

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## 특정 대상 템플릿 검색 {#get}

에 GET 요청을 수행하여 특정 대상 템플릿에 대한 세부 정보를 검색할 수 있습니다 `/authoring/audience-templates` 엔드포인트 및 검색할 대상 템플릿의 인스턴스 ID를 제공합니다.

**API 형식**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 검색할 대상 메타데이터 템플릿의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 대상 템플릿에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```


## 특정 대상 템플릿 삭제 {#delete}

에 DELETE 요청을 만들어 지정된 대상 템플릿을 삭제할 수 있습니다 `/authoring/audience-templates` 요청 경로에서 삭제할 대상 템플릿의 ID를 제공하고 끝점입니다.

**API 형식**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 다음 `id` 삭제할 대상 템플릿의 일부입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 빈 HTTP 응답과 함께 HTTP 상태 200을 반환합니다.

## API 오류 처리

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 대상 메타데이터 템플릿을 사용할 시점과 를 사용하여 대상 메타데이터 템플릿을 구성하는 방법을 알 수 있습니다. `/authoring/audience-templates` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](./configure-destination-instructions.md) 대상 구성 프로세스에 이 단계가 어떤 영향을 주는지 이해하기 위해 노력합니다.
