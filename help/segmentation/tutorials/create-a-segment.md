---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 세그먼트 만들기
topic: tutorial
translation-type: tm+mt
source-git-commit: a6a1ecd9ce49c0a55e14b0d5479ca7315e332904

---


# 세그먼트 만들기

이 문서에서는 세그멘테이션 API를 사용하여 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하기 위한 자습서를 [제공합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

사용자 인터페이스를 사용하여 세그먼트를 만드는 방법에 대한 자세한 내용은 세그먼트 빌더 [안내서를](../ui/overview.md)참조하십시오.

## 시작하기

이 자습서에서는 대상 세그먼트 만들기와 관련된 다양한 Adobe Experience Platform 서비스에 대해 잘 이해해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [실시간 고객 프로필](../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.
- [Adobe Experience Platform 세그멘테이션 서비스](../home.md):실시간 고객 프로필 데이터를 통해 고객 세그먼트를 만들 수 있습니다.
- [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

다음 섹션에서는 플랫폼 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 세그먼트 정의 개발

세그멘테이션의 첫 번째 단계는 **세그먼트 정의라는**&#x200B;구문으로 표시되는 세그먼트를 정의하는 것입니다. 세그먼트 정의는 PQL(프로필 쿼리 언어)으로 작성된 쿼리를 캡슐화하는 개체입니다. 이 개체를 PQL 조건이라고도 **합니다**. PQL은 실시간 고객 프로필에 제공하는 레코드 또는 시간 시리즈 데이터와 관련된 조건을 기반으로 세그먼트에 대한 규칙을 정의합니다. PQL [쿼리 작성에 대한 자세한 내용은 PQL 안내서를](../pql/overview.md) 참조하십시오.

실시간 고객 프로필 API에서 `/segment/definitions` 종단점에 대한 POST 요청을 만들어 새 세그먼트 정의를 만들 수 있습니다. 다음 예에서는 세그먼트를 성공적으로 정의하기 위해 필요한 정보를 포함하여 정의 요청의 형식을 지정하는 방법에 대해 대략적으로 설명합니다.

세그먼트 정의는 일괄 세그먼테이션 및 스트리밍 세그먼테이션의 두 가지 방법으로 평가할 수 있습니다. 일괄 세그먼테이션은 사전 설정 일정을 기반으로 하거나 평가가 수동으로 트리거될 때 세그먼트를 평가하지만, 스트리밍 세그멘테이션은 데이터가 플랫폼에서 인제스트되는 즉시 세그먼트를 평가합니다. 이 자습서는 **일괄 세그먼테이션을 사용합니다**. 스트리밍 세그멘테이션에 대한 자세한 내용은 스트리밍 세그멘테이션에 대한 [개요를 참조하십시오](../api/streaming-segmentation.md).

**API 형식**

```http
POST /segment/definitions
```

**요청**

다음 요청은 &quot;MyProfile&quot;이라는 스키마에 대한 새 세그먼트 정의를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| 속성 | 설명 |
| --------- | ------------ | 
| `name` | **필수 여부.** 세그먼트를 참조하는 고유한 이름입니다. |
| `schema` | **필수 여부.** 세그먼트의 엔티티와 연결된 스키마입니다. 필드 `id` 또는 `name` 필드로 구성됩니다. |
| `expression` | **필수 여부.** 세그먼트 정의에 대한 필드 정보를 포함하는 엔티티입니다. |
| `expression.type` | 표현식 유형을 지정합니다. 현재 &quot;PQL&quot;만 지원됩니다. |
| `expression.format` | 값의 표현식 구조를 나타냅니다. 현재 지원되는 형식은 다음과 같습니다. <ul><li>`pql/text`:게시된 PQL 문법에 따라 세그먼트 정의의 텍스트 표현입니다.  예, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | 에 표시된 유형을 따르는 표현식입니다 `expression.format`. |
| `mergePolicyId` | 내보낸 데이터에 사용할 병합 정책의 식별자입니다. 자세한 내용은 [병합 정책 구성 문서를](../../profile/api/merge-policies.md)참조하십시오. |
| `description` | 사람이 읽을 수 있는 정의에 대한 설명입니다. |

**응답**

성공적인 응답은 시스템 생성, 읽기 전용 등 새로 만든 세그먼트 정의의 세부 사항을 반환하며, `id` 이 방법은 이 자습서의 후반부에 사용됩니다.

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## 대상 예측 및 미리 보기

세그먼트 정의를 개발할 때 실시간 고객 프로필 내에서 예측 및 미리 보기 도구를 사용하여 요약 수준 정보를 보고 예상 고객을 분리할 수 있습니다. 예상치는 예상 대상 크기 및 신뢰 간격과 같은 세그먼트 정의에 대한 통계 정보를 제공합니다. 미리 보기에서는 세그먼트 정의에 대한 적격한 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다.

대상을 예상 및 미리 보기하여 PQL 예측 결과를 생성하고 이를 업데이트된 세그먼트 정의에서 사용할 수 있도록 최적화할 수 있습니다.

세그먼트를 미리 보거나 견적을 받는 데 필요한 두 가지 단계가 있습니다.

1. [미리 보기 작업 만들기](#create-a-preview-job)
2. [미리 보기 작업의 ID를 사용하여 예상 또는 미리 보기](#view-an-estimate-or-preview) 보기

### 예상 생성 방법

데이터 샘플은 세그먼트를 평가하고 적격한 프로필 수를 계산하는 데 사용됩니다. 새로운 데이터는 매일 아침(오전 7-9AM UTC인 12AM-2PT 사이) 메모리에 로드되며 모든 세그멘테이션 쿼리는 해당 일의 샘플 데이터를 사용하여 예측됩니다. 따라서 추가된 새 필드 또는 수집된 추가 데이터는 다음 날 추정에 반영됩니다.

샘플 크기는 프로필 스토어의 전체 개체 수에 따라 달라집니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 저장소의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1~2천만 | 100만 |
| 2천만 명 이상 | 총계의 5% |

추정은 일반적으로 10-15초 이상 실행되며, 추정치는 대략적인 추정으로 시작하여 더 많은 기록을 읽으면서 세부적으로 진행됩니다.

### 미리 보기 작업 만들기

종단점에 POST 요청을 만들어 새 미리 보기 작업을 만들 수 `/preview` 있습니다.

**API 형식**

```http
POST /preview
```

**요청**

다음 요청은 새 미리 보기 작업을 만듭니다. 요청 본문에는 세그먼트와 관련된 쿼리 정보가 포함되어 있습니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `predicateExpression` | 데이터를 쿼리할 PQL 표현식입니다. |
| `predicateModel` | 프로필 데이터가 기반으로 하는 XDM 스키마의 이름입니다. |

**응답**

성공적인 응답은 ID 및 현재 처리 상태를 포함하여 새로 만든 미리 보기 작업의 세부 사항을 반환합니다.

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `state` | 미리 보기 작업의 현재 상태입니다. 처리가 완료될 때까지 &quot;RUNNING&quot; 상태가 되며, 여기서 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `previewId` | 다음 섹션에 설명된 대로 예측 또는 미리 보기를 볼 때 조회 목적으로 사용할 미리 보기 작업의 ID입니다. |

### 예상 또는 미리 보기 보기

서로 다른 쿼리가 완료하는 데 다른 시간이 걸릴 수 있으므로 예측 및 미리 보기 프로세스가 비동기식으로 실행됩니다. 쿼리가 시작되면 API 호출을 사용하여 진행 중인 예상 또는 미리 보기의 현재 상태를 검색(GET)할 수 있습니다.

실시간 고객 프로필 API를 사용하여 미리 보기 작업의 현재 상태를 ID로 조회할 수 있습니다. 상태가 &quot;RESULT_READY&quot;인 경우 결과를 볼 수 있습니다. 예상 또는 미리 보기를 볼지 여부에 따라 각각 API에 자체 종점이 있습니다. 두 가지 모두에 대한 예는 아래에 나와 있습니다.

### 예상 보기

**API 형식**

```http
GET /estimate/{PREVIEW_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{PREVIEW_ID}` | 보려는 미리 보기 작업의 ID입니다. |

**요청**

다음 요청은 이전 단계에서 `previewId` 만든 견적을 사용하여 견적을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 예상 세부 정보를 반환합니다.

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `state` | 미리 보기 작업의 현재 상태입니다. 처리가 완료될 때까지 &quot;RUNNING&quot;이 되며 이 시점에서 &quot;RESULT_READY&quot; 또는 &quot;FAILED&quot;가 됩니다. |
| `_links.preview` | 미리 보기 작업의 현재 상태가 &quot;RESULT_READY&quot;이면 이 속성은 예상 값을 볼 수 있는 URL을 제공합니다. |

### 미리 보기 보기

**API 형식**

```http
GET /preview/{PREVIEW_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{PREVIEW_ID}` | 보려는 미리 보기 작업의 ID입니다. |

**요청**

다음 요청은 이전 단계에서 `previewId` 만든 미리 보기를 사용하여 미리 보기를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 미리 보기의 세부 정보를 반환합니다.

```json
{
   "results": [{
         "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
               "XID_COOKIE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
               },
               "XID_PROFILE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
               }
            }
         }
      },
      {
         "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
               "XID_COOKIE_ID_2-1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

               },
               "XID_PROFILE_ID_2": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
               }
            }
         },
         "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
         },
         "state": "RESULT_READY",
         "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
         }
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## 다음 단계

세그먼트 정의를 개발, 테스트 및 저장한 후에는 세그먼트 작업을 만들어 실시간 고객 프로필 API를 사용하여 대상을 만들 수 있습니다. 이를 수행하는 방법에 대한 자세한 내용은 세그먼트 결과 [](./evaluate-a-segment.md) 평가 및 액세스에 대한 자습서를 참조하십시오.