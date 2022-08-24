---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;대상;대상;API;api;
title: 대상 API 엔드포인트
topic-legacy: developer guide
description: Adobe Experience Platform 세그멘테이션 서비스 API의 대상 종단점을 사용하면 조직의 대상을 프로그래밍 방식으로 관리할 수 있습니다.
source-git-commit: 2a0c1f55115c541962f7bd3b7b11d367da50ff3b
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 3%

---


# 대상 끝점

대상은 유사한 행동 및/또는 특성을 공유하는 사람들의 컬렉션입니다. 이러한 사람 컬렉션은 Adobe Experience Platform을 사용하거나 외부 소스에서 생성할 수 있습니다. 를 사용할 수 있습니다 `/audiences` 대상을 프로그래밍 방식으로 검색, 만들기, 업데이트 및 삭제할 수 있는 세분화 API의 끝점입니다.

## 시작하기

이 안내서에서 사용되는 엔드포인트는 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 [시작 안내서](./getting-started.md) 필수 헤더 및 예제 API 호출을 읽는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보입니다.

## 대상자 목록 검색 {#list}

에 GET 요청을 작성하여 조직의 모든 대상자 목록을 검색할 수 있습니다 `/audiences` 엔드포인트.

**API 형식**

다음 `/audiences` endpoint는 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 리소스를 나열할 때 값비싼 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 종단점을 호출하면 조직에서 사용할 수 있는 모든 대상이 검색됩니다. 여러 매개 변수를 앰퍼샌드( )로 구분하여 포함할 수 있습니다`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

대상자 목록을 검색할 때 다음 쿼리 매개 변수를 사용할 수 있습니다.

| 쿼리 매개 변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `start` | 반환된 대상의 시작 오프셋을 지정합니다. | `start=5` |
| `limit` | 페이지당 반환되는 최대 대상 수를 지정합니다. | `limit=10` |
| `sort` | 결과를 정렬 기준으로 지정합니다. 형식으로 작성됩니다 `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | 대상자를 지정할 수 있는 필터입니다 **정확히** 속성 값과 일치합니다. 형식으로 작성됩니다 `property=` | `property=audienceId==test-audience-id` |
| `name` | 이름을 갖는 대상을 지정할 수 있는 필터입니다 **contain** 제공된 값입니다. 이 값은 대/소문자를 구분하지 않습니다. | `name=Sample` |
| `description` | 설명이 있는 대상을 지정할 수 있는 필터입니다 **contain** 제공된 값입니다. 이 값은 대/소문자를 구분하지 않습니다. | `description=Test Description` |
| `withMetrics` | 대상 외에 지표를 반환하는 필터입니다. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>대상의 경우, 지표는 `metrics` 프로필 카운트, 만들기 및 업데이트 타임스탬프에 대한 정보를 포함합니다.

**지표 없음**

다음 요청/응답 쌍이 `withMetrics` 쿼리 매개 변수가 없습니다.

**요청**

