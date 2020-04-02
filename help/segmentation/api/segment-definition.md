---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 세그먼트 정의
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# 세그먼트 정의 개발자 가이드

Adobe Experience Platform을 사용하면 프로파일 그룹에서 특정 속성 또는 행동 그룹을 정의하는 세그먼트를 만들 수 있습니다.

이 개발자 안내서에서는 세그먼트 정의에 대한 다음 영역에 대한 지침을 제공합니다.

- [세그먼트 정의 목록 검색](#retrieve-a-list-of-segment-definitions)
- [새 세그먼트 정의 만들기](#create-a-new-segment-definition)
- [특정 세그먼트 정의 검색](#retrieve-a-specific-segment-definition)
- [특정 세그먼트 정의 삭제](#delete-a-specific-segment-definition)
- [특정 세그먼트 정의 업데이트](#update-a-specific-segment-definition)

## 시작하기

이 안내서에서 사용되는 API 끝점은 세그멘테이션 API의 일부입니다. 계속하기 전에 세그멘테이션 개발자 [안내서를](./getting-started.md)검토하십시오.

특히 세그멘테이션 개발자 안내서의 [시작 섹션은](./getting-started.md#getting-started) 관련 항목에 대한 링크, 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

## 세그먼트 정의 목록 검색

IMS에 대한 모든 세그먼트 정의 목록을 `/segment/definitions` 끝점에 GET 요청을 수행하여 검색할 수 있습니다.

**API 형식**

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*선택*&#x200B;사항) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다.

**쿼리 매개 변수**

다음은 세그먼트 정의를 나열하기 위한 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 세그먼트 정의가 검색됩니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `start` | ??? |
| `limit` | 페이지당 반환되는 세그먼트 정의 수를 지정합니다. |
| `page` | 세그먼트 정의 결과를 시작할 페이지를 지정합니다. |
| `sort` | 결과를 정렬할 필드를 지정합니다. |
| `evaluationInfo.continuous.enabled` | 세그먼트 정의가 스트리밍을 활성화하는지 여부를 지정합니다. |

**요청**

```shell
cur -X GET https://platform.adobe.io/data/core/ups/segment/definitions?QUERY \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 세그먼트 정의 목록이 있는 HTTP 상태 200을 JSON으로 반환합니다.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{\"nodeType\":\"select\",\"variables\":[{\"nodeType\":\"varDecl\",\"varName\":\"_Checkouts1\",\"from\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"xEvent\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}},\"where\":{\"nodeType\":\"fnApply\",\"fnName\":\"equals\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"eventType\",\"object\":{\"nodeType\":\"varRef\",\"varName\":\"_Checkouts1\"}},{\"literalType\":\"String\",\"nodeType\":\"literal\",\"value\":\"commerce.checkouts\"},{\"nodeType\":\"literal\",\"literalType\":\"Boolean\",\"value\":true}]}}]}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        ... ,
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"and\",\"params\":[{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"points\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"_acpstardust\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"Double\",\"nodeType\":\"literal\",\"value\":2}]},{\"nodeType\":\"fnApply\",\"fnName\":\"equals\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"testLoyaltyID\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"_acpstardust\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"String\",\"nodeType\":\"literal\",\"value\":\"\"},{\"nodeType\":\"literal\",\"literalType\":\"Boolean\",\"value\":false}]}]}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 4,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 4,
        "limit": 100
    },
    "link": {}
}
```

## 새 세그먼트 정의 만들기

종단점에 POST 요청을 만들어 새 세그먼트 정의를 만들 수 `/segment/definitions` 있습니다.

**API 형식**

```http
POST /segment/definitions
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
  "name": "People who ordered in the last 30 days",
  "profileInstanceId": "ups",
  "description": "Last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "payloadSchema": "string",
  "ttlInDays": 60,
  "creationTime": 0,
  "updateTime": 0,
  "updateEpoch": 0
}
 '
```

설명체

**응답**

성공적인 응답은 새로 만든 세그먼트 정의에 대한 세부 사항과 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

본문 및 머리글 설명

## 특정 세그먼트 정의 검색

종단점에 GET 요청을 하고 요청 경로에서 세그먼트 정의의 `/segment/definitions` `id` 값을 제공하여 특정 세그먼트 정의에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}`:검색할 세그먼트 정의의 `id` 값입니다.

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 세그먼트 정의에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

## 특정 세그먼트 정의 삭제

종단점에 DELETE 요청을 하고 요청 경로에 세그먼트 정의의 `/segment/definitions` `id` 값을 제공하여 지정된 세그먼트 정의를 삭제하도록 요청할 수 있습니다.

**API 형식**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}` 삭제할 세그먼트 정의의 `id` 값입니다.

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 메시지가 없는 HTTP 상태 200을 반환합니다.

## 특정 세그먼트 정의 업데이트

종단점에 PATCH 요청을 하고 요청 경로에서 세그먼트 정의의 `/segment/definitions` `id` 값을 제공하여 지정된 세그먼트 정의를 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}`:업데이트할 세그먼트 정의의 `id` 값입니다.

**요청**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}
'
```

설명체

**응답**

성공적인 응답은 새로 업데이트된 세그먼트 정의에 대한 세부 사항과 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

본문 및 머리글 설명

## 다음 단계
