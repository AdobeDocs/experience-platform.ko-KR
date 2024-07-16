---
title: 계산된 속성 API 끝점
description: Real-Time Customer Profile API를 사용하여 계산된 속성을 생성, 보기, 업데이트 및 삭제하는 방법을 알아봅니다.
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 94c94b8a3757aca1a04ff4ffc3c62e84602805cc
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 1%

---

# 계산된 속성 API 끝점

>[!IMPORTANT]
>
>API에 대한 액세스가 제한됩니다. 계산된 속성 API에 대한 액세스 권한을 받는 방법을 알아보려면 Adobe 지원 센터에 문의하십시오.

계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화에서 사용할 수 있도록 자동으로 계산됩니다. 이 안내서에는 `/attributes` 끝점을 사용하여 기본 CRUD 작업을 수행하기 위한 샘플 API 호출이 포함되어 있습니다.

계산된 특성에 대해 자세히 알아보려면 [계산된 특성 개요](overview.md)를 읽는 것부터 시작하십시오.

## 시작하기

이 가이드에 사용된 API 끝점은 [실시간 고객 프로필 API](https://www.adobe.com/go/profile-apis-en)의 일부입니다.

계속하기 전에 [프로필 API 시작 안내서](../api/getting-started.md)에서 권장 설명서에 대한 링크, 이 설명서에 표시되는 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

또한 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 레지스트리 시작 안내서](../../xdm/api/getting-started.md#know-your-tenant_id): 이 안내서 전체의 응답에 표시되는 `{TENANT_ID}`에 대한 정보가 제공됩니다.

## 계산된 속성 목록 검색 {#list}

`/attributes` 끝점에 대한 GET 요청을 수행하여 조직에 대해 계산된 모든 특성 목록을 검색할 수 있습니다.

**API 형식**

`/attributes` 끝점은 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 리소스를 나열할 때 비싼 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 계산된 특성이 검색됩니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다.

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

계산된 속성 목록을 검색할 때 다음 쿼리 매개 변수를 사용할 수 있습니다.

| 쿼리 매개 변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `limit` | 응답의 일부로 반환되는 최대 항목 수를 지정하는 매개 변수입니다. 이 매개 변수의 최소값은 1이고 최대값은 40입니다. 이 매개 변수가 포함되지 않으면 기본적으로 20개 항목이 반환됩니다. | `limit=20` |
| `offset` | 항목을 반환하기 전에 건너뛸 항목의 수를 지정하는 매개 변수입니다. | `offset=5` |
| `sortBy` | 반환된 항목이 정렬되는 순서를 지정하는 매개 변수입니다. 사용 가능한 옵션은 `name`, `status`, `updateEpoch` 및 `createEpoch`입니다. 정렬 옵션 앞에 `-`을(를) 포함하지 않거나 포함하여 오름차순으로 정렬할지 내림차순으로 정렬할지 선택할 수도 있습니다. 기본적으로 항목은 `updateEpoch`별로 내림차순으로 정렬됩니다. | `sortBy=name` |
| `property` | 다양한 계산된 속성 필드를 필터링할 수 있는 매개변수. 지원되는 속성은 `name`, `createEpoch`, `mergeFunction.value`, `updateEpoch` 및 `status`입니다. 지원되는 작업은 나열된 속성에 따라 다릅니다. <ul><li>`name`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`createEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`updateEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**요청**

다음 요청은 조직에서 업데이트된 마지막 3개의 계산된 속성을 검색합니다.

+++ 계산된 속성 목록을 검색하는 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 조직 및 샌드박스에 속한 최근 3개의 업데이트된 계산된 속성 목록과 함께 HTTP 상태 200을 반환합니다.

+++ 계산된 속성 목록을 검색하기 위한 샘플 응답입니다.

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `_links` | 결과의 마지막 페이지, 결과의 다음 페이지, 결과의 이전 페이지 또는 결과의 현재 페이지에 액세스하는 데 필요한 페이지 매김 정보를 포함하는 객체입니다. |
| `computedAttributes` | 쿼리 매개 변수를 기반으로 하여 계산된 속성을 포함하는 배열입니다. 계산된 특성 배열에 대한 자세한 내용은 [특정 계산된 특성 검색 섹션](#get)에서 확인할 수 있습니다. |
| `_page` | 반환된 결과에 대한 메타데이터를 포함하는 객체입니다. 여기에는 현재 오프셋, 반환되는 계산된 속성 수, 반환되는 계산된 속성의 총 수 및 반환되는 계산된 속성 제한에 대한 정보가 포함됩니다. |

+++

## 계산된 속성 만들기 {#create}

계산된 특성을 만들려면 먼저 만들려는 계산된 특성의 세부 정보가 포함된 요청 본문으로 `/attributes` 끝점에 대한 POST 요청을 시작합니다.

**API 형식**

```http
POST /attributes
```

**요청**

+++ 새 계산된 속성을 만들기 위한 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 계산된 속성 필드의 이름(문자열)입니다. 계산된 속성의 이름은 공백 또는 밑줄 없이 영숫자로만 구성할 수 있습니다. 이 값 **must**&#x200B;은(는) 계산된 모든 특성 중에서 고유합니다. 이 이름은 `displayName`의 camelCase 버전이어야 합니다. |
| `description` | 계산된 속성에 대한 설명입니다. 이 기능은 조직 내의 다른 사용자가 사용할 올바른 계산된 속성을 결정하는 데 도움이 되므로 여러 계산된 속성이 정의된 경우에 특히 유용합니다. |
| `displayName` | 계산된 속성의 표시 이름입니다. Adobe Experience Platform UI 내에서 계산된 속성을 나열할 때 표시되는 이름입니다. |
| `expression` | 만들려는 계산된 속성의 쿼리 표현식을 나타내는 개체입니다. |
| `expression.type` | 표현식의 유형입니다. 현재는 PQL만 지원됩니다. |
| `expression.format` | 표현식의 형식입니다. 현재 `pql/text`만 지원됩니다. |
| `expression.value` | 표현식의 값입니다. |
| `keepCurrent` | 빠른 새로 고침을 사용하여 계산된 속성 값을 최신 상태로 유지할지 여부를 결정하는 부울입니다. 현재 이 값은 `false`(으)로 설정해야 합니다. |
| `duration` | 계산된 속성에 대한 전환 확인 기간을 나타내는 개체입니다. 전환 확인 기간은 계산된 속성을 계산하기 위해 되돌릴 수 있는 기간을 나타냅니다. |
| `duration.count` | 전환 확인 기간 기간을 나타내는 숫자입니다. 가능한 값은 `duration.unit` 필드의 값에 따라 다릅니다. <ul><li>`HOURS`: 1-24</li><li>`DAYS`: 1-7</li><li>`WEEKS`: 1-4</li><li>`MONTHS`: 1-6</li></ul> |
| `duration.unit` | 전환 확인 기간에 사용할 시간 단위를 나타내는 문자열입니다. 가능한 값은 `HOURS`, `DAYS`, `WEEKS` 및 `MONTHS`입니다. |
| `status` | 계산된 속성의 상태입니다. 가능한 값은 `DRAFT` 및 `NEW`입니다. |

+++

**응답**

성공적인 응답은 새로 생성된 계산된 속성에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 새 계산된 속성을 만들 때의 샘플 응답입니다.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 만든 계산된 속성에 대한 시스템 생성 ID입니다. |
| `status` | 계산된 속성의 상태입니다. `DRAFT` 또는 `NEW`일 수 있습니다. |
| `createEpoch` | 계산된 속성이 생성된 시간(초)입니다. |
| `updateEpoch` | 계산된 속성이 마지막으로 업데이트된 시간(초)입니다. |
| `createdBy` | 계산된 속성을 만든 사용자의 ID입니다. |

+++

## 특정 계산된 속성 검색 {#get}

`/attributes` 끝점에 GET 요청을 하고 요청 경로에서 검색하려는 계산된 특성의 ID를 제공하여 특정 계산된 특성에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**요청**

+++ 특정 계산된 속성을 검색하기 위한 샘플 요청입니다.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 지정된 계산된 속성에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 특정 계산된 속성을 검색할 때의 샘플 응답입니다.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 다른 API 작업 중에 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 ID입니다. |
| `type` | 반환된 객체가 계산된 속성임을 보여 주는 문자열입니다. |
| `name` | 계산된 속성의 이름입니다. |
| `displayName` | 계산된 속성의 표시 이름입니다. Adobe Experience Platform UI 내에서 계산된 속성을 나열할 때 표시되는 이름입니다. |
| `description` | 계산된 속성에 대한 설명입니다. 이 기능은 조직 내의 다른 사용자가 사용할 올바른 계산된 속성을 결정하는 데 도움이 되므로 여러 계산된 속성이 정의된 경우에 특히 유용합니다. |
| `imsOrgId` | 계산된 속성이 속한 조직의 ID입니다. |
| `sandbox` | 샌드박스 객체에는 계산된 속성이 구성된 샌드박스의 세부 정보가 포함됩니다. 이 정보는 요청에서 전송된 샌드박스 헤더에서 가져옵니다. 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하세요. |
| `path` | 계산된 특성에 대한 `path`입니다. |
| `keepCurrent` | 빠른 새로 고침을 사용하여 계산된 속성 값을 최신 상태로 유지할지 여부를 결정하는 부울입니다. |
| `expression` | 계산된 속성의 표현식이 포함된 객체입니다. |
| `mergeFunction` | 계산된 속성에 대한 병합 함수를 포함하는 객체입니다. 이 값은 계산된 속성의 표현식 내에서 해당 집계 매개변수를 기반으로 합니다. 가능한 값은 `SUM`, `MIN`, `MAX` 및 `MOST_RECENT`입니다. |
| `status` | 계산된 속성의 상태입니다. `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED` 또는 `DISABLED` 값 중 하나일 수 있습니다. |
| `schema` | 표현식이 평가되는 스키마에 대한 정보를 포함하는 객체입니다. 현재 `_xdm.context.profile`만 지원됩니다. |
| `lastEvaluationTs` | 계산된 속성이 마지막으로 평가된 시기를 나타내는 타임스탬프입니다. |
| `createEpoch` | 계산된 속성이 생성된 시간(초)입니다. |
| `updateEpoch` | 계산된 속성이 마지막으로 업데이트된 시간(초)입니다. |
| `createdBy` | 계산된 속성을 만든 사용자의 ID입니다. |

+++

## 특정 계산된 속성 삭제 {#delete}

`/attributes` 끝점에 DELETE 요청을 하고 요청 경로에 삭제하려는 계산된 특성의 ID를 제공하여 특정 계산된 특성을 삭제할 수 있습니다.

>[!IMPORTANT]
>
>삭제 요청은 **초안**(`DRAFT`) 상태의 계산된 특성만 삭제하는 데 사용할 수 있습니다. 이 끝점 **은(는) 다른 상태에서 계산된 특성을 삭제하는 데 사용할 수 없습니다**.

**API 형식**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | 삭제하려는 계산된 특성의 `id` 값입니다. |

**요청**

+++ 계산된 속성을 삭제하기 위한 샘플 요청입니다.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 삭제된 계산된 속성에 대한 세부 정보와 함께 HTTP 상태 202를 반환합니다.

+++ 계산된 속성을 삭제할 때의 샘플 응답입니다.

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## 특정 계산된 속성 업데이트

`/attributes` 끝점에 PATCH 요청을 하고 요청 경로에 업데이트하려는 계산된 특성의 ID를 제공하여 특정 계산된 특성을 업데이트할 수 있습니다.

>[!IMPORTANT]
>
>계산된 속성을 업데이트할 때에는 다음 필드만 업데이트할 수 있습니다.
>
>- 현재 상태가 `NEW`인 경우 상태를 `DISABLED`(으)로만 변경할 수 있습니다.
>- 현재 상태가 `DRAFT`인 경우 `name`, `description`, `keepCurrent`, `expression` 및 `duration` 필드의 값을 변경할 수 있습니다. 상태를 `DRAFT`에서 `NEW`(으)로 변경할 수도 있습니다. `mergeFunction` 또는 `path`과(와) 같은 시스템 생성 필드를 변경하면 오류가 반환됩니다.
>- 현재 상태가 `PROCESSING` 또는 `PROCESSED`인 경우 상태를 `DISABLED`(으)로만 변경할 수 있습니다.

**API 형식**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | 업데이트할 계산된 특성의 `id` 값입니다. |

**요청**

다음 요청은 계산된 특성의 상태를 `DRAFT`에서 `NEW`(으)로 업데이트합니다.

+++ 계산된 속성을 업데이트하기 위한 샘플 요청입니다.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**응답**

성공적인 응답은 새로 업데이트된 계산된 속성에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 계산된 속성을 업데이트할 때의 샘플 응답입니다.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## 다음 단계

이제 계산된 속성에 대한 기본 사항을 배웠으므로 조직에 대해 속성 정의를 시작할 준비가 되었습니다. Experience Platform UI에서 계산된 특성을 사용하는 방법에 대해 알아보려면 [계산된 특성 UI 안내서](./ui.md)를 읽어 보십시오.
