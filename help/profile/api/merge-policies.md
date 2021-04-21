---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 병합 정책 API 끝점
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform을 사용하면 여러 소스에서 수집한 데이터 조각을 결합하여 개별 고객을 전체적으로 확인할 수 있습니다. 이러한 데이터를 취합할 때 병합 정책은 Platform에서 데이터의 우선 순위를 정하는 방법과 데이터를 결합하여 통합 뷰를 생성하는 데 사용하는 규칙입니다.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2560'
ht-degree: 1%

---

# 정책 병합 끝점

Adobe Experience Platform을 사용하면 여러 소스에서 수집한 데이터 조각을 결합하여 개별 고객을 전체적으로 확인할 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책은 데이터 우선 순위를 지정하는 방법과 통합 보기를 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다.[!DNL Platform]

예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직은 여러 데이터 세트에 나타나는 해당 단일 고객과 관련된 여러 프로필 조각을 갖게 됩니다. 이러한 조각을 Platform(플랫폼)으로 인제스트하면 해당 고객에 대한 단일 프로파일을 만들기 위해 병합됩니다. 여러 소스의 데이터가 충돌하면(예: 한 조각은 고객을 &quot;single&quot;로, 다른 조각은 고객을 &quot;기혼&quot;으로 나열합니다) 병합 정책은 각 개인에 대해 프로필에 포함할 정보를 결정합니다.

RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. 이 안내서에서는 API를 사용하여 병합 정책을 사용하는 단계를 제공합니다.