다음 요청은 조직에서 생성한 마지막 5개의 대상을 검색합니다.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**응답** {#no-metrics}

성공적인 응답은 조직에서 JSON으로 만든 대상 목록과 함께 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>다음 응답은 스페이스에 대해 잘렸으며 반환된 첫 번째 대상만 표시합니다.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
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
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| 속성 | 대상 유형 | 설명 |
| -------- | ------------- | ----------- | 
| `id` | 둘 다 | 대상에 대해 시스템에서 생성한 읽기 전용 식별자입니다. |
| `audienceId` | 둘 다 | 대상이 플랫폼에서 생성한 대상자인 경우 이 값은 와 동일한 값입니다 `id`. 대상이 외부에서 생성되면 이 값은 클라이언트가 제공합니다. |
| `schema` | 둘 다 | 대상의 Experience Data Model(XDM) 스키마. |
| `imsOrgId` | 둘 다 | 대상이 속한 조직의 ID입니다. |
| `sandbox` | 둘 다 | 대상이 속하는 샌드박스에 대한 정보입니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md). |
| `name` | 둘 다 | 대상의 이름입니다. |
| `description` | 둘 다 | 대상자에 대한 설명입니다. |
| `expression` | 플랫폼 생성 | 대상의 PQL(프로필 쿼리 언어) 표현식입니다. PQL 표현식에 대한 자세한 내용은 [PQL 표현식 안내서](../pql/overview.md). |
| `mergePolicyId` | 플랫폼 생성 | 대상이 연결된 병합 정책의 ID입니다. 병합 정책에 대한 자세한 내용은 [정책 병합 안내서](../../profile/api/merge-policies.md). |
| `evaluationInfo` | 플랫폼 생성 | 대상을 평가하는 방법을 표시합니다. 가능한 평가 방법에는 일괄 처리, 스트리밍 또는 에지가 포함됩니다. 평가 방법에 대한 자세한 내용은 [세분화 개요](../home.md) |
| `dependents` | 둘 다 | 현재 대상에 의존하는 대상 ID의 배열입니다. 세그먼트의 세그먼트인 대상을 만드는 경우 사용됩니다. |
| `dependencies` | 둘 다 | 대상이 의존하는 대상 ID의 배열입니다. 세그먼트의 세그먼트인 대상을 만드는 경우 사용됩니다. |
| `type` | 둘 다 | 대상이 플랫폼 생성인지 아니면 외부에서 생성된 대상인지 여부를 표시하는 시스템 생성 필드입니다. 가능한 값은 다음과 같습니다 `SegmentDefinition` 및 `ExternalAudience`. A `SegmentDefinition` 는 플랫폼에서 생성된 대상을, `ExternalAudience` 는 플랫폼에서 생성되지 않은 대상을 나타냅니다. |
| `createdBy` | 둘 다 | 대상자를 만든 사용자의 ID입니다. |
| `labels` | 둘 다 | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |
| `namespace` | 둘 다 | 대상이 속한 네임스페이스입니다. 가능한 값은 다음과 같습니다 `AAM`, `AAMSegments`, `AAMTraits`, 및 `AEPSegments`. |
| `audienceMeta` | 외부 | 외부에서 생성된 대상에서 외부에서 생성된 메타데이터입니다. |

**지표 사용**

다음 요청/응답 쌍이 `withMetrics` 쿼리 매개 변수가 있습니다.

**요청**

다음 요청은 조직에서 생성한 지표를 사용하여 마지막 5개의 대상을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 조직의 JSON으로 대상 목록과 함께 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>다음 응답은 스페이스에 대해 잘렸으며 반환된 첫 번째 대상만 표시합니다.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "existing": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

