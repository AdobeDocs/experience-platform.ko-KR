---
keywords: Experience Platform;홈;자주 찾는 항목;데이터 거버넌스;데이터 사용 정책
solution: Experience Platform
title: API에서 데이터 거버넌스 정책 만들기
type: Tutorial
description: Policy Service API를 사용하여 데이터 거버넌스 정책을 만드는 방법을 알아봅니다.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 2%

---

# API에서 데이터 거버넌스 정책 만들기

다음 [정책 서비스 API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 데이터 거버넌스 정책을 만들고 관리하여 특정 데이터 사용 레이블이 포함된 데이터에 대해 취할 수 있는 마케팅 작업을 결정할 수 있습니다.

이 문서에서는 를 사용하여 거버넌스 정책을 만드는 단계별 자습서를 제공합니다. [!DNL Policy Service] API.

>[!NOTE]
>
>액세스 제어 정책을 만드는 방법에 대한 단계는 `/policies` 에 대한 엔드포인트 가이드 [액세스 제어 API](../../access-control/abac/api/policies.md). 동의 정책을 만드는 방법을 알아보려면 다음을 참조하십시오. [정책 UI 안내서](./user-guide.md#consent-policy).

## 시작하기

이 자습서에서는 정책 생성 및 평가와 관련된 다음 주요 개념에 대한 작업 이해를 필요로 합니다.

* [Adobe Experience Platform 데이터 거버넌스](../home.md): 다음에 사용되는 프레임워크 [!DNL Platform] 데이터 사용 규정 준수를 시행합니다.
   * [데이터 사용 레이블](../labels/overview.md): 데이터 사용 레이블은 XDM 데이터 필드에 적용되며, 데이터 액세스 방법에 대한 제한을 지정합니다.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

이 자습서를 시작하기 전에 다음을 검토하십시오. [개발자 안내서](../api/getting-started.md) 를 성공적으로 호출하기 위해 알아야 하는 중요한 정보 [!DNL Policy Service] 필수 헤더와 예제 API 호출을 읽는 방법을 포함한 API.

## 마케팅 액션 정의 {#define-action}

데이터 거버넌스 프레임워크에서 마케팅 작업은 [!DNL Experience Platform] 데이터 소비자는 데이터 사용 정책 위반 여부를 확인할 필요가 있습니다.

데이터 사용 정책을 만드는 첫 번째 단계는 정책이 평가할 마케팅 작업을 결정하는 것입니다. 이 작업은 다음 옵션 중 하나를 사용하여 수행할 수 있습니다.

* [기존 마케팅 액션 조회](#look-up)
* [새 마케팅 액션 만들기](#create-new)

### 기존 마케팅 액션 조회 {#look-up}

다음 중 하나에 GET 요청을 하여 정책에서 평가할 기존 마케팅 작업을 조회할 수 있습니다. `/marketingActions` 엔드포인트.

**API 형식**

에서 제공하는 마케팅 작업을 조회하고 있는지 여부에 따라 다름 [!DNL Experience Platform] 또는 조직에서 만든 사용자 지정 마케팅 작업에서 `marketingActions/core` 또는 `marketingActions/custom` 엔드포인트.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**요청**

다음 요청은 `marketingActions/custom` endpoint - IMS 조직에서 정의한 모든 마케팅 작업 목록을 가져옵니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 찾은 총 마케팅 액션 수를 반환합니다(`count`) 내의 마케팅 활동 자체에 대한 세부 사항을 나열합니다. `children` 배열입니다.

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{ORG_ID}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `_links.self.href` | 내의 각 항목 `children` 배열에는 나열된 마케팅 작업에 대한 URI ID가 포함됩니다. |

사용할 마케팅 작업을 찾으면 그 값을 기록합니다 `href` 속성. 이 값은 의 다음 단계에서 사용됩니다. [정책 만들기](#create-policy).

### 새 마케팅 액션 만들기 {#create-new}

에 PUT 요청을 하여 새 마케팅 작업을 만들 수 있습니다. `/marketingActions/custom/` 엔드포인트 및 요청 경로 끝에 마케팅 작업의 이름을 제공하는 기능.

**API 형식**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 만들려는 새 마케팅 액션의 이름입니다. 이 이름은 마케팅 작업의 기본 식별자 역할을 하므로 고유해야 합니다. 가장 좋은 방법은 마케팅 액션에 설명적이지만 간결한 이름을 지정하는 것입니다. |

**요청**

다음 요청은 &quot;exportToThirdParty&quot;라는 새 사용자 지정 마케팅 작업을 만듭니다. 다음 사항에 주목하십시오. `name` 에서 요청 페이로드는 요청 경로에 제공된 이름과 동일합니다.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 만들려는 마케팅 액션의 이름입니다. 이 이름은 요청 경로에 제공된 이름과 일치해야 합니다. 그렇지 않으면 400(잘못된 요청) 오류가 발생합니다. |
| `description` | 사람이 인식할 수 있는 마케팅 액션에 대한 설명입니다. |

**응답**

성공적인 응답은 HTTP 상태 201(생성됨) 및 새로 생성된 마케팅 작업의 세부 정보를 반환합니다.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `_links.self.href` | 마케팅 액션의 URI ID입니다. |

새로 만든 마케팅 작업의 URI ID를 기록합니다. 해당 ID는 정책을 만드는 다음 단계에서 사용됩니다.

## 정책 만들기 {#create-policy}

새 정책을 만들려면 마케팅 작업을 금지하는 사용 레이블 표현식과 함께 마케팅 작업의 URI ID를 제공해야 합니다.

이 표현식을 정책 표현식이라고 하며 (A) 레이블 또는 (B) 연산자와 피연산자 중 하나를 포함하는 객체이지만 둘 다 포함하는 것은 아닙니다. 또한 각 피연산자는 정책 표현식 객체이기도 합니다. 예를 들어 다음과 같은 경우 데이터를 서드파티에 내보내는 것과 관련된 정책이 금지될 수 있습니다. `C1 OR (C3 AND C7)` 레이블이 있습니다. 이 표현식은 다음과 같이 지정됩니다.

```json
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
}
```

>[!NOTE]
>
>OR 및 AND 연산자만 지원됩니다.

정책 표현식을 구성했으면 의 POST 요청을 통해 새 정책을 만들 수 있습니다. `/policies/custom` 엔드포인트.

**API 형식**

```http
POST /policies/custom
```

**요청**

다음 요청은 요청 페이로드에 마케팅 작업과 정책 표현식을 제공하여 &quot;데이터를 서드파티에 내보내기&quot;라는 정책을 만듭니다.

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

| 속성 | 설명 |
| --- | --- |
| `marketingActionRefs` | 를 포함하는 배열 `href` 마케팅 액션 값, 다음에서 얻음: [이전 단계](#define-action). 위의 예에서는 마케팅 작업이 한 개만 나열되지만 여러 작업을 제공할 수도 있습니다. |
| `deny` | 정책 표현식 객체입니다. 정책이에서 참조한 마케팅 작업을 거부하도록 하는 사용 레이블 및 조건을 정의합니다. `marketingActionRefs`. |

**응답**

성공적인 응답은 HTTP 상태 201(생성됨) 및 새로 생성된 정책의 세부 사항을 반환합니다.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
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
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 정책을 고유하게 식별하는 읽기 전용, 시스템 생성 값입니다. |

다음 단계에서 정책을 활성화하는 데 사용되므로 새로 만든 정책의 URI ID를 기록합니다.

## 정책 활성화

>[!NOTE]
>
>에 정책을 유지하려면 이 단계는 선택 사항입니다. `DRAFT` 상태, 기본적으로 정책의 상태는 로 설정되어 있어야 합니다. `ENABLED` 평가에 참여하기 위해. 다음 안내서를 참조하십시오 [정책 시행](../enforcement/api-enforcement.md) 의 정책에 대한 예외를 설정하는 방법에 대한 자세한 내용 `DRAFT` 상태.

기본적으로 이 있는 정책 `status` 속성이 로 설정됨 `DRAFT` 평가에 참여하지 마십시오. 에 PATCH 요청을 하여 평가를 위한 정책을 활성화할 수 있습니다. `/policies/custom/` 엔드포인트 및 요청 경로 종료 시 정책에 대한 고유 식별자 제공

**API 형식**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 다음 `id` 활성화할 정책 값입니다. |

**요청**

다음 요청은 다음에 대한 PATCH 작업을 수행합니다. `status` 정책의 속성, 값 변경 `DRAFT` 끝 `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| 속성 | 설명 |
| --- | --- |
| `op` | 수행할 PATCH 작업의 유형입니다. 이 요청은 &quot;바꾸기&quot; 작업을 수행합니다. |
| `path` | 업데이트할 필드의 경로입니다. 정책을 활성화할 때 값을 &quot;/status&quot;로 설정해야 합니다. |
| `value` | 에 지정된 속성에 지정할 새 값 `path`. 이 요청은 정책을 다음과 같이 설정합니다. `status` 속성을 &quot;ENABLED&quot;로 바꿉니다. |

**응답**

성공적인 응답은 HTTP 상태 200(OK) 및 업데이트된 정책의 세부 정보와 함께 를 반환합니다. `status` 이제 다음으로 설정됨 `ENABLED`.

```json
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
    "createdUser": "{CREATED_USER}",
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
```

## 다음 단계

이 자습서에 따라 마케팅 작업에 대한 데이터 사용 정책을 성공적으로 만들었습니다. 이제 의 자습서를 계속할 수 있습니다. [데이터 사용 정책 시행](../enforcement/api-enforcement.md) 정책 위반을 확인하고 experience 애플리케이션에서 처리하는 방법을 알아봅니다.

에서 사용할 수 있는 여러 작업에 대한 자세한 내용은 [!DNL Policy Service] API에서 다음을 참조하십시오. [정책 서비스 개발자 안내서](../api/getting-started.md). 다음에 대한 정책 시행 방법에 대한 정보: [!DNL Real-Time Customer Profile] 데이터, 다음에 대한 자습서 참조 [대상 세그먼트에 대한 데이터 사용 규정 준수](../../segmentation/tutorials/governance.md).

에서 사용 정책을 관리하는 방법에 대해 알아보려면 [!DNL Experience Platform] 사용자 인터페이스를 참조하십시오. [정책 사용 안내서](user-guide.md).
