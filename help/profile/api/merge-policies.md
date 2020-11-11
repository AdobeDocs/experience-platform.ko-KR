---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 정책 병합 - 실시간 고객 프로필 API
topic: guide
translation-type: tm+mt
source-git-commit: 6bfc256b50542e88e28f8a0c40cec7a109a05aa6
workflow-type: tm+mt
source-wordcount: '2494'
ht-degree: 1%

---


# 정책 병합 끝점

Adobe Experience Platform을 사용하면 여러 소스에서 수집한 데이터 조각을 취합하여 각 개별 고객에 대한 전체 상황을 파악할 수 있습니다. 이 데이터를 취합할 때 병합 정책은 데이터의 우선 순위를 매기는 방법과 데이터를 결합하여 통합 뷰를 생성하는 데 [!DNL Platform] 사용하는 규칙입니다.

예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직은 단일 고객과 관련된 여러 프로필 조각을 여러 데이터 세트에 표시할 수 있습니다. 이러한 조각을 Platform(플랫폼)으로 인제스트하면 해당 고객에 대한 단일 프로파일을 만들기 위해 병합됩니다. 여러 소스의 데이터가 충돌하는 경우(예: 한 조각은 고객을 &quot;single&quot;로 나열하고 다른 조각은 고객을 &quot;기혼&quot;으로 나열합니다) 병합 정책에 따라 각 개인에 대한 프로필에 포함할 정보가 결정됩니다.

RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. 이 안내서에서는 API를 사용하여 병합 정책을 사용하는 단계를 제공합니다.

UI를 사용하여 병합 정책을 사용하려면 [병합 정책 사용 안내서를 참조하십시오](../ui/merge-policies.md).

## 시작하기

이 안내서에서 사용되는 API 끝점은 이 끝점의 일부입니다 [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). 계속하기 전에 [시작하기 가이드](getting-started.md) 에서 관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오 [!DNL Experience Platform] .

## 병합 정책의 구성 요소 {#components-of-merge-policies}

병합 정책은 IMS 조직에 대한 개인 정책이므로 필요한 특정 방식으로 스키마를 병합하기 위해 다른 정책을 만들 수 있습니다. 데이터에 액세스하는 모든 API는 병합 정책을 필요로 하지만, 기본값이 명시적으로 제공되지 않으면 사용됩니다. [!DNL Profile] [!DNL Platform] 조직에 기본 병합 정책을 제공하거나 특정 XDM(Experience Data Model) 스키마 클래스에 대한 병합 정책을 만들어 조직의 기본값으로 표시할 수 있습니다.

각 조직에는 스키마 클래스당 여러 개의 병합 정책이 있을 수 있지만 각 클래스에는 하나의 기본 병합 정책만 있을 수 있습니다. 스키마 클래스의 이름이 제공되고 병합 정책이 필요하지만 제공되지 않는 경우 기본값으로 설정된 병합 정책이 사용됩니다.

