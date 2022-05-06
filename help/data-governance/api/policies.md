---
keywords: Experience Platform;홈;인기 항목;정책 적용;API 기반 적용;데이터 거버넌스
solution: Experience Platform
title: 정책 API 끝점
topic-legacy: developer guide
description: 데이터 사용 정책은 Experience Platform 내에서 데이터를 수행할 수 있도록 허용하거나 제한하는 마케팅 작업 종류를 설명하는 조직에서 사용하는 규칙입니다. /policy 엔드포인트는 데이터 사용 정책 보기, 만들기, 업데이트 또는 삭제와 관련된 모든 API 호출에 사용됩니다.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 2%

---

# 정책 끝점

데이터 사용 정책은 내에서 데이터를 수행할 수 있도록 허용되거나 제한된 마케팅 작업 종류를 설명하는 규칙입니다 [!DNL Experience Platform]. 다음 `/policies` 의 엔드포인트 [!DNL Policy Service API] 조직의 데이터 사용 정책을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 API 엔드포인트는 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 계속하기 전에 [시작 안내서](getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 모든 호출을 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다 [!DNL Experience Platform] API.

## 정책 목록 검색 {#list}

모든 항목을 나열할 수 있습니다 `core` 또는 `custom` 에 GET 요청을 수행하여 정책을 만듭니다. `/policies/core` 또는 `/policies/custom`각각 입니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 다음이 포함됩니다 `children` 검색된 각 정책의 세부 사항을 나열하는 배열입니다 `id` 값. 를 사용할 수 있습니다 `id` 수행할 특정 정책의 필드 [조회](#lookup), [업데이트](#update), 및 [delete](#delete) 해당 정책에 대한 요청.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `status` | 정책의 현재 상태입니다. 다음 세 가지 가능한 상태가 있습니다. `DRAFT`, `ENABLED`, 또는 `DISABLED`. 기본적으로 `ENABLED` 정책은 평가에 참여한다. 다음 사항에 대한 개요를 참조하십시오. [정책 평가](../enforcement/overview.md) 추가 정보. |
| `marketingActionRefs` | 정책에 적용 가능한 모든 마케팅 작업의 URI를 나열하는 배열입니다. |
| `description` | 정책의 사용 사례와 추가적인 컨텍스트를 제공하는 선택적 설명입니다. |
| `deny` | 정책의 관련 마케팅 작업이 수행되는 것을 제한하는 특정 데이터 사용 레이블을 설명하는 객체입니다. 의 섹션을 참조하십시오. [정책 만들기](#create-policy) 를 참조하십시오. |

## 정책 조회 {#look-up}

해당 정책을 포함하여 특정 정책을 찾을 수 있습니다. `id` GET 요청의 경로에 있는 속성입니다.

**API 형식**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 다음 `id` 조회하고 싶은 정책 중 |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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
| `status` | 정책의 현재 상태입니다. 다음 세 가지 가능한 상태가 있습니다. `DRAFT`, `ENABLED`, 또는 `DISABLED`. 기본적으로 `ENABLED` 정책은 평가에 참여한다. 다음 사항에 대한 개요를 참조하십시오. [정책 평가](../enforcement/overview.md) 추가 정보. |
| `marketingActionRefs` | 정책에 적용 가능한 모든 마케팅 작업의 URI를 나열하는 배열입니다. |
| `description` | 정책의 사용 사례와 추가적인 컨텍스트를 제공하는 선택적 설명입니다. |
| `deny` | 정책의 관련 마케팅 작업이 수행되는 것을 제한하는 특정 데이터 사용 레이블을 설명하는 객체입니다. 의 섹션을 참조하십시오. [정책 만들기](#create-policy) 를 참조하십시오. |

## 사용자 지정 정책 만들기 {#create-policy}

에서 [!DNL Policy Service] API인 정책은 다음과 같이 정의됩니다.

* 특정 마케팅 작업에 대한 참조
* 마케팅 작업이 수행되지 않도록 제한하는 데이터 사용 레이블을 설명하는 식입니다

후자의 요구 사항을 충족하려면 정책 정의에 데이터 사용 레이블 존재 여부에 대한 부울 식이 포함되어야 합니다. 이 식을 정책 표현식이라고 합니다.

정책 표현식은 `deny` 각 정책 정의 내의 속성입니다. 단순 예제 `deny` 단일 레이블이 있는지 확인하는 객체는 다음과 같습니다.

```json
"deny": {
    "label": "C1"
}
```

그러나 많은 정책에서는 데이터 사용 레이블 존재 와 관련된 더 복잡한 조건을 지정합니다. 이러한 사용 사례를 지원하기 위해 정책 표현식을 설명하는 부울 작업을 포함할 수도 있습니다. 정책 식 개체에는 레이블 또는 연산자와 피연산자가 있어야 하지만 둘 다 포함되지는 않습니다. 그러면 각 피연산자가 정책 표현식 개체이기도 합니다.

예를 들어, `C1 OR (C3 AND C7)` 정책의 레이블은 `deny` 속성은 다음과 같이 지정됩니다.

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
| `operator` | 동위 항목에 제공된 레이블 간의 조건부 관계를 나타냅니다 `operands` 배열입니다. 허용되는 값은 다음과 같습니다. <ul><li>`OR`: 표현식에 `operands` 배열이 있습니다.</li><li>`AND`: 표현식의 모든 레이블이 `operands` 배열이 있습니다.</li></ul> |
| `operands` | 각 객체가 단일 레이블이나 추가 쌍을 나타내는 객체의 배열입니다 `operator` 및 `operands` 속성을 사용합니다. 에 레이블 및/또는 작업이 있는지 여부 `operands` 배열이 동위 요소의 값에 따라 true 또는 false로 확인됩니다 `operator` 속성을 사용합니다. |
| `label` | 정책에 적용되는 단일 데이터 사용 레이블의 이름입니다. |

에 POST 요청을 작성하여 새 사용자 지정 정책을 만들 수 있습니다 `/policies/custom` 엔드포인트.

**API 형식**

```http
POST /policies/custom
```

**요청**

다음 요청은 마케팅 작업을 제한하는 새 정책을 만듭니다 `exportToThirdParty` 레이블이 포함된 데이터에 대해 수행 `C1 OR (C3 AND C7)`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | 정책의 현재 상태입니다. 다음 세 가지 가능한 상태가 있습니다. `DRAFT`, `ENABLED`, 또는 `DISABLED`. 기본적으로 `ENABLED` 정책은 평가에 참여한다. 다음 사항에 대한 개요를 참조하십시오. [정책 평가](../enforcement/overview.md) 추가 정보. |
| `marketingActionRefs` | 정책에 적용 가능한 모든 마케팅 작업의 URI를 나열하는 배열입니다. 마케팅 작업에 대한 URI는 아래에 제공됩니다 `_links.self.href` 에 대한 응답에서 [마케팅 작업 조회](./marketing-actions.md#look-up). |
| `description` | 정책의 사용 사례와 추가적인 컨텍스트를 제공하는 선택적 설명입니다. |
| `deny` | 정책의 관련 마케팅 작업에서 특정 데이터 사용 레이블을 설명하는 정책 표현식은 수행할 수 없습니다. |

**응답**

성공적인 응답은 정책을 포함하여 새로 만든 정책의 세부 정보를 반환합니다 `id`. 이 값은 읽기 전용이며 정책을 만들 때 자동으로 할당됩니다.

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
    "imsOrg": "{ORG_ID}",
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
>사용자 지정 정책만 업데이트할 수 있습니다. 핵심 정책을 활성화하거나 비활성화하려면 [활성화된 핵심 정책 목록 업데이트](#update-enabled-core).

PUT 요청의 경로에 해당 ID를 제공하여 정책의 업데이트된 양식이 포함된 페이로드를 통해 기존 사용자 지정 정책을 업데이트할 수 있습니다. 즉, PUT 요청은 기본적으로 정책을 다시 기록합니다.

>[!NOTE]
>
>의 섹션을 참조하십시오. [사용자 지정 정책의 일부 업데이트](#patch) 정책을 덮어쓰지 않고 정책에 대해 하나 이상의 필드만 업데이트하려는 경우

**API 형식**

```http
PUT /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 다음 `id` 업데이트할 정책의 일부입니다. |

**요청**

이 예에서 데이터를 타사로 내보내기 위한 조건이 변경되었으며, 이제 이 마케팅 작업을 거부할 수 있도록 만든 정책이 필요합니다. `C1 AND C5` 데이터 레이블이 있습니다.

다음 요청은 새 정책 표현식을 포함하도록 기존 정책을 업데이트합니다. 이 요청은 기본적으로 정책을 다시 쓰기 때문에, 일부 값이 업데이트되지 않더라도 모든 필드를 페이로드에 포함해야 합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | 정책의 현재 상태입니다. 다음 세 가지 가능한 상태가 있습니다. `DRAFT`, `ENABLED`, 또는 `DISABLED`. 기본적으로 `ENABLED` 정책은 평가에 참여한다. 다음 사항에 대한 개요를 참조하십시오. [정책 평가](../enforcement/overview.md) 추가 정보. |
| `marketingActionRefs` | 정책에 적용 가능한 모든 마케팅 작업의 URI를 나열하는 배열입니다. 마케팅 작업에 대한 URI는 아래에 제공됩니다 `_links.self.href` 에 대한 응답에서 [마케팅 작업 조회](./marketing-actions.md#look-up). |
| `description` | 정책의 사용 사례와 추가적인 컨텍스트를 제공하는 선택적 설명입니다. |
| `deny` | 정책의 관련 마케팅 작업에서 특정 데이터 사용 레이블을 설명하는 정책 표현식은 수행할 수 없습니다. 의 섹션을 참조하십시오. [정책 만들기](#create-policy) 를 참조하십시오. |

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
    "imsOrg": "{ORG_ID}",
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
>사용자 지정 정책만 업데이트할 수 있습니다. 핵심 정책을 활성화하거나 비활성화하려면 [활성화된 핵심 정책 목록 업데이트](#update-enabled-core).

PATCH 요청을 사용하여 정책의 특정 부분을 업데이트할 수 있다. 정책을 다시 쓰는 PUT 요청과 달리, PATCH 요청은 요청 본문에 지정된 속성만 업데이트합니다. 이 기능은 적절한 속성(`/status`) 및 해당 값( )`ENABLED` 또는 `DISABLED`).

>[!NOTE]
>
>PATCH 요청에 대한 페이로드는 JSON 패치 형식을 따릅니다. 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md) 를 참조하십시오.

다음 [!DNL Policy Service] API는 JSON 패치 작업을 지원합니다 `add`, `remove`, 및 `replace`및 를 사용하면 아래 예와 같이 여러 업데이트를 하나의 호출로 결합할 수 있습니다.

**API 형식**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 다음 `id` 속성을 업데이트할 정책의 속성 |

**요청**

다음 요청에서는 두 가지를 사용합니다 `replace` 정책 상태를 변경할 작업 `DRAFT` to `ENABLED`, 및 를 업데이트하여 `description` 새 설명이 있는 필드.

>[!IMPORTANT]
>
>단일 요청으로 여러 PATCH 작업을 전송할 때 배열에 표시되는 순서대로 처리됩니다. 필요한 경우 요청을 올바른 순서로 전송하는지 확인합니다.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

사용자 지정 정책을 포함하여 삭제할 수 있습니다 `id` DELETE 요청의 경로.

>[!WARNING]
>
>삭제된 정책은 복구할 수 없습니다. 가장 좋은 방법은 다음과 같습니다 [조회(GET) 요청 수행](#lookup) 먼저 정책을 보고 제거할 정책이 올바른지 확인합니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 빈 본문이 있는 HTTP 상태 200(OK)을 반환합니다.

정책을 다시 조회(GET)하여 삭제를 확인할 수 있습니다. 정책이 성공적으로 삭제된 경우 HTTP 404(찾을 수 없음) 오류가 표시됩니다.

## 활성화된 핵심 정책 목록 검색 {#list-enabled-core}

기본적으로 활성화된 데이터 사용 정책만 평가에 참여합니다. 조직에 GET 요청을 수행하여 현재 조직에서 활성화한 핵심 정책 목록을 검색할 수 있습니다 `/enabledCorePolicies` 엔드포인트.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `policyIds` 배열입니다.

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
  "imsOrg": "{ORG_ID}",
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

기본적으로 활성화된 데이터 사용 정책만 평가에 참여합니다. 에 PUT 요청을 함으로써 `/enabledCorePolicies` endpoint, 단일 호출을 사용하여 조직에 대해 활성화된 핵심 정책 목록을 업데이트할 수 있습니다.

>[!NOTE]
>
>이 종단점에 의해 핵심 정책만 활성화하거나 비활성화할 수 있습니다. 사용자 지정 정책을 활성화하거나 비활성화하려면 [정책의 일부 업데이트](#patch).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `policyIds` | 활성화할 핵심 정책 ID 목록입니다. 포함되지 않은 모든 핵심 정책은 `DISABLED` 상태 및 은 평가에 참여할 수 없습니다. |

**응답**

성공적인 응답은 다음 항목 아래에 활성화된 핵심 정책의 업데이트된 목록을 반환합니다 `policyIds` 배열입니다.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
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

새 정책을 정의하거나 기존 정책을 업데이트하면 [!DNL Policy Service] 특정 레이블 또는 데이터 세트에 대해 마케팅 작업을 테스트하고 정책이 예상대로 위반을 발생하는지 여부를 확인하는 API입니다. 의 안내서를 참조하십시오. [정책 평가 끝점](./evaluation.md) 추가 정보.
