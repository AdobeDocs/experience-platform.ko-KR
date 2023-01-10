---
keywords: Experience Platform;개발자 안내서;엔드포인트;데이터 과학 작업 공간;인기 항목;통찰력;sensei 기계 학습 api
solution: Experience Platform
title: 통찰력 API 엔드포인트
description: 인사이트에는 관련 평가 지표를 표시하여 데이터 과학자가 최적 ML 모델을 평가하고 선택할 수 있도록 하는 데 사용되는 지표가 포함되어 있습니다.
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# 통찰력 끝점

인사이트에는 관련 평가 지표를 표시하여 데이터 과학자가 최적 ML 모델을 평가하고 선택할 수 있도록 하는 데 사용되는 지표가 포함되어 있습니다.

## 인사이트 목록 검색

인사이트 엔드포인트에 대한 단일 GET 요청을 수행하여 인사이트 목록을 검색할 수 있습니다.  결과를 필터링하는 데 도움이 되도록 요청 경로에 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 [자산 검색을 위한 쿼리 매개 변수](./appendix.md#query).

**API 형식**

```http
GET /insights
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 인사이트 목록을 포함하는 페이로드를 반환하며 각 인사이트에 고유한 식별자( )가 있습니다 `id` ). 또한 `context` 인사이트 이벤트 및 지표 데이터와 관련된 해당 특정 인사이트와 연관된 고유 식별자를 포함합니다.

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 인사이트에 해당하는 ID입니다. |
| `experimentId` | 유효한 실험 ID입니다. |
| `experimentRunId` | 올바른 실험 실행 ID입니다. |
| `modelId` | 유효한 모델 ID입니다. |

## 특정 인사이트 검색

특정 인사이트를 조회하기 위해 GET 요청을 수행하고 유효한 인사이트를 제공합니다 `{INSIGHT_ID}` 를 입력합니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 [자산 검색을 위한 쿼리 매개 변수](./appendix.md#query).

**API 형식**

```http
GET /insights/{INSIGHT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{INSIGHT_ID}` | Sensei 인사이트의 고유 식별자입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 인사이트 고유 식별자( )를 포함하는 페이로드를 반환합니다`id`). 또한 `context` 인사이트 이벤트 및 지표 데이터와 관련된 특정 인사이트와 연관된 고유 식별자를 포함합니다.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 인사이트에 해당하는 ID입니다. |
| `experimentId` | 유효한 실험 ID입니다. |
| `experimentRunId` | 올바른 실험 실행 ID입니다. |
| `modelId` | 유효한 모델 ID입니다. |

## 새 모델 인사이트 추가

POST 요청 및 새 모델 인사이트에 대한 컨텍스트, 이벤트 및 지표를 제공하는 페이로드를 수행하여 새 모델 인사이트를 만들 수 있습니다. 새 모델 인사이트를 만드는 데 사용되는 컨텍스트 필드는 기존 서비스가 연결되어 있을 필요가 없지만, 해당 ID 중 하나 이상을 제공하여 새 모델 인사이트를 기존 서비스로 만들 수 있습니다.

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
  }
```

**API 형식**

```http
POST /insights
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**응답**

성공적으로 응답하면 가 있는 페이로드가 반환됩니다 `{INSIGHT_ID}` 및 초기 요청에서 제공한 모든 매개 변수입니다.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| 속성 | 설명 |
| --- | --- |
| `insightId` | 성공적인 POST 요청이 수행된 경우 이 특정 인사이트를 위해 생성되는 고유 ID입니다. |

## 알고리즘에 대한 기본 지표 목록 검색

지표 종단점에 대한 단일 GET 요청을 수행하여 모든 알고리즘과 기본 지표 목록을 검색할 수 있습니다. 특정 지표를 쿼리하려면 GET 요청을 수행하고 유효한 지표를 제공합니다 `{ALGORITHM}` 를 입력합니다.

**API 형식**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ALGORITHM}` | 알고리즘 유형의 식별자입니다. |

**요청**

다음 요청은 쿼리를 포함하고 알고리즘 식별자를 사용하여 특정 지표를 검색합니다 `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음을 포함하는 페이로드를 반환합니다 `algorithm` 고유 식별자 및 기본 지표 배열입니다.

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```
