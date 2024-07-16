---
solution: Experience Platform
title: API를 사용하여 대상 세그먼트에 데이터 사용 규정 준수 적용
type: Tutorial
description: 이 튜토리얼에서는 API를 사용하여 데이터 사용 준수 세그먼트 정의를 적용하는 단계를 다룹니다.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 6%

---

# API를 사용하여 세그먼트 정의에 데이터 사용 규정 준수 적용

이 튜토리얼에서는 API를 사용하여 세그먼트 정의에 대한 데이터 사용 규정 준수를 적용하는 단계를 다룹니다.

## 시작하기

이 자습서에서는 [!DNL Adobe Experience Platform]의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile]은(는) 제네릭 조회 엔터티 저장소이며 [!DNL Platform] 내의 [!DNL Experience Data Model (XDM)] 데이터를 관리하는 데 사용됩니다. 프로필은 다양한 엔터프라이즈 데이터 에셋에서 데이터를 병합하고 통합 프레젠테이션의 해당 데이터에 대한 액세스를 제공합니다.
   - [병합 정책](../../profile/api/merge-policies.md): 특정 조건에서 통합 보기에 병합할 수 있는 데이터를 결정하기 위해 [!DNL Real-Time Customer Profile]에서 사용하는 규칙입니다. 데이터 거버넌스 목적을 위해 병합 정책을 구성할 수 있습니다.
- [[!DNL Segmentation]](../home.md): [!DNL Real-Time Customer Profile]이(가) 프로필 스토어에 포함된 큰 개인 그룹을 유사한 트레이트를 공유하고 마케팅 전략에 유사하게 반응하는 작은 그룹으로 나누는 방법입니다.
- [데이터 거버넌스](../../data-governance/home.md): 데이터 거버넌스는 다음 구성 요소를 사용하여 데이터 사용 레이블 지정 및 적용을 위한 인프라를 제공합니다.
   - [데이터 사용 레이블](../../data-governance/labels/user-guide.md): 각 데이터를 처리하는 민감도 수준으로 데이터 세트와 필드를 설명하는 데 사용되는 레이블입니다.
   - [데이터 사용 정책](../../data-governance/policies/overview.md): 특정 데이터 사용 레이블로 분류된 데이터에 대해 허용되는 마케팅 작업을 나타내는 구성
   - [정책 적용](../../data-governance/enforcement/overview.md): 데이터 사용 정책을 적용하고 정책 위반을 구성하는 데이터 작업을 방지할 수 있습니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Platform] API를 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

## 세그먼트 정의에 대한 병합 정책 조회 {#merge-policy}

이 워크플로우는 알려진 세그먼트 정의에 액세스함으로써 시작됩니다. [!DNL Real-Time Customer Profile]에서 사용할 수 있도록 설정된 세그먼트 정의에 해당 세그먼트 정의 내에 병합 정책 ID가 포함되어 있습니다. 이 병합 정책에는 세그먼트 정의에 포함될 데이터 세트에 대한 정보가 포함되어 있으며 해당 데이터 사용 레이블이 포함됩니다.

[!DNL Segmentation] API를 사용하면 해당 ID로 세그먼트 정의를 조회하여 연결된 병합 정책을 찾을 수 있습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 세그먼트 정의의 세부 정보를 반환합니다.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{ORG_ID}",
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
| `mergePolicyId` | 세그먼트 정의에 사용되는 병합 정책의 ID입니다. 이 값은 다음 단계에서 사용됩니다. |

## 병합 정책에서 소스 데이터 세트 찾기 {#datasets}

병합 정책에는 소스 데이터 세트에 대한 정보가 포함되며 이 정보에는 데이터 사용 레이블이 포함됩니다. [!DNL Profile] API에 대한 GET 요청에 병합 정책 ID를 제공하여 병합 정책의 세부 정보를 조회할 수 있습니다. 병합 정책에 대한 자세한 내용은 [병합 정책 끝점 안내서](../../profile/api/merge-policies.md)를 참조하십시오.

