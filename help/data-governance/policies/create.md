---
keywords: Experience Platform;home;popular topics;data governance;data usage policy
solution: Experience Platform
title: 데이터 사용 정책 만들기
topic: policies
type: Tutorial
description: 정책 서비스 API를 사용하면 데이터 사용 정책을 만들고 관리하여 특정 데이터 사용 레이블이 포함된 데이터에 대해 수행할 수 있는 마케팅 작업을 결정할 수 있습니다. 이 문서에서는 정책 서비스 API를 사용하여 정책을 만들기 위한 단계별 자습서를 제공합니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 2%

---


# API에서 데이터 사용 정책 만들기

정책 [서비스 API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) 사용하면 데이터 사용 정책을 만들고 관리하여 특정 데이터 사용 레이블이 포함된 데이터에 대해 수행할 수 있는 마케팅 작업을 결정할 수 있습니다.

이 문서에서는 [!DNL Policy Service] API를 사용하여 정책을 만들기 위한 단계별 자습서를 제공합니다. API에서 제공되는 다양한 작업에 대한 보다 포괄적인 지침은 [정책 서비스 개발자 안내서를 참조하십시오](../api/getting-started.md).

## 시작하기

이 자습서에서는 정책을 만들고 평가하는 데 관련된 다음 주요 개념을 제대로 이해해야 합니다.

