---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 병합 정책 API 끝점
type: Documentation
description: Adobe Experience Platform을 사용하면 여러 소스에서 데이터 조각을 함께 가져와서 결합하여 각 개별 고객에 대한 전체 보기를 볼 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책은 Platform이 데이터 우선 순위가 지정되는 방법과 통합 보기를 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 1%

---

# 병합 정책 끝점

Adobe Experience Platform을 사용하면 여러 소스에서 데이터 조각을 함께 가져와서 결합하여 각 개별 고객에 대한 전체 보기를 볼 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책이 [!DNL Platform] 는 데이터의 우선 순위가 지정되는 방식과 결합할 데이터를 파악하여 통합 보기를 만듭니다.

예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 표시되는 해당 단일 고객과 관련된 여러 프로필 조각이 있습니다. 이러한 조각을 Platform에 수집하면 병합되어 해당 고객에 대한 단일 프로필을 만듭니다. 여러 소스의 데이터가 충돌하면(예: 한 조각은 고객을 &quot;단일&quot;로 나열하고 다른 조각은 고객을 &quot;기혼&quot;으로 나열함) 병합 정책은 개별 프로필에 포함할 정보를 결정합니다.

RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. 이 안내서에서는 API를 사용하여 병합 정책 작업을 제공합니다.

UI를 사용하여 병합 정책을 작업하려면 [병합 정책 UI 안내서](../merge-policies/ui-guide.md). 일반적으로 병합 정책 및 Experience Platform 내의 해당 역할에 대해 자세히 알아보려면 [정책 병합 개요](../merge-policies/overview.md).

## 시작하기

