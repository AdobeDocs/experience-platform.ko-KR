---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance;testing
solution: Experience Platform
title: 정책 서비스 API를 사용하여 데이터 사용 정책 적용
topic: enforcement
type: Tutorial
description: 데이터에 대한 데이터 사용 레이블을 만들고 해당 레이블에 대한 마케팅 작업에 대한 사용 정책을 만들었다면 정책 서비스 API를 사용하여 데이터 세트에 대해 수행된 마케팅 작업 또는 임의 레이블 그룹이 정책 위반인지 여부를 평가할 수 있습니다. 그런 다음 API 응답을 기반으로 정책 위반을 처리하도록 자체 내부 프로토콜을 설정할 수 있습니다.
translation-type: tm+mt
source-git-commit: 00688e271b3c1e3ad1a17ceb6045e3316bd65961
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---


# API를 사용하여 데이터 사용 정책 [!DNL Policy Service] 적용

데이터에 대한 데이터 사용 레이블을 만들고 해당 레이블에 대한 마케팅 작업에 대한 사용 정책을 만들었으면 데이터 세트 또는 임의 레이블 그룹에 대해 수행된 마케팅 작업이 정책 위반인지 여부를 평가하는 데 이 [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) 를 사용할 수 있습니다. 그런 다음 API 응답을 기반으로 정책 위반을 처리하도록 자체 내부 프로토콜을 설정할 수 있습니다.

>[!NOTE]
>
>기본적으로 상태가 설정된 정책만 평가에 참여할 `ENABLED` 수 있습니다. 정책이 평가에 참여할 수 있도록 `DRAFT` 하려면 요청 경로 `includeDraft=true` 에 쿼리 매개 변수를 포함해야 합니다.

이 문서에서는 API를 사용하여 다양한 시나리오에서 정책 위반을 확인하는 방법에 대한 단계를 제공합니다. [!DNL Policy Service]

## 시작하기

이 자습서에서는 데이터 사용 정책을 적용하는 데 관련된 다음 주요 개념을 제대로 이해해야 합니다.

* [데이터 거버넌스](../home.md):데이터 사용 규정 준수를 [!DNL Platform] 적용하는 프레임워크입니다.
   * [데이터 사용 레이블](../labels/overview.md):데이터 사용 레이블은 데이터 집합(및/또는 해당 데이터 집합 내의 개별 필드)에 적용되며 데이터 사용 방법에 대한 제한을 지정합니다.
   * [데이터 사용 정책](../policies/overview.md):데이터 사용 정책은 특정 데이터 사용 레이블 세트에 대해 허용되거나 제한된 마케팅 작업의 종류를 설명하는 규칙입니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이 자습서를 시작하기 전에 필수 헤더 및 예제 API 호출 읽기 방법 등 [API를 성공적으로 호출하기 위해 알아야 할 중요한 정보가 있는](../api/getting-started.md) 개발자 가이드를 [!DNL Policy Service] 검토하십시오.

## 레이블 및 마케팅 활동 사용 평가

데이터 세트 내에 있다고 가정할 데이터 사용 레이블 세트에 대해 마케팅 작업을 테스트하여 정책을 평가할 수 있습니다. 이 작업은 아래 예제와 같이 레이블이 쉼표로 구분된 값 목록으로 제공되는 `duleLabels` 쿼리 매개 변수를 사용하여 수행됩니다.

**API 형식**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 평가하고 있는 데이터 사용 정책과 연관된 마케팅 작업의 이름. |
| `{LABEL_1}` | 마케팅 작업을 테스트하는 데이터 사용 레이블입니다. 하나 이상의 레이블을 제공해야 합니다. 여러 레이블을 제공할 때는 쉼표로 구분해야 합니다. |

**요청**

다음 요청은 레이블 및 `exportToThirdParty` 에 대해 마케팅 작업을 `C1` 테스트합니다 `C3`. 이 자습서에서 이전에 작성한 데이터 사용 정책은 레이블을 해당 정책 표현식에 있는 조건 중 하나로 `C1` `deny` 정의하므로 마케팅 작업에서 정책 위반을 트리거해야 합니다.