* [[!DNL 데이터 거버넌스]](../home.md):데이터 사용 규정 준수를 [!DNL Platform] 적용하는 프레임워크입니다.
* [데이터 사용 레이블](../labels/overview.md):데이터 사용 레이블은 XDM 데이터 필드에 적용되어 데이터 액세스 방법에 대한 제한을 지정합니다.
* [[!DNL 경험 데이터 모델(XDM)]](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이 자습서를 시작하기 전에 필수 헤더 및 예제 API 호출 읽기 방법 등 [API를 성공적으로 호출하기 위해 알아야 할 중요한 정보가 있는](../api/getting-started.md) 개발자 가이드를 [!DNL Policy Service] 검토하십시오.

## 마케팅 작업 정의 {#define-action}

이 [!DNL Data Governance] 프레임워크에서 마케팅 작업은 [!DNL Experience Platform] 데이터 소비자가 취하는 동작으로, 데이터 사용 정책 위반을 확인해야 합니다.

데이터 사용 정책을 만드는 첫 번째 단계는 정책이 평가할 마케팅 작업을 결정하는 것입니다. 다음 옵션 중 하나를 사용하여 수행할 수 있습니다.

* [기존 마케팅 작업 조회](#look-up)
* [새 마케팅 작업 만들기](#create-new)

### 기존 마케팅 작업 조회 {#look-up}

엔드포인트 중 하나에 GET 요청을 함으로써 정책에 의해 평가될 기존 마케팅 작업을 조회할 수 `/marketingActions` 있습니다.

**API 형식**

조직에서 제공하는 마케팅 작업 [!DNL Experience Platform] 또는 조직에서 만든 사용자 지정 마케팅 작업을 조회하는지 여부에 따라 각각 `marketingActions/core` 또는 `marketingActions/custom` 끝점을 사용합니다.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**요청**

다음 요청은 IMS 조직에서 정의한 모든 마케팅 작업 목록을 가져오는 끝점을 사용합니다. `marketingActions/custom`

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 발견된 총 마케팅 작업 수를 반환하고(`count`) 배열에서 마케팅 활동의 세부 사항을 `children` 나열합니다.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `_links.self.href` | 배열 내의 각 항목에는 나열된 마케팅 작업에 `children` 대한 URI ID가 포함됩니다. |

사용할 마케팅 작업을 찾으면 해당 `href` 속성의 값을 기록합니다. 이 값은 정책을 [만드는 다음 단계에서 사용됩니다](#create-policy).

### Create a new marketing action {#create-new}

종단점에 PUT 요청을 만들고 요청 경로 끝에 마케팅 `/marketingActions/custom/` 작업의 이름을 제공하여 새 마케팅 작업을 만들 수 있습니다.

**API 형식**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 만들려는 새 마케팅 작업의 이름입니다. 이 이름은 마케팅 작업의 기본 식별자 역할을 하므로 고유해야 합니다. 가장 좋은 방법은 마케팅 활동에 설명적이지만 간결하게 지정하는 것입니다. |

**요청**

다음 요청은 &quot;exportToThirdParty&quot;라는 새 사용자 지정 마케팅 작업을 만듭니다. 요청 페이로드 `name` 의 이름이 요청 경로에 제공된 이름과 동일하다는 점을 참고하십시오.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 만들려는 마케팅 작업의 이름입니다. 이 이름은 요청 경로에 제공된 이름과 일치해야 합니다. 그렇지 않으면 400(잘못된 요청) 오류가 발생합니다. |
| `description` | 마케팅 활동에 대한 사람이 읽을 수 있는 설명입니다. |

**응답**

성공적인 응답은 HTTP 상태 201(만들음)과 새로 만든 마케팅 작업의 세부 정보를 반환합니다.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{IMS_ORG}",
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
| `_links.self.href` | 마케팅 작업의 URI ID입니다. |

정책을 만드는 다음 단계에서 사용되므로 새로 만든 마케팅 작업의 URI ID를 기록합니다.

## 정책 만들기 {#create-policy}

새 정책을 만들려면 마케팅 작업을 금지하는 사용 레이블 표현식과 함께 마케팅 작업의 URI ID를 제공해야 합니다.

이 식을 정책 표현식이라고 하며 (A) 레이블 또는 (B) 연산자와 피연산자가 들어 있지만 둘 다 포함하는 개체입니다. 또한 각 피연산자는 정책 표현식 개체이기도 합니다. 예를 들어 레이블이 있는 경우 데이터 제3자로 내보내기에 관한 정책을 사용할 수 `C1 OR (C3 AND C7)` 없습니다. 이 식은 다음과 같이 지정됩니다.

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

정책 표현식을 구성한 후에는 끝점에 POST 요청을 만들어 새 정책을 만들 수 `/policies/custom` 있습니다.

**API 형식**

```http
POST /policies/custom
```

**요청**

다음 요청은 요청 페이로드에서 마케팅 작업 및 정책 표현식을 제공하여 &quot;데이터를 제3자로 내보내기&quot;라는 정책을 만듭니다.

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
| `marketingActionRefs` | 마케팅 작업의 `href` 값이 들어 있는 배열이며 [이전 단계에서 얻습니다](#define-action). 위의 예는 하나의 마케팅 작업만 나열하지만 여러 작업을 제공할 수도 있습니다. |
| `deny` | 정책 표현식 개체입니다. 정책에서 에서 참조되는 마케팅 작업을 거부하는 사용 레이블 및 조건을 정의합니다 `marketingActionRefs`. |

**응답**

성공적인 응답은 HTTP 상태 201(만들음)과 새로 만든 정책의 세부 정보를 반환합니다.

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
    "imsOrg": "{IMS_ORG}",
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
| `id` | 정책을 고유하게 식별하는 읽기 전용 시스템 생성 값. |

다음 단계에서 정책을 활성화하는 데 사용되므로 새로 만든 정책의 URI ID를 기록합니다.

## 정책 사용

>[!NOTE]
>
>정책을 `DRAFT` 상태로 유지하려면 이 단계는 선택 사항이지만, 평가에 참여하려면 기본적으로 정책에 해당 상태가 설정되어 있어야 `ENABLED` 합니다. 정책에 대한 예외를 만드는 방법에 대한 자세한 내용은 [정책](../enforcement/api-enforcement.md) 집행에 대한 `DRAFT` 가이드를 참조하십시오.

기본적으로 속성이 설정된 정책은 평가에 참여하지 `status` `DRAFT` 않습니다. 종단점에 PATCH 요청을 만들고 요청 경로 끝에 정책에 대한 고유 식별자를 제공하여 정책을 평가하도록 할 수 있습니다. `/policies/custom/`

**API 형식**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{POLICY_ID}` | 활성화할 정책의 `id` 값. |

**요청**

다음 요청은 정책의 속성에 대한 PATCH 작업 `status` 을 수행하여 해당 값을 에서 (으)로 변경합니다 `DRAFT` `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `path` | 업데이트할 필드의 경로입니다. 정책을 활성화할 때는 값을 &quot;/status&quot;로 설정해야 합니다. |
| `value` | 에 지정된 속성에 할당할 새 값 `path`. 이 요청은 정책의 `status` 속성을 &quot;ENABLED&quot;로 설정합니다. |

**응답**

성공적인 응답은 HTTP 상태 200(OK) 및 업데이트된 정책의 세부 정보를 `status` 이제 로 설정합니다 `ENABLED`.

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
    "imsOrg": "{IMS_ORG}",
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

이 튜토리얼을 따라 마케팅 작업에 대한 데이터 사용 정책을 만들었습니다. 이제 데이터 사용 정책 [을](../enforcement/api-enforcement.md) 적용하는 튜토리얼에서 정책 위반을 확인하고 경험 애플리케이션에서 이를 처리하는 방법을 배울 수 있습니다.

API에서 사용 가능한 다양한 작업에 대한 자세한 내용은 [!DNL Policy Service] 정책 서비스 개발자 안내서를 참조하십시오 [](../api/getting-started.md). 데이터에 대한 정책을 적용하는 방법에 대한 자세한 내용은 대상 세그먼트에 대한 데이터 사용 규정 [!DNL Real-time Customer Profile] 준수 적용 자습서를 참조하십시오 [](../../segmentation/tutorials/governance.md).

사용자 인터페이스에서 사용 정책을 관리하는 방법에 대한 자세한 내용은 [!DNL Experience Platform] 정책 사용 설명서를 참조하십시오 [](user-guide.md).