이 안내서에서 사용되는 API 엔드포인트는 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 계속하기 전에 [시작 안내서](getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 모든 호출을 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다 [!DNL Experience Platform] API.

## 병합 정책의 구성 요소 {#components-of-merge-policies}

병합 정책은 조직의 개인 정보이므로 필요한 특정 방식으로 스키마를 병합하기 위한 다양한 정책을 만들 수 있습니다. 모든 API에 액세스 [!DNL Profile] 데이터에는 병합 정책이 필요하지만, 이 정책을 명시적으로 제공하지 않으면 기본값이 사용됩니다. [!DNL Platform] 는 조직에 기본 병합 정책을 제공하거나 특정 XDM(Experience Data Model) 스키마 클래스에 대한 병합 정책을 만들어 조직의 기본값으로 표시할 수 있습니다.

각 조직은 스키마 클래스당 여러 병합 정책을 가질 수 있지만 각 클래스에는 하나의 기본 병합 정책만 있을 수 있습니다. 스키마 클래스의 이름을 제공하고 병합 정책이 필요하지만 제공되지 않은 경우 기본값으로 설정된 병합 정책이 사용됩니다.

>[!NOTE]
>
>새 병합 정책을 기본값으로 설정하면 이전에 기본값으로 설정된 기존 병합 정책이 자동으로 업데이트되어 더 이상 기본값으로 사용되지 않습니다.

모든 프로필 소비자가 모서리에서 동일한 보기를 사용하여 작업하도록 하기 위해 병합 정책을 에지 상태에서 활성으로 표시할 수 있습니다. 세그먼트가 에지(에지 세그먼트로 표시됨)에서 활성화되려면 에지에서 활성으로 표시된 병합 정책에 연결해야 합니다. 세그먼트가 **not** edge에서 활성으로 표시된 병합 정책에 연결된 세그먼트는 edge에서 활성으로 표시되지 않고 스트리밍 세그먼트로 표시됩니다.

또한 각 조직은 **하나** 에지 상태에서 활성화된 병합 정책. 병합 정책이 Edge에서 활성 상태인 경우, Edge Profile, Edge Segmentation 및 Destinations on Edge와 같은 에지의 다른 시스템에 사용할 수 있습니다.

### 병합 정책 개체 완료

전체 병합 정책 개체는 프로필 조각 병합의 측면을 제어하는 환경 설정 집합을 나타냅니다.

**정책 개체 병합**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| 속성 | 설명 |
|---|---|
| `id` | 생성 시 지정된 시스템에서 생성한 고유 식별자입니다 |
| `name` | 목록 보기에서 병합 정책을 식별할 수 있는 친숙한 이름입니다. |
| `imsOrgId` | 이 병합 정책이 속한 조직 ID |
| `schema.name` | 의 일부 [`schema`](#schema) 개체, `name` 필드에는 병합 정책이 관련된 XDM 스키마 클래스가 포함되어 있습니다. 스키마 및 클래스에 대한 자세한 내용은 [XDM 설명서](../../xdm/home.md). |
| `version` | [!DNL Platform] 병합 정책의 버전을 유지 관리했습니다. 병합 정책이 업데이트될 때마다 이 읽기 전용 값이 증가합니다. |
| `identityGraph` | [ID 그래프](#identity-graph) 관련 ID를 얻을 id 그래프를 나타내는 개체입니다. 모든 관련 ID에 대해 발견된 프로필 조각이 병합됩니다. |
| `attributeMerge` | [속성 병합](#attribute-merge) 데이터 충돌 시 병합 정책이 프로필 속성의 우선 순위를 지정하는 방법을 나타내는 개체입니다. |
| `isActiveOnEdge` | 이 병합 정책을 에지에서 사용할 수 있는지 여부를 나타내는 부울 값입니다. 기본적으로 이 값은 다음과 같습니다 `false`. |
| `default` | 이 병합 정책이 지정된 스키마의 기본값인지 여부를 나타내는 부울 값. |
| `updateEpoch` | 병합 정책에 대한 마지막 업데이트 날짜입니다. |

**병합 정책 예**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### ID 그래프 {#identity-graph}

[Adobe Experience Platform Identity 서비스](../../identity-service/home.md) 에서는 전체적으로 및 각 조직에 대해 사용되는 ID 그래프를 관리합니다. [!DNL Experience Platform]. 다음 `identityGraph` 병합 정책의 특성은 사용자의 관련 ID를 결정하는 방법을 정의합니다.

**identityGraph 개체**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

위치 `{IDENTITY_GRAPH_TYPE}` 는 다음 중 하나입니다.

* **&quot;none&quot;:** ID 결합을 수행하지 않습니다.
* **&quot;pdg&quot;:** 개인 ID 그래프를 기반으로 ID 결합을 수행합니다.

**예`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 속성 병합 {#attribute-merge}

프로필 조각은 특정 사용자에 대해 존재하는 ID 목록 중 하나의 ID에 대한 프로필 정보입니다. ID 그래프 유형을 사용하면 두 개 이상의 ID가 발생할 수 있는 경우 프로필 속성이 충돌할 가능성이 있고 우선 순위를 지정해야 합니다. 사용 `attributeMerge`를 설정하는 경우 키 값(레코드 데이터) 유형 데이터 세트 간 병합 충돌이 발생하는 경우 우선 순위를 지정할 프로필 속성을 지정할 수 있습니다.

**attributeMerge 개체**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

위치 `{ATTRIBUTE_MERGE_TYPE}` 는 다음 중 하나입니다.

* **`timestampOrdered`**: (기본값) 마지막으로 업데이트된 프로필에 우선 순위를 지정합니다. 이 병합 유형을 사용하면 `data` 속성이 필요하지 않습니다.
* **`dataSetPrecedence`**: 제공된 데이터 세트를 기반으로 프로필 조각에 우선 순위를 지정합니다. 한 데이터 세트에 있는 정보가 다른 데이터 세트에 있는 데이터보다 선호되거나 신뢰할 수 있는 경우 사용할 수 있습니다. 이 병합 유형을 사용하는 경우 `order` 우선 순위 순서로 데이터 세트를 나열하므로 특성이 필요합니다.
   * **`order`**: &quot;dataSetPriority&quot;를 사용하면 `order` 데이터 세트 목록과 함께 배열을 제공해야 합니다. 목록에 포함되지 않은 데이터 세트는 병합되지 않습니다. 즉, 데이터 세트를 명시적으로 나열하여 프로필에 병합해야 합니다. 다음 `order` 배열에는 우선 순위 순서로 데이터 세트의 ID가 나열됩니다.

#### 예 `attributeMerge` 개체 사용 `dataSetPrecedence` 유형

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### 예 `attributeMerge` 개체 사용 `timestampOrdered` 유형

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 스키마 {#schema}

스키마 개체는 이 병합 정책을 만들 XDM(Experience Data Model) 스키마 클래스를 지정합니다.

**`schema`개체**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

위치 값 `name` 는 병합 정책과 연결된 스키마가 기반으로 하는 XDM 클래스의 이름입니다.

**예`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

XDM과 Experience Platform에서 스키마 작업에 대한 자세한 내용은 다음을 참조하십시오 [XDM 시스템 개요](../../xdm/home.md).

## 병합 정책 액세스 {#access-merge-policies}

사용 [!DNL Real-Time Customer Profile] API, `/config/mergePolicies` 끝점을 사용하면 조회 요청을 수행하여 ID로 특정 병합 정책을 보거나 특정 기준으로 필터링된 조직의 모든 병합 정책에 액세스할 수 있습니다. 를 사용할 수도 있습니다 `/config/mergePolicies/bulk-get` ID로 여러 병합 정책을 검색하는 끝점입니다. 이러한 각 호출을 수행하는 단계는 다음 섹션에 요약되어 있습니다.

### ID로 단일 병합 정책 액세스

에 GET 요청을 수행하여 해당 ID로 단일 병합 정책에 액세스할 수 있습니다 `/config/mergePolicies` 엔드포인트 및 포함 `mergePolicyId` 를 입력합니다.

**API 형식**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| 매개 변수 | 설명 |
|---|---|
| `{mergePolicyId}` | 삭제할 병합 정책의 식별자입니다. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**응답**

성공적인 응답이 병합 정책의 세부 정보를 반환합니다.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

자세한 내용은 [병합 정책 구성 요소](#components-of-merge-policies) 병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 섹션을 참조하십시오.

### ID로 여러 병합 정책 검색

에 POST 요청을 만들어 여러 병합 정책을 검색할 수 있습니다 `/config/mergePolicies/bulk-get` 요청 본문에서 검색할 병합 정책의 ID를 포함하여 끝점입니다.

**API 형식**

```http
POST /config/mergePolicies/bulk-get
```

**요청**

요청 본문은 세부 정보를 검색할 각 병합 정책에 대해 &quot;id&quot;를 포함하는 개별 개체가 있는 &quot;ids&quot; 배열을 포함합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**응답**

성공적인 응답은 HTTP 상태 207(다중 상태) 및 POST 요청에 ID가 제공된 병합 정책의 세부 사항을 반환합니다.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

자세한 내용은 [병합 정책 구성 요소](#components-of-merge-policies) 병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 섹션을 참조하십시오.

### 기준별로 여러 병합 정책 나열

조직에 GET 요청을 실행하여 조직 내에 여러 병합 정책을 나열할 수 있습니다 `/config/mergePolicies` endpoint 및 using 선택적 쿼리 매개 변수를 사용하여 응답을 필터링, 순서 및 페이징합니다. 여러 매개 변수를 앰퍼샌드(&amp;)로 구분하여 포함할 수 있습니다. 매개 변수 없이 이 종단점을 호출하면 조직에서 사용할 수 있는 모든 병합 정책을 검색합니다.

**API 형식**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
|---|---|
| `default` | 병합 정책이 스키마 클래스의 기본값인지 여부를 기준으로 결과를 필터링하는 부울 값입니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. 기본값: 20년 |
| `orderBy` | 결과를 정렬 기준으로 사용할 필드를 지정합니다. `orderBy=name` 또는 `orderBy=+name` 이름으로 오름차순으로 정렬하거나, `orderBy=-name`을 입력하여 내림차순으로 정렬합니다. 이 값을 생략하면 기본 정렬 `name` 오름차순으로 표시합니다. |
| `isActiveOnEdge` | 병합 정책이 에지 상태에서 활성 상태인지 여부를 기준으로 결과를 필터링하는 부울 값입니다. |
| `schema.name` | 사용 가능한 병합 정책을 검색할 스키마의 이름입니다. |
| `identityGraph.type` | 결과는 ID 그래프 유형별로 필터링합니다. 가능한 값에는 &quot;없음&quot; 및 &quot;pdg&quot;(개인 그래프)가 포함됩니다. |
| `attributeMerge.type` | 사용된 속성 병합 유형별로 결과를 필터링합니다. 가능한 값에는 &quot;timestampOrdered&quot; 및 &quot;dataSetPriority&quot;가 포함됩니다. |
| `start` | 페이지 오프셋 - 검색할 데이터의 시작 ID를 지정합니다. 기본값: 0 |
| `version` | 병합 정책의 특정 버전을 사용하려는 경우 이 항목을 지정하십시오. 기본적으로 최신 버전이 사용됩니다. |

에 대한 자세한 내용은 `schema.name`, `identityGraph.type`, 및 `attributeMerge.type`를 참조하려면 [병합 정책 구성 요소](#components-of-merge-policies) 섹션 을 참조하십시오.


**요청**

다음 요청은 지정된 스키마에 대한 모든 병합 정책을 나열합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**응답**

성공적인 응답은 요청에 전송된 쿼리 매개 변수로 지정된 기준을 충족하는 페이지 매김 정책의 목록을 반환합니다.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| 속성 | 설명 |
|---|---|
| `_links.next.href` | 다음 결과 페이지의 URI 주소입니다. 이 URI를 동일한 종단점에 대한 다른 API 호출에 대한 요청 매개 변수로 사용하여 페이지를 확인합니다. 다음 페이지가 없으면 이 값은 빈 문자열입니다. |

## 병합 정책 만들기

에 POST 요청을 작성하여 조직에 대한 새 병합 정책을 만들 수 있습니다 `/config/mergePolicies` 엔드포인트.

**API 형식**

```http
POST /config/mergePolicies
```

**요청**
다음 요청은 페이로드에 제공된 속성 값으로 구성된 새 병합 정책을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| 속성 | 설명 |
|---|---|
| `name` | 목록 보기에서 병합 정책을 식별할 수 있는 친근한 이름입니다. |
| `identityGraph.type` | 병합할 관련 ID를 가져올 ID 그래프 유형입니다. 가능한 값: &quot;없음&quot; 또는 &quot;pdg&quot;(개인 그래프) |
| `attributeMerge` | 데이터 충돌 시 프로필 속성 값의 우선 순위를 지정하는 방법입니다. |
| `schema` | 병합 정책과 연결된 XDM 스키마 클래스입니다. |
| `isActiveOnEdge` | 이 병합 정책이 에지 상태에서 활성 상태인지 여부를 지정합니다. |
| `default` | 이 병합 정책이 스키마의 기본값인지 여부를 지정합니다. |

자세한 내용은 [병합 정책 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.

**응답**

성공한 응답은 새로 만든 병합 정책의 세부 정보를 반환합니다.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

자세한 내용은 [병합 정책 구성 요소](#components-of-merge-policies) 병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 섹션을 참조하십시오.

## 병합 정책 업데이트 {#update}

개별 속성(PATCH)을 편집하거나 새 속성(PUT)으로 전체 병합 정책을 덮어써서 기존 병합 정책을 수정할 수 있습니다. 각 예제는 아래에 나와 있습니다.

### 개별 병합 정책 필드 편집

에 PATCH 요청을 만들어 병합 정책에 대한 개별 필드를 편집할 수 있습니다 `/config/mergePolicies/{mergePolicyId}` endpoint:

**API 형식**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 매개 변수 | 설명 |
|---|---|
| `{mergePolicyId}` | 삭제할 병합 정책의 식별자입니다. |

**요청**

다음 요청은 지정된 병합 정책의 값을 변경하여 업데이트 `default` 속성 대상 `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| 속성 | 설명 |
|---|---|
| `op` | 수행할 작업을 지정합니다. 다른 PATCH 작업의 예는 [JSON 패치 설명서](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | 업데이트할 필드의 경로입니다. 허용되는 값은 다음과 같습니다. &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | 지정된 필드를 로 설정할 값입니다. |

자세한 내용은 [병합 정책 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.


**응답**

성공적인 응답은 새로 업데이트된 병합 정책의 세부 정보를 반환합니다.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

### 병합 정책 덮어쓰기

병합 정책을 수정하는 또 다른 방법은 PUT 요청을 사용하는 것입니다. 이 요청은 전체 병합 정책을 덮어씁니다.

**API 형식**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 매개 변수 | 설명 |
|---|---|
| `{mergePolicyId}` | 덮어쓸 병합 정책의 식별자입니다. |

**요청**

다음 요청은 지정된 병합 정책을 덮어쓰고, 해당 속성 값을 페이로드에서 제공된 값으로 바꿉니다. 이 요청은 기존 병합 정책을 완전히 대체하므로 원래 병합 정책을 정의할 때 필요한 모든 필드를 제공해야 합니다. 그러나 이번에는 변경할 필드에 대해 업데이트된 값을 제공하고 있습니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "isActiveOnEdge": true,
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| 속성 | 설명 |
|---|---|
| `name` | 목록 보기에서 병합 정책을 식별할 수 있는 친근한 이름입니다. |
| `identityGraph` | 병합할 관련 ID를 가져올 ID 그래프입니다. |
| `attributeMerge` | 데이터 충돌 시 프로필 속성 값의 우선 순위를 지정하는 방법입니다. |
| `schema` | 병합 정책과 연결된 XDM 스키마 클래스입니다. |
| `isActiveOnEdge` | 이 병합 정책이 에지 상태에서 활성 상태인지 여부를 지정합니다. |
| `default` | 이 병합 정책이 스키마의 기본값인지 여부를 지정합니다. |

자세한 내용은 [병합 정책 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.

**응답**

성공적인 응답이 업데이트된 병합 정책의 세부 정보를 반환합니다.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## 병합 정책 삭제

병합 정책은 DELETE 요청을 수행하여 삭제할 수 있습니다 `/config/mergePolicies` 요청 경로에서 삭제할 병합 정책의 ID를 포함하여 끝점입니다.

>[!NOTE]
>
>병합 정책이 `isActiveOnEdge` true로 설정되고, 병합 정책 **사용할 수 없음** 삭제합니다. 다음 중 하나를 사용합니다 [PATCH](#edit-individual-merge-policy-fields) 또는 [PUT](#overwrite-a-merge-policy) 병합 정책을 삭제하기 전에 업데이트하기 위한 끝점입니다.

**API 형식**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 매개 변수 | 설명 |
|---|---|
| `{mergePolicyId}` | 삭제할 병합 정책의 식별자입니다. |

**요청**

다음 요청은 병합 정책을 삭제합니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

삭제 요청이 성공하면 HTTP 상태 200(OK) 및 빈 응답 본문을 반환합니다. 성공적으로 삭제를 확인하려면 GET 요청을 수행하여 해당 ID로 병합 정책을 볼 수 있습니다. 병합 정책이 삭제되면 HTTP 상태 404(찾을 수 없음) 오류가 표시됩니다.

## 다음 단계

조직에 대한 병합 정책을 만들고 구성하는 방법을 알고 있으므로 이 방법을 사용하여 플랫폼 내에서 고객 프로필 보기를 조정하고 [!DNL Real-Time Customer Profile] 데이터.

자세한 내용은 [Adobe Experience Platform 세그멘테이션 서비스 설명서](../../segmentation/home.md) 세그먼트 정의 및 작업을 시작합니다.
