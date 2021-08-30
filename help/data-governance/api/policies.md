---
keywords: Experience Platform;홈;인기 항목;정책 적용;API 기반 적용;데이터 거버넌스
solution: Experience Platform
title: 정책 API 끝점
topic-legacy: developer guide
description: 데이터 사용 정책은 Experience Platform 내에서 데이터를 수행할 수 있도록 허용하거나 제한하는 마케팅 작업 종류를 설명하는 조직에서 사용하는 규칙입니다. /policy 엔드포인트는 데이터 사용 정책 보기, 만들기, 업데이트 또는 삭제와 관련된 모든 API 호출에 사용됩니다.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 2%

---

# 정책 끝점

데이터 사용 정책은 [!DNL Experience Platform] 내의 데이터에 대해 수행할 수 있거나 제한할 수 있는 마케팅 작업 종류를 설명하는 규칙입니다. [!DNL Policy Service API]의 `/policies` 종단점을 사용하면 조직의 데이터 사용 정책을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 API 엔드포인트는 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)의 일부입니다. 계속하기 전에 [시작 안내서](getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출을 읽는 방법에 대한 안내서 및 [!DNL Experience Platform] API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 검토하십시오.

## 정책 목록 검색 {#list}

각각 `/policies/core` 또는 `/policies/custom`에 GET 요청을 하여 모든 `core` 또는 `custom` 정책을 나열할 수 있습니다.

**API 형식**

```http
GET /policies/core
GET /policies/custom
```

**요청**

다음 요청은 조직에서 정의한 사용자 정의 정책 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답에는 `id` 값을 포함하여 검색된 각 정책의 세부 정보를 나열하는 `children` 배열이 포함됩니다. 특정 정책의 `id` 필드를 사용하여 [조회](#lookup), [업데이트](#update) 및 [삭제](#delete) 요청을 수행할 수 있습니다.

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
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
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `_page.count` | 검색된 총 정책 수입니다. |
| `name` | 정책의 표시 이름입니다. |
| `status` | 정책의 현재 상태입니다. 다음 세 가지 가능한 상태가 있습니다. `DRAFT`, `ENABLED` 또는 `DISABLED`. 기본적으로 `ENABLED` 정책만 평가에 참여합니다. 자세한 내용은 [정책 평가](../enforcement/overview.md)의 개요를 참조하십시오. |
| `marketingActionRefs` | 정책에 적용 가능한 모든 마케팅 작업의 URI를 나열하는 배열입니다. |
| `description` | 정책의 사용 사례와 추가적인 컨텍스트를 제공하는 선택적 설명입니다. |
| `deny` | 정책의 관련 마케팅 작업이 수행되는 것을 제한하는 특정 데이터 사용 레이블을 설명하는 객체입니다. 이 속성에 대한 자세한 내용은 [정책 만들기](#create-policy)의 섹션을 참조하십시오. |

## 정책 조회 {#look-up}

GET 요청 경로에 해당 정책의 `id` 속성을 포함하여 특정 정책을 조회할 수 있습니다.

**API 형식**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 조회할 정책의 `id` |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 정책의 세부 사항을 반환합니다.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
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
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| 속성 | 설명 |
| --- | --- |
| `name` | 정책의 표시 이름입니다. |
| `status` | 정책의 현재 상태입니다. 다음 세 가지 가능한 상태가 있습니다. `DRAFT`, `ENABLED` 또는 `DISABLED`. 기본적으로 `ENABLED` 정책만 평가에 참여합니다. 자세한 내용은 [정책 평가](../enforcement/overview.md)의 개요를 참조하십시오. |
| `marketingActionRefs` | 정책에 적용 가능한 모든 마케팅 작업의 URI를 나열하는 배열입니다. |
| `description` | 정책의 사용 사례와 추가적인 컨텍스트를 제공하는 선택적 설명입니다. |
| `deny` | 정책의 관련 마케팅 작업이 수행되는 것을 제한하는 특정 데이터 사용 레이블을 설명하는 객체입니다. 이 속성에 대한 자세한 내용은 [정책 만들기](#create-policy)의 섹션을 참조하십시오. |

## 사용자 지정 정책 만들기 {#create-policy}

[!DNL Policy Service] API에서 정책은 다음과 같이 정의됩니다.

* 특정 마케팅 작업에 대한 참조
* 마케팅 작업이 수행되지 않도록 제한하는 데이터 사용 레이블을 설명하는 식입니다

후자의 요구 사항을 충족하려면 정책 정의에 데이터 사용 레이블 존재 여부에 대한 부울 식이 포함되어야 합니다. 이 식을 정책 표현식이라고 합니다.

정책 표현식은 각 정책 정의 내에서 `deny` 속성 형식으로 제공됩니다. 단일 레이블이 있는지 확인하는 간단한 `deny` 개체의 예는 다음과 같습니다.

```json
"deny": {
    "label": "C1"
}
```

그러나 많은 정책에서는 데이터 사용 레이블 존재 와 관련된 더 복잡한 조건을 지정합니다. 이러한 사용 사례를 지원하기 위해 정책 표현식을 설명하는 부울 작업을 포함할 수도 있습니다. 정책 식 개체에는 레이블 또는 연산자와 피연산자가 있어야 하지만 둘 다 포함되지는 않습니다. 그러면 각 피연산자가 정책 표현식 개체이기도 합니다.

예를 들어 `C1 OR (C3 AND C7)` 레이블이 있는 데이터에 대해 마케팅 작업이 수행되지 않도록 하는 정책을 정의하려면 정책의 `deny` 속성이 다음과 같이 지정됩니다.

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `operator` | 동위 `operands` 배열에 제공된 레이블 간의 조건부 관계를 나타냅니다. 허용되는 값은 다음과 같습니다. <ul><li>`OR`: 배열에 레이블이 있으면 표현식 `operands` 이 true로 확인됩니다.</li><li>`AND`: 배열에 있는 모든 레이블이 있는 경우에만 표현식 `operands` 이 true로 확인됩니다.</li></ul> |
| `operands` | 각 객체가 단일 레이블 또는 추가 `operator` 및 `operands` 속성 쌍을 나타내는 객체 배열입니다. `operands` 배열에 레이블 및/또는 작업이 있으면 동위 `operator` 속성의 값을 기준으로 true 또는 false로 확인됩니다. |
| `label` | 정책에 적용되는 단일 데이터 사용 레이블의 이름입니다. |

`/policies/custom` 종단점에 POST 요청을 하여 새 사용자 지정 정책을 만들 수 있습니다.

**API 형식**

```http
POST /policies/custom
```

**요청**

다음 요청은 마케팅 작업 `exportToThirdParty`이 `C1 OR (C3 AND C7)` 레이블이 포함된 데이터에 대해 수행되지 않도록 제한하는 새 정책을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 정책의 표시 이름입니다. |
| `status` | 정책의 현재 상태입니다. 다음 세 가지 가능한 상태가 있습니다. `DRAFT`, `ENABLED` 또는 `DISABLED`. 기본적으로 `ENABLED` 정책만 평가에 참여합니다. 자세한 내용은 [정책 평가](../enforcement/overview.md)의 개요를 참조하십시오. |
| `marketingActionRefs` | 정책에 적용 가능한 모든 마케팅 작업의 URI를 나열하는 배열입니다. 마케팅 작업의 URI는 [마케팅 작업 조회](./marketing-actions.md#look-up)에 대한 응답에서 `_links.self.href` 아래에 제공됩니다. |
| `description` | 정책의 사용 사례와 추가적인 컨텍스트를 제공하는 선택적 설명입니다. |
| `deny` | 정책의 관련 마케팅 작업에서 특정 데이터 사용 레이블을 설명하는 정책 표현식은 수행할 수 없습니다. |

**응답**

성공적으로 응답하면 `id`을 포함하여 새로 만든 정책의 세부 정보가 반환됩니다. 이 값은 읽기 전용이며 정책을 만들 때 자동으로 할당됩니다.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 사용자 지정 정책 업데이트 {#update}

>[!IMPORTANT]
>
>사용자 지정 정책만 업데이트할 수 있습니다. 핵심 정책을 활성화하거나 비활성화하려면 [활성화된 핵심 정책 목록 업데이트](#update-enabled-core)에서 섹션을 참조하십시오.

PUT 요청의 경로에 해당 ID를 제공하여 정책의 업데이트된 양식이 포함된 페이로드를 통해 기존 사용자 지정 정책을 업데이트할 수 있습니다. 즉, PUT 요청은 기본적으로 정책을 다시 기록합니다.

>[!NOTE]
>
>정책에 대해 하나 이상의 필드만 업데이트하려면 덮어쓰지 않고 [사용자 지정 정책](#patch)의 부분 업데이트 섹션을 참조하십시오.

**API 형식**

```http
PUT /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 업데이트할 정책의 `id` |

**요청**

이 예제에서 데이터를 타사로 내보내기 위한 조건이 변경되었으며, 이제 `C1 AND C5` 데이터 레이블이 있는 경우 이 마케팅 작업을 거부하도록 만든 정책이 필요합니다.

다음 요청은 새 정책 표현식을 포함하도록 기존 정책을 업데이트합니다. 이 요청은 기본적으로 정책을 다시 쓰기 때문에, 일부 값이 업데이트되지 않더라도 모든 필드를 페이로드에 포함해야 합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 정책의 표시 이름입니다. |
| `status` | 정책의 현재 상태입니다. 다음 세 가지 가능한 상태가 있습니다. `DRAFT`, `ENABLED` 또는 `DISABLED`. 기본적으로 `ENABLED` 정책만 평가에 참여합니다. 자세한 내용은 [정책 평가](../enforcement/overview.md)의 개요를 참조하십시오. |
| `marketingActionRefs` | 정책에 적용 가능한 모든 마케팅 작업의 URI를 나열하는 배열입니다. 마케팅 작업의 URI는 [마케팅 작업 조회](./marketing-actions.md#look-up)에 대한 응답에서 `_links.self.href` 아래에 제공됩니다. |
| `description` | 정책의 사용 사례와 추가적인 컨텍스트를 제공하는 선택적 설명입니다. |
| `deny` | 정책의 관련 마케팅 작업에서 특정 데이터 사용 레이블을 설명하는 정책 표현식은 수행할 수 없습니다. 이 속성에 대한 자세한 내용은 [정책 만들기](#create-policy)의 섹션을 참조하십시오. |

**응답**

성공적인 응답은 업데이트된 정책의 세부 정보를 반환합니다.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 사용자 지정 정책의 일부 업데이트 {#patch}

>[!IMPORTANT]
>
>사용자 지정 정책만 업데이트할 수 있습니다. 핵심 정책을 활성화하거나 비활성화하려면 [활성화된 핵심 정책 목록 업데이트](#update-enabled-core)에서 섹션을 참조하십시오.

PATCH 요청을 사용하여 정책의 특정 부분을 업데이트할 수 있다. 정책을 다시 쓰는 PUT 요청과 달리, PATCH 요청은 요청 본문에 지정된 속성만 업데이트합니다. 이 기능은 적절한 속성(`/status`)과 해당 값(`ENABLED` 또는 `DISABLED`)에 대한 경로를 제공해야 하므로 정책을 활성화하거나 비활성화하려는 경우에 특히 유용합니다.

>[!NOTE]
>
>PATCH 요청에 대한 페이로드는 JSON 패치 형식을 따릅니다. 허용되는 구문에 대한 자세한 내용은 [API fundamentals 안내서](../../landing/api-fundamentals.md)를 참조하십시오.

[!DNL Policy Service] API는 JSON 패치 작업 `add`, `remove` 및 `replace`을 지원하며, 아래 예와 같이 여러 업데이트를 하나의 호출로 결합할 수 있습니다.

**API 형식**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 속성을 업데이트할 정책의 `id` |

**요청**

다음 요청에서는 두 개의 `replace` 작업을 사용하여 정책 상태를 `DRAFT`에서 `ENABLED`(으)로 변경하고, 새 설명으로 `description` 필드를 업데이트합니다.

>[!IMPORTANT]
>
>단일 요청으로 여러 PATCH 작업을 전송할 때 배열에 표시되는 순서대로 처리됩니다. 필요한 경우 요청을 올바른 순서로 전송하는지 확인합니다.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**응답**

성공적인 응답은 업데이트된 정책의 세부 정보를 반환합니다.


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
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
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 사용자 지정 정책 삭제 {#delete}

DELETE 요청 경로에 `id` 을 포함하여 사용자 지정 정책을 삭제할 수 있습니다.

>[!WARNING]
>
>삭제된 정책은 복구할 수 없습니다. 먼저 [조회(GET) 요청](#lookup)을 수행하여 정책을 보고 제거할 정책이 올바른지 확인하는 것이 좋습니다.

**API 형식**

```http
DELETE /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 삭제할 정책의 ID입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 빈 본문이 있는 HTTP 상태 200(OK)을 반환합니다.

정책을 다시 조회(GET)하여 삭제를 확인할 수 있습니다. 정책이 성공적으로 삭제된 경우 HTTP 404(찾을 수 없음) 오류가 표시됩니다.

## 활성화된 핵심 정책 목록 검색 {#list-enabled-core}

기본적으로 활성화된 데이터 사용 정책만 평가에 참여합니다. `/enabledCorePolicies` 종단점에 GET 요청을 수행하여 조직에서 현재 활성화된 핵심 정책 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /enabledCorePolicies
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `policyIds` 배열 아래에 활성화된 핵심 정책 목록을 반환합니다.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## 활성화된 핵심 정책 목록 업데이트 {#update-enabled-core}

기본적으로 활성화된 데이터 사용 정책만 평가에 참여합니다. `/enabledCorePolicies` 종단점에 PUT 요청을 수행하면 단일 호출을 사용하여 조직에 대해 활성화된 핵심 정책 목록을 업데이트할 수 있습니다.

>[!NOTE]
>
>이 종단점에 의해 핵심 정책만 활성화하거나 비활성화할 수 있습니다. 사용자 지정 정책을 활성화하거나 비활성화하려면 [정책의 일부를 업데이트하는 섹션을 참조하십시오](#patch).

**API 형식**

```http
PUT /enabledCorePolicies
```

**요청**

다음 요청은 페이로드에 제공된 ID를 기반으로 활성화된 핵심 정책 목록을 업데이트합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `policyIds` | 활성화할 핵심 정책 ID 목록입니다. 포함되지 않은 모든 핵심 정책은 `DISABLED` 상태로 설정되며 평가에 참여하지 않습니다. |

**응답**

성공적인 응답은 `policyIds` 배열 아래에 활성화된 핵심 정책의 업데이트된 목록을 반환합니다.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## 다음 단계

새 정책을 정의하거나 기존 정책을 업데이트했으면 [!DNL Policy Service] API를 사용하여 특정 레이블 또는 데이터 세트에 대해 마케팅 작업을 테스트하고 정책이 예상대로 위반을 발생하는지 여부를 확인할 수 있습니다. 자세한 내용은 [정책 평가 엔드포인트](./evaluation.md)에 대한 안내서를 참조하십시오.
