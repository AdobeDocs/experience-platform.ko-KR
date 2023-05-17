---
description: 이 페이지에서는 Adobe Experience Platform Destination SDK을 통해 대상 템플릿을 만드는 데 사용되는 API 호출을 보여줍니다.
title: 대상 템플릿 만들기
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# 대상 템플릿 만들기

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Destination SDK을 사용하여 만든 일부 대상의 경우, 대상에서 세그먼트 메타데이터를 프로그래밍 방식으로 만들기, 업데이트 또는 삭제하기 위해 대상 메타데이터 구성을 만들어야 합니다. 이 페이지에서는 `/authoring/audience-templates` 구성을 만들기 위한 API 엔드포인트.

이 종단점을 통해 구성할 수 있는 기능에 대한 자세한 내용은 [대상 메타데이터 관리](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 템플릿 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 대상 템플릿 만들기 {#create}

을(를) 만들어 새 대상 템플릿을 만들 수 있습니다 `POST` 에 요청 `/authoring/audience-templates` 엔드포인트.

**API 형식**

```http
POST /authoring/audience-templates
```

+++요청

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 템플릿을 만듭니다. 아래 페이로드에는 `/authoring/audience-templates` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

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
| `requestBody` | 문자열 | API로 전송해야 하는 메시지 본문의 콘텐츠를 지정합니다. 에 추가해야 하는 매개 변수 `requestBody` 개체는 API에서 허용하는 필드에 따라 다릅니다. 예를 보려면 [첫 번째 템플릿 예](../functionality/audience-metadata-management.md#example-1) 을 참조하십시오. |
| `responseFields.name` | 문자열 | API가 호출될 때 반환하는 응답 필드를 지정합니다. 예를 보려면 [템플릿 예](../functionality/audience-metadata-management.md#examples) 을 참조하십시오. |
| `responseFields.value` | 문자열 | API가 호출될 때 반환하는 응답 필드의 값을 지정합니다. |
| `responseErrorFields.name` | 문자열 | API가 호출될 때 반환하는 응답 필드를 지정합니다. 예를 보려면 [ 템플릿 예](../functionality/audience-metadata-management.md#examples) 을 참조하십시오. |
| `responseErrorFields.value` | 문자열 | 대상의 API 호출 응답에서 반환되는 오류 메시지를 구문 분석합니다. 이러한 오류 메시지는 Experience Platform 사용자 인터페이스의 사용자에게 표시됩니다. |
| `validations.field` | 문자열 | 대상에 API 호출을 수행하기 전에 모든 필드에 대한 유효성 검사를 실행해야 하는지 여부를 나타냅니다. 예를 들어 `{{validations.accountId}}` 을 입력하여 사용자의 계정 ID를 확인합니다. |
| `validations.regex` | 문자열 | 유효성 검사가 전달되도록 필드를 구성하는 방법을 나타냅니다. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 새로 만든 대상 템플릿에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

## API 오류 처리

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 대상 템플릿을 사용할 시점과 를 사용하여 대상 템플릿을 구성하는 방법을 알 수 있습니다. `/authoring/audience-templates` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md) 대상 구성 프로세스에 이 단계가 어떤 영향을 주는지 이해하기 위해 노력합니다.
