---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 대상 템플릿을 검색하는 데 사용되는 API 호출을 예시합니다.
title: 대상자 템플릿 검색
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---


# 대상자 템플릿 검색

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

이 페이지는 대상 메타데이터 템플릿을 검색하는 데 사용할 수 있는 API 요청 및 페이로드를 구현합니다. `/authoring/audience-templates` API 엔드포인트.

이 끝점을 통해 구성할 수 있는 기능에 대한 자세한 설명은 을 참조하십시오. [대상자 메타데이터 관리](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상자 템플릿 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 대상자 템플릿 검색 {#retrieve}

다음을 수행하여 기존 대상 템플릿을 검색할 수 있습니다. `GET` 에 대한 요청 `/authoring/audience-templates` 엔드포인트.

**API 형식**

다음 API 형식을 사용하여 계정에 대한 모든 대상 템플릿을 검색합니다.

```http
GET /authoring/audience-templates
```

다음 API 형식을 사용하여 로 정의된 특정 대상 템플릿을 검색합니다. `{INSTANCE_ID}` 매개 변수.

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

다음 두 요청은 전달 여부에 따라 IMS 조직의 모든 대상 템플릿을 검색하거나 특정 대상 템플릿을 검색합니다. `INSTANCE_ID` 요청의 매개 변수입니다.

아래에서 각 탭을 선택하여 해당 페이로드를 확인합니다.

>[!BEGINTABS]

>[!TAB 모든 대상 템플릿 검색]

다음 요청은 을 기반으로 액세스 권한이 있는 대상 템플릿 목록을 검색합니다. [!DNL IMS Org ID] 샌드박스 구성.

+++요청

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++응답

성공적인 응답은 다음을 기반으로 액세스 권한이 있는 대상 템플릿 목록과 함께 HTTP 상태 200을 반환합니다. [!DNL IMS Org ID] 및 사용한 샌드박스 이름입니다. 1개 `instanceId` 은 하나의 대상 템플릿에 해당합니다.

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

+++

>[!TAB 특정 대상자 템플릿 검색]

다음 요청은 을 기반으로 액세스 권한이 있는 대상 템플릿 목록을 검색합니다. [!DNL IMS Org ID] 샌드박스 구성.

+++요청

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 검색할 대상 템플릿의 ID입니다. |

+++

+++응답

성공적인 응답은 HTTP 상태 200을 반환하며, 해당 대상 템플릿의 세부 정보는 다음과 같습니다. `{INSTANCE_ID}` 호출 시 제공됩니다.

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

+++

>[!ENDTABS]

## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 이제 를 사용하여 대상 서버 구성에 대한 세부 사항을 검색하는 방법을 알게 됩니다. `/authoring/destination-servers` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md) 대상을 구성하는 프로세스에 이 단계가 어디에 적합한지 이해할 수 있습니다.