---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 실험
topic: Developer guide
translation-type: tm+mt
source-git-commit: 63a128202826ec39911e70d34dda9dfb2bc585b2
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 4%

---


# 실험

모델 개발 및 트레이닝은 실험 수준에서 이루어집니다. 실험 단계는 MLInestment, 트레이닝 실행 및 점수 지정으로 구성됩니다.

## 실험 만들기 {#create-an-experiment}

요청 페이로드에서 이름과 유효한 MLInestment ID를 제공하는 동안 POST 요청을 수행하여 실험을 만들 수 있습니다.

>[!NOTE] UI의 모델 교육과 달리, 명시적 API 호출을 통해 실험을 만들면 교육 실행을 자동으로 만들고 실행하지 않습니다.

**API 형식**

```http
POST /experiments
```

**요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "{MLINSTANCE_ID}"
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 실험 이름을 지정합니다. 이 실험에 해당하는 교육 실행은 교육 실행 이름으로 UI에 표시할 이 값을 상속합니다. |
| `mlInstanceId` | 유효한 MLInestment ID입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 실험물의 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 교육 또는 점수 실행 만들기 및 실행 {#experiment-training-scoring}

POST 요청을 수행하고 유효한 실험 ID를 제공하고 실행 작업을 지정하여 교육 또는 점수 지정 실행을 만들 수 있습니다. Experiment에 기존 및 성공적인 교육 실행이 있는 경우에만 점수 지정 실행을 생성할 수 있습니다. 교육 실행을 성공적으로 생성하면 모델 교육 절차가 초기화되고 성공적으로 완료하면 교육 모델이 생성됩니다. Experiment는 지정된 시간 동안 단일 트레이닝된 모델만 활용할 수 있도록 이전에 있던 모델 대신 훈련된 모델을 생성합니다.

**API 형식**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID. |

**요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| 속성 | 설명 |
| --- | --- |
| `{TASK}` | 실행 작업을 지정합니다. 이 값을 교육 `train` , 점수 `score` 지정 또는 기능 파이프라인 `featurePipeline` 에 대해 설정합니다. |

**응답**

성공적인 응답은 상속된 기본 교육 또는 점수 매개 변수, 실행 고유 ID(`{RUN_ID}`)를 포함하여 새로 만든 실행에 대한 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "{RUN_ID}",
    "mode": "{TASK}",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## 실험 목록 검색

단일 GET 요청을 수행하고 유효한 MLInestment ID를 쿼리 매개 변수로 제공하여 특정 MLInestion에 속하는 실험 목록을 검색할 수 있습니다. 사용 가능한 질의 목록은 자산 검색을 위한 [쿼리 매개 변수의 부록 섹션을 참조하십시오](./appendix.md#query).


**API 형식**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 해당 특정 MLInestment에 속하는 실험 목록을 검색하려면 유효한 MLInestion ID를 제공하십시오. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId=={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 동일한 MLInestment ID(ID)를 공유하는 실험 목록을`{MLINSTANCE_ID}`반환합니다.

```json
{
    "children": [
        {
            "id": "{EXPERIMENT_ID}",
            "name": "A name for this Experiment",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 1",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 2",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## 특정 실험 검색 {#retrieve-specific}

요청 경로에 원하는 실험 ID를 포함하는 GET 요청을 수행하여 특정 실험 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
GET /experiments/{EXPERIMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 실험들의 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 실험 실행 목록 검색

단일 GET 요청을 수행하고 유효한 실험 ID를 제공하여 특정 실험에 속하는 교육 또는 점수 실행 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에서 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 매개 변수의 전체 목록은 자산 검색을 위한 [쿼리 매개 변수의 부록 섹션을 참조하십시오](./appendix.md#query).

>[!NOTE] 여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(&amp;)로 구분해야 합니다.

**API 형식**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID. |
| `{QUERY_PARAMETER}` | 결과를 필터링하는 데 사용되는 [사용 가능한 쿼리 매개](./appendix.md#query) 변수 중 하나입니다. |
| `{VALUE}` | 이전 쿼리 매개 변수의 값입니다. |

**요청**

다음 요청에는 쿼리가 포함되어 있으며 일부 Experiment에 속하는 교육 실행 목록을 검색합니다.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 실행 목록과 각 세부 정보가 포함된 페이로드를 반환하고 실험 실행 ID(`{RUN_ID}`)를 포함합니다.

```json
{
    "children": [
        {
            "id": "{RUN_ID}",
            "mode": "train",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId=={EXPERIMENT_ID},deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## 실험 업데이트

요청 경로에 대상 실험 ID가 포함된 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공함으로써 기존 실험을 업데이트할 수 있습니다.

>[!TIP] 이 PUT 요청의 성공을 보장하기 위해, 먼저 GET 요청을 수행하여 ID로 실험을 [검색하는 것이 좋습니다](#retrieve-specific). 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청의 페이로드로 적용합니다.

다음 샘플 API 호출은 처음 이러한 속성을 갖는 동안 실험 이름을 업데이트합니다.

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**API 형식**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID. |

**요청**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**응답**

성공적인 응답은 실험 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "An updated name",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## 실험 삭제

요청 경로에 대상 실험 ID를 포함하는 DELETE 요청을 수행하여 단일 실험 결과를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
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
    "detail": "Experiment successfully deleted"
}
```

## MLInstice ID로 실험 삭제

MLInestion ID를 쿼리 매개 변수로 포함하는 DELETE 요청을 수행하여 특정 MLInestion에 속하는 모든 실험을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| 매개 변수 | 설명 |
| --- | ---|
| `{MLINSTANCE_ID}` | 유효한 MLInestment ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId={MLINSTANCE_ID} \
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
    "detail": "Experiments successfully deleted"
}
```