>[!NOTE]
>
>데이터 사용 레이블은 대/소문자를 구분합니다. 정책 위반은 정책 표현식에 정의된 레이블이 정확히 일치하는 경우에만 발생합니다. 이 예에서 레이블은 `C1` 위반을 트리거하지만 레이블은 그렇지 `c1` 않습니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 마케팅 작업에 대한 URL, 테스트된 사용 레이블 및 해당 레이블에 대한 작업을 테스트한 결과 위반된 정책 목록을 반환합니다. 이 예에서 &quot;데이터를 제3자로 내보내기&quot; 정책은 마케팅 작업이 예상 정책 위반을 트리거했음을 나타내는 `violatedPolicies` 배열에 표시됩니다.

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
| `violatedPolicies` | 제공된 항목에 대해 마케팅 작업(지정된)을 테스트하여 위반된 정책 `marketingActionRef`을 나열하는 배열입니다 `duleLabels`. |

## 데이터 세트를 사용하여 평가

레이블을 수집할 수 있는 하나 이상의 데이터 세트에 대해 마케팅 작업을 테스트하여 데이터 사용 정책을 평가할 수 있습니다. 이 작업은 아래 예와 같이 요청 본문 내에 데이터 세트 ID에 POST `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` 를 요청하고 제공하여 수행됩니다.

**API 형식**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 평가하고 있는 정책과 연관된 마케팅 작업의 이름. |

**요청**

다음 요청은 세 개의 서로 다른 데이터 세트에 대해 `exportToThirdParty` 마케팅 작업을 테스트합니다. 데이터 세트는 페이로드에서 제공하는 배열에서 유형 및 ID로 참조됩니다.

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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| 속성 | 설명 |
| --- | --- |
| `entityType` | 페이로드 배열의 각 항목은 정의되는 엔티티 유형을 나타내야 합니다. 이 경우 값은 항상 &quot;dataSet&quot;입니다. |
| `entityId` | 페이로드 배열의 각 항목은 데이터 세트에 대한 고유 ID를 제공해야 합니다. |
| `entityMeta.fields` | (선택 사항) 데이터 세트 스키마의 특정 필드를 참조하는 [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 문자열 배열. 이 배열이 포함된 경우 배열에 포함된 필드만 평가에 참여합니다. 배열에 포함되지 않은 스키마 필드는 평가에 참여할 수 없습니다.<br><br>이 필드가 포함되지 않으면 데이터 집합 스키마 내의 모든 필드가 평가에 포함됩니다. |

**응답**

성공적인 응답은 마케팅 작업에 대한 URL, 제공된 데이터 세트에서 수집된 사용 레이블 및 해당 레이블에 대한 작업을 테스트한 결과 위반된 정책 목록을 반환합니다. 이 예에서 &quot;데이터를 제3자로 내보내기&quot; 정책은 마케팅 작업이 예상 정책 위반을 트리거했음을 나타내는 `violatedPolicies` 배열에 표시됩니다.

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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
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
| `duleLabels` | 요청 페이로드에 제공된 데이터 세트에서 추출된 데이터 사용 레이블 목록입니다. |
| `discoveredLabels` | 요청 페이로드에서 제공된 데이터 세트 목록으로, 각 데이터세트에 있는 데이터 세트 수준 및 필드 수준 레이블을 표시합니다. |
| `violatedPolicies` | 제공된 항목에 대해 마케팅 작업(지정된)을 테스트하여 위반된 정책 `marketingActionRef`을 나열하는 배열입니다 `duleLabels`. |

## 다음 단계

이 문서를 읽으면 데이터 세트 또는 데이터 사용 레이블 세트에 대한 마케팅 작업을 수행할 때 정책 위반을 확인하는 데 성공했습니다. API 응답에서 반환된 데이터를 사용하여 경험 애플리케이션 내에서 프로토콜을 설정하여 정책 위반이 발생할 때 적절하게 적용할 수 있습니다.

대상 세그먼트에 대한 데이터 사용 정책을 적용하는 방법에 대한 단계 [!DNL Real-time Customer Profile]는 다음 [자습서를 참조하십시오](../../segmentation/tutorials/governance.md).