>[!NOTE]
>
>새 병합 정책을 기본값으로 설정하면 이전에 기본값으로 설정된 기존 병합 정책이 더 이상 기본값으로 사용되지 않도록 자동으로 업데이트됩니다.

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
| `identityGraph` | [관련 ID를 얻을 ID 그래프를 나타내는 ID 그래프](#identity-graph) 개체 모든 관련 ID에 대해 찾은 프로필 조각이 병합됩니다. |
| `attributeMerge` | [데이터 충돌 시 병합 정책이 프로필 속성의 우선 순위를 지정하는 방법을 나타내는 속성 병합](#attribute-merge) 개체입니다. |
| `schema.name` | 개체 [`schema`](#schema) 의 일부, `name` 필드에는 병합 정책이 관련된 XDM 스키마 클래스가 들어 있습니다. 스키마 및 클래스에 대한 자세한 내용은 [XDM 설명서를 참조하십시오](../../xdm/home.md). |
| `default` | 이 병합 정책이 지정된 스키마의 기본값인지 여부를 나타내는 부울 값입니다. |
| `version` | [!DNL Platform] 병합 정책을 유지 관리합니다. 이 읽기 전용 값은 병합 정책이 업데이트될 때마다 증가합니다. |
| `updateEpoch` | 병합 정책에 대한 마지막 업데이트 날짜 |

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

[Adobe Experience Platform ID 서비스](../../identity-service/home.md) (Facebook Identity Service)는 전역적으로 및 각 조직에 사용되는 ID 그래프를 관리합니다 [!DNL Experience Platform]. 병합 정책의 `identityGraph` 속성은 사용자의 관련 ID를 결정하는 방법을 정의합니다.

**identityGraph 객체**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

다음 `{IDENTITY_GRAPH_TYPE}` 중 하나가 어디입니까?

* **&quot;none&quot;:** ID를 결합하지 않습니다.
* **&quot;pdg&quot;:** 개인 ID 그래프를 기반으로 ID 스티칭을 수행합니다.

**예`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 속성 병합 {#attribute-merge}

프로필 조각은 특정 사용자에 대해 존재하는 ID 목록 중 하나의 ID에 대한 프로필 정보입니다. ID 그래프 유형이 사용한 경우 둘 이상의 ID가 있을 경우 충돌하는 프로필 속성과 우선 순위를 지정해야 합니다. 를 `attributeMerge`사용하면 키 값(레코드 데이터) 형식 데이터 집합 간에 병합이 충돌할 경우 우선 순위를 지정할 프로필 속성을 지정할 수 있습니다.

**attributeMerge 개체**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

다음 `{ATTRIBUTE_MERGE_TYPE}` 중 하나가 어디입니까?

* **`timestampOrdered`**:(기본값) 마지막으로 업데이트된 프로필에 우선 순위를 지정합니다. 이 병합 유형을 사용하면 속성이 `data` 필요하지 않습니다. `timestampOrdered` 또한 데이터 세트 내 또는 데이터 세트 간에 프로필 조각을 병합할 때 우선하는 사용자 지정 타임스탬프를 지원합니다. 자세한 내용은 사용자 지정 타임스탬프 [사용에 대한 부록 섹션을 참조하십시오](#custom-timestamps).
* **`dataSetPrecedence`** :프로필 조각을 원래 있던 데이터 세트에 따라 우선 순위를 지정합니다. 한 데이터 세트에 있는 정보가 다른 데이터 세트에 있는 데이터를 통해 선호되거나 신뢰할 수 있는 경우 이 기능을 사용할 수 있습니다. 이 병합 유형을 사용하는 경우 우선 순위 순서로 데이터 세트를 나열하므로 `order` 속성이 필요합니다.
   * **`order`**:&quot;dataSetPriority&quot;를 사용하는 경우 데이터 집합 목록과 함께 `order` 배열을 제공해야 합니다. 목록에 포함되지 않은 데이터 세트는 병합되지 않습니다. 즉, 데이터 세트를 명시적으로 나열하여 프로필로 병합해야 합니다. 이 `order` 배열에는 데이터 집합의 ID가 우선 순위 순서로 나열됩니다.

#### 유형을 사용하는 `attributeMerge` 예제 `dataSetPrecedence` 개체

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

#### 유형을 사용하는 `attributeMerge` 예제 `timestampOrdered` 개체

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 스키마 {#schema}

스키마 개체는 이 병합 정책을 만드는 XDM(Experience Data Model) 스키마 클래스를 지정합니다.

**`schema`개체**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

여기서 값 `name` 은 병합 정책과 연관된 스키마가 기반으로 하는 XDM 클래스의 이름입니다.

**예`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

XDM 및 Experience Platform의 스키마 작업에 대한 자세한 내용은 [XDM 시스템 개요를 읽어 보시기 바랍니다](../../xdm/home.md).

## 병합 정책 액세스 {#access-merge-policies}

API를 사용하여 [!DNL Real-time Customer Profile] 종단점을 통해 `/config/mergePolicies` 조회 요청을 수행하여 ID로 특정 병합 정책을 보거나 특정 기준에 따라 필터링된 IMS 조직의 모든 병합 정책에 액세스할 수 있습니다. 끝점을 사용하여 ID로 여러 병합 정책을 검색할 수도 있습니다. `/config/mergePolicies/bulk-get` 이러한 각 호출을 수행하는 단계는 다음 섹션에 요약되어 있습니다.

### ID로 단일 병합 정책 액세스

종단점에 GET 요청을 수행하고 요청 경로에 해당 정책을 포함하여 ID로 단일 병합 정책 `/config/mergePolicies` `mergePolicyId` 에 액세스할 수 있습니다.

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

성공적인 응답은 병합 정책의 세부 사항을 반환합니다.

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

병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 병합 정책 [](#components-of-merge-policies) 구성 요소를 참조하십시오.

### ID로 여러 병합 정책 검색

종단점에 POST 요청을 만들고 요청 본문에 검색할 병합 정책의 ID를 포함하여 여러 병합 정책을 검색할 수 있습니다. `/config/mergePolicies/bulk-get`

**API 형식**

```http
POST /config/mergePolicies/bulk-get
```

**요청**

요청 본문에는 세부 사항을 검색할 각 병합 정책에 대해 &quot;id&quot;가 포함된 개별 개체가 있는 &quot;ids&quot; 배열이 포함됩니다.

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

성공적인 응답은 HTTP 상태 207(다중 상태)과 POST 요청에 ID가 제공된 병합 정책의 세부 정보를 반환합니다.

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

병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 병합 정책 [](#components-of-merge-policies) 구성 요소를 참조하십시오.

### 기준별로 여러 병합 정책 목록 지정

IMS 내에 여러 병합 정책을 나열할 수 있습니다. 조직에 GET 요청을 보내고 선택적 쿼리 매개 변수를 사용하여 응답을 필터링, 순서 지정 및 게시합니다. `/config/mergePolicies` 여러 매개 변수를 앰퍼샌드(&amp;)로 구분하여 포함할 수 있습니다. 매개 변수가 없는 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 병합 정책을 검색합니다.

**API 형식**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
|---|---|
| `default` | 병합 정책이 스키마 클래스에 대한 기본값인지 여부에 따라 필터링하는 부울 값입니다. |
| `limit` | 페이지에 포함된 결과 수를 제어하기 위해 페이지 크기 제한을 지정합니다. 기본값:20년 |
| `orderBy` | 결과를 오름차순으로 정렬하거나 이름을 기준으로 정렬하거나 내림차순으로 정렬하는 `orderBy=name` 필드 `orderBy=+name` 를 `orderBy=-name`지정합니다. 이 값을 생략하면 기본적으로 오름차순 `name` 으로 정렬됩니다. |
| `schema.name` | 사용 가능한 병합 정책을 검색할 스키마의 이름입니다. |
| `identityGraph.type` | ID 그래프 유형별로 결과를 필터링합니다. 가능한 값에는 &quot;none&quot; 및 &quot;pdg&quot;(비공개 그래프)가 포함됩니다. |
| `attributeMerge.type` | 사용된 속성 병합 유형별로 결과를 필터링합니다. 가능한 값에는 &quot;timestampOrdered&quot; 및 &quot;dataSetPriority&quot;가 포함됩니다. |
| `start` | 페이지 오프셋 - 데이터를 검색할 시작 ID를 지정합니다. 기본값:0 |
| `version` | 병합 정책의 특정 버전을 사용하려는 경우 이를 지정합니다. 기본적으로 최신 버전이 사용됩니다. |

병합 정책 `schema.name`, `identityGraph.type`및 `attributeMerge.type`에 대한 자세한 내용은 이 안내서 [에서 제공하는 병합 정책](#components-of-merge-policies) 구성 요소를 참조하십시오.


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

성공적인 응답은 요청에 전송된 쿼리 매개 변수에 의해 지정된 기준을 충족하는 병합 정책의 페이지 지정 목록을 반환합니다.

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
| `_links.next.href` | 결과 다음 페이지의 URI 주소입니다. 이 URI를 동일한 끝점에 대한 다른 API 호출에 대한 요청 매개 변수로 사용하여 페이지를 봅니다. 다음 페이지가 없는 경우 이 값은 빈 문자열이 됩니다. |

## 병합 정책 만들기

종단점에 POST 요청을 만들어 조직에 대한 새 병합 정책을 만들 수 `/config/mergePolicies` 있습니다.

**API 형식**

```http
POST /config/mergePolicies
```

**요청**&#x200B;다음 요청은 페이로드에서 제공하는 속성 값으로 구성된 새 병합 정책을 만듭니다.

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
| `name` | 목록 보기에서 병합 정책을 식별할 수 있는 친숙한 이름입니다. |
| `identityGraph.type` | 병합할 관련 ID를 가져올 ID 그래프 유형입니다. 가능한 값:&quot;none&quot; 또는 &quot;pdg&quot;(비공개 그래프) |
| `attributeMerge` | 데이터 충돌 시 프로필 속성 값의 우선 순위를 지정하는 방식입니다. |
| `schema` | 병합 정책과 연결된 XDM 스키마 클래스입니다. |
| `default` | 이 병합 정책이 스키마의 기본값인지 여부를 지정합니다. |

자세한 내용은 병합 정책 [의 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.

**응답**

성공적인 응답은 새로 만든 병합 정책의 세부 사항을 반환합니다.

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

병합 정책을 구성하는 각 개별 요소에 대한 자세한 내용은 이 문서의 시작 부분에 있는 병합 정책 [](#components-of-merge-policies) 구성 요소를 참조하십시오.

## 병합 정책 업데이트 {#update}

개별 속성(PATCH)을 편집하거나 새 특성(PUT)으로 전체 병합 정책을 덮어써서 기존 병합 정책을 수정할 수 있습니다. 각 예는 아래에 나와 있습니다.

### 개별 병합 정책 필드 편집

종단점에 PATCH 요청을 만들어 병합 정책에 대한 개별 필드를 편집할 수 `/config/mergePolicies/{mergePolicyId}` 있습니다.

**API 형식**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 매개 변수 | 설명 |
|---|---|
| `{mergePolicyId}` | 삭제할 병합 정책의 식별자입니다. |

**요청**

다음 요청은 속성 값을 변경하여 지정된 병합 정책을 `default` 업데이트합니다 `true`.

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
| `op` | 수행할 작업을 지정합니다. 다른 PATCH 작업의 예는 [JSON 패치 문서에서 확인할 수 있습니다.](http://jsonpatch.com) |
| `path` | 업데이트할 필드의 경로입니다. 허용된 값은 다음과 같습니다.&quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | 지정된 필드를 설정할 값입니다. |

자세한 내용은 병합 정책 [의 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.


**응답**

성공적인 응답은 새로 업데이트된 병합 정책의 세부 사항을 반환합니다.

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

다음 요청은 지정한 병합 정책을 덮어쓰고 속성 값을 페이로드에서 제공된 정책으로 대체합니다. 이 요청은 기존 병합 정책을 완전히 대체하므로 병합 정책을 처음 정의할 때 필요한 모든 동일한 필드를 제공해야 합니다. 하지만 이번에는 변경할 필드에 대한 업데이트된 값을 제공합니다.

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
| `name` | 목록 보기에서 병합 정책을 식별할 수 있는 친숙한 이름입니다. |
| `identityGraph` | 병합할 관련 ID를 가져올 ID 그래프입니다. |
| `attributeMerge` | 데이터 충돌 시 프로필 속성 값의 우선 순위를 지정하는 방식입니다. |
| `schema` | 병합 정책과 연결된 XDM 스키마 클래스입니다. |
| `default` | 이 병합 정책이 스키마의 기본값인지 여부를 지정합니다. |

자세한 내용은 병합 정책 [의 구성 요소](#components-of-merge-policies) 섹션을 참조하십시오.


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

종단점에 DELETE 요청을 만들고 요청 경로에서 삭제하려는 병합 정책의 ID를 포함하여 병합 정책을 삭제할 수 있습니다. `/config/mergePolicies`

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

삭제 요청이 성공하면 HTTP 상태 200(OK) 및 빈 응답 본문을 반환합니다. 삭제에 성공했는지 확인하려면 GET 요청을 수행하여 병합 정책을 ID로 볼 수 있습니다. 병합 정책을 삭제하면 HTTP 상태 404(찾을 수 없음) 오류가 표시됩니다.

## 다음 단계

조직의 병합 정책을 만들고 구성하는 방법을 알고 있으므로 이러한 정책을 사용하여 플랫폼 내에서 고객 프로필 보기를 조정하고 데이터를 통해 고객 세그먼트를 만들 수 [!DNL Real-time Customer Profile] 있습니다. 세그먼트 정의 및 작업을 시작하려면 [Adobe Experience Platform 세그멘테이션 서비스 설명서를](../../segmentation/home.md) 참조하십시오.

## 부록

이 섹션에서는 병합 정책을 사용한 작업과 관련된 보충 정보를 제공합니다.

### 사용자 지정 타임스탬프 사용 {#custom-timestamps}

레코드가 Experience Platform으로 수집되면 수집 시 시스템 타임스탬프를 획득하여 레코드에 추가됩니다. 병합 정책 `timestampOrdered` 의 `attributeMerge` 유형으로 선택하면 시스템 타임스탬프를 기반으로 프로필이 병합됩니다. 즉, 레코드를 플랫폼으로 인제스트한 때의 타임스탬프를 기반으로 병합이 수행됩니다.

사용자 지정 타임스탬프를 제공하고 병합 정책이 시스템 타임스탬프가 아닌 사용자 지정 타임스탬프를 준수하도록 하는 경우, 레코드를 순서가 맞지 않는 경우 데이터 채우기 또는 올바른 이벤트 순서 확인과 같은 사용 사례가 있을 수 있습니다.

사용자 지정 타임스탬프를 사용하려면 프로필 스키마에 해당 타임스탬프를 추가해야 [[!DNL External Source System Audit Details Mixin]](#mixin-details) 합니다. 사용자 지정 타임스탬프가 추가되면 `xdm:lastUpdatedDate` 필드를 사용하여 채울 수 있습니다. 레코드가 채워지는 `xdm:lastUpdatedDate` 필드를 사용하여 수집되면 Experience Platform은 해당 필드를 사용하여 데이터 집합 내 및 전체의 레코드 또는 프로필 조각을 병합합니다. If `xdm:lastUpdatedDate` is not present, or not pliced, will continue to use the system timestamp.

>[!NOTE]
>
>같은 레코드에서 PATCH을 보낼 때 타임스탬프가 `xdm:lastUpdatedDate` 채워지는지 확인해야 합니다.

스키마 레지스트리 API를 사용하여 스키마를 사용하는 방법에 대한 단계별 지침을 보려면 API를 사용하여 스키마를 만드는 방법을 [튜토리얼을 참조하십시오](../../xdm/tutorials/create-schema-api.md).

UI를 사용하여 사용자 지정 타임스탬프를 사용하려면 [병합 정책 사용자 안내서의 사용자 지정 타임스탬프](../ui/merge-policies.md#custom-timestamps) 사용 섹션을 참조하십시오 [](../ui/merge-policies.md).

#### [!DNL External Source System Audit Details Mixin] 세부 정보 {#mixin-details}

다음 예제는 [!DNL External Source System Audit Details Mixin] 전체 믹싱 JSON은 GitHub의 [XDM(Public Experience Data Model)에서도 볼](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json) 수 있습니다.

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