**API 형식**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | [이전 단계](#merge-policy)에서 얻은 병합 정책의 ID입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 병합 정책의 세부 정보를 반환합니다.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
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
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `schema.name` | 병합 정책과 연결된 스키마의 이름입니다. |
| `attributeMerge.type` | 병합 정책에 대한 데이터 우선 순위 구성 유형입니다. 값이 `dataSetPrecedence`이면 이 병합 정책과 연결된 데이터 세트가 `attributeMerge > data > order` 아래에 나열됩니다. 값이 `timestampOrdered`이면 `schema.name`에서 참조된 스키마와 연결된 모든 데이터 세트가 병합 정책에 사용됩니다. |
| `attributeMerge.data.order` | `attributeMerge.type`이(가) `dataSetPrecedence`인 경우 이 특성은 이 병합 정책에 사용되는 데이터 세트의 ID를 포함하는 배열입니다. 이러한 ID는 다음 단계에서 사용됩니다. |

## 정책 위반에 대한 데이터 세트 평가

>[!NOTE]
>
> 이 단계에서는 특정 레이블이 포함된 데이터에 대해 특정 마케팅 작업을 수행할 수 없도록 하는 활성 데이터 사용 정책이 하나 이상 있다고 가정합니다. 평가 중인 데이터 세트에 적용 가능한 사용 정책이 없는 경우 [정책 만들기 자습서](../../data-governance/policies/create.md)에 따라 한 개를 만든 후 이 단계를 계속하십시오.

병합 정책의 원본 데이터 세트의 ID를 얻으면 [정책 서비스 API](https://www.adobe.io/experience-platform-apis/references/policy-service/)를 사용하여 특정 마케팅 작업에 대해 해당 데이터 세트를 평가하여 데이터 사용 정책 위반을 확인할 수 있습니다.

데이터 세트를 평가하려면 아래 예와 같이 POST 본문 내에 데이터 세트 ID를 제공하면서 요청 경로에 마케팅 작업의 이름을 제공해야 합니다.

**API 형식**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 매개변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 평가 중인 데이터 세트 사용 정책과 연관된 마케팅 액션의 이름입니다. 정책이 Adobe 또는 조직에서 정의되었는지 여부에 따라 각각 `/marketingActions/core` 또는 `/marketingActions/custom`을(를) 사용해야 합니다. |

**요청**

다음 요청은 [이전 단계](#datasets)에서 가져온 데이터 세트에 대해 `exportToThirdParty` 마케팅 작업을 테스트합니다. 요청 페이로드는 각 데이터 세트의 ID를 포함하는 배열입니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | 페이로드 배열의 각 항목은 정의할 엔티티 유형을 나타내야 합니다. 이 사용 사례의 경우 값은 항상 &quot;dataSet&quot;입니다. |
| `entityID` | 페이로드 배열의 각 항목은 데이터 세트에 대한 고유 ID를 제공해야 합니다. |

**응답**

성공적인 응답은 마케팅 작업에 대한 URI, 제공된 데이터 세트에서 수집된 데이터 사용 레이블 및 해당 레이블에 대해 작업을 테스트한 결과 위반된 데이터 사용 정책 목록을 반환합니다. 이 예제에서는 마케팅 작업이 정책 위반을 트리거했음을 나타내는 &quot;데이터를 서드파티로 내보내기&quot; 정책이 `violatedPolicies` 배열에 표시됩니다.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
| `discoveredLabels` | 요청 페이로드에 제공된 데이터 세트 목록으로, 각 페이로드에서 찾은 데이터 세트 수준 및 필드 수준 레이블을 표시합니다. |
| `violatedPolicies` | 제공된 `duleLabels`에 대해 마케팅 작업(`marketingActionRef`에 지정됨)을 테스트하여 위반된 데이터 사용 정책을 나열하는 배열입니다. |

API 응답에서 반환된 데이터를 사용하여 경험 애플리케이션 내에 프로토콜을 설정하여 정책 위반이 발생할 때 적절하게 적용할 수 있습니다.

## 데이터 필드 필터링

세그먼트 정의가 평가를 통과하지 못하면 아래에 설명된 두 가지 방법 중 하나를 통해 세그먼트 정의에 포함된 데이터를 조정할 수 있습니다.

### 세그먼트 정의의 병합 정책 업데이트

세그먼트 정의의 병합 정책을 업데이트하면 세그먼트 작업 실행 시 포함될 데이터 세트와 필드가 조정됩니다. 자세한 내용은 API 병합 정책 자습서에서 [기존 병합 정책 업데이트](../../profile/api/merge-policies.md#update)에 대한 섹션을 참조하십시오.

### 세그먼트 정의를 내보낼 때 특정 데이터 필드 제한

[!DNL Segmentation] API를 사용하여 세그먼트 정의를 데이터 세트로 내보낼 때 `fields` 매개 변수를 사용하여 내보내기에 포함된 데이터를 필터링할 수 있습니다. 이 매개 변수에 추가된 모든 데이터 필드는 내보내기에 포함되는 반면, 다른 모든 데이터 필드는 제외됩니다.

이름이 &quot;A&quot;, &quot;B&quot; 및 &quot;C&quot;인 데이터 필드가 있는 세그먼트 정의를 고려하십시오. 필드 &quot;C&quot;만 내보내려면 `fields` 매개 변수에 필드 &quot;C&quot;만 포함됩니다. 이렇게 하면 세그먼트 정의를 내보낼 때 필드 &quot;A&quot; 및 &quot;B&quot;가 제외됩니다.

자세한 내용은 세그먼테이션 자습서의 [세그먼트 정의 내보내기](./evaluate-a-segment.md#export) 섹션을 참조하십시오.

## 다음 단계

이 자습서에 따라 세그먼트 정의와 연결된 데이터 사용 레이블을 조회하고 특정 마케팅 작업에 대한 정책 위반을 테스트했습니다. [!DNL Experience Platform]의 데이터 거버넌스에 대한 자세한 내용은 [데이터 거버넌스](../../data-governance/home.md)의 개요를 참조하십시오.
