---
keywords: Experience Platform;홈;인기 항목;정책 적용;자동 적용;API 기반 적용;데이터 거버넌스
solution: Experience Platform
title: 정책 평가 API 끝점
topic-legacy: developer guide
description: 마케팅 작업이 생성되고 정책이 정의되면 정책 서비스 API를 사용하여 특정 작업에 의해 정책이 위반되는지 평가할 수 있습니다. 반환된 제약 조건은 데이터 사용 레이블이 포함된 지정된 데이터에 대한 마케팅 작업을 시도하여 위반될 정책 집합을 만듭니다.
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 1%

---

# 정책 평가 끝점

마케팅 작업이 생성되고 데이터 사용 정책이 정의된 후에는 [!DNL Policy Service] 특정 작업에 의해 정책이 위반되는지 평가하는 API입니다. 반환된 제약 조건은 데이터 사용 레이블이 포함된 지정된 데이터에 대한 마케팅 작업을 시도하여 위반될 정책 집합을 만듭니다.

기본적으로 상태가 로 설정된 정책만 `ENABLED` 평가에 참여합니다. 그러나 쿼리 매개 변수를 사용할 수 있습니다 `?includeDraft=true` 다음을 포함합니다. `DRAFT` 평가 정책.

평가 요청은 다음 세 가지 방법 중 하나로 수행할 수 있습니다.

1. 마케팅 작업과 데이터 사용 레이블 세트가 있는 경우 작업이 정책을 위반합니까?
1. 마케팅 작업과 하나 이상의 데이터 세트가 있는 경우 작업이 정책을 위반합니까?
1. 마케팅 작업, 하나 이상의 데이터 세트 및 이러한 각 데이터 세트 내에 있는 하나 이상의 필드의 하위 세트가 있는 경우 작업이 정책을 위반합니까?

## 시작하기

