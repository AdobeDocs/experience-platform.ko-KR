---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 대상 템플릿을 만드는 데 사용되는 API 호출을 예시합니다.
title: 대상자 템플릿 만들기
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 3%

---

# 대상자 템플릿 만들기

>[!IMPORTANT]
>
>**API 끝점**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Destination SDK을 사용하여 만든 일부 대상의 경우 대상에서 대상 메타데이터를 프로그래밍 방식으로 생성, 업데이트 또는 삭제하려면 대상 메타데이터 구성을 만들어야 합니다. 이 페이지에서는 `/authoring/audience-templates` API 끝점을 사용하여 구성을 만드는 방법을 보여 줍니다.

이 끝점을 통해 구성할 수 있는 기능에 대한 자세한 설명은 [대상 메타데이터 관리](../functionality/audience-metadata-management.md)를 참조하십시오.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상자 템플릿 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 대상자 템플릿 만들기 {#create}

`/authoring/audience-templates` 끝점에 대해 `POST` 요청을 수행하여 새 대상 템플릿을 만들 수 있습니다.

**API 형식**

```http
POST /authoring/audience-templates
```

+++요청

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 템플릿을 만듭니다. 아래 페이로드에는 `/authoring/audience-templates` 끝점에서 허용하는 모든 매개 변수가 포함되어 있습니다. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "metadataTemplate": {
    "name": "Test Webhook Audience Template",
    "create": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "update": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "PUT",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "delete": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "createDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/createDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "updateDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/updateDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "deleteDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/deleteDestination",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
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
| `name` | 문자열 | 대상의 대상 메타데이터 템플릿 이름입니다. 이 이름은 Experience Platform 사용자 인터페이스의 모든 파트너별 오류 메시지에 표시됩니다. |
| `url` | 문자열 | 플랫폼에서 대상 및/또는 데이터 흐름을 생성, 업데이트, 삭제 또는 확인하는 데 사용되는 API의 URL 및 엔드포인트. 두 가지 업계 예는 `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 및 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`입니다. |
| `httpMethod` | 문자열 | 대상에서 대상을 프로그래밍 방식으로 만들기, 업데이트, 삭제 또는 확인하기 위해 종단점에서 사용되는 메서드입니다. 예: `POST`, `PUT`, `DELETE` |
| `headers.header` | 문자열 | API 호출에 추가해야 하는 모든 HTTP 헤더를 지정합니다. 예, `"Content-Type"` |
| `headers.value` | 문자열 | API 호출에 추가해야 하는 HTTP 헤더 값을 지정합니다. 예, `"application/x-www-form-urlencoded"` |
| `requestBody` | 문자열 | API로 전송해야 하는 메시지 본문의 콘텐츠를 지정합니다. `requestBody` 개체에 추가해야 하는 매개 변수는 API에서 허용하는 필드에 따라 다릅니다. 메시지 본문에 포함할 수 있는 내용을 알아보려면 [지원되는 매크로 설명서](../functionality/audience-metadata-management.md#macros)를 참조하세요. |
| `responseFields.name` | 문자열 | 호출 시 API가 반환하는 응답 필드를 지정합니다. 예를 들어 대상 메타데이터 기능 문서에서 [템플릿 예제](../functionality/audience-metadata-management.md#examples)를 참조하십시오. |
| `responseFields.value` | 문자열 | API가 호출될 때 반환되는 응답 필드의 값을 지정합니다. |
| `responseErrorFields.name` | 문자열 | 호출 시 API가 반환하는 응답 필드를 지정합니다. 예를 들어 대상 메타데이터 기능 문서에서 [템플릿 예제](../functionality/audience-metadata-management.md#examples)를 참조하십시오. |
| `responseErrorFields.value` | 문자열 | 대상의 API 호출 응답에 대해 반환되는 모든 오류 메시지를 구문 분석합니다. 이러한 오류 메시지는 Experience Platform 사용자 인터페이스의 사용자에게 표시됩니다. |
| `validations.field` | 문자열 | 대상에 대한 API 호출이 수행되기 전에 모든 필드에 대해 유효성 검사를 실행해야 하는지 여부를 나타냅니다. 예를 들어 `{{validations.accountId}}`을(를) 사용하여 사용자의 계정 ID를 확인할 수 있습니다. |
| `validations.regex` | 문자열 | 유효성 검사를 통과하기 위해 필드를 구조화하는 방법을 나타냅니다. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 새로 생성된 대상 템플릿에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

## API 오류 처리

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. Experience Platform 문제 해결 안내서에서 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계

이제 이 문서를 읽고 나면 대상 템플릿을 사용할 시점과 `/authoring/audience-templates` API 끝점을 사용하여 대상 템플릿을 구성하는 방법을 알 수 있습니다. [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md)을 읽어 대상을 구성하는 프로세스에 이 단계가 어디에 맞는지 이해합니다.
