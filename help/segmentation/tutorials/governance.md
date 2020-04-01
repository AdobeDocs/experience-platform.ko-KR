---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 고객 세그먼트에 대한 데이터 사용 규정 준수
topic: tutorial
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# API를 사용하여 대상 세그먼트에 대한 데이터 사용 규정 준수 적용

이 자습서에서는 API를 사용하여 실시간 고객 프로필 대상 세그먼트에 대한 데이터 사용 규정 준수를 적용하기 위한 단계를 설명합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [실시간 고객 프로필](../../profile/home.md):실시간 고객 프로필은 범용 조회 엔티티 스토어이며 플랫폼 내에서 XDM(Experience Data Model) 데이터를 관리하는 데 사용됩니다. 프로필은 다양한 엔터프라이즈 데이터 에셋에 데이터를 취합하여 통합 프레젠테이션에서 해당 데이터에 액세스할 수 있도록 합니다.
   - [정책 병합](../../profile/api/merge-policies.md):실시간 고객 프로필에서 특정 조건에서 통합 보기로 병합할 수 있는 데이터를 결정하기 위해 사용하는 규칙입니다. 데이터 거버넌스 용도로 병합 정책을 구성할 수 있습니다.
- [세그멘테이션](../home.md):실시간 고객 프로필은 프로필 스토어에 포함된 대규모 개인 그룹을 비슷한 트레이트를 공유하고 마케팅 전략과 유사하게 반응하는 작은 그룹으로 나누는 방법입니다.
- [데이터 거버넌스](../../data-governance/home.md):데이터 거버넌스는 다음 구성 요소를 사용하여 데이터 사용 레이블 지정 및 실행(DULE)을 위한 인프라를 제공합니다.
   - [데이터 사용 레이블](../../data-governance/labels/user-guide.md):각 데이터를 처리하는 민감도 수준 측면에서 데이터 세트와 필드를 설명하는 데 사용되는 레이블입니다.
   - [데이터 사용 정책](../../data-governance/api/getting-started.md):특정 데이터 사용 레이블로 분류된 데이터에 대해 허용되는 마케팅 작업을 나타내는 구성입니다.

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

