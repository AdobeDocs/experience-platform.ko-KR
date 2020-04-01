---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 정책
topic: developer guide
translation-type: tm+mt
source-git-commit: 08d02e7323f75c450e7a250835f26a569685cdd1

---


# 정책

데이터 사용 정책은 조직에서 경험 플랫폼 내에서 데이터를 수행할 수 있도록 허용되거나 제한된 마케팅 활동의 종류를 설명하는 규칙입니다.

끝점은 데이터 사용 정책 보기, 만들기, 업데이트 또는 삭제와 관련된 모든 API 호출에 사용됩니다. `/policies`

## 모든 정책 나열

정책 목록을 보려면 지정된 컨테이너에 대한 모든 정책을 반환하거나 `/policies/core` GET 요청을 `/policies/custom` 수행할 수 있습니다.

**API 형식**

```http
GET /policies/core
GET /policies/custom
```

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 지정된 컨테이너 내의 총 정책 수를 보여주는 &quot;카운트&quot;와 각 정책을 포함한 세부 사항을 보여 주는 &quot;카운트&quot;가 포함됩니다 `id`. 이 `id` 필드는 특정 정책을 보기 위한 조회 요청을 수행하고 업데이트 및 삭제 작업을 수행하는 데 사용됩니다.

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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
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

## 특정 정책 찾기

각 정책에는 특정 정책의 세부 사항을 요청하는 데 사용할 수 있는 `id` 필드가 포함되어 있습니다. 정책을 알 수 `id` 없는 경우 이전 단계에서와 같이 목록(GET) 요청을 사용하여 특정 컨테이너(`core` 또는 `custom`) 내의 모든 정책을 나열할 수 있습니다.

**API 형식**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 정책 세부 사항( `id` (이 필드는 요청에서 `id` 보낸 것과 일치해야 함), `name``status`, `description`및 정책 기반이 되는 마케팅 작업에 대한 참조 링크)를 포함합니다`marketingActionRefs`.

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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 정책 만들기 {#create-policy}

정책을 만들려면 마케팅 활동을 금지하는 DULE 레이블 표현과 함께 마케팅 작업을 포함해야 합니다. 정책 정의에는 DULE 레이블이 있는 것과 관련된 부울 표현인 `deny` 속성이 포함되어야 합니다.

이 식을 a라고 `PolicyExpression` 하며 레이블 _또는_ 연산자 및 피연산자가 포함된 개체이지만 둘 다 포함하는 __ 것은 아닙니다. 또한 각 피연산자도 `PolicyExpression` 개체입니다. 예를 들어 레이블이 있는 경우 데이터를 제3자로 내보내기에 관한 정책을 사용할 수 `C1 OR (C3 AND C7)` 없습니다. 이 식은 다음과 같이 지정됩니다.

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

**API 형식**

```http
POST /policies/custom
```

**요청**

```SHELL
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
          "../marketingActions/custom/exportToThirdParty"
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

**응답**

성공적으로 만들어지면 HTTP 상태 201(작성됨)이 수신되고 응답 본문에는 새로 만든 정책을 비롯하여 해당 정책의 세부 정보가 포함됩니다 `id`. 이 값은 읽기 전용이며 정책을 만들 때 자동으로 할당됩니다.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 정책 업데이트

데이터 사용 정책을 만든 후 업데이트해야 할 수 있습니다. 이는 업데이트된 정책 양식이 포함된 페이로드가 포함된 정책에 대한 PUT 요청을 `id` 통해 전체적으로 수행됩니다. 즉, PUT 요청은 기본적으로 정책을 _다시_ 작성하므로, 아래 예와 같이 본문에는 모든 필수 정보가 포함되어야 합니다.

**API 형식**

```http
PUT /policies/custom/{id}
```

**요청**

이 예에서는 데이터를 제3자로 내보내기 위한 조건이 변경되었으며 이제 데이터 레이블이 있는 경우 이 마케팅 작업을 거부하도록 만든 정책이 필요합니다. `C1 AND (C3 OR C7)` 다음 호출을 사용하여 기존 정책을 업데이트합니다.

```SHELL
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
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**응답**

업데이트 요청이 성공하면 HTTP 상태 200(확인)이 반환되고 응답 본문에 업데이트된 정책이 표시됩니다. 이 `id` 값은 요청에서 `id` 보낸 것과 일치해야 합니다.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 정책의 일부 업데이트

PATCH 요청을 사용하여 정책의 특정 부분을 업데이트할 수 있습니다. 정책을 _다시 쓰는_ PUT 요청과 달리 PATCH 요청은 요청 본문에 지정된 경로만 업데이트합니다. 이 기능은 (`/status`) 업데이트할 특정 경로와 해당 값(`ENABLE` 또는 `DISABLE`)만 보내야 하므로 정책을 활성화하거나 비활성화할 때 특히 유용합니다.

정책 서비스 API는 현재 &quot;add&quot;, &quot;replace&quot; 및 &quot;remove&quot; PATCH 작업을 지원하고 다음 예와 같이, 여러 업데이트를 배열 내에 하나의 개체로 추가하여 하나의 호출로 결합할 수 있습니다.

**API 형식**

```http
PATCH /policies/custom/{id}
```

**요청**

이 예에서는 &quot;바꾸기&quot; 작업을 사용하여 정책 상태를 &quot;DRAFT&quot;에서 &quot;ENABLED&quot;로 변경하고 설명 필드를 새 설명으로 업데이트합니다. &quot;삭제&quot; 작업을 사용하여 정책 설명을 제거한 다음 &quot;추가&quot; 작업을 사용하여 다음과 같이 새 항목을 한 번 추가했을 수도 있습니다.

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

단일 요청에서 여러 PATCH 작업을 전송할 때는 이러한 작업이 배열에 표시되는 순서대로 처리되므로 필요한 경우 올바른 순서로 요청을 보내야 합니다.

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

업데이트 요청이 성공하면 HTTP 상태 200(OK)이 반환되고 응답 본문에 업데이트된 정책이 표시됩니다(&quot;status&quot;는 이제 &quot;ENABLED&quot;이고 &quot;description&quot;이 변경되었습니다.). 정책은 요청에서 전송된 정책과 일치해야 `id` 합니다 `id` .


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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 정책 삭제

만든 정책을 제거해야 하는 경우 삭제할 정책의 DELETE 요청을 실행하여 삭제할 `id` 수 있습니다. 먼저 조회(GET) 요청을 수행하여 정책을 보고 제거할 올바른 정책인지 확인하는 것이 좋습니다. **한 번 삭제하면 정책을 복구할 수 없습니다.**

**API 형식**

```http
DELETE /policies/custom/{id}
```

**요청**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

정책이 성공적으로 삭제되면 HTTP 상태 200(확인)으로 응답 본문이 비어 있게 됩니다.

정책을 다시 조회(GET)하여 삭제를 확인할 수 있습니다. 정책이 제거되었기 때문에 &quot;찾을 수 없음&quot; 오류 메시지와 함께 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.
