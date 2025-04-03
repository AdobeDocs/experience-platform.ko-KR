---
title: 대상 API 엔드포인트
description: Adobe Experience Platform 세그멘테이션 서비스 API의 대상 끝점을 사용하여 프로그래밍 방식으로 조직의 대상을 만들고, 관리하고, 업데이트합니다.
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 2ec6bacb44dc9b31fcd5cb4c457ba109a921aa84
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 2%

---

# 대상자 엔드포인트

대상자는 유사한 행동 및/또는 특성을 공유하는 사람들의 컬렉션입니다. 이러한 사람 컬렉션은 Adobe Experience Platform을 사용하거나 외부 소스에서 생성할 수 있습니다. Segmentation API에서 대상을 프로그래밍 방식으로 검색, 만들기, 업데이트 및 삭제할 수 있는 `/audiences` 끝점을 사용할 수 있습니다.

## 시작하기

이 가이드에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 대상자 목록 검색 {#list}

`/audiences` 끝점에 대한 GET 요청을 통해 조직의 모든 대상 목록을 검색할 수 있습니다.

**API 형식**

`/audiences` 끝점은 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 리소스를 나열할 때 비싼 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 대상이 검색됩니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다.

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

>[!NOTE]
>
>쿼리 매개 변수 없이 이 끝점을 사용하는 경우 비활성 대상은 **반환되지 않습니다**. 그러나 이 끝점을 `property=audienceId` 쿼리 매개 변수와 함께 사용하면 비활성 대상 **will**&#x200B;이(가) 반환됩니다.

대상자 목록을 검색할 때 다음 쿼리 매개 변수를 사용할 수 있습니다.

| 쿼리 매개 변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `start` | 반환된 대상의 시작 오프셋을 지정합니다. | `start=5` |
| `limit` | 페이지당 반환되는 최대 대상자 수를 지정합니다. | `limit=10` |
| `sort` | 결과를 정렬하는 순서를 지정합니다. `attributeName:[desc/asc]` 형식으로 작성되었습니다. | `sort=updateTime:desc` |
| `property` | **정확히**&#x200B;이(가) 특성 값과 일치하는 대상을 지정할 수 있는 필터입니다. `property=` 형식으로 작성되었습니다. | `property=audienceId==test-audience-id` |
| `name` | 제공된 값에 대해 이름이 **포함**&#x200B;된 대상을 지정할 수 있는 필터입니다. 이 값은 대/소문자를 구분하지 않습니다. | `name=Sample` |
| `description` | 제공된 값을 **포함**&#x200B;하는 설명의 대상을 지정할 수 있는 필터입니다. 이 값은 대/소문자를 구분하지 않습니다. | `description=Test Description` |
| `entityType` | 찾고 있는 대상 유형을 지정할 수 있는 필터입니다. | `entityType=_xdm.context.account` |

**요청**

다음 요청은 조직에서 만든 마지막 두 대상을 검색합니다.

+++대상자 목록을 검색하는 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 조직에서 JSON으로 생성된 대상자 목록과 함께 HTTP 상태 200을 반환합니다.

+++조직에 속한 마지막 두 명의 대상을 만든 샘플 응답

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "pageSize": 2,
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| 속성 | 대상자 유형 | 설명 |
| -------- | ------------- | ----------- | 
| `id` | 모두 | 대상에 대해 시스템에서 생성한 읽기 전용 식별자입니다. |
| `audienceId` | 모두 | 대상이 플랫폼에서 생성한 대상이면 `id`과(와) 동일한 값입니다. 대상자가 외부에서 생성된 경우 이 값은 클라이언트가 제공합니다. |
| `schema` | 모두 | 대상의 XDM(Experience Data Model) 스키마. |
| `imsOrgId` | 모두 | 대상자가 속한 조직의 ID입니다. |
| `sandbox` | 모두 | 대상자가 속한 샌드박스에 대한 정보. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하세요. |
| `name` | 모두 | 대상자의 이름입니다. |
| `description` | 모두 | 대상자에 대한 설명. |
| `expression` | 플랫폼 생성 | 대상의 Profile Query Language(PQL) 표현식입니다. PQL 식에 대한 자세한 내용은 [PQL 식 안내서](../pql/overview.md)를 참조하세요. |
| `mergePolicyId` | 플랫폼 생성 | 대상자가 연결된 병합 정책의 ID입니다. 병합 정책에 대한 자세한 내용은 [병합 정책 안내서](../../profile/api/merge-policies.md)를 참조하십시오. |
| `evaluationInfo` | 플랫폼 생성 | 대상을 평가하는 방법을 표시합니다. 가능한 평가 방법에는 일괄 처리, 동기(스트리밍) 또는 연속(에지)이 포함됩니다. 평가 방법에 대한 자세한 내용은 [세그먼테이션 개요](../home.md)를 참조하세요. |
| `dependents` | 모두 | 현재 대상에 종속되는 대상 ID 배열. 세그먼트의 세그먼트인 대상자를 만드는 경우 사용됩니다. |
| `dependencies` | 모두 | 대상이 종속된 대상 ID의 배열입니다. 세그먼트의 세그먼트인 대상자를 만드는 경우 사용됩니다. |
| `type` | 모두 | 대상자가 플랫폼에서 생성되었는지 또는 외부에서 생성된 대상자인지 여부를 표시하는 시스템 생성 필드입니다. 가능한 값은 `SegmentDefinition` 및 `ExternalSegment`입니다. `SegmentDefinition`은(는) 플랫폼에서 생성된 대상을 참조하지만 `ExternalSegment`은(는) 플랫폼에서 생성되지 않은 대상을 참조합니다. |
| `originName` | 모두 | 대상자의 이름을 참조하는 필드입니다. 플랫폼 생성 대상의 경우 이 값은 `REAL_TIME_CUSTOMER_PROFILE`이 됩니다. Audience Orchestration에서 생성된 대상의 경우 이 값은 `AUDIENCE_ORCHESTRATION`이 됩니다. Adobe Audience Manager에서 생성된 대상의 경우 이 값은 `AUDIENCE_MANAGER`이 됩니다. 외부에서 생성된 다른 대상의 경우 이 값은 `CUSTOM_UPLOAD`이 됩니다. |
| `createdBy` | 모두 | 대상자를 만든 사용자의 ID입니다. |
| `labels` | 모두 | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |
| `namespace` | 모두 | 대상자가 속한 네임스페이스입니다. 가능한 값은 `AAM`, `AAMSegments`, `AAMTraits` 및 `AEPSegments`입니다. |
| `linkedAudienceRef` | 모두 | 다른 대상 관련 시스템에 대한 식별자를 포함하는 객체입니다. |

+++

## 새 대상 만들기 {#create}

`/audiences` 끝점에 대한 POST 요청을 수행하여 새 대상을 만들 수 있습니다.

**API 형식**

```http
POST /audiences
```

**요청**

+++ 플랫폼 생성 대상자 만들기에 대한 샘플 요청

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "AEPSegments",
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
| `name` | 대상자의 이름입니다. |
| `description` | 대상자에 대한 설명. |
| `type` | 대상자가 플랫폼에서 생성되었는지 또는 외부에서 생성된 대상자인지 여부를 표시하는 필드입니다. 가능한 값은 `SegmentDefinition` 및 `ExternalSegment`입니다. `SegmentDefinition`은(는) 플랫폼에서 생성된 대상을 참조하지만 `ExternalSegment`은(는) 플랫폼에서 생성되지 않은 대상을 참조합니다. |
| `expression` | 대상의 Profile Query Language(PQL) 표현식입니다. PQL 식에 대한 자세한 내용은 [PQL 식 안내서](../pql/overview.md)를 참조하세요. |
| `schema` | 대상의 XDM(Experience Data Model) 스키마. |
| `labels` | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |

+++

**응답**

성공적인 응답은 새로 생성된 대상자에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

+++플랫폼 생성 대상자를 만들 때의 샘플 응답입니다.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
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
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## 지정된 대상자 조회 {#get}

`/audiences` 끝점에 대한 GET 요청을 만들고 요청 경로에서 검색하려는 대상의 ID를 제공하여 특정 대상에 대한 자세한 정보를 조회할 수 있습니다.

**API 형식**

```http
GET /audiences/{AUDIENCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 검색하려는 대상자의 ID입니다. 이 필드는 `id` 필드이며 `audienceId` 필드는 **이(가) 아닙니다**. |

**요청**

+++대상자 검색에 대한 샘플 요청

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 지정된 대상에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

+++플랫폼 생성 대상자를 검색할 때의 샘플 응답입니다.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## 대상자 덮어쓰기 {#put}

`/audiences` 끝점에 대한 PUT 요청을 만들고 요청 경로에 업데이트하려는 대상의 ID를 제공하여 특정 대상을 업데이트(덮어쓰기)할 수 있습니다.

**API 형식**

```http
PUT /audiences/{AUDIENCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 업데이트할 대상자의 ID입니다. 이 필드는 `id` 필드이며 `audienceId` 필드는 **이(가) 아닙니다**. |

**요청**

+++전체 대상 업데이트에 대한 샘플 요청입니다.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-platform-audience-id",
    "name": "New Platform audience",
    "namespace": "AEPSegments",
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country=\"US\""
    }
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| 속성 | 설명 |
| -------- | ----------- | 
| `audienceId` | 대상자의 ID입니다. 외부에서 생성된 대상자에 대해 이 값은 사용자에 의해 제공될 수 있다. |
| `name` | 대상자의 이름입니다. |
| `namespace` | 대상자를 위한 네임스페이스입니다. |
| `description` | 대상자에 대한 설명. |
| `type` | 대상자가 플랫폼에서 생성되었는지 또는 외부에서 생성된 대상자인지 여부를 표시하는 시스템 생성 필드입니다. 가능한 값은 `SegmentDefinition` 및 `ExternalSegment`입니다. `SegmentDefinition`은(는) Experience Platform에서 생성된 대상을 참조하고 `ExternalSegment`은(는) Experience Platform에서 생성되지 않은 대상을 참조합니다. |
| `expression` | 대상의 PQL 표현식이 포함된 객체입니다. |
| `lifecycleState` | 대상의 상태입니다. 가능한 값은 `draft`, `published` 및 `inactive`입니다. `draft`은(는) 대상을 만들 때, `published`은(는) 대상을 게시할 때, `inactive`은(는) 대상이 더 이상 활성화되지 않을 때를 나타냅니다. |
| `datasetId` | 대상 데이터를 찾을 수 있는 데이터 세트의 ID입니다. |
| `labels` | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |

+++

**응답**

성공적인 응답은 새로 업데이트된 대상자의 세부 정보와 함께 HTTP 상태 200을 반환합니다. 대상의 세부 사항은 Experience Platform 생성 대상인지 또는 외부에서 생성된 대상인지에 따라 다릅니다.

+++전체 대상을 업데이트할 때의 샘플 응답입니다.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## 대상자 업데이트 {#patch}

`/audiences` 끝점에 대한 PATCH 요청을 만들고 요청 경로에 업데이트할 대상의 ID를 제공하여 특정 대상을 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 업데이트할 대상자의 ID입니다. 이 필드는 `id` 필드이며 `audienceId` 필드는 **이(가) 아닙니다**. |

**요청**

+++ 대상자 업데이트에 대한 샘플 요청입니다.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "op": "add",
        "path": "/lifecycleState",
        "value": "inactive"
    }
 ]'
