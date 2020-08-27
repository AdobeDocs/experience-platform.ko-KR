---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 고객 세그먼트에 대한 데이터 사용 규정 준수
topic: tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---


# API를 사용하여 대상 세그먼트에 대한 데이터 사용 규정 준수

이 자습서에서는 API를 사용하여 대상 세그먼트에 대한 데이터 사용 규정 준수를 [!DNL Real-time Customer Profile] 적용하는 단계를 다룹니다.

## 시작하기

이 자습서에서는 다음의 구성 요소에 대해 작업해야 [!DNL Adobe Experience Platform]합니다.

- [[!DNL 실시간 고객 프로필]](../../profile/home.md): [!DNL Real-time Customer Profile] 은 범용 조회 엔티티 저장소이며, XDM( [!DNL Experience Data Model] Lookup Entity) 데이터를 관리하는 데 사용됩니다 [!DNL Platform]. 프로필은 다양한 엔터프라이즈 데이터 에셋에 있는 데이터를 병합하고 통합 프레젠테이션에서 해당 데이터에 액세스할 수 있도록 합니다.
   - [정책 병합](../../profile/api/merge-policies.md):특정 조건 [!DNL Real-time Customer Profile] 에서 통합 보기로 병합할 수 있는 데이터를 결정하는 데 사용되는 규칙입니다. 병합 정책은 [!DNL Data Governance] 목적에 따라 구성할 수 있습니다.
