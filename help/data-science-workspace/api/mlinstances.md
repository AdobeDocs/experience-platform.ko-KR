---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: MLInasses
topic: Developer guide
translation-type: tm+mt
source-git-commit: 0197c2f5e304f2fc194289b064cc37c91bb658c8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 4%

---


# MLInasses

MLInstice는 기존 [엔진](./engines.md) 및 교육 매개 변수, 점수 매개 변수 또는 하드웨어 리소스 구성을 정의하는 적절한 구성 집합을 결합한 것입니다.

## MLInestment 만들기 {#create-an-mlinstance}

유효한 엔진 ID(Engine Id)와 적절한 기본 구성 세트로 구성된 요청 페이로드를 제공하면서 POST 요청을 수행하여 MLIninstance를 만들 수`{ENGINE_ID}`있습니다.

엔진 ID가 PySpark 또는 Spark Engine을 참조하는 경우 코어 수 또는 메모리 양과 같은 컴퓨팅 리소스의 양을 구성할 수 있습니다. Python Engine이 참조되는 경우 트레이닝과 점수 지정을 위해 CPU나 GPU를 사용할 수 있습니다. 자세한 내용은 [PySpark 및 Spark 리소스 구성](./appendix.md#resource-config) 및 [Python CPU 및 GPU 구성에](./appendix.md#cpu-gpu-config) 대한 부록 섹션을 참조하십시오.

**API 형식**

```http
POST /mlInstances
```

**요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | MLInestion에 대해 원하는 이름입니다. 이 MLInposition에 해당하는 모델은 UI에 모델 이름으로 표시할 이 값을 상속합니다. |
| `description` | MLInestment에 대한 선택적 설명입니다. 이 MLInposition에 해당하는 모델은 이 값을 상속하여 UI에 모델 설명으로 표시합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 값을 빈 문자열로 설정합니다. |
| `engineId` | 기존 엔진의 ID입니다. |
| `tasks` | 트레이닝, 점수 지정 또는 기능 파이프라인을 위한 구성 집합. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 MLInposition의 세부 사항이 포함된 페이로드를 반환합니다.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## MLInasses 목록 검색

단일 GET 요청을 수행하여 MLInestment 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에서 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 질의 목록은 자산 검색을 위한 [쿼리 매개 변수의 부록 섹션을 참조하십시오](./appendix.md#query).

**API 형식**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETER}` | 결과를 필터링하는 데 사용되는 [사용 가능한 쿼리 매개](./appendix.md#query) 변수 중 하나입니다. |
| `{VALUE}` | 이전 쿼리 매개 변수의 값입니다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 MLInestas 및 해당 세부 사항 목록을 반환합니다.

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## 특정 MLInestment 검색 {#retrieve-specific}

요청 경로에서 원하는 MLInposition의 ID를 포함하는 GET 요청을 수행하여 특정 MLInence의 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 원하는 MLInestment의 ID입니다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 MLInestment의 세부 사항을 반환합니다.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## MLInestment 업데이트

요청 경로에서 대상 MLInestions의 ID를 포함하는 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공함으로써 기존 MLInestment를 업데이트할 수 있습니다.

>[!TIP] 이 PUT 요청의 성공을 보장하기 위해, 먼저 ID로 MLInposition을 [검색하기 위한 GET 요청을 수행하는 것이 좋습니다](#retrieve-specific). 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청의 페이로드로 적용합니다.

다음 샘플 API 호출은 처음에 이러한 속성을 갖는 동안 MLInestion의 교육 및 점수 매개 변수를 업데이트합니다.

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**API 형식**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 유효한 MLInestment ID입니다. |

**요청**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**응답**

성공적인 응답은 MLIneste의 업데이트된 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## 엔진 ID로 MLInestment 삭제

엔진 ID를 쿼리 매개 변수로 포함하는 DELETE 요청을 수행하여 동일한 엔진을 공유하는 모든 MLInestas를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ENGINE_ID}` | 유효한 엔진 ID. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstances successfully deleted"
}
```

## MLInestment 삭제

요청 경로에 대상 MLInstice의 ID를 포함하는 DELETE 요청을 수행하여 단일 MLInestment를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 유효한 MLInestment ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstance deletion was successful"
}
```
