---
keywords: Experience Platform; 개발자 안내서; 끝점; 데이터 과학 작업 영역; 인기 있는 주제; ml인스턴스; Sensei Machine Learning API
solution: Experience Platform
title: MLInstances API 엔드포인트
description: MLInstance는 기존 엔진과 교육 매개 변수, 점수 매기기 매개 변수 또는 하드웨어 리소스 구성을 정의하는 적절한 구성 집합의 쌍입니다.
role: Developer
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 3%

---

# MLInstances 엔드포인트

>[!NOTE]
>
>Data Science 작업 영역은(는) 더 이상 구매할 수 없습니다.
>
>이 설명서는 데이터 과학 작업 영역 이전에 사용 권한이 있는 기존 고객을 대상으로 합니다.

MLInstance는 기존 [엔진](./engines.md) 과 교육 매개 변수, 점수 매기기 매개 변수 또는 하드웨어 리소스 구성을 정의하는 적절한 구성 집합의 쌍입니다.

## MLInstance 만들기 {#create-an-mlinstance}

유효한 엔진 ID(`{ENGINE_ID}`)와 적절한 기본 구성 집합으로 구성된 요청 페이로드를 제공하면서 POST 요청을 수행하여 MLInstance를 만들 수 있습니다.

엔진 ID가 PySpark 또는 Spark 엔진을 참조하는 경우 코어 수 또는 메모리 양과 같은 계산 리소스의 양을 구성할 수 있습니다. Python 엔진이 참조되는 경우 교육 및 채점 목적으로 CPU 또는 GPU 사용 중에서 선택할 수 있습니다. 자세한 내용은 PySpark 및 Spark 리소스 구성[&#128279;](./appendix.md#resource-config)과 [Python CPU 및 GPU 구성](./appendix.md#cpu-gpu-config)에 대한 부록 섹션을 참조하세요.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | MLInstance에 대해 원하는 이름입니다. 이 MLInstance에 해당하는 모델은 이 값을 상속하여 UI 내에 모델 이름으로 표시됩니다. |
| `description` | MLInstance에 대한 선택적 설명입니다. 이 MLInstance에 해당하는 모델은 모델의 설명으로 UI 에 표시될 이 값을 상속합니다. 이 속성 요소는 필수입니다. 설명을 제공하지 않으려면 해당 값을 빈 문자열로 설정합니다. |
| `engineId` | 기존 엔진의 ID입니다. |
| `tasks` | 교육, 점수 매기기 또는 기능 파이프라인에 대한 구성 집합입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 MLInstance의 세부 정보가 포함된 페이로드를 반환합니다.

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

## MLInstance 목록 검색

단일 GET 요청 수행을 수행하여 MLInstance 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에서 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 자산 검색을[&#128279;](./appendix.md#query) 위한 쿼리 매개 변수에 대한 부록 섹션을 참조하십시오.

**API 형식**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 매개변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETER}` | 결과를 필터링하는 데 사용할 수 있는 쿼리 매개 변수[&#128279;](./appendix.md#query) 중 하나입니다. |
| `{VALUE}` | 이전 쿼리 매개 변수의 값입니다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 MLInstance 목록 및 해당 세부 정보를 반환합니다.

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

## 특정 MLInstance 검색 {#retrieve-specific}

요청 경로에서 원하는 MLInstance의 ID를 포함하는 GET 요청을 수행하여 특정 MLInstance의 세부 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 원하는 MLInstance의 ID입니다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 MLInstance의 세부 정보를 반환합니다.

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

## MLInstance 업데이트

요청 경로에 타겟 MLInstance의 ID를 포함하는 PUT 요청을 통해 해당 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공하여 기존 MLInstance를 업데이트할 수 있습니다.

>[!TIP]
>
>이 PUT 요청의 성공을 보장하려면 먼저 GET 요청을 수행하여 [ID](#retrieve-specific)로 MLInstance를 검색하는 것이 좋습니다. 그런 다음 반환된 JSON 객체를 수정 및 업데이트하고 수정된 JSON 객체 전체를 PUT 요청 페이로드로 적용합니다.

다음 샘플 API 호출은 처음에 이러한 속성을 갖는 동안 MLInstance의 교육 및 점수 매기기 매개 변수를 업데이트합니다.

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

| 매개변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 유효한 MLInstance ID입니다. |

**요청**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공적인 응답은 MLInstance의 업데이트된 세부 정보가 포함된 페이로드를 반환합니다.

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

## 엔진 ID별 MLInstance 삭제

엔진 ID를 쿼리 매개 변수로 포함하는 DELETE 요청을 수행하여 동일한 엔진을 공유하는 모든 MLInstance를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{ENGINE_ID}` | 유효한 엔진 ID. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## MLInstance 삭제

요청 경로에 타겟 MLInstance의 ID를 포함하는 DELETE 요청을 수행하여 단일 MLInstance를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 유효한 MLInstance ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
