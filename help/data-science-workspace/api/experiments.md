---
keywords: Experience Platform;개발자 안내서;엔드포인트;데이터 과학 작업 공간;인기 항목;실험;sensei 기계 학습 api
solution: Experience Platform
title: 실험 API 끝점
topic-legacy: Developer guide
description: 모델 개발 및 교육은 실험 수준에서 수행됩니다. 실험 수준에서 실험은 MLInstance, 교육 실행 및 점수 책정 실행으로 구성됩니다.
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# 실험 끝점

모델 개발 및 교육은 실험 수준에서 수행됩니다. 실험 수준에서 실험은 MLInstance, 교육 실행 및 점수 책정 실행으로 구성됩니다.

## 실험 만들기 {#create-an-experiment}

요청 페이로드에서 이름 및 유효한 MLInstance ID를 제공하면서 POST 요청을 수행하여 실험을 만들 수 있습니다.

>[!NOTE]
>
>UI의 모델 교육과 달리, 명시적 API 호출을 통해 실험을 만들면 교육 실행이 자동으로 만들어지고 실행되지 않습니다.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 실험에 대해 원하는 이름입니다. 이 실험에 해당하는 교육 실행은 UI에 표시되는 이 값을 교육 실행 이름으로 상속합니다. |
| `mlInstanceId` | 유효한 MLInstance ID입니다. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 만든 실험의 세부 정보가 포함된 페이로드를 반환합니다`id`).

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 교육 또는 점수 실행 생성 및 실행 {#experiment-training-scoring}

POST 요청을 수행하고 유효한 실험 ID를 제공하고 실행 작업을 지정하여 교육 또는 점수부여 실행을 생성할 수 있습니다. 실험 결과에 기존의 성공적인 교육 실행이 있는 경우에만 점수부여 실행을 생성할 수 있습니다. 훈련 실행을 성공적으로 생성하면 모델 교육 절차가 초기화되고 성공적으로 완료되면 숙련된 모델이 생성됩니다. 훈련된 모델을 생성하면 이전에 기존의 모델을 대체하게 되므로 Experiment는 지정된 시간에 하나의 훈련된 모델만 활용할 수 있습니다.

**API 형식**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID입니다. |

**요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| 속성 | 설명 |
| --- | --- |
| `{TASK}` | 실행 작업을 지정합니다. 이 값을 다음 중 하나로 설정합니다. `train` 교육 `score` 점수 책정 `featurePipeline` 피쳐 파이프라인용. |

**응답**

성공적인 응답은 상속된 기본 교육 또는 점수 매개 변수 및 실행의 고유 ID( )를 포함하여 새로 생성된 실행의 세부 정보가 포함된 페이로드를 반환합니다`{RUN_ID}`).

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
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

단일 GET 요청을 수행하고 유효한 MLInstance ID를 쿼리 매개 변수로 제공하여 특정 MLInstance에 속하는 실험 목록을 검색할 수 있습니다. 사용 가능한 쿼리 목록은 [자산 검색을 위한 쿼리 매개 변수](./appendix.md#query).


**API 형식**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 해당 특정 MLInstance에 속하는 실험 목록을 검색하려면 올바른 MLInstance ID를 제공하십시오. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 동일한 MLInstance ID(`{MLINSTANCE_ID}`).

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
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

요청 경로에 원하는 실험 ID를 포함하는 GET 요청을 수행하여 특정 실험의 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
GET /experiments/{EXPERIMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID입니다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 실험들의 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 실험 실행 목록 검색

단일 GET 요청을 수행하고 유효한 실험 ID를 제공하여 특정 실험에 속하는 교육 또는 점수 실행 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 매개 변수의 전체 목록은 부록 섹션을 참조하십시오. [자산 검색을 위한 쿼리 매개 변수](./appendix.md#query).

>[!NOTE]
>
>여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(&amp;)로 구분해야 합니다.

**API 형식**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID입니다. |
| `{QUERY_PARAMETER}` | 다음 중 하나 [사용 가능한 쿼리 매개 변수](./appendix.md#query) 결과를 필터링하는 데 사용됩니다. |
| `{VALUE}` | 이전 쿼리 매개 변수의 값입니다. |

**요청**

다음 요청에는 쿼리가 포함되어 있으며 일부 실험에 속하는 교육 실행 목록을 검색합니다.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 실행 목록과 해당 실험 실행 ID( )를 포함하여 각 세부 사항이 포함된 페이로드를 반환합니다`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## 실험 업데이트

요청 경로에서 target 실험 ID를 포함하는 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공하여 기존 실험을 업데이트할 수 있습니다.

>[!TIP]
>
>이 PUT 요청의 성공을 보장하기 위해 먼저 GET 요청을 수행하십시오로서 [id로 실험 검색](#retrieve-specific). 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청의 페이로드로 적용합니다.

다음 샘플 API 호출은 처음에 이러한 속성을 갖는 동안 Experiment 이름을 업데이트합니다.

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
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
| `{EXPERIMENT_ID}` | 유효한 실험 ID입니다. |

**요청**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**응답**

성공적인 응답은 실험에서 업데이트된 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## 실험 삭제

요청 경로에 target 실험 ID가 포함된 DELETE 요청을 수행하여 단일 실험을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXPERIMENT_ID}` | 유효한 실험 ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
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
    "detail": "Experiment successfully deleted"
}
```

## MLInstance ID로 실험 삭제

MLInstance ID를 쿼리 매개 변수로 포함하는 DELETE 요청을 수행하여 특정 MLInstance에 속하는 모든 실험을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| 매개 변수 | 설명 |
| --- | ---|
| `{MLINSTANCE_ID}` | 유효한 MLInstance ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "Experiments successfully deleted"
}
```