> [!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 세그먼트 정의에 대한 병합 정책 조회

이 워크플로우는 알려진 대상 세그먼트에 액세스하여 시작합니다. 실시간 고객 프로필에서 사용할 수 있는 세그먼트에는 세그먼트 정의 내에 병합 정책 ID가 포함되어 있습니다. 이 병합 정책에는 세그먼트에 포함할 데이터 집합에 대한 정보가 포함되며, 여기에는 적용 가능한 데이터 사용 레이블이 포함됩니다.

세그멘테이션 [API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)사용하여 ID로 세그먼트 정의를 조회하여 연관된 병합 정책을 찾을 수 있습니다.

**API 형식**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 조회할 세그먼트 정의의 ID입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 세그먼트 정의의 세부 사항을 반환합니다.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
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
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `mergePolicyId` | 세그먼트 정의에 사용된 병합 정책의 ID입니다. 다음 단계에서 사용됩니다. |

## 병합 정책에서 원본 데이터 집합 찾기

병합 정책에는 소스 데이터 세트에 대한 정보가 포함되며, 여기에는 DULE 레이블이 포함됩니다. 프로필 API에 GET 요청에서 병합 정책 ID를 제공하여 병합 정책의 세부 사항을 조회할 수 있습니다.

**API 형식**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | [이전 단계에서](#lookup-a-merge-policy-for-a-segment-definition)얻은 병합 정책의 ID입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 병합 정책의 세부 사항을 반환합니다.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `schema.name` | 병합 정책과 연결된 스키마의 이름입니다. |
| `attributeMerge.type` | 병합 정책의 데이터 우선 순위 구성 유형입니다. 이 값이 `dataSetPrecedence`이면 이 병합 정책과 연결된 데이터 집합이 아래에 나열됩니다 `attributeMerge > data > order`. 이 값이 `timestampOrdered`이면 에서 참조되는 스키마와 연결된 모든 데이터 집합이 병합 정책에 `schema.name` 의해 사용됩니다. |
| `attributeMerge.data.order` | 이 `attributeMerge.type` 경우 이 `dataSetPrecedence`속성은 이 병합 정책에 사용된 데이터 집합의 ID를 포함하는 배열입니다. 이러한 ID는 다음 단계에서 사용됩니다. |

## 소스 데이터 집합에 대한 데이터 사용 레이블 조회

병합 정책의 소스 데이터 집합의 ID를 수집했으면 이러한 ID를 사용하여 데이터 집합 자체에 대해 구성된 데이터 사용 레이블 및 여기에 포함된 특정 데이터 필드를 조회할 수 있습니다.

Catalog Service API [에 대한](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) 다음 호출은 요청 경로에서 해당 ID를 제공하여 단일 데이터 집합과 연결된 데이터 사용 레이블을 검색합니다.

**API 형식**

```http
GET /dataSets/{DATASET_ID}/dule
```

| 속성 | 설명 |
| -------- | ----------- |
| `{DATASET_ID}` | 데이터 사용 레이블을 조회하려는 데이터 집합의 ID입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 집합 전체와 연결된 데이터 사용 레이블 목록 및 소스 스키마와 연결된 특정 데이터 필드를 반환합니다.

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `dataset` | 데이터 집합 전체에 적용된 데이터 사용 레이블이 들어 있는 개체입니다. |
| `schemaFields` | 데이터 사용 레이블이 적용된 특정 스키마 필드를 나타내는 개체의 배열입니다. |
| `schemaFields.path` | 데이터 사용 레이블이 동일한 개체에 나열되는 스키마 필드의 경로입니다. |

## 데이터 필드 필터링

> [!NOTE] 이 단계는 선택 사항입니다. 데이터 사용 레이블을 [찾는 이전 단계의 결과를 기반으로 세그먼트에 포함된 데이터를 조정하지 않으려면 정책 위반에](#lookup-data-usage-labels-for-the-source-datasets)대한 데이터를 [](#evaluate-data-for-policy-violations)평가하는 마지막 단계로 건너뛸 수 있습니다.

대상 세그먼트에 포함된 데이터를 조정하려면 다음 두 방법 중 하나를 사용하여 조정할 수 있습니다.

### 세그먼트 정의의 병합 정책 업데이트

세그먼트 정의의 병합 정책을 업데이트하면 세그먼트 작업이 실행될 때 포함할 데이터 세트와 필드가 조정됩니다. 자세한 내용은 병합 정책 자습서의 기존 병합 정책 [](../../profile/api/merge-policies.md) 업데이트에 대한 섹션을 참조하십시오.

### 세그먼트를 내보낼 때 특정 데이터 필드 제한

실시간 고객 프로필 API를 사용하여 세그먼트를 데이터 세트로 내보낼 때 `fields` 매개 변수를 사용하여 내보내기에 포함된 데이터를 필터링할 수 있습니다. 이 매개 변수에 추가된 모든 데이터 필드는 내보내기에 포함되는 반면 다른 모든 데이터 필드는 제외됩니다.

&quot;A&quot;, &quot;B&quot; 및 &quot;C&quot;라는 데이터 필드가 있는 세그먼트를 고려하십시오. &quot;C&quot; 필드만 내보내려면 매개 변수에 &quot;C&quot; 필드만 포함됩니다. `fields` 이렇게 하면 세그먼트를 내보낼 때 &quot;A&quot; 및 &quot;B&quot; 필드가 제외됩니다.

자세한 내용은 세그멘테이션 자습서의 세그먼트 [](./evaluate-a-segment.md#export-a-segment) 내보내기에 대한 섹션을 참조하십시오.

## 정책 위반에 대한 데이터 평가

이제 대상 세그먼트와 연관된 데이터 사용 레이블을 수집했으므로 마케팅 작업에 대해 이러한 레이블을 테스트하여 데이터 사용 정책 위반을 평가할 수 있습니다. DULE Policy Service API를 사용하여 정책 평가를 수행하는 [방법에](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)대한 자세한 내용은 [정책 평가에](../../data-governance/enforcement/overview.md)대한 문서를 참조하십시오.

## 다음 단계

이 자습서를 따라 대상 세그먼트와 연관된 데이터 사용 레이블을 조회하고 특정 마케팅 작업에 대한 정책 위반을 테스트했습니다. 경험 플랫폼의 데이터 거버넌스에 대한 자세한 내용은 데이터 거버넌스 [개요를](../../data-governance/home.md)참조하십시오.