다음은 속성 목록입니다 **독점** 변환 후 `withMetrics` 응답합니다. 표준 대상 속성을 알아보려면 [이전 섹션](#no-metrics).

| 속성 | 설명 |
| -------- | ----------- |
| `metrics.imsOrgId` | 대상자의 조직 ID입니다. |
| `metrics.sandbox` | 대상자와 관련된 샌드박스 정보입니다. |
| `metrics.jobId` | 대상자를 처리하고 있는 세그먼트 작업의 ID입니다. |
| `metrics.type` | 세그먼트 작업 유형입니다. 다음 중 하나일 수 있습니다 `export` 또는 `batch_segmentation`. |
| `metrics.id` | 대상자의 ID입니다. |
| `metrics.data` | 대상과 관련된 지표입니다. 여기에는 대상자에 포함된 총 프로필 수, 네임스페이스별로 총 프로필 수, 상태별로 총 프로필 수 등의 정보가 포함됩니다. |
| `metrics.createEpoch` | 대상자를 만든 때를 보여주는 타임스탬프입니다. |
| `metrics.updateEpoch` | 대상을 마지막으로 업데이트한 시간을 보여주는 타임스탬프입니다. |

## 새 대상 만들기 {#create}

에 POST 요청을 만들어 새 대상을 만들 수 있습니다 `/audiences` 엔드포인트.

**API 형식**

```http
POST /audiences
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| 속성 | 설명 |
| -------- | ----------- | 
| `name` | 대상의 이름입니다. |
| `description` | 대상자에 대한 설명입니다. |
| `type` | 대상이 플랫폼 생성인지 아니면 외부에서 생성된 대상인지 여부를 표시하는 필드입니다. 가능한 값은 다음과 같습니다 `SegmentDefinition` 및 `ExternalAudience`. A `SegmentDefinition` 는 플랫폼에서 생성된 대상을, `ExternalAudience` 는 플랫폼에서 생성되지 않은 대상을 나타냅니다. |
| `expression` | 대상의 PQL(프로필 쿼리 언어) 표현식입니다. PQL 표현식에 대한 자세한 내용은 [PQL 표현식 안내서](../pql/overview.md). |
| `schema` | 대상의 Experience Data Model(XDM) 스키마. |
| `labels` | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |

**응답**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## 지정된 대상 조회 {#get}

에 GET 요청을 수행하여 특정 대상에 대한 자세한 정보를 조회할 수 있습니다 `/audiences` 요청 경로에서 검색할 대상자의 ID를 제공하고 끝점입니다.

**API 형식**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| 매개 변수 | 설명 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 검색하려는 대상의 ID입니다. |
| `property=withmetrics==true` | 대상 지표로 지정된 대상을 검색하려는 경우 사용할 수 있는 선택적 쿼리 매개 변수입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 대상에 대한 정보와 함께 HTTP 상태 200을 반환합니다. 응답이 Adobe Experience Platform 또는 외부 소스에서 대상이 생성되는지 여부에 따라 달라집니다.

**플랫폼 생성**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**외부에서 생성됨**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## 대상의 필드 업데이트 {#update-field}

에 PATCH 요청을 만들어 특정 대상의 필드를 업데이트할 수 있습니다 `/audiences` 요청 경로에서 업데이트할 대상자의 ID를 제공하고 끝점입니다.

**API 형식**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 업데이트할 대상자의 ID입니다. |

**요청**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| 속성 | 설명 |
| -------- | ----------- |
| `op` | 대상을 업데이트하는 경우 이 값은 항상 입니다 `add`. |
| `path` | 업데이트할 필드의 경로입니다. |
| `value` | 필드를 업데이트할 값입니다. |

**응답**

성공적인 응답은 새로 업데이트된 대상에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## 대상자 업데이트 {#put}

에 PUT 요청을 만들어 특정 대상을 업데이트(덮어쓰기)할 수 있습니다 `/audiences` 요청 경로에서 업데이트할 대상자의 ID를 제공하고 끝점입니다.

**API 형식**

```http
PUT /audiences/{AUDIENCE_ID}
```

**요청**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| 속성 | 설명 |
| -------- | ----------- | 
| `audienceId` | 대상자의 ID입니다. 외부 대상에서 사용됩니다 |
| `name` | 대상의 이름입니다. |
| `namespace` |  |
| `description` | 대상자에 대한 설명입니다. |
| `type` | 대상이 플랫폼 생성인지 아니면 외부에서 생성된 대상인지 여부를 표시하는 시스템 생성 필드입니다. 가능한 값은 다음과 같습니다 `SegmentDefinition` 및 `ExternalAudience`. A `SegmentDefinition` 는 플랫폼에서 생성된 대상을, `ExternalAudience` 는 플랫폼에서 생성되지 않은 대상을 나타냅니다. |
| `lifecycle` | 대상자의 상태입니다. 가능한 값은 다음과 같습니다 `draft`, `published`, `inactive`, 및 `archived`. `draft` 대상이 만들어지는 시기를 나타냅니다. `published` 대상이 게시되면 `inactive` 대상자가 더 이상 활성 상태가 아닌 경우 `archived` 대상자가 삭제되는 경우 |
| `datasetId` | 대상 데이터를 찾을 수 있는 데이터 세트의 ID입니다. |
| `labels` | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |

**응답**

성공적인 응답은 새로 업데이트된 대상자의 세부 정보와 함께 HTTP 상태 200을 반환합니다. 대상자의 세부 사항은 플랫폼에서 생성한 대상인지 또는 외부에서 생성된 대상인지에 따라 달라집니다.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## 대상자 삭제 {#delete}

에 DELETE 요청을 만들어 특정 대상을 삭제할 수 있습니다 `/audiences` 요청 경로에서 삭제할 대상자의 ID를 제공하고 끝점입니다.

**API 형식**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 삭제할 대상자의 ID입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 메시지가 없는 HTTP 상태 204를 반환합니다.
