---
solution: Experience Platform
title: 세그먼트 정의 API 엔드포인트
description: Adobe Experience Platform Segmentation Service API의 세그먼트 정의 엔드포인트를 사용하면 조직의 세그먼트 정의를 프로그래밍 방식으로 관리할 수 있습니다.
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: f35fb6aae6aceb75391b1b615ca067a72918f4cf
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 2%

---

# 세그먼트 정의 엔드포인트

Adobe Experience Platform을 사용하면 프로필 그룹에서 특정 속성이나 동작 그룹을 정의하는 세그먼트 정의를 만들 수 있습니다. 세그먼트 정의는 [!DNL Profile Query Language](PQL)로 작성된 쿼리를 캡슐화하는 개체입니다. 세그먼트 정의는 프로필에 적용되어 대상자를 만듭니다. 이 개체(세그먼트 정의)는 PQL 술어라고도 합니다. PQL 조건자는 [!DNL Real-Time Customer Profile]에 제공한 레코드 또는 시계열 데이터와 관련된 조건을 기반으로 세그먼트 정의에 대한 규칙을 정의합니다. PQL 쿼리 작성에 대한 자세한 내용은 [PQL 안내서](../pql/overview.md)를 참조하십시오.

이 안내서에서는 세그먼트 정의를 더 잘 이해하는 데 도움이 되는 정보를 제공하며 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 시작하기

