---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 정책
topic: developer guide
translation-type: tm+mt
source-git-commit: 2997243622a7483ae23e21487128cea6badecb80

---


# 정책 평가

마케팅 작업이 생성되어 정책이 정의되면 정책 서비스 API를 사용하여 특정 작업으로 인해 정책이 위반되는지 평가할 수 있습니다. 반환된 제약 조건은 데이터 사용 레이블이 들어 있는 지정된 데이터에 대한 마케팅 작업을 시도하면 위반될 일련의 정책을 가져옵니다.

기본적으로 상태가 &quot;ENABLED&quot;로 설정된 **정책만 평가에**&#x200B;참여하지만 쿼리 매개 변수를 사용하여 &quot;DRAFT&quot; 정책을 평가에 `?includeDraft=true` 포함할 수 있습니다.

평가 요청은 다음 세 가지 방법 중 하나로 수행할 수 있습니다.

1. 데이터 사용 레이블 및 마케팅 활동이 있는 경우, 이러한 조치가 정책을 위반합니까?
1. 하나 이상의 데이터 세트와 마케팅 활동이 있는 경우, 이러한 조치가 정책을 위반합니까?
1. 하나 이상의 데이터 집합과 이러한 데이터 세트 내에 하나 이상의 필드의 하위 세트가 있는 경우 작업이 정책을 위반합니까?

## 데이터 사용 레이블 및 마케팅 작업을 사용하여 정책 평가

데이터 사용 레이블이 존재함을 기반으로 정책 위반을 평가하려면 요청 중에 데이터에 표시할 레이블 세트를 지정해야 합니다. 이 작업은 쿼리 매개 변수를 사용하여 수행됩니다. 여기서 데이터 사용 레이블은 다음 예와 같이 쉼표로 구분된 값 목록으로 제공됩니다.

**API 형식**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**요청**

