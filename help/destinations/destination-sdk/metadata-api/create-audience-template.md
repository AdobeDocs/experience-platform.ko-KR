---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 대상 템플릿을 만드는 데 사용되는 API 호출을 예시합니다.
title: 대상자 템플릿 만들기
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 4%

---

# 대상자 템플릿 만들기

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Destination SDK을 사용하여 만든 일부 대상의 경우 대상에서 대상 메타데이터를 프로그래밍 방식으로 생성, 업데이트 또는 삭제하려면 대상 메타데이터 구성을 만들어야 합니다. 이 페이지에서는 사용 방법을 보여 줍니다. `/authoring/audience-templates` 구성을 만들기 위한 API 엔드포인트.

이 끝점을 통해 구성할 수 있는 기능에 대한 자세한 설명은 을 참조하십시오. [대상자 메타데이터 관리](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상자 템플릿 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 대상자 템플릿 만들기 {#create}

다음을 수행하여 새 대상 템플릿을 만들 수 있습니다. `POST` 에 대한 요청 `/authoring/audience-templates` 엔드포인트.

**API 형식**

```http
POST /authoring/audience-templates
```

+++요청

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 템플릿을 만듭니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/audience-templates` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

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
| `url` | 문자열 | 플랫폼에서 대상을 생성, 업데이트, 삭제 또는 확인하는 데 사용되는 API의 URL 및 엔드포인트. 두 가지 업계 예는 다음과 같습니다. `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 및 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | 문자열 | 대상에서 대상을 프로그래밍 방식으로 만들기, 업데이트, 삭제 또는 확인하기 위해 종단점에서 사용되는 메서드입니다. 예: `POST`, `PUT`, `DELETE` |
| `headers.header` | 문자열 | API 호출에 추가해야 하는 모든 HTTP 헤더를 지정합니다. 예, `"Content-Type"` |
| `headers.value` | 문자열 | API 호출에 추가해야 하는 HTTP 헤더 값을 지정합니다. 예, `"application/x-www-form-urlencoded"` |
| `requestBody` | 문자열 | API로 전송해야 하는 메시지 본문의 콘텐츠를 지정합니다. 에 추가해야 하는 매개 변수 `requestBody` 개체는 API가 허용하는 필드에 따라 다릅니다. 예를 보려면 [첫 번째 템플릿 예](../functionality/audience-metadata-management.md#example-1) 대상 메타데이터 기능 문서에서 참조하십시오. |
| `responseFields.name` | 문자열 | 호출 시 API가 반환하는 응답 필드를 지정합니다. 예를 보려면 [템플릿 예](../functionality/audience-metadata-management.md#examples) 대상 메타데이터 기능 문서에서 참조하십시오. |
| `responseFields.value` | 문자열 | API가 호출될 때 반환되는 응답 필드의 값을 지정합니다. |
| `responseErrorFields.name` | 문자열 | 호출 시 API가 반환하는 응답 필드를 지정합니다. 예를 보려면 [템플릿 예](../functionality/audience-metadata-management.md#examples) 대상 메타데이터 기능 문서에서 참조하십시오. |
| `responseErrorFields.value` | 문자열 | 대상의 API 호출 응답에 대해 반환되는 모든 오류 메시지를 구문 분석합니다. 이러한 오류 메시지는 Experience Platform 사용자 인터페이스의 사용자에게 표시됩니다. |
| `validations.field` | 문자열 | 대상에 대한 API 호출이 수행되기 전에 모든 필드에 대해 유효성 검사를 실행해야 하는지 여부를 나타냅니다. 예를 들어 다음을 사용할 수 있습니다. `{{validations.accountId}}` 을 클릭하여 사용자의 계정 ID를 확인합니다. |
| `validations.regex` | 문자열 | 유효성 검사를 통과하기 위해 필드를 구조화하는 방법을 나타냅니다. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 새로 생성된 대상 템플릿에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

## API 오류 처리

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계

이 문서를 읽고 나면 이제 대상 템플릿을 사용할 시점과 을 사용하여 대상 템플릿을 구성하는 방법을 이해할 수 있습니다. `/authoring/audience-templates` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md) 대상을 구성하는 프로세스에 이 단계가 어디에 적합한지 이해할 수 있습니다.
