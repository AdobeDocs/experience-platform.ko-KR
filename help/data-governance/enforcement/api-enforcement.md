---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 정책 서비스 API를 사용하여 데이터 사용 정책 적용
topic: enforcement
translation-type: tm+mt
source-git-commit: 3e5245a718295cc5318c277a5cf9ee71da2a911b

---


# 정책 서비스 API를 사용하여 데이터 사용 정책 적용

데이터에 대한 데이터 사용 레이블을 만들고 해당 레이블에 대한 마케팅 작업에 대한 사용 정책을 만들었다면 DULE Policy Service API를 사용하여 데이터 [세트에](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) 대해 수행된 마케팅 작업 또는 임의 레이블 그룹이 정책 위반을 구성하는지 평가할 수 있습니다. 그런 다음 자체 내부 프로토콜을 설정하여 API 응답을 기반으로 정책 위반을 처리할 수 있습니다.

>[!NOTE] 기본적으로 상태가 설정되는 정책만 평가에 참여할 `ENABLED` 수 있습니다. 정책이 평가에 참여하도록 `DRAFT` 허용하려면 쿼리 매개 변수를 요청 `includeDraft=true` 경로에 포함해야 합니다.

이 문서에서는 정책 서비스 API를 사용하여 다른 시나리오에서 정책 위반을 확인하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서에서는 DULE 정책 시행과 관련된 다음 주요 개념을 제대로 이해해야 합니다.

* [데이터 거버넌스](../home.md):Platform이 데이터 사용 규정을 적용하는 프레임워크
   * [데이터 사용 레이블](../labels/overview.md):데이터 사용 레이블은 데이터 집합(및/또는 해당 데이터 집합 내의 개별 필드)에 적용되어 데이터 사용 방법에 대한 제한을 지정합니다.
   * [데이터 사용 정책](../policies/overview.md):데이터 사용 정책은 특정 DULE 레이블 세트에 대해 허용되거나 제한되는 마케팅 작업의 종류를 설명하는 규칙입니다.
* [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이 자습서를 시작하기 전에 [개발자 가이드에서](../api/getting-started.md) 필수 헤더 및 예제 API 호출 방법을 포함하여 DULE Policy Service API를 성공적으로 호출하기 위해 알아야 할 중요한 정보를 검토하십시오.

## DULE 레이블 및 마케팅 작업 사용 평가

데이터 세트 내에 있다고 가정할 일련의 DULE 레이블에 대해 마케팅 작업을 테스트하여 정책을 평가할 수 있습니다. 이 작업은 `duleLabels` 쿼리 매개 변수를 사용하여 수행됩니다. 여기서 DULE 레이블은 아래 예와 같이 쉼표로 구분된 값 목록으로 제공됩니다.

**API 형식**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 평가 중인 DULE 정책과 연관된 마케팅 작업의 이름. |
| `{LABEL_1}` | 마케팅 작업을 테스트할 데이터 사용 레이블입니다. 하나 이상의 레이블을 제공해야 합니다. 여러 레이블을 제공할 때는 쉼표로 구분해야 합니다. |

**요청**

다음 요청은 레이블과 `exportToThirdParty` `C1` `C3`관련하여 마케팅 작업을 테스트합니다. 이 자습서에서 이전에 만든 데이터 사용 정책은 레이블을 해당 정책 표현식의 조건 중 하나로 정의하므로 마케팅 작업은 정책 위반을 트리거해야 합니다. `C1` `deny`

>[!NOTE] 데이터 사용 레이블은 대/소문자를 구분합니다. 정책 위반은 정책 표현식에 정의된 레이블이 정확히 일치할 때만 발생합니다. 이 예에서 레이블은 `C1` 위반을 트리거하지만 `c1` 레이블은 그렇지 않습니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 마케팅 작업에 대한 URL, 테스트된 DULE 레이블 및 해당 레이블에 대한 작업을 테스트한 결과 위반된 DULE 정책 목록을 반환합니다. 이 예에서는 마케팅 작업으로 예상되는 정책 위반이 발생했음을 나타내는 &quot;데이터를 타사(Export Data to Third Party)&quot; 정책이 `violatedPolicies` 배열에 표시됩니다.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
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
| `violatedPolicies` | 제공된 항목에 대한 마케팅 작업(에 `marketingActionRef`지정됨)을 테스트하여 위반된 DULE 정책을 나열하는 `duleLabels`배열입니다. |

## 데이터 집합 사용 평가

DULE 레이블을 수집할 수 있는 하나 이상의 데이터 세트에 대해 마케팅 작업을 테스트하여 DULE 정책을 평가할 수 있습니다. 이 작업은 아래 예와 같이 요청 본문 내에 데이터 세트 ID를 제공하고 POST 요청을 `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` 수행하여 수행됩니다.

**API 형식**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 평가 중인 DULE 정책과 연관된 마케팅 작업의 이름. |

**요청**

다음 요청은 세 개의 서로 다른 데이터 세트에 대해 `exportToThirdParty` 마케팅 작업을 테스트합니다. 데이터 세트는 페이로드에 제공된 배열에서 유형 및 ID로 참조됩니다.

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
      "entityId": "5c423dc25f2f2e00005e2319"
    },
    {
      "entityType": "dataSet",
      "entityId": "5cc323e15410ef14b749481e"
    },
    {
      "entityType": "dataSet",
      "entityId": "5cc1fb685410ef14b748c55f"
    }
  ]'
```

| 속성 | 설명 |
| --- | --- |
| `entityType` | 페이로드 배열의 각 항목은 정의된 엔티티 유형을 나타내야 합니다. 이 사용 사례의 경우 값은 항상 &quot;dataSet&quot;이 됩니다. |
| `entityId` | 페이로드 배열의 각 항목은 데이터 세트에 대한 고유 ID를 제공해야 합니다. |

**응답**

성공적인 응답은 마케팅 작업에 대한 URL, 제공된 데이터 세트에서 수집된 DULE 레이블 및 해당 레이블에 대한 작업을 테스트한 결과 위반된 DULE 정책 목록을 반환합니다. 이 예에서는 마케팅 작업으로 예상되는 정책 위반이 발생했음을 나타내는 &quot;데이터를 타사(Export Data to Third Party)&quot; 정책이 `violatedPolicies` 배열에 표시됩니다.

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
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
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
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
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
            "entityId": "5cc1fb685410ef14b748c55f",
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
| `duleLabels` | 요청 페이로드에 제공된 데이터 세트에서 추출된 DULE 레이블 목록입니다. |
| `discoveredLabels` | 요청 페이로드에 제공된 데이터 집합 목록으로, 각 데이터세트에 있는 데이터 집합 수준 및 필드 수준 DULE 레이블이 표시됩니다. |
| `violatedPolicies` | 제공된 항목에 대한 마케팅 작업(에 `marketingActionRef`지정됨)을 테스트하여 위반된 DULE 정책을 나열하는 `duleLabels`배열입니다. |

## 다음 단계

이 문서를 읽으면 데이터 세트 또는 DULE 레이블 세트에 대한 마케팅 작업을 수행할 때 정책 위반을 확인하는 데 성공했습니다. API 응답에서 반환되는 데이터를 사용하면 경험 애플리케이션 내에서 프로토콜을 설정하여 정책 위반이 발생할 때 적절히 적용할 수 있습니다.

실시간 고객 프로필에서 고객 세그먼트에 대한 데이터 사용 정책을 적용하는 방법에 대한 단계는 다음 [자습서를](../../segmentation/tutorials/governance.md)참조하십시오.