```

| 속성 | 설명 |
| -------- | ----------- |
| `op` | 수행된 PATCH 작업 유형입니다. 이 끝점의 경우 이 값은 **always** `/add`입니다. |
| `path` | 업데이트할 필드의 경로입니다. `id`, `audienceId` 및 `namespace` **과(와) 같은 시스템 생성 필드는 편집할 수 없습니다**. |
| `value` | `path`에 지정된 속성에 새 값이 할당되었습니다. |

+++

**응답**

성공적인 응답은 업데이트된 대상이 있는 HTTP 상태 200을 반환합니다.

+++대상의 필드를 패치할 때 샘플 응답.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab5",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "inactive",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## 대상자 삭제 {#delete}

`/audiences` 끝점에 대한 DELETE 요청을 만들고 요청 경로에 삭제할 대상의 ID를 제공하여 특정 대상을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 삭제할 대상자의 ID입니다. 이 필드는 `id` 필드이며 `audienceId` 필드는 **이(가) 아닙니다**. |

**요청**

+++ 대상자 삭제에 대한 샘플 요청입니다.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 메시지 없이 HTTP 상태 204를 반환합니다.

## 여러 대상 검색 {#bulk-get}

`/audiences/bulk-get` 끝점에 대한 POST 요청을 만들고 검색하려는 대상의 ID를 제공하여 여러 대상을 검색할 수 있습니다.

**API 형식**

```http
POST /audiences/bulk-get
```

**요청**

+++ 여러 대상을 검색하기 위한 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**응답**

성공적인 응답은 요청된 대상자에 대한 정보와 함께 HTTP 상태 207을 반환합니다.

+++ 여러 대상을 검색할 때의 샘플 응답입니다.

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
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
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
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
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++


## 다음 단계

이제 이 안내서를 읽고 Adobe Experience Platform API를 사용하여 대상을 만들고, 관리하고, 삭제하는 방법을 더 잘 이해하게 되었습니다. UI를 사용한 대상자 관리에 대한 자세한 내용은 [세그멘테이션 UI 안내서](../ui/overview.md)를 참조하십시오.
