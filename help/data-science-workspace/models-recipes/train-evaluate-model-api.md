---
keywords: Experience Platform;교육 및 평가;Data Science Workspace;인기 주제;Sensei 머신 러닝 API
solution: Experience Platform
title: Sensei 머신 러닝 API를 사용하여 모델 교육 및 평가
type: Tutorial
description: 이 자습서에서는 Sensei 머신 러닝 API 호출을 사용하여 모델을 만들고, 교육하고, 평가하는 방법을 보여줍니다.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# 다음을 사용하여 모델 교육 및 평가 [!DNL Sensei Machine Learning] API


이 자습서에서는 API 호출을 사용하여 모델을 만들고, 교육하고, 평가하는 방법을 보여줍니다. 을(를) 참조하십시오 [이 문서](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) API 설명서의 세부 목록을 참조하십시오.

## 전제 조건

다음 [API를 사용하여 패키지된 레시피 가져오기](./import-packaged-recipe-api.md) API를 사용하여 모델을 교육하고 평가하는 데 필요한 엔진 생성.

다음 [Experience Platform API 인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) API 호출을 시작합니다.

이제 자습서에서 다음 값을 가져야 합니다.

- `{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.
- `{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.
- `{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.

- 지능형 서비스의 도커 이미지에 대한 링크

## API 워크플로우

교육용 실험 실행을 만들기 위해 API를 사용할 예정입니다. 이 자습서에서는 엔진, 인스턴스 및 실험 끝점에 중점을 둡니다. 다음 차트는 세 가지 간의 관계를 간략하게 설명하고 실행 및 모델에 대한 개념도 소개합니다.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>용어 &quot;엔진&quot;, &quot;MLInstance&quot;, &quot;MLService&quot;, &quot;실험&quot; 및 &quot;모델&quot;은 UI에서 다른 용어로 지칭됩니다. UI에서 가져오는 경우 다음 표에서 차이점을 매핑합니다.

| UI 용어 | API 용어 |
| --- | --- |
| 레시피 | 엔진 |
| 모델 | MLInstance |
| 교육 실행 | 실험 |
| 서비스 | MLSservice |

### 인스턴스 만들기

다음 요청을 사용하여 MLInstance를 만들 수 있습니다. 다음을 사용하게 됩니다. `{ENGINE_ID}` 에서 엔진을 만들 때 반환됨 [API를 사용하여 패키지된 레시피 가져오기](./import-packaged-recipe-ui.md) 튜토리얼.

**요청**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.\
`{JSON_PAYLOAD}`: MLInstance 구성 자습서에서 사용하는 예는 다음과 같습니다.

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE]
>
>다음에서 `{JSON_PAYLOAD}`, 에서는 교육 및 채점에 사용되는 매개 변수를 정의합니다. `tasks` 배열입니다. 다음 `{ENGINE_ID}` 는 사용하려는 엔진의 ID이고 `tag` 필드는 인스턴스를 식별하는 데 사용되는 선택적 매개 변수입니다.

응답에는 `{INSTANCE_ID}` 생성된 MLInstance를 나타냅니다. 구성이 다른 여러 모델 인스턴스를 만들 수 있습니다.

**응답**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`: MLInstance가 생성되는 엔진을 나타내는 이 ID입니다.\
`{INSTANCE_ID}`: MLInstance를 나타내는 ID입니다.

### 실험 만들기

실험은 데이터 과학자가 훈련하는 동안 성과가 좋은 모델에 도달하기 위해 사용합니다. 여러 실험에는 데이터 세트, 기능, 학습 매개 변수 및 하드웨어 변경이 포함됩니다. 다음은 실험을 만드는 예제입니다.

**요청**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.\
`{JSON_PAYLOAD}`: 만들어진 실험 개체입니다. 자습서에서 사용하는 예는 다음과 같습니다.

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: MLInstance를 나타내는 ID입니다.

실험 생성의 응답은 다음과 같습니다.

**응답**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`: 방금 만든 실험을 나타내는 ID입니다.
`{INSTANCE_ID}`: MLInstance를 나타내는 ID입니다.

### 교육을 위해 예약된 실험 만들기

예약된 실험은 API 호출을 통해 각 단일 실험 실행을 만들 필요가 없도록 사용됩니다. 대신 실험 생성 중에 필요한 모든 매개 변수를 제공하고 각 실행은 주기적으로 생성됩니다.

예약된 실험 생성을 나타내려면 다음을 추가해야 합니다. `template` 섹션 을 참조하십시오. 위치 `template`, 실행 예약에 필요한 모든 매개 변수가 포함됩니다. `tasks`, (어떤 작업을 수행하는지 나타냄) `schedule`: 예약된 실행의 타이밍을 나타냅니다.

**요청**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.\
`{JSON_PAYLOAD}`: 게시할 데이터 세트입니다. 자습서에서 사용하는 예는 다음과 같습니다.

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

우리가 실험과 몸을 만들 때 `{JSON_PAYLOAD}`는 다음 중 하나를 포함해야 합니다. `mlInstanceId` 또는 `mlInstanceQuery` 매개 변수. 이 예에서 예약된 실험은 20분마다 실행을 호출하며 `cron` 매개 변수, 다음에서 시작 `startTime` 종료 시간: `endTime`.

**응답**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`: 실험을 나타내는 ID입니다.\
`{INSTANCE_ID}`: MLInstance를 나타내는 ID입니다.


### 교육을 위한 실험 실행 만들기

실험 엔터티가 만들어지면 아래 호출을 사용하여 교육 실행을 만들고 실행할 수 있습니다. 다음이 필요합니다. `{EXPERIMENT_ID}` 무엇에 대해 말하라 `mode` 요청 본문에서 를 트리거하려고 합니다.

**요청**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: 타깃팅할 실험에 해당하는 ID입니다. 이는 실험을 생성할 때 응답에서 찾을 수 있습니다.\
`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.\
`{JSON_PAYLOAD}`: 교육 실행을 만들려면 본문에 다음 내용을 포함해야 합니다.

```JSON
{
    "mode":"Train"
}
```

다음을 포함하여 구성 매개 변수를 재정의할 수도 있습니다. `tasks` 배열:

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

다음 응답을 받게 되어 사용자에게 다음이 표시됩니다. `{EXPERIMENT_RUN_ID}` 및 아래의 구성 `tasks`.

**응답**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: 실험 실행을 나타내는 ID입니다.\
`{EXPERIMENT_ID}`: 실험 실행이 진행 중인 실험을 나타내는 ID입니다.

### 실험 실행 상태 검색

실험 실행의 상태는 다음을 사용하여 쿼리할 수 있습니다. `{EXPERIMENT_RUN_ID}`.

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: 실험을 나타내는 ID입니다.\
`{EXPERIMENT_RUN_ID}`: 실험 실행을 나타내는 ID입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.

**응답**

GET 호출은에서 상태를 제공합니다. `state` 아래와 같은 매개 변수:

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`: 실험 실행을 나타내는 ID입니다.\
`{EXPERIMENT_ID}`: 실험 실행이 진행 중인 실험을 나타내는 ID입니다.

이외에도 `DONE` state, 기타 상태는 다음과 같습니다.
- `PENDING`
- `RUNNING`
- `FAILED`

자세한 내용은 아래에서 확인할 수 있습니다. `tasklogs` 매개 변수.

### 훈련된 모델 검색

교육 중에 위에서 만든 훈련된 모델을 가져오려면 다음 요청을 수행합니다.

**요청**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: 타깃팅할 실험 실행에 해당하는 ID입니다. 실험 실행을 만들 때 응답에서 찾을 수 있습니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.

응답은 생성된 훈련된 모델을 나타냅니다.

**응답**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`: 모델에 해당하는 ID.\
`{EXPERIMENT_ID}`: 실험 실행이 포함된 실험에 해당하는 ID입니다.\
`{EXPERIMENT_RUN_ID}`: 실험 실행에 해당하는 ID입니다.

### 예약된 실험 중지 및 삭제

다음 시간 이전에 예약된 실험의 실행을 중지하려면 `endTime`에 대한 DELETE 요청을 쿼리하여 이 작업을 수행할 수 있습니다. `{EXPERIMENT_ID}`

**요청**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: 실험에 해당하는 ID.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.

>[!NOTE]
>
>API 호출로 새 실험 실행 생성이 비활성화됩니다. 하지만 이미 실행 중인 실험 실행의 실행은 중지되지 않습니다.

다음은 실험이 성공적으로 삭제되었음을 알리는 응답입니다.

**응답**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 다음 단계

이 튜토리얼에서는 API를 사용하여 엔진, 실험, 예약된 실험 실행 및 훈련된 모델을 만드는 방법을 살펴보았습니다. 다음에서 [다음 연습](./score-model-api.md), 가장 성과가 좋은 훈련된 모델을 사용하여 새 데이터 세트에 점수를 매겨 예측을 수행할 수 있습니다.