- [[!DNL 세그멘테이션]](../home.md):프로필 스토어에 포함된 대규모 개인 그룹을 비슷한 특성을 공유하고 마케팅 전략과 유사하게 반응하는 작은 그룹으로 나누는 방법 [!DNL Real-time Customer Profile] .
- [[!DNL 데이터 거버넌스]](../../data-governance/home.md): [!DNL Data Governance] 다음 구성 요소를 사용하여 데이터 사용 레이블 지정 및 실행(DULE)을 위한 인프라를 제공합니다.
   - [데이터 사용 레이블](../../data-governance/labels/user-guide.md):각 데이터를 처리하는 민감도 수준에서 데이터 세트와 필드를 설명하는 데 사용되는 레이블입니다.
   - [데이터 사용 정책](../../data-governance/policies/overview.md):특정 데이터 사용 레이블로 분류된 데이터에 허용되는 마케팅 작업을 나타내는 구성
   - [정책 실행](../../data-governance/enforcement/overview.md):데이터 사용 정책을 적용하고 정책 위반을 구성하는 데이터 작업을 방지할 수 있습니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 [!DNL Platform] 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 세그먼트 정의에 대한 병합 정책 검색 {#merge-policy}

이 워크플로우는 알려진 대상 세그먼트에 액세스하여 시작합니다. 에서 사용할 수 있는 세그먼트에는 세그먼트 정의 내에 [!DNL Real-time Customer Profile] 병합 정책 ID가 포함됩니다. 이 병합 정책에는 세그먼트에 포함할 데이터 집합에 대한 정보가 포함되며, 이 정보에는 적용 가능한 데이터 사용 레이블이 포함됩니다.

API를 사용하여 [!DNL Segmentation] ID로 세그먼트 정의를 검색하여 관련 병합 정책을 찾을 수 있습니다.

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

## 병합 정책에서 소스 데이터 집합 찾기 {#datasets}

병합 정책에는 소스 데이터 집합에 대한 정보가 포함되며, 여기에는 데이터 사용 레이블이 포함됩니다. GET 요청에서 병합 정책 ID를 API에 제공하여 병합 정책의 세부 사항을 조회할 수 [!DNL Profile] 있습니다. 병합 정책에 대한 자세한 내용은 [병합 정책 끝점 안내서를 참조하십시오](../../profile/api/merge-policies.md).

**API 형식**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | [이전 단계에서 얻은 병합 정책의 ID](#merge-policy). |

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
| `attributeMerge.type` | 병합 정책에 대한 데이터 우선 순위 구성 유형입니다. 이 값이 `dataSetPrecedence`이면 이 병합 정책에 연결된 데이터 집합이 아래에 나열됩니다 `attributeMerge > data > order`. 값이 이 `timestampOrdered`값이면, 에서 참조되는 스키마와 관련된 모든 데이터 집합 `schema.name` 이 병합 정책에 사용됩니다. |
| `attributeMerge.data.order` | 이 `attributeMerge.type` 경우 이 `dataSetPrecedence`속성은 이 병합 정책에 사용된 데이터 집합의 ID를 포함하는 배열입니다. 이러한 ID는 다음 단계에서 사용됩니다. |

## 데이터 세트에 정책 위반 평가

>[!NOTE]
>
> 이 단계에서는 특정 레이블을 포함하는 데이터에 대해 특정 마케팅 작업을 수행할 수 없도록 하는 활성 데이터 사용 정책이 하나 이상 있다고 가정합니다. 평가 중인 데이터 세트에 대해 적용 가능한 사용 정책이 없는 경우 [정책 작성 자습서에](../../data-governance/policies/create.md) 따라 하나를 만든 후 이 단계를 계속 진행하십시오.

병합 정책의 소스 데이터 집합의 ID를 얻은 후에는 [DULE Policy Service API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) 사용하여 데이터 사용 정책 위반을 확인하기 위해 특정 마케팅 작업에 대해 이러한 데이터 세트를 평가할 수 있습니다.

데이터 세트를 평가하려면 아래 예와 같이 요청 본문 내에 데이터 세트 ID를 제공하면서 POST 요청 경로에 마케팅 작업의 이름을 제공해야 합니다.

**API 형식**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 데이터 세트를 평가하는 데이터 사용 정책과 연결된 마케팅 작업의 이름. 정책이 Adobe에 의해 정의되었는지 또는 조직에 의해 정의되었는지 여부에 따라 각각 `/marketingActions/core` 또는 `/marketingActions/custom`를 사용해야 합니다. |

**요청**

다음 요청은 `exportToThirdParty` 이전 단계에서 얻은 데이터 세트에 대해 마케팅 작업을 테스트합니다 [](#datasets). 요청 페이로드가 각 데이터 집합의 ID를 포함하는 배열입니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| 속성 | 설명 |
| --- | --- |
| `entityType` | 페이로드 배열의 각 항목은 정의되는 엔티티 유형을 나타내야 합니다. 이 경우 값은 항상 &quot;dataSet&quot;입니다. |
| `entityID` | 페이로드 배열의 각 항목은 데이터 세트에 대한 고유 ID를 제공해야 합니다. |

**응답**

성공적인 응답은 마케팅 작업에 대한 URI, 제공된 데이터 세트에서 수집된 데이터 사용 레이블 및 해당 레이블에 대한 작업을 테스트한 결과 위반된 데이터 사용 정책 목록을 반환합니다. 이 예에서 &quot;데이터를 제3자로 내보내기&quot; 정책은 마케팅 작업이 정책 위반을 트리거했음을 나타내는 `violatedPolicies` 배열에 표시됩니다.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{IMS_ORG}",
  "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
  "duleLabels": [
    "C1",
    "C2",
    "C4",
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C2",
            ],
            "path": "/properties/_customer"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/geoUnit"
          },
          {
            "labels": [
              "C1"
            ],
            "path": "/properties/identityMap"
          }
        ]
      }
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/createdByBatchID"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/faxPhone"
          }
        ]
      }
    }
  ],
  "violatedPolicies": [
    {
      "name": "Export Data to Third Party",
      "status": "ENABLED",
      "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
      ],
      "description": "Conditions under which data cannot be exported to a third party",
      "deny": {
        "operator": "OR",
        "operands": [
          {
            "label": "C1"
          },
          {
            "operator": "AND",
            "operands": [
              {
                "label": "C3"
              },
              {
                "label": "C7"
              }
            ]
          }
        ]
      },
      "imsOrg": "{IMS_ORG}",
      "created": 1565651746693,
      "createdClient": "{CREATED_CLIENT}",
      "createdUser": "{CREATED_USER",
      "updated": 1565723012139,
      "updatedClient": "{UPDATED_CLIENT}",
      "updatedUser": "{UPDATED_USER}",
      "_links": {
        "self": {
          "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
      },
      "id": "5d51f322e553c814e67af1a3"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `duleLabels` | 제공된 데이터 세트에서 추출된 데이터 사용 레이블 목록입니다. |
| `discoveredLabels` | 요청 페이로드에서 제공된 데이터 세트 목록으로, 각 데이터세트에 있는 데이터 세트 수준 및 필드 수준 레이블을 표시합니다. |
| `violatedPolicies` | 제공된 항목에 대해 마케팅 작업(지정된)을 테스트하여 위반된 데이터 사용 정책 `marketingActionRef`을 나열하는 배열입니다 `duleLabels`. |

API 응답에서 반환되는 데이터를 사용하여 경험 애플리케이션 내에서 프로토콜을 설정하여 정책 위반이 발생할 때 적절하게 적용할 수 있습니다.

## 데이터 필드 필터링

대상 세그먼트가 평가를 통과하지 못하는 경우, 아래에 설명된 두 방법 중 하나를 통해 세그먼트에 포함된 데이터를 조정할 수 있습니다.

### 세그먼트 정의의 병합 정책 업데이트

세그먼트 정의의 병합 정책을 업데이트하면 세그먼트 작업이 실행될 때 포함할 데이터 세트와 필드가 조정됩니다. 자세한 내용은 API 병합 정책 자습서의 기존 병합 정책 [](../../profile/api/merge-policies.md#update) 업데이트 섹션을 참조하십시오.

### 세그먼트를 내보낼 때 특정 데이터 필드 제한

API를 사용하여 세그먼트를 데이터 세트에 내보낼 때 내보내기에 포함된 데이터를 [!DNL Segmentation] `fields` 매개 변수를 사용하여 필터링할 수 있습니다. 이 매개 변수에 추가된 모든 데이터 필드는 내보내기에 포함되지만 다른 모든 데이터 필드는 제외됩니다.

&quot;A&quot;, &quot;B&quot; 및 &quot;C&quot;라는 데이터 필드가 있는 세그먼트를 고려하십시오. &quot;C&quot; 필드만 내보내려면 매개 변수에 &quot;C&quot; 필드만 `fields` 포함됩니다. 이렇게 하면 세그먼트를 내보낼 때 &quot;A&quot; 및 &quot;B&quot; 필드가 제외됩니다.

자세한 내용은 [세그멘테이션 자습서의 세그먼트](./evaluate-a-segment.md#export) 내보내기에 대한 섹션을 참조하십시오.

## 다음 단계

이 튜토리얼을 따라 대상 세그먼트와 연관된 데이터 사용 레이블을 조회하고 특정 마케팅 작업에 대한 정책 위반을 테스트했습니다. 에 대한 자세한 내용 [!DNL Data Governance] 은 [!DNL Experience Platform][!DNL 데이터 거버넌스] [에 대한 개요를 읽어 보십시오](../../data-governance/home.md).