이 가이드에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 세그먼트 정의 목록 검색 {#list}

`/segment/definitions` 끝점에 대한 GET 요청을 통해 조직의 모든 세그먼트 정의 목록을 검색할 수 있습니다.

**API 형식**

`/segment/definitions` 끝점은 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 값비싼 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 세그먼트 정의를 검색합니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다.

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**쿼리 매개 변수**

+++ 사용 가능한 쿼리 매개 변수 목록입니다.

| 매개변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `start` | 반환된 세그먼트 정의에 대한 시작 오프셋을 지정합니다. | `start=4` |
| `limit` | 페이지당 반환되는 세그먼트 정의 수를 지정합니다. | `limit=20` |
| `page` | 세그먼트 정의 결과가 시작될 페이지를 지정합니다. | `page=5` |
| `sort` | 결과를 정렬할 필드를 지정합니다. `[attributeName]:[desc/asc]` 형식으로 작성되었습니다. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | 세그먼트 정의가 스트리밍을 사용하는지 여부를 지정합니다. | `evaluationInfo.continuous.enabled=true` |

+++

**요청**

다음 요청은 조직 내에 게시된 마지막 두 개의 세그먼트 정의를 검색합니다.

+++ 세그먼트 정의 목록을 검색하는 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 지정된 조직에 대한 세그먼트 정의 목록이 JSON인 HTTP 상태 200을 반환합니다.

+++ 세그먼트 정의 목록을 검색할 때의 샘플 응답입니다.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
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
                "value": "{PQL_EXPRESSION}"
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
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
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
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

+++

## 새 세그먼트 정의 만들기 {#create}

`/segment/definitions` 끝점에 대한 POST 요청을 수행하여 새 세그먼트 정의를 만들 수 있습니다.

>[!IMPORTANT]
>
>API를 통해 만들어진 세그먼트 정의는 **편집할 수 없습니다** 세그먼트 빌더를 사용하여 편집할 수 없습니다.

**API 형식**

```http
POST /segment/definitions
```

**요청**

새 세그먼트 정의를 만들 때 `pql/text` 또는 `pql/json` 형식으로 만들 수 있습니다.

>[!BEGINTABS]

>[!TAB pql/text 사용]

+++ 세그먼트 정의를 만드는 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "schema": {
            "name": "_xdm.context.profile"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 세그먼트 정의를 참조할 고유한 이름. |
| `description` | (선택 사항) 생성 중인 세그먼트 정의에 대한 설명입니다. |
| `expression` | 세그먼트 정의에 대한 필드 정보를 포함하는 엔티티입니다. |
| `expression.type` | 표현식 유형을 지정합니다. 현재는 &quot;PQL&quot;만 지원됩니다. |
| `expression.format` | 값의 식 구조를 나타냅니다. 지원되는 값은 `pql/text` 및 `pql/json`입니다. |
| `expression.value` | `expression.format`에 표시된 형식을 준수하는 식입니다. |
| `evaluationInfo` | (선택 사항) 생성 중인 세그먼트 정의 유형입니다. 일괄 처리 세그먼트를 만들려면 `evaluationInfo.batch.enabled`을(를) true로 설정하십시오. 스트리밍 세그먼트를 만들려면 `evaluationInfo.continuous.enabled`을(를) true로 설정하십시오. 가장자리 세그먼트를 만들려면 `evaluationInfo.synchronous.enabled`을(를) true로 설정하십시오. 비워 두면 세그먼트 정의가 **일괄 처리** 세그먼트로 만들어집니다. |
| `schema` | 세그먼트의 엔티티와 연결된 스키마입니다. `id` 또는 `name` 필드로 구성됩니다. |

+++

>[!TAB pql/json 사용]

+++ 세그먼트 정의를 만드는 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/json",
            "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"a\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}},{\"nodeType\":\"fieldLookup\",\"fieldName\":\"b\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}]}"
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
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string"
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 세그먼트 정의를 참조할 고유한 이름. |
| `description` | (선택 사항) 생성 중인 세그먼트 정의에 대한 설명입니다. |
| `evaluationInfo` | (선택 사항) 생성 중인 세그먼트 정의 유형입니다. 일괄 처리 세그먼트를 만들려면 `evaluationInfo.batch.enabled`을(를) true로 설정하십시오. 스트리밍 세그먼트를 만들려면 `evaluationInfo.continuous.enabled`을(를) true로 설정하십시오. 가장자리 세그먼트를 만들려면 `evaluationInfo.synchronous.enabled`을(를) true로 설정하십시오. 비워 두면 세그먼트 정의가 **일괄 처리** 세그먼트로 만들어집니다. |
| `schema` | 세그먼트의 엔티티와 연결된 스키마입니다. `id` 또는 `name` 필드로 구성됩니다. |
| `expression` | 세그먼트 정의에 대한 필드 정보를 포함하는 엔티티입니다. |
| `expression.type` | 표현식 유형을 지정합니다. 현재는 &quot;PQL&quot;만 지원됩니다. |
| `expression.format` | 값의 식 구조를 나타냅니다. |
| `expression.value` | `expression.format`에 표시된 형식을 준수하는 식입니다. |

+++

>[!ENDTABS]

**응답**

성공적인 응답은 새로 생성된 세그먼트 정의에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 세그먼트 정의를 생성할 때 샘플 응답.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 생성된 세그먼트 정의에 대한 시스템 생성 ID입니다. |
| `evaluationInfo` | 세그먼트 정의가 받게 될 평가 유형을 나타내는 개체입니다. 일괄 처리, 스트리밍(연속이라고도 함) 또는 Edge(동기화라고도 함) 세그멘테이션일 수 있습니다. |

+++

## 특정 세그먼트 정의 검색 {#get}

`/segment/definitions` 끝점에 대한 GET 요청을 만들고 요청 경로에서 검색하려는 세그먼트 정의의 ID를 제공하여 특정 세그먼트 정의에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 검색할 세그먼트 정의의 `id` 값입니다. |

**요청**

+++ 세그먼트 정의를 검색하기 위한 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 지정된 세그먼트 정의에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 세그먼트 정의를 검색할 때의 샘플 응답입니다.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 세그먼트 정의에 대한 시스템 생성 읽기 전용 ID입니다. |
| `name` | 세그먼트 정의를 참조할 고유한 이름. |
| `schema` | 세그먼트의 엔티티와 연결된 스키마입니다. `id` 또는 `name` 필드로 구성됩니다. |
| `expression` | 세그먼트 정의에 대한 필드 정보를 포함하는 엔티티입니다. |
| `expression.type` | 표현식 유형을 지정합니다. 현재는 &quot;PQL&quot;만 지원됩니다. |
| `expression.format` | 값의 식 구조를 나타냅니다. 현재 지원되는 형식은 다음과 같습니다. <ul><li>`pql/text`: 게시된 PQL 문법에 따른 세그먼트 정의의 텍스트 표현입니다.  예: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | `expression.format`에 표시된 형식을 준수하는 식입니다. |
| `description` | 사람이 인식할 수 있는 정의 설명. |
| `evaluationInfo` | 세그먼트 정의가 받게 될 평가, 일괄 처리, 스트리밍(연속이라고도 함) 또는 에지(동기화라고도 함) 유형을 나타내는 개체입니다. |

+++

## 세그먼트 정의 벌크 검색 {#bulk-get}

`/segment/definitions/bulk-get` 끝점에 대한 POST 요청을 만들고 요청 본문에 세그먼트 정의의 `id` 값을 제공하여 지정된 여러 세그먼트 정의에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
POST /segment/definitions/bulk-get
```

**요청**

+++ 대량으로 끝점 가져오기를 사용할 때의 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

+++

**응답**

성공적인 응답은 요청된 세그먼트 정의와 함께 HTTP 상태 207을 반환합니다.

+++ 대량으로 끝점 가져오기를 사용할 때의 샘플 응답입니다.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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

    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 세그먼트 정의에 대한 시스템 생성 읽기 전용 ID입니다. |
| `name` | 세그먼트 정의를 참조할 고유한 이름. |
| `schema` | 세그먼트의 엔티티와 연결된 스키마입니다. `id` 또는 `name` 필드로 구성됩니다. |
| `expression` | 세그먼트 정의에 대한 필드 정보를 포함하는 엔티티입니다. |
| `expression.type` | 표현식 유형을 지정합니다. 현재는 &quot;PQL&quot;만 지원됩니다. |
| `expression.format` | 값의 식 구조를 나타냅니다. 현재 지원되는 형식은 다음과 같습니다. <ul><li>`pql/text`: 게시된 PQL 문법에 따른 세그먼트 정의의 텍스트 표현입니다.  예: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | `expression.format`에 표시된 형식을 준수하는 식입니다. |
| `description` | 사람이 인식할 수 있는 정의 설명. |
| `evaluationInfo` | 세그먼트 정의가 받게 될 평가, 일괄 처리, 스트리밍(연속이라고도 함) 또는 에지(동기화라고도 함) 유형을 나타내는 개체입니다. |

+++

## 특정 세그먼트 정의 삭제 {#delete}

`/segment/definitions` 끝점에 대한 DELETE 요청을 만들고 요청 경로에 삭제할 세그먼트 정의의 ID를 제공하여 특정 세그먼트 정의의 삭제를 요청할 수 있습니다.

>[!NOTE]
>
> 대상 활성화 **할 수 없음**&#x200B;에 사용되는 세그먼트 정의를 삭제할 수 없습니다.

**API 형식**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 삭제할 세그먼트 정의의 `id` 값입니다. |

**요청**

+++ 세그먼트 정의 삭제에 대한 샘플 요청입니다.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 메시지 없이 HTTP 상태 200을 반환합니다.

## 특정 세그먼트 정의 업데이트

`/segment/definitions` 끝점에 대한 PATCH 요청을 만들고 요청 경로에 업데이트하려는 세그먼트 정의의 ID를 제공하여 특정 세그먼트 정의를 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 업데이트할 세그먼트 정의의 `id` 값입니다. |

**요청**

다음 요청은 작업 주소 국가를 미국에서 캐나다로 업데이트합니다.

+++ 세그먼트 정의를 업데이트하기 위한 샘플 요청입니다.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

+++

**응답**

성공적인 응답은 새로 업데이트된 세그먼트 정의에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 세그먼트 정의를 업데이트할 때의 샘플 응답입니다.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
        "value": "workAddress.country = \"CA\""
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

+++

## 세그먼트 정의 변환

`/segment/conversion` 끝점에 POST 요청을 하여 `pql/text`에서 `pql/json` 또는 `pql/json` 사이의 세그먼트 정의를 `pql/text`(으)로 변환할 수 있습니다.

**API 형식**

```http
POST /segment/conversion
```

**요청**

다음 요청은 세그먼트 정의의 형식을 `pql/text`에서 `pql/json`(으)로 변경합니다.

+++ 세그먼트 정의를 변환하는 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "payloadSchema": "string"
    }'
```

+++

**응답**

성공적인 응답은 새로 변환된 세그먼트 정의에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 세그먼트 정의를 변환할 때의 샘플 응답입니다.

```json
{
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

+++

## 다음 단계

이제 이 안내서를 읽고 세그먼트 정의가 작동하는 방식을 보다 잘 이해할 수 있습니다. 세그먼트 만들기에 대한 자세한 내용은 [세그먼트 만들기](../tutorials/create-a-segment.md) 자습서를 참조하십시오.