아래 예제 요청은 레이블 C1 및 C3에 대해 마케팅 작업을 평가합니다. 데이터 사용 레이블을 사용하여 정책을 평가할 때는 다음 사항에 유의하십시오.
* **데이터 사용 레이블은 대/소문자를 구분합니다.** 위에 표시된 요청은 위반된 정책을 반환하는 반면, 소문자 레이블을 사용하여 동일한 요청을 합니다(예:( `"c1,c3"`, `"C1,c3"`, `"c1,C3"`)는 그렇지 않습니다.
* **정책 표현식의`AND`및`OR`연산자에 주의하십시오.** 이 예에서, 요청에 레이블(`C1` 또는 `C3`)이 단독으로 표시되었다면 마케팅 작업이 이 정책을 위반하지 않았을 것입니다. 위반된 정책을 반환하려면 두 레이블(`C1 AND C3`)이 필요합니다. 정책을 신중하게 평가하고 동일한 주의를 기울여 정책 표현식을 정의하는지 확인합니다.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 객체에는 요청에서 전송된 레이블과 일치해야 하는 `duleLabels` 배열이 포함됩니다. 데이터 사용 레이블에 대해 지정된 마케팅 작업을 수행하는 경우 해당 `violatedPolicies` 배열에 영향을 받는 정책(또는 정책)의 세부 사항이 포함됩니다. 정책을 위반하지 않으면 `violatedPolicies` 배열이 비어 있는 것으로 표시됩니다(`[]`).

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
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
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
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

## 데이터 세트 및 마케팅 활동을 사용하여 정책 평가

데이터 사용 레이블을 수집할 수 있는 하나 이상의 데이터 세트에 대한 ID를 지정하여 정책 위반을 평가할 수도 있습니다. 이 작업은 마케팅 작업에 대한 코어 또는 사용자 지정 `/constraints` 끝점에 대한 POST 요청을 수행하고 아래와 같이 요청 본문 내에 데이터 집합 ID를 지정하여 수행됩니다.

**API 형식**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**요청**

요청 본문에는 각 데이터 집합 ID에 대한 개체가 포함된 배열이 포함되어 있습니다. 요청 본문을 전송하므로 &quot;Content-Type:다음 예와 같이 application/json&quot; 요청 헤더가 필요합니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

**응답**

응답 개체에는 지정된 데이터 집합 내에 있는 모든 레이블의 통합 목록이 포함된 `duleLabels` 배열이 포함됩니다. 이 목록에는 데이터 세트 내의 모든 필드에 데이터 세트 및 필드 수준 레이블이 포함되어 있습니다.

또한 응답에는 각 데이터 세트에 대한 개체가 들어 있는 `discoveredLabels` 배열이 포함되어 있으며 데이터 세트 및 필드 수준 레이블로 `datasetLabels` 분류되어 있습니다. 각 필드 수준 레이블에는 해당 레이블이 있는 특정 필드의 경로가 표시됩니다.

지정된 마케팅 작업이 데이터 집합 `duleLabels` 내의 와 관련된 정책을 위반하는 경우, `violatedPolicies` 배열에 영향을 받는 정책(또는 정책)의 세부 정보가 포함됩니다. 정책을 위반하지 않으면 `violatedPolicies` 배열이 비어 있는 것으로 표시됩니다(`[]`).

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
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
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

## 데이터 세트, 필드 및 마케팅 활동을 사용하여 정책 평가

하나 이상의 데이터 집합 ID를 제공하는 것 외에도 각 데이터 집합 내에서 필드 하위 집합을 지정할 수 있으므로 해당 필드의 데이터 사용 레이블만 평가해야 합니다. 데이터 집합만 포함하는 POST 요청과 유사하게, 이 요청은 각 데이터 세트에 대한 특정 필드를 요청 본문에 추가합니다.

데이터 집합 필드를 사용하여 정책을 평가할 때는 다음 사항에 유의하십시오.

* **필드 이름은 대/소문자를 구분합니다.** 필드를 제공할 때는 데이터 세트에 표시되는 대로 정확하게 작성해야 합니다(예: `firstName` vs `firstname`).
* **데이터 집합 레이블 상속입니다.** 데이터 사용 레이블은 여러 수준에서 적용할 수 있으며 아래로 상속됩니다. 정책 평가가 예상한 대로 반환되지 않는 경우 필드 수준에서 적용된 레이블 외에 데이터 세트에서 필드로 상속된 레이블을 확인하십시오.

**API 형식**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**요청**

요청 본문에는 각 데이터 집합 ID에 대한 개체가 포함된 배열과 평가에 사용해야 하는 해당 데이터 집합 내의 필드 하위 집합이 포함되어 있습니다. 요청 본문을 전송하므로 &quot;Content-Type:다음 예와 같이 application/json&quot; 요청 헤더가 필요합니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

**응답**

응답 객체에는 지정된 필드에 있는 레이블의 통합 목록이 포함된 `duleLabels` 배열이 포함됩니다. 여기에는 데이터 세트 레이블도 포함되며, 이러한 레이블은 필드에 상속됩니다.

제공된 필드의 데이터에 대해 지정된 마케팅 작업을 수행함으로써 정책을 위반하는 경우, `violatedPolicies` 배열에 영향을 받는 정책(또는 정책)의 세부 사항이 포함됩니다. 정책을 위반하지 않으면 `violatedPolicies` 배열이 비어 있는 것으로 표시됩니다(`[]`).

아래 응답에서 이제 요청 본문에 지정된 필드만 포함되므로 각 데이터 세트에 대한 목록과 `duleLabels` 같이 목록의 `discoveredLabels` 단축을 확인할 수 있습니다. 이전에 위반된 정책인 &quot;타깃팅 광고 또는 컨텐츠&quot;가 두 `C4 AND C6` 레이블을 모두 필요로 하므로 더 이상 위반이 발생하지 않으며 `violatedPolicies` 배열이 비어 있는 것으로 나타납니다.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
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
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
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
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## 실시간 고객 프로파일을 위한 정책 평가

정책 서비스 API를 사용하여 실시간 고객 프로필 세그먼트 사용과 관련된 정책 위반을 확인할 수도 있습니다. 자세한 내용은 대상 세그먼트에 [](../../segmentation/tutorials/governance.md) 대한 데이터 사용 규정 준수 적용에 대한 자습서를 참조하십시오.