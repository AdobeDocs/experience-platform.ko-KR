---
description: 이 페이지에서는 "/authoring/audience-templates" API 엔드포인트를 사용하여 수행할 수 있는 모든 API 작업에 대해 설명합니다.
title: 대상 메타데이터 끝점 API 작업
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 4%

---

# 대상 메타데이터 끝점 API 작업

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

이 페이지에서는 다음을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/audience-templates` API 엔드포인트. 이 끝점을 사용할 시기에 대한 설명은 다음을 참조하십시오. [대상자 메타데이터 관리](./audience-metadata-management.md).

## 대상 템플릿 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 새 대상 템플릿 만들기 {#create}

에 POST 요청을 하여 새 대상 템플릿을 만들 수 있습니다. `/authoring/audience-templates` 엔드포인트.

**API 형식**

```http
POST /authoring/audience-templates
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 메타데이터 템플릿을 만듭니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/audience-templates` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

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
| `name` | 문자열 | 대상의 대상 메타데이터 템플릿 이름입니다. 이 이름은에서 구문 분석한 오류 메시지가 표시되고 Experience Platform 사용자 인터페이스의 모든 파트너별 오류 메시지에 표시됩니다. `metadataTemplate.create.errorSchemaMap`. |
| `url` | 문자열 | 플랫폼에서 대상/세그먼트를 생성, 업데이트, 삭제 또는 확인하는 데 사용되는 API의 URL 및 엔드포인트. 두 가지 업계 예는 다음과 같습니다. `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 및 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | 문자열 | 대상에서 세그먼트/대상을 프로그래밍 방식으로 만들거나, 업데이트하거나, 삭제하거나, 유효성을 검사하는 데 종단점에 사용되는 메서드입니다. 예: `POST`, `PUT`, `DELETE` |
| `headers.header` | 문자열 | API 호출에 추가해야 하는 모든 HTTP 헤더를 지정합니다. 예, `"Content-Type"` |
| `headers.value` | 문자열 | API 호출에 추가해야 하는 HTTP 헤더 값을 지정합니다. 예, `"application/x-www-form-urlencoded"` |
| `requestBody` | 문자열 | API로 전송해야 하는 메시지 본문의 콘텐츠를 지정합니다. 에 추가해야 하는 매개 변수 `requestBody` 개체는 API가 허용하는 필드에 따라 다릅니다. 예를 보려면 [첫 번째 템플릿 예](./audience-metadata-management.md#example-1) 대상 메타데이터 기능 문서에서 참조하십시오. |
| `responseFields.name` | 문자열 | 호출 시 API가 반환하는 응답 필드를 지정합니다. 예를 보려면 [템플릿 예](./audience-metadata-management.md#examples) 대상 메타데이터 기능 문서에서 참조하십시오. |
| `responseFields.value` | 문자열 | API가 호출될 때 반환되는 응답 필드의 값을 지정합니다. |
| `responseErrorFields.name` | 문자열 | 호출 시 API가 반환하는 응답 필드를 지정합니다. 예를 보려면 [ 템플릿 예](./audience-metadata-management.md#examples) 대상 메타데이터 기능 문서에서 참조하십시오. |
| `responseErrorFields.value` | 문자열 | 대상의 API 호출 응답에 대해 반환되는 모든 오류 메시지를 구문 분석합니다. 이러한 오류 메시지는 Experience Platform 사용자 인터페이스의 사용자에게 표시됩니다. |
| `validations.field` | 문자열 | 대상에 대한 API 호출이 수행되기 전에 모든 필드에 대해 유효성 검사를 실행해야 하는지 여부를 나타냅니다. 예를 들어 다음을 사용할 수 있습니다. `{{validations.accountId}}` 을 클릭하여 사용자의 계정 ID를 확인합니다. |
| `validations.regex` | 문자열 | 유효성 검사를 통과하기 위해 필드를 구조화하는 방법을 나타냅니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 새로 생성된 대상 템플릿에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

## 대상자 템플릿 업데이트 {#update}

에 PUT 요청을 하여 기존 대상 템플릿을 업데이트할 수 있습니다. `/authoring/audience-templates` 엔드포인트 및 업데이트하려는 대상 템플릿의 인스턴스 ID 제공 호출 본문에서 업데이트된 템플릿을 제공합니다.

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

## 대상자 템플릿 목록 검색 {#retrieve-list}

에 GET 요청을 하여 IMS 조직에 대한 모든 대상 템플릿 목록을 검색할 수 있습니다. `/authoring/audience-templates` 엔드포인트.

**API 형식**


```http
GET /authoring/audience-templates
```

**요청**

다음 요청은 IMS 조직 및 샌드박스 구성을 기반으로 액세스 권한이 있는 대상 템플릿 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 사용한 IMS 조직 ID와 샌드박스 이름을 기반으로 액세스 권한이 있는 대상 메타데이터 템플릿 목록과 함께 HTTP 상태 200을 반환합니다. 1개 `instanceId` 은 하나의 대상에 대한 템플릿에 해당합니다. 응답은 간결성을 위해 잘립니다.

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

## 특정 대상자 템플릿 검색 {#get}

에 GET 요청을 하여 특정 대상 템플릿에 대한 자세한 정보를 검색할 수 있습니다. `/authoring/audience-templates` 엔드포인트 및 검색할 대상 템플릿의 인스턴스 ID 제공

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

성공적인 응답은 지정된 대상 템플릿에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

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

에 DELETE 요청을 하여 지정된 대상 템플릿을 삭제할 수 있습니다. `/authoring/audience-templates` 엔드포인트 및 요청 경로에서 삭제하고자 하는 대상 템플릿의 ID를 제공합니다.

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

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계

이제 이 문서를 읽고 나면 대상 메타데이터 템플릿을 사용해야 하는 시기와 를 사용하여 대상 메타데이터 템플릿을 구성하는 방법을 이해할 수 있습니다. `/authoring/audience-templates` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](./configure-destination-instructions.md) 대상을 구성하는 프로세스에 이 단계가 어디에 적합한지 이해할 수 있습니다.