이 안내서에서 사용되는 API 엔드포인트는 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 계속하기 전에 [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 모든 호출을 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다 [!DNL Experience Platform] API.

## 데이터 사용 레이블을 사용하여 정책 위반 평가 {#labels}

를 사용하여 특정 데이터 사용 레이블 세트가 있는지에 따라 정책 위반을 평가할 수 있습니다 `duleLabels` GET 요청의 쿼리 매개 변수.

**API 형식**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 데이터 사용 레이블 세트에 대해 테스트할 마케팅 작업의 이름입니다. 를 만들어 사용 가능한 마케팅 작업 목록을 검색할 수 있습니다 [마케팅 작업 엔드포인트에 대한 GET 요청](./marketing-actions.md#list). |
| `{LABELS_LIST}` | 마케팅 작업을 테스트할 데이터 사용량 레이블 이름의 쉼표로 구분된 목록입니다. 예: `duleLabels=C1,C2,C3`<br><br>레이블 이름은 대/소문자를 구분합니다. 에서 대/소문자를 구분하고 `duleLabels` 매개 변수. |

**요청**

아래 예제 요청은 레이블 C1 및 C3에 대해 마케팅 작업을 평가합니다.

>[!IMPORTANT]
>
>다음 사항에 유의하십시오 `AND` 및 `OR` 정책 표현식의 연산자 아래 예제에서 레이블(`C1` 또는 `C3`)은 요청에서 외상으로 나타났으며 마케팅 조치가 이 정책을 위반하지는 않았을 것입니다. 두 레이블을 모두 사용합니다(`C1` 및 `C3`) 위반된 정책을 반환합니다. 정책을 신중하게 평가하고 정책 표현식을 동일한 수준으로 정의하는지 확인합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 다음이 포함됩니다 `violatedPolicies` 제공된 레이블에 대해 마케팅 작업을 수행한 결과 위반된 정책의 세부 정보가 포함된 배열입니다. 위반된 정책이 없으면 `violatedPolicies` 배열이 비어 있습니다.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## 데이터 세트를 사용하여 정책 위반 평가 {#datasets}

데이터 사용 레이블을 수집할 수 있는 하나 이상의 데이터 세트 세트를 기준으로 정책 위반을 평가할 수 있습니다. 이 작업은 POST 요청을 `/constraints` 특정 마케팅 활동에 대한 종단점 및 요청 본문 내에 데이터 세트 ID 목록을 제공합니다.

**API 형식**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 하나 이상의 데이터 세트에 대해 테스트할 마케팅 작업의 이름입니다. 를 만들어 사용 가능한 마케팅 작업 목록을 검색할 수 있습니다 [마케팅 작업 엔드포인트에 대한 GET 요청](./marketing-actions.md#list). |

**요청**

다음 요청은 를 수행합니다 `crossSiteTargeting` 모든 정책 위반을 평가하기 위해 데이터 세트 3개에 대한 마케팅 작업입니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | 동위 항목에 ID가 표시된 엔티티의 유형입니다 `entityId` 속성을 사용합니다. 현재 허용되는 값은 `dataSet`. |
| `entityId` | 마케팅 작업을 테스트할 데이터 세트의 ID입니다. 데이터 세트에 대한 GET 요청을 수행하여 데이터 세트 및 해당 ID 목록을 가져올 수 있습니다 `/dataSets` 의 엔드포인트 [!DNL Catalog Service] API. 다음 안내서를 참조하십시오. [목록 [!DNL Catalog] 개체](../../catalog/api/list-objects.md) 추가 정보. |

**응답**

성공적인 응답에는 다음이 포함됩니다 `violatedPolicies` 제공된 데이터 세트에 대해 마케팅 작업을 수행한 결과로 위반된 정책의 세부 사항을 포함하는 배열입니다. 위반된 정책이 없으면 `violatedPolicies` 배열이 비어 있습니다.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

| 속성 | 설명 |
| --- | --- |
| `duleLabels` | 응답 개체에는 다음이 포함됩니다 `duleLabels` 지정된 데이터 세트에 있는 모든 레이블의 통합 목록을 포함하는 배열입니다. 이 목록에는 데이터 집합 내의 모든 필드에 데이터 집합 및 필드 수준 레이블이 포함되어 있습니다. |
| `discoveredLabels` | 응답에는 `discoveredLabels` 각 데이터 세트에 대한 개체를 포함하는 배열, 표시 `datasetLabels` 데이터 세트 및 필드 수준 레이블로 분류됩니다. 각 필드 수준 레이블에는 해당 레이블이 있는 특정 필드의 경로가 표시됩니다. |

## 특정 데이터 집합 필드를 사용하여 정책 위반 평가 {#fields}

하나 이상의 데이터 세트 내에서 필드 하위 집합을 기반으로 정책 위반을 평가할 수 있으므로 해당 필드에 적용된 데이터 사용 레이블만 평가됩니다.

데이터 집합 필드를 사용하여 정책을 평가할 때는 다음 사항에 유의하십시오.

* **필드 이름은 대/소문자를 구분합니다**: 필드를 제공할 때는 데이터 세트에 나타나는 대로 정확히 작성해야 합니다(예: `firstName` vs `firstname`).
* **데이터 집합 레이블 상속**: 데이터 집합에 있는 개별 필드는 데이터 집합 수준에서 적용된 모든 레이블을 상속합니다. 정책 평가가 예상대로 반환되지 않는 경우 필드 수준에서 적용된 레이블 외에 데이터 세트 수준에서 필드로 상속되었을 수 있는 레이블을 확인해야 합니다.

**API 형식**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 데이터 집합 필드의 하위 집합에 대해 테스트할 마케팅 작업의 이름입니다. 를 만들어 사용 가능한 마케팅 작업 목록을 검색할 수 있습니다 [마케팅 작업 엔드포인트에 대한 GET 요청](./marketing-actions.md#list). |

**요청**

다음 요청은 마케팅 작업을 테스트합니다 `crossSiteTargeting` 를 설정하는 것이 좋습니다. 페이로드는 와 유사합니다 [데이터 세트만 포함된 평가 요청](#datasets), 레이블을 수집할 각 데이터 세트에 대한 특정 필드를 추가합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| 속성 | 설명 |
| --- | --- |
| `entityType` | 동위 항목에 ID가 표시된 엔티티의 유형입니다 `entityId` 속성을 사용합니다. 현재 허용되는 값은 `dataSet`. |
| `entityId` | 마케팅 작업에 대해 필드를 평가할 데이터 세트의 ID입니다. 데이터 세트에 대한 GET 요청을 수행하여 데이터 세트 및 해당 ID 목록을 가져올 수 있습니다 `/dataSets` 의 엔드포인트 [!DNL Catalog Service] API. 다음 안내서를 참조하십시오. [목록 [!DNL Catalog] 개체](../../catalog/api/list-objects.md) 추가 정보. |
| `entityMeta.fields` | JSON 포인터 문자열 형태로 제공되는 데이터 세트의 스키마 내의 특정 필드에 대한 경로 배열입니다. 의 섹션을 참조하십시오. [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 를 참조하십시오. |

**응답**

성공적인 응답에는 다음이 포함됩니다 `violatedPolicies` 제공된 데이터 세트 필드에 대해 마케팅 작업을 수행한 결과로 위반된 정책의 세부 사항을 포함하는 배열입니다. 위반된 정책이 없으면 `violatedPolicies` 배열이 비어 있습니다.

아래 예제 응답을 와 비교 [데이터 세트만 포함된 응답](#datasets)수집된 레이블 목록이 더 짧습니다. 다음 `discoveredLabels` 요청 본문에 지정된 필드만 포함되므로 각 데이터 세트에 대해서도 감소했습니다. 또한, 이전에 위반되었던 정책 `Targeting Ads or Content` 둘 다 필요 `C4 AND C6` 표시할 레이블이며, 따라서 는 더 이상 비어 있는 `violatedPolicies` 배열입니다.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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

## 일괄 정책 평가 {#bulk}

다음 `/bulk-eval` 엔드포인트를 사용하면 단일 API 호출에서 여러 평가 작업을 실행할 수 있습니다.

**API 형식**

```http
POST /bulk-eval
```

**요청**

벌크 평가 요청의 페이로드는 개체 배열이어야 합니다. 수행할 각 평가 작업에 대해 하나씩 수행합니다. 데이터 세트 및 필드를 기반으로 하여 평가하는 작업의 경우, `entityList` 배열을 제공해야 합니다. 데이터 사용 레이블을 기준으로 평가하는 작업의 경우, `labels` 배열을 제공해야 합니다.

>[!WARNING]
>
>나열된 평가 작업에 `entityList` 그리고 `labels` array로 설정하면 오류가 발생합니다. 데이터 세트와 레이블을 모두 기반으로 동일한 마케팅 작업을 평가하려면 해당 마케팅 작업에 대해 별도의 평가 작업을 포함해야 합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| 속성 | 설명 |
| --- | --- |
| `evalRef` | 정책 위반에 대한 레이블 또는 데이터 세트에 대해 테스트하는 마케팅 작업의 URI입니다. |
| `includeDraft` | 기본적으로 활성화된 정책만 평가에 참여합니다. If `includeDraft` 가 로 설정되어 있습니다. `true`에 있는 정책 `DRAFT` 상태도 참여합니다. |
| `labels` | 마케팅 작업을 테스트할 데이터 사용 레이블의 배열입니다.<br><br>**중요 사항**: 이 속성을 사용하는 경우 `entityList` 속성은 동일한 개체에 포함되지 않아야 합니다. 데이터 세트 및/또는 필드를 사용하여 동일한 마케팅 작업을 평가하려면 를 포함하는 요청 페이로드에 별도의 개체를 포함해야 합니다 `entityList` 배열입니다. |
| `entityList` | 마케팅 작업을 테스트할 데이터 세트 및 해당 데이터 세트 내의 특정 필드(선택 사항) 배열입니다.<br><br>**중요 사항**: 이 속성을 사용하는 경우 `labels` 속성은 동일한 개체에 포함되지 않아야 합니다. 특정 데이터 사용 레이블을 사용하여 동일한 마케팅 작업을 평가하려면 를 포함하는 요청 페이로드에 별도의 개체를 포함해야 합니다 `labels` 배열입니다. |
| `entityType` | 마케팅 작업을 테스트할 엔티티 유형입니다. 현재, 전용 `dataSet` 가 지원됩니다. |
| `entityId` | 마케팅 작업을 테스트할 데이터 세트의 ID입니다. |
| `entityMeta.fields` | (선택 사항) 마케팅 작업을 테스트할 데이터 세트 내의 특정 필드 목록입니다. |

**응답**

성공적인 응답은 일련의 평가 결과를 반환합니다. 요청에서 전송된 각 정책 평가 작업에 대해 하나씩 표시됩니다.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{ORG_ID}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## 정책 평가 [!DNL Real-Time Customer Profile]

다음 [!DNL Policy Service] API를 사용하여 [!DNL Real-Time Customer Profile] 세그먼트 를 참조하십시오. 다음에서 자습서를 참조하십시오. [대상 세그먼트에 대한 데이터 사용 규정 준수 적용](../../segmentation/tutorials/governance.md) 추가 정보.
