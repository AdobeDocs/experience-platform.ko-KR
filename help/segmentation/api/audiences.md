---
title: 대상 API 엔드포인트
description: Adobe Experience Platform 세그멘테이션 서비스 API의 대상 끝점을 사용하여 프로그래밍 방식으로 조직의 대상을 만들고, 관리하고, 업데이트합니다.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 3%

---

# 대상자 엔드포인트

대상자는 유사한 행동 및/또는 특성을 공유하는 사람들의 컬렉션입니다. 이러한 사람 컬렉션은 Adobe Experience Platform을 사용하거나 외부 소스에서 생성할 수 있습니다. 다음을 사용할 수 있습니다. `/audiences` 프로그래밍 방식으로 대상을 검색, 만들기, 업데이트 및 삭제할 수 있는 Segmentation API의 종단점입니다.

## 시작하기

이 안내서에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 대상자 목록 검색 {#list}

에 GET 요청을 하여 조직의 모든 대상 목록을 검색할 수 있습니다. `/audiences` 엔드포인트.

**API 형식**

다음 `/audiences` 엔드포인트는 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 리소스를 나열할 때 비싼 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 대상이 검색됩니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

대상자 목록을 검색할 때 다음 쿼리 매개 변수를 사용할 수 있습니다.

| 쿼리 매개 변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `start` | 반환된 대상의 시작 오프셋을 지정합니다. | `start=5` |
| `limit` | 페이지당 반환되는 최대 대상자 수를 지정합니다. | `limit=10` |
| `sort` | 결과를 정렬하는 순서를 지정합니다. 이 이름은 형식으로 작성됩니다. `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | 다음과 같은 대상을 지정할 수 있는 필터 **정확하게** 속성 값과 일치합니다. 이 이름은 형식으로 작성됩니다. `property=` | `property=audienceId==test-audience-id` |
| `name` | 이름을 가진 대상자를 지정할 수 있는 필터 **contain** 제공된 값. 이 값은 대/소문자를 구분하지 않습니다. | `name=Sample` |
| `description` | 설명이 있는 대상자를 지정할 수 있는 필터 **contain** 제공된 값. 이 값은 대/소문자를 구분하지 않습니다. | `description=Test Description` |

**요청**

다음 요청은 조직에서 만든 마지막 두 대상을 검색합니다.

+++대상자 목록을 검색하는 샘플 요청입니다.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=2 \
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
| `audienceId` | 모두 | 대상자가 플랫폼에서 생성한 대상자인 경우 이 값은 과 같습니다. `id`. 대상자가 외부에서 생성된 경우 이 값은 클라이언트가 제공합니다. |
| `schema` | 모두 | 대상의 XDM(Experience Data Model) 스키마. |
| `imsOrgId` | 모두 | 대상자가 속한 조직의 ID입니다. |
| `sandbox` | 모두 | 대상자가 속한 샌드박스에 대한 정보. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md). |
| `name` | 모두 | 대상자의 이름입니다. |
| `description` | 모두 | 대상자에 대한 설명. |
| `expression` | 플랫폼 생성 | 대상자의 PQL(프로필 쿼리 언어) 표현식입니다. PQL 표현식에 대한 자세한 내용은 [PQL 표현식 안내서](../pql/overview.md). |
| `mergePolicyId` | 플랫폼 생성 | 대상자가 연결된 병합 정책의 ID입니다. 병합 정책에 대한 자세한 내용은 [병합 정책 안내서](../../profile/api/merge-policies.md). |
| `evaluationInfo` | 플랫폼 생성 | 대상을 평가하는 방법을 표시합니다. 가능한 평가 방법에는 일괄 처리, 동기(스트리밍) 또는 연속(에지)이 포함됩니다. 평가 방법에 대한 자세한 내용은 [세그먼테이션 개요](../home.md) |
| `dependents` | 모두 | 현재 대상에 종속되는 대상 ID 배열. 세그먼트의 세그먼트인 대상자를 만드는 경우 사용됩니다. |
| `dependencies` | 모두 | 대상이 종속된 대상 ID의 배열입니다. 세그먼트의 세그먼트인 대상자를 만드는 경우 사용됩니다. |
| `type` | 모두 | 대상자가 플랫폼에서 생성되었는지 또는 외부에서 생성된 대상자인지 여부를 표시하는 시스템 생성 필드입니다. 가능한 값은 다음과 같습니다. `SegmentDefinition` 및 `ExternalSegment`. A `SegmentDefinition` 는 플랫폼에서 생성된 대상자를 참조하지만 `ExternalSegment` 는 플랫폼에서 생성되지 않은 대상을 나타냅니다. |
| `originName` | 모두 | 대상자의 이름을 참조하는 필드입니다. 플랫폼 생성 대상의 경우 이 값은 다음과 같습니다. `REAL_TIME_CUSTOMER_PROFILE`. Audience Orchestration에서 생성된 대상의 경우 이 값은 다음과 같습니다. `AUDIENCE_ORCHESTRATION`. Adobe Audience Manager에서 생성된 대상의 경우 이 값은 다음과 같습니다. `AUDIENCE_MANAGER`. 기타 외부 생성 대상의 경우 이 값은 다음과 같습니다. `CUSTOM_UPLOAD`. |
| `createdBy` | 모두 | 대상자를 만든 사용자의 ID입니다. |
| `labels` | 모두 | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |
| `namespace` | 모두 | 대상자가 속한 네임스페이스입니다. 가능한 값은 다음과 같습니다. `AAM`, `AAMSegments`, `AAMTraits`, 및 `AEPSegments`. |
| `linkedAudienceRef` | 모두 | 다른 대상 관련 시스템에 대한 식별자를 포함하는 객체입니다. |

+++

## 새 대상 만들기 {#create}

에 POST 요청을 하여 새 대상을 만들 수 있습니다. `/audiences` 엔드포인트.

**API 형식**

```http
POST /audiences
```

**요청**

>[!BEGINTABS]

>[!TAB 플랫폼 생성 대상자]

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
        ],
        "ttlInDays": 60
    }'
```

| 속성 | 설명 |
| -------- | ----------- | 
| `name` | 대상자의 이름입니다. |
| `description` | 대상자에 대한 설명. |
| `type` | 대상자가 플랫폼에서 생성되었는지 또는 외부에서 생성된 대상자인지 여부를 표시하는 필드입니다. 가능한 값은 다음과 같습니다. `SegmentDefinition` 및 `ExternalSegment`. A `SegmentDefinition` 는 플랫폼에서 생성된 대상자를 참조하지만 `ExternalSegment` 는 플랫폼에서 생성되지 않은 대상을 나타냅니다. |
| `expression` | 대상자의 PQL(프로필 쿼리 언어) 표현식입니다. PQL 표현식에 대한 자세한 내용은 [PQL 표현식 안내서](../pql/overview.md). |
| `schema` | 대상의 XDM(Experience Data Model) 스키마. |
| `labels` | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |
| `ttlInDays` | 대상의 데이터 만료 값(일)을 나타냅니다. |

+++

>[!TAB 외부에서 생성된 대상자]

+++ 외부에서 생성된 대상자 만들기에 대한 샘플 요청

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "audienceId":"test-external-audience-id",
        "name":"externalAudience",
        "namespace":"aam",
        "description":"Last 30 days",
        "type":"ExternalSegment",
        "originName":"CUSTOM_UPLOAD",
        "lifecycleState":"published",
        "datasetId":"6254cf3c97f8e31b639fb14d",
        "labels":[
            "core/C1"
        ],
        "linkedAudienceRef":{
            "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- | 
| `audienceId` | 대상자에 대해 사용자가 제공한 ID입니다. |
| `name` | 대상자의 이름입니다. |
| `namespace` | 대상자를 위한 네임스페이스입니다. |
| `description` | 대상자에 대한 설명. |
| `type` | 대상자가 플랫폼에서 생성되었는지 또는 외부에서 생성된 대상자인지 여부를 표시하는 필드입니다. 가능한 값은 다음과 같습니다. `SegmentDefinition` 및 `ExternalSegment`. A `SegmentDefinition` 는 플랫폼에서 생성된 대상자를 참조하지만 `ExternalSegment` 는 플랫폼에서 생성되지 않은 대상을 나타냅니다. |
| `originName` | 대상자의 기원 이름입니다. 외부에서 생성된 대상자의 경우 기본값은 입니다. `CUSTOM_UPLOAD`. 기타 지원되는 값은 다음과 같습니다 `REAL_TIME_CUSTOMER_PROFILE`, `CUSTOM_UPLOAD`, `AUDIENCE_ORCHESTRATION`, 및 `AUDIENCE_MATCH`. |
| `lifecycleState` | 만들려는 대상의 초기 상태를 결정하는 선택적 필드입니다. 지원되는 값: `draft`, `published`, 및 `inactive`. |
| `datasetId` | 대상을 구성하는 데이터를 찾을 수 있는 데이터 세트의 ID입니다. |
| `labels` | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |
| `audienceMeta` | 외부에서 생성된 대상자에 속하는 메타데이터입니다. |
| `linkedAudienceRef` | 다른 대상 관련 시스템에 대한 식별자를 포함하는 객체입니다. 여기에는 다음이 포함될 수 있습니다. <ul><li>`flowId`: 이 ID는 대상 데이터를 가져오는 데 사용된 데이터 흐름에 대상을 연결하는 데 사용됩니다. 필요한 ID에 대한 자세한 내용은 [데이터 흐름 안내서 만들기](../../sources/tutorials/api/collect/cloud-storage.md).</li><li>`aoWorkflowId`: 이 ID는 대상자를 관련 Audience Orchestration 구성에 연결하는 데 사용됩니다.&lt;/li/> <li>`payloadFieldGroupRef`: 이 ID는 대상자의 구조를 설명하는 XDM 필드 그룹 스키마를 참조하는 데 사용됩니다. 이 필드의 값에 대한 자세한 내용은 [XDM 필드 그룹 엔드포인트 안내서](../../xdm/api/field-groups.md).</li><li>`audienceFolderId`: 이 ID는 대상자의 Adobe Audience Manager에 있는 폴더 ID를 참조하는 데 사용됩니다. 이 API에 대한 자세한 내용은 [Adobe Audience Manager API 안내서](https://bank.demdex.com/portal/swagger/index.html#/Segment%20Folder%20API).</ul> |

+++

>[!ENDTABS]

**응답**

성공적인 응답은 새로 생성된 대상자에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

>[!BEGINTABS]

>[!TAB 플랫폼 생성 대상자]

+++플랫폼 생성 대상자를 만들 때의 샘플 응답입니다.

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

>[!TAB 외부에서 생성된 대상자]

+++외부에서 생성된 대상자를 만들 때 샘플 응답.

```json
{
   "id": "322f9f62-cd27-11ec-9d64-0242ac120002",
   "audienceId": "test-external-audience-id",
   "name": "externalAudience",
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
   "labels": [
      "core/C1"
   ],
   "linkedAudienceRef": {
      "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
   },
   "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
   "creationTime": 1650251290000,
   "updateEpoch": 1650251290,
   "updateTime": 1650251290000,
   "createEpoch": 1650251290
}
```

+++

## 지정된 대상자 조회 {#get}

에 GET 요청을 하여 특정 대상에 대한 자세한 정보를 조회할 수 있습니다. `/audiences` 엔드포인트 및 요청 경로에서 검색할 대상자의 ID 제공.

**API 형식**

```http
GET /audiences/{AUDIENCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 검색하려는 대상자의 ID입니다. 이 은(는) `id` 필드 및 **아님** 다음 `audienceId` 필드. |

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

성공적인 응답은 지정된 대상에 대한 정보와 함께 HTTP 상태 200을 반환합니다. 대상이 Adobe Experience Platform으로 생성되는지 또는 외부 소스로 생성되는지에 따라 응답이 달라집니다.

>[!BEGINTABS]

>[!TAB 플랫폼 생성 대상자]

+++플랫폼 생성 대상자를 검색할 때의 샘플 응답입니다.

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
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB 외부에서 생성된 대상자]

+++외부에서 생성된 대상자를 검색할 때의 샘플 응답입니다.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "test-external-audience-id",
    "name": "externalAudience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "active",
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

+++

>[!ENDTABS]

## 대상의 필드 업데이트 {#update-field}

에 PATCH 요청을 하여 특정 대상의 필드를 업데이트할 수 있습니다. `/audiences` 엔드포인트 및 요청 경로에 업데이트할 대상자의 ID 제공

**API 형식**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 업데이트할 대상자의 ID입니다. 이 은(는) `id` 필드 및 **아님** 다음 `audienceId` 필드. |

**요청**

+++대상의 필드를 업데이트하는 샘플 요청입니다.

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
| `op` | 대상을 업데이트하는 경우 이 값은 항상 입니다. `add`. |
| `path` | 업데이트할 필드의 경로입니다. |
| `value` | 필드를 업데이트할 값입니다. |

+++

**응답**

성공적인 응답은 새로 업데이트된 대상에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

+++대상의 필드를 업데이트할 때의 샘플 응답입니다.

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
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## 대상자 업데이트 {#put}

에 PUT 요청을 하여 특정 대상을 업데이트(덮어쓰기)할 수 있습니다. `/audiences` 엔드포인트 및 요청 경로에 업데이트할 대상자의 ID 제공

**API 형식**

```http
PUT /audiences/{AUDIENCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 업데이트할 대상자의 ID입니다. 이 은(는) `id` 필드 및 **아님** 다음 `audienceId` 필드. |

**요청**

+++전체 대상자 업데이트에 대한 샘플 요청입니다.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "description": "Last 30 days",
    "type": "ExternalSegment",
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
| `type` | 대상자가 플랫폼에서 생성되었는지 또는 외부에서 생성된 대상자인지 여부를 표시하는 시스템 생성 필드입니다. 가능한 값은 다음과 같습니다. `SegmentDefinition` 및 `ExternalSegment`. A `SegmentDefinition` 는 플랫폼에서 생성된 대상자를 참조하지만 `ExternalSegment` 는 플랫폼에서 생성되지 않은 대상을 나타냅니다. |
| `lifecycleState` | 대상의 상태입니다. 가능한 값은 다음과 같습니다. `draft`, `published`, 및 `inactive`. `draft` 대상자를 만들 때 을 나타냅니다. `published` 대상자가 게시될 때 및 `inactive` 대상이 더 이상 활성 상태가 아닌 경우. |
| `datasetId` | 대상 데이터를 찾을 수 있는 데이터 세트의 ID입니다. |
| `labels` | 대상과 관련된 객체 수준 데이터 사용 및 속성 기반 액세스 제어 레이블입니다. |

+++

**응답**

성공적인 응답은 새로 업데이트된 대상자의 세부 정보와 함께 HTTP 상태 200을 반환합니다. 대상자에 대한 세부 정보는 플랫폼 생성 대상자인지 또는 외부에서 생성된 대상자인지에 따라 달라집니다.

+++전체 대상을 업데이트할 때의 샘플 응답입니다.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
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

## 대상자 삭제 {#delete}

에 DELETE 요청을 하여 특정 대상을 삭제할 수 있습니다. `/audiences` 엔드포인트 및 요청 경로에서 삭제하려는 대상자의 ID 제공.

**API 형식**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 삭제할 대상자의 ID입니다. 이 은(는) `id` 필드 및 **아님** 다음 `audienceId` 필드. |

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

에 POST 요청을 하여 여러 대상을 검색할 수 있습니다. `/audiences/bulk-get` 엔드포인트 및 검색할 대상자의 ID 제공

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
         "ttlInDays": 30,
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

## 여러 대상 업데이트 {#bulk-patch}

에 POST 요청을 하여 여러 대상자의 프로필 및 레코드 수를 업데이트할 수 있습니다. `/audiences/bulk-patch-metric` 엔드포인트 및 업데이트하려는 대상자의 ID 제공

**API 형식**

```http
POST /audiences/bulk-patch-metric
```

**요청**

+++ 여러 대상을 업데이트하는 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-patch-metric
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "jobId": "12345",
    "jobType": "AO",
    "resources": [
        {
            "audienceId": "QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "namespace": "AAMTraits",
            "operations": [
                {
                    "op": "add",
                    "path": "/metrics/data",
                    "value": {
                        "totalProfiles": 11037
                    }
                },
            ]
        },
        {
            "audienceId": "QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "namespace": "AAMTraits",
            "operations": [
                {
                    "op": "add",
                    "path": "/metrics/data",
                    "value": {
                        "totalProfiles": 523
                    }
                }
            ]
        }
    ]
    }
```

<table>
<thead>
<tr>
<th>매개변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>jobId</code></td>
<td>업데이트를 실행할 작업의 ID입니다.</td>
</tr>
<tr>
<td><code>jobType</code></td>
<td>업데이트를 실행할 작업 유형입니다. 이 값은 다음 중 하나일 수 있습니다. <code>export</code> 또는 <code>AO</code>.</td>
</tr>
<tr>
<td><code>audienceId</code></td>
<td>업데이트할 대상자의 ID입니다. 이 은(는) <code>audienceId</code> 값, 및 <strong>아님</strong> 다음 <code>id</code> 대상자의 값입니다.</td>
</tr>
<tr>
<td><code>namespace</code></td>
<td>업데이트할 대상자의 네임스페이스입니다.</td>
</tr>
<tr>
<td><code>operations</code></td>
<td>대상자를 업데이트하는 데 사용되는 정보가 포함된 객체입니다.</td>
</tr>
<tr>
<td><code>operations.op</code></td>
<td>패치에 사용되는 작업입니다. 여러 대상을 업데이트할 때 이 값은 다음과 같습니다. <strong>항상</strong> <code>add</code>.</td>
</tr>
<tr>
<td><code>operations.path</code></td>
<td>업데이트할 필드의 경로입니다. 현재는 두 개의 경로만 지원됩니다. <code>/metrics/data</code> 을(를) 업데이트할 때 <strong>프로필</strong> 및 수 <code>/recordMetrics/data</code> 을(를) 업데이트할 때 <strong>기록</strong> 카운트.</td>
</tr>
<tr>
<td><code>operations.value</code></td>
<td>
업데이트할 필드의 값입니다. 프로필 수를 업데이트할 때 이 값은 다음과 같이 표시됩니다. 
<pre>
{ "totalProfiles": 123456 }
</pre>
레코드 수를 업데이트할 때 이 값은 다음과 같이 표시됩니다. 
<pre>
{ "recordCount": 123456 }
</pre>
</td>
</tr>
</tbody>
</table>

+++

**응답**

성공적인 응답은 업데이트된 대상에 대한 세부 정보와 함께 HTTP 상태 207을 반환합니다.

+++ 여러 대상을 업데이트하기 위한 샘플 응답입니다.

```json
{
   "resources":[
      {
         "audienceId":"QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",

         "namespace": "AAMTraits",
         "status":200
      },
      {
         "audienceId":"QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1vcmlnaW4tdGVzdDE_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",

         "namespace": "AAMTraits",
         "status":200
      }
   ]
}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `status` | 업데이트된 대상자의 상태입니다. 반환된 상태가 200이면 대상이 성공적으로 업데이트되었습니다. 대상자를 업데이트할 수 없는 경우, 대상자가 업데이트되지 않은 이유를 설명하는 오류가 반환됩니다. |

+++

## 다음 단계

이제 이 안내서를 읽고 Adobe Experience Platform API를 사용하여 대상을 만들고, 관리하고, 삭제하는 방법을 더 잘 이해하게 되었습니다. UI를 사용하는 대상자 관리에 대한 자세한 내용은 [세그멘테이션 UI 안내서](../ui/overview.md).