UI를 사용하여 병합 정책을 사용하려면 [병합 정책 UI 안내서](../ui/merge-policies.md)를 참조하십시오.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 병합 정책의 구성 요소 {#components-of-merge-policies}

병합 정책은 IMS 조직에 비공개입니다. 필요한 특정 방식으로 스키마를 병합하기 위해 다른 정책을 만들 수 있습니다. [!DNL Profile] 데이터에 액세스하는 모든 API에는 병합 정책이 필요하지만 명시적으로 제공되지 않은 경우에는 기본값이 사용됩니다. [!DNL Platform] 조직에 기본 병합 정책을 제공하거나 특정 XDM(Experience Data Model) 스키마 클래스에 대한 병합 정책을 만들어 조직의 기본값으로 표시할 수 있습니다.

각 조직에는 스키마 클래스당 여러 병합 정책이 있을 수 있지만 각 클래스는 하나의 기본 병합 정책만 가질 수 있습니다. 스키마 클래스의 이름을 제공하고 병합 정책이 필요하지만 제공되지 않는 경우 기본값으로 설정된 병합 정책이 사용됩니다.

>[!NOTE]
>
>새 병합 정책을 기본값으로 설정하면 이전에 기본값으로 설정된 기존 병합 정책이 자동으로 업데이트되어 더 이상 기본값으로 사용되지 않습니다.

### 전체 병합 정책 개체

전체 병합 정책 개체는 프로필 조각 병합의 측면을 제어하는 환경 설정 집합을 나타냅니다.

**정책 개체 병합**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
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
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| 속성 | 설명 |
|---|---|
| `id` | 생성 시 지정된 시스템에서 생성된 고유 식별자 |
| `name` | 목록 보기에서 병합 정책을 식별할 수 있는 친숙한 이름입니다. |
| `imsOrgId` | 이 병합 정책이 속하는 조직 ID |
| `identityGraph` | [관련 ](#identity-graph) ID를 받을 ID 그래프를 나타내는 ID 그래픽 프로젝트입니다. 모든 관련 ID에 대해 찾은 프로필 조각이 병합됩니다. |
| `attributeMerge` | [데이터 ](#attribute-merge) 충돌 시 병합 정책이 프로필 속성의 우선 순위를 지정하는 방법을 나타내는 속성 병합 객체입니다. |
| `schema.name` | [`schema`](#schema) 개체의 일부, `name` 필드에는 병합 정책이 관련된 XDM 스키마 클래스가 포함되어 있습니다. 스키마 및 클래스에 대한 자세한 내용은 [XDM 설명서](../../xdm/home.md)를 참조하십시오. |
| `default` | 이 병합 정책이 지정된 스키마의 기본값인지 여부를 나타내는 부울 값입니다. |
| `version` | [!DNL Platform] 병합 정책의 유지 관리 버전. 이 읽기 전용 값은 병합 정책이 업데이트될 때마다 증가합니다. |
| `updateEpoch` | 병합 정책의 마지막 업데이트 날짜. |

**병합 정책 예**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
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
        "default": true,
        "updateEpoch": 1551660639
    }
```

### ID 그래프 {#identity-graph}

[Adobe Experience Platform Identity ](../../identity-service/home.md) Services는 각 조직의 전역 및 각 조직에 사용되는 ID 그래프를 생성합니다 [!DNL Experience Platform]. 병합 정책의 `identityGraph` 속성은 사용자의 관련 ID를 결정하는 방법을 정의합니다.

**identityGraph 객체**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

여기서 `{IDENTITY_GRAPH_TYPE}`은(는) 다음 중 하나입니다.

* **&quot;none&quot;:ID** 스티칭을 수행하지 않습니다.
* **&quot;pdg&quot;:** 개인 ID 그래프를 기반으로 ID 스티칭을 수행합니다.

**예`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 특성 병합 {#attribute-merge}

프로필 조각은 특정 사용자에 대해 존재하는 ID 목록 중 하나의 ID에 대한 프로필 정보입니다. ID 그래프 유형이 사용되면 둘 이상의 ID가 있을 경우 프로필 속성이 충돌할 가능성이 있으며 우선 순위를 지정해야 합니다. `attributeMerge`을 사용하여 키 값(레코드 데이터) 유형 데이터 세트 간 병합 충돌이 발생하는 경우 우선 순위를 지정할 프로필 속성을 지정할 수 있습니다.

**attributeMerge 객체**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

여기서 `{ATTRIBUTE_MERGE_TYPE}`은(는) 다음 중 하나입니다.

* **`timestampOrdered`**:(기본값) 마지막으로 업데이트된 프로필에 우선 순위를 지정합니다. 이 병합 유형을 사용하면 `data` 속성이 필요하지 않습니다. `timestampOrdered` 또한 데이터 세트 내 또는 여러 데이터 세트에서 프로필 조각을 병합할 때 우선하는 사용자 지정 타임스탬프를 지원합니다. 자세한 내용은 사용자 지정 타임스탬프](#custom-timestamps)를 사용하여 [의 부록 섹션을 참조하십시오.
* **`dataSetPrecedence`** :프로필 조각을 원래 있던 데이터 세트에 따라 우선적으로 프로필 조각을 지정합니다. 한 데이터 세트에 있는 정보를 선호하거나 다른 데이터 세트에 있는 데이터를 통해 신뢰할 수 있는 경우에 사용할 수 있습니다. 이 병합 유형을 사용할 때는 우선 순위 순서로 데이터 세트를 나열하므로 `order` 속성이 필요합니다.
   * **`order`**:&quot;dataSetPriority&quot;를 사용하는 경우  `order` 데이터 집합 목록과 함께 배열을 제공해야 합니다. 목록에 포함되지 않은 데이터 세트는 병합되지 않습니다. 즉, 데이터 세트를 명시적으로 나열하여 프로필로 병합해야 합니다. `order` 배열은 우선 순위의 순서로 데이터 세트의 ID를 나열합니다.

#### `dataSetPrecedence` 유형을 사용하는 `attributeMerge` 개체 예

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### `timestampOrdered` 유형을 사용하는 `attributeMerge` 개체 예

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

여기서 `name` 값은 병합 정책과 연결된 스키마가 기반으로 하는 XDM 클래스의 이름입니다.

**예`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

XDM에 대한 자세한 내용과 Experience Platform의 스키마 작업을 보려면 [XDM 시스템 개요](../../xdm/home.md)를 읽으십시오.

## 병합 정책 액세스 {#access-merge-policies}

[!DNL Real-time Customer Profile] API를 사용하여 `/config/mergePolicies` 종단점을 사용하면 조회 요청을 수행하여 ID별로 특정 병합 정책을 보거나 특정 기준에 따라 필터링된 조직의 모든 병합 정책에 액세스할 수 있습니다. 또한 `/config/mergePolicies/bulk-get` 끝점을 사용하여 ID로 여러 병합 정책을 검색할 수도 있습니다. 이러한 각 호출을 수행하는 단계는 다음 섹션에 요약되어 있습니다.

### ID로 단일 병합 정책 액세스

요청 경로에 `/config/mergePolicies` 끝점과 `mergePolicyId`을 포함하여 ID로 단일 병합 정책에 액세스할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**응답**

성공적인 응답은 병합 정책의 세부 정보를 반환합니다.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
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
    "default": false,
    "updateEpoch": 1551127597
}
```

병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 [병합 정책 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.

### ID로 여러 병합 정책 검색

요청 본문에서 검색하려는 병합 정책의 ID를 포함하여 POST 요청을 `/config/mergePolicies/bulk-get` 끝점에 만들고 여러 병합 정책을 검색할 수 있습니다.

**API 형식**

```http
POST /config/mergePolicies/bulk-get
```

**요청**

요청 본문에는 세부 사항을 검색할 각 병합 정책에 대해 &quot;id&quot;가 포함된 개별 객체가 포함된 &quot;ids&quot; 배열이 포함되어 있습니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

성공적인 응답은 HTTP 상태 207(다중 상태) 및 POST 요청에 ID가 제공된 병합 정책의 세부 정보를 반환합니다.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
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
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
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
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 [병합 정책 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.

### 기준별로 여러 병합 정책을 나열합니다.

IMS 내에 여러 병합 정책을 나열할 수 있습니다. 조직은 `/config/mergePolicies` 끝점에 GET 요청을 전달하고 선택적 쿼리 매개 변수를 사용하여 응답을 필터링, 순서 지정 및 페이지로 설정합니다. 여러 매개 변수를 앰퍼샌드(&amp;)로 구분하여 포함할 수 있습니다. 매개 변수 없이 이 끝점을 호출하면 조직에 사용할 수 있는 모든 병합 정책을 검색합니다.

**API 형식**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
|---|---|
| `default` | 병합 정책이 스키마 클래스에 대한 기본값인지 여부를 기준으로 결과를 필터링하는 부울 값입니다. |
| `limit` | 페이지에 포함된 결과 수를 제어하기 위해 페이지 크기 제한을 지정합니다. 기본값:20년 |
| `orderBy` | 결과를 `orderBy=name` 또는 `orderBy=+name` 형식으로 정렬하여 오름차순으로 정렬하거나 `orderBy=-name` 내림차순으로 정렬할 필드를 지정합니다. 이 값을 생략하면 `name`의 기본 정렬이 오름차순으로 정렬됩니다. |
| `schema.name` | 사용 가능한 병합 정책을 검색할 스키마의 이름입니다. |
| `identityGraph.type` | ID 그래프 유형별로 결과를 필터링합니다. 가능한 값에는 &quot;none&quot; 및 &quot;pdg&quot;(비공개 그래프)가 포함됩니다. |
| `attributeMerge.type` | 사용된 특성 병합 유형별로 결과를 필터링합니다. 가능한 값에는 &quot;timestampOrdered&quot; 및 &quot;dataSetPriority&quot;가 포함됩니다. |
| `start` | 페이지 오프셋 - 검색할 데이터의 시작 ID를 지정합니다. 기본값:0 |
| `version` | 병합 정책의 특정 버전을 사용하려면 이 옵션을 지정합니다. 기본적으로 최신 버전이 사용됩니다. |

`schema.name`, `identityGraph.type` 및 `attributeMerge.type`에 대한 자세한 내용은 이 안내서의 앞에서 제공되는 병합 정책](#components-of-merge-policies) 섹션의 [구성 요소를 참조하십시오.


**요청**

다음 요청은 지정된 스키마에 대한 모든 병합 정책을 나열합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**응답**

성공적인 응답은 요청에 전송된 쿼리 매개 변수에 의해 지정된 기준을 충족하는 여러 페이지로 구분된 병합 정책 목록을 반환합니다.

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
            "imsOrgId": "{IMS_ORG}",
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
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
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
| `_links.next.href` | 다음 결과 페이지의 URI 주소입니다. 이 URI를 동일한 종단점에 대한 다른 API 호출에 대한 요청 매개 변수로 사용하여 페이지를 봅니다. 다음 페이지가 없는 경우 이 값은 빈 문자열이 됩니다. |

## 병합 정책 만들기

`/config/mergePolicies` 끝점에 POST 요청을 하여 조직에 대한 새 병합 정책을 만들 수 있습니다.

**API 형식**

```http
POST /config/mergePolicies
```

**요청다음**
요청은 페이로드에서 제공하는 속성 값으로 구성된 새 병합 정책을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| 속성 | 설명 |
|---|---|
| `name` | 목록 보기에서 병합 정책을 식별할 수 있는 사람 친화적인 이름입니다. |
| `identityGraph.type` | 병합할 관련 ID를 가져올 ID 그래프 유형입니다. 가능한 값:&quot;없음&quot; 또는 &quot;pdg&quot;(비공개 그래프) |
| `attributeMerge` | 데이터 충돌 시 프로필 속성 값의 우선 순위를 지정하는 방법입니다. |
| `schema` | 병합 정책과 연결된 XDM 스키마 클래스입니다. |
| `default` | 이 병합 정책이 스키마의 기본값인지 여부를 지정합니다. |

자세한 내용은 병합 정책의 [구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.

**응답**

성공적으로 응답하면 새로 만든 병합 정책의 세부 정보가 반환됩니다.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
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
    "default": true,
    "updateEpoch": 1551898378
}
```

병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 [병합 정책 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.

## 병합 정책 {#update} 업데이트

개별 특성(PATCH)을 편집하거나 전체 병합 정책을 새 특성(PUT)으로 덮어써서 기존 병합 정책을 수정할 수 있습니다. 각 예는 아래에 나와 있습니다.

### 개별 병합 정책 필드 편집

`/config/mergePolicies/{mergePolicyId}` 끝점에 PATCH 요청을 하여 병합 정책에 대한 개별 필드를 편집할 수 있습니다.

**API 형식**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 매개 변수 | 설명 |
|---|---|
| `{mergePolicyId}` | 삭제할 병합 정책의 식별자입니다. |

**요청**

다음 요청은 `default` 속성의 값을 `true`으로 변경하여 지정된 병합 정책을 업데이트합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `op` | 수행할 작업을 지정합니다. 다른 PATCH 작업의 예는 [JSON 패치 문서](http://jsonpatch.com)에서 찾을 수 있습니다. |
| `path` | 업데이트할 필드의 경로입니다. 허용된 값은 다음과 같습니다.&quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | 지정된 필드를 설정할 값입니다. |

자세한 내용은 병합 정책의 [구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.


**응답**

성공적으로 응답하면 새로 업데이트된 병합 정책의 세부 정보가 반환됩니다.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
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
    "default": true,
    "updateEpoch": 1551898378
}
```

### 병합 정책 덮어쓰기

병합 정책을 수정하는 또 다른 방법은 PUT 요청을 사용하여 전체 병합 정책을 덮어씁니다.

**API 형식**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 매개 변수 | 설명 |
|---|---|
| `{mergePolicyId}` | 덮어쓸 병합 정책의 식별자입니다. |

**요청**

다음 요청은 지정된 병합 정책을 덮어쓰고 속성 값을 페이로드에서 제공된 병합 정책으로 바꿉니다. 이 요청은 기존 병합 정책을 완전히 대체하므로 병합 정책을 처음 정의할 때 필요한 모든 필드를 제공해야 합니다. 그러나 이번에는 변경할 필드에 대한 업데이트된 값을 제공합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
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
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| 속성 | 설명 |
|---|---|
| `name` | 목록 보기에서 병합 정책을 식별할 수 있는 사람 친화적인 이름입니다. |
| `identityGraph` | 병합할 관련 ID를 가져올 ID 그래프입니다. |
| `attributeMerge` | 데이터 충돌 시 프로필 속성 값의 우선 순위를 지정하는 방법입니다. |
| `schema` | 병합 정책과 연결된 XDM 스키마 클래스입니다. |
| `default` | 이 병합 정책이 스키마의 기본값인지 여부를 지정합니다. |

자세한 내용은 병합 정책의 [구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.


**응답**

성공적인 응답은 업데이트된 병합 정책의 세부 정보를 반환합니다.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
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
    "default": true,
    "updateEpoch": 1551898378
}
```

## 병합 정책 삭제

병합 정책은 요청 경로에서 삭제할 병합 정책의 ID를 포함하여 `/config/mergePolicies` 끝점에 DELETE 요청을 함으로써 삭제할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

삭제 요청이 성공하면 HTTP 상태 200(OK) 및 빈 응답 본문을 반환합니다. 삭제에 성공했는지 확인하려면 GET 요청을 수행하여 병합 정책을 ID로 볼 수 있습니다. 병합 정책이 삭제되면 HTTP 상태 404(찾을 수 없음) 오류가 표시됩니다.

## 다음 단계

조직의 병합 정책을 만들고 구성하는 방법을 알고 있으므로 이러한 정책을 사용하여 플랫폼 내의 고객 프로필 보기를 조정하고 [!DNL Real-time Customer Profile] 데이터에서 대상 세그먼트를 만들 수 있습니다. 세그먼트 정의 및 작업을 시작하려면 [Adobe Experience Platform 세그멘테이션 서비스 설명서](../../segmentation/home.md)를 참조하십시오.

## 부록

이 섹션에서는 병합 정책 작업과 관련된 추가 정보를 제공합니다.

### 사용자 지정 타임스탬프 사용 {#custom-timestamps}

레코드가 Experience Platform에 수집되면 수집 시 시스템 타임스탬프를 가져와 레코드에 추가합니다. 병합 정책의 `attributeMerge` 유형으로 `timestampOrdered`을 선택하면 시스템 타임스탬프를 기반으로 프로필이 병합됩니다. 즉, 병합은 레코드를 Platform으로 인제스트한 시간에 대한 타임스탬프를 기반으로 수행됩니다.

때때로 레코드를 주문하지 않으면 데이터를 채우거나 올바른 이벤트 순서를 유지하는 등 사용자 지정 타임스탬프를 제공하고 병합 정책이 시스템 타임스탬프가 아닌 사용자 지정 타임스탬프를 준수하도록 하는 등의 사용 사례가 있을 수 있습니다.

사용자 지정 타임스탬프를 사용하려면 [[!DNL External Source System Audit Details Mixin]](#mixin-details)을(를) 프로필 스키마에 추가해야 합니다. 사용자 지정 타임스탬프가 추가되면 `xdm:lastUpdatedDate` 필드를 사용하여 채울 수 있습니다. 레코드를 `xdm:lastUpdatedDate` 필드가 채워진 상태로 인제스트할 때 Experience Platform은 해당 필드를 사용하여 데이터 집합 내 및 데이터 집합 간에 레코드 또는 프로필 조각을 병합합니다. `xdm:lastUpdatedDate`이(가) 없거나 채워지지 않으면 플랫폼에서는 시스템 타임스탬프를 계속 사용합니다.

>[!NOTE]
>
>동일한 레코드에 PATCH을 보낼 때 `xdm:lastUpdatedDate` 타임스탬프가 채워졌는지 확인해야 합니다.

스키마에 믹스를 추가하는 방법을 비롯하여 스키마 레지스트리 API를 사용하여 스키마 작업에 대한 단계별 지침을 보려면 [튜토리얼에서 API](../../xdm/tutorials/create-schema-api.md)을 사용하여 스키마를 만드는 방법을 참조하십시오.

UI를 사용하여 사용자 지정 타임스탬프를 사용하려면 [병합 정책 사용자 안내서](../ui/merge-policies.md)의 [사용자 지정 타임스탬프](../ui/merge-policies.md#custom-timestamps)에 있는 섹션을 참조하십시오.

#### [!DNL External Source System Audit Details Mixin] 세부 정보  {#mixin-details}

다음 예제는 [!DNL External Source System Audit Details Mixin]에서 채워진 필드를 보여줍니다. 전체 믹싱 JSON은 GitHub의 [공개 경험 데이터 모델(XDM) 보고서](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json)에서도 볼 수 있습니다.

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```
