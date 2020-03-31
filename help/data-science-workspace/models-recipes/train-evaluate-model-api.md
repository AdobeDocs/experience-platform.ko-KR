---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: 모델 트레이닝 및 평가(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 모델 트레이닝 및 평가(API)


이 자습서에서는 API 호출을 사용하여 모델을 생성, 교육 및 평가하는 방법을 보여줍니다. API 설명서의 자세한 목록은 [이 문서를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 참조하십시오.

## 전제 조건

API [를 사용하여](./import-packaged-recipe-api.md) 패키징된 레서피 가져오기를 사용하여 엔진 제작을 수행합니다. 이 방법은 API를 사용하여 모델을 트레이닝하고 평가하는 데 필요합니다.

이 자습서에 [따라](../../tutorials/authentication.md) API 호출 작업을 시작할 수 있습니다.

이제 튜토리얼에서 다음 값을 사용할 수 있습니다.

- `{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.
- `{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명
- `{API_KEY}`:고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값

- 지능형 서비스의 Docker 이미지에 연결

## API 워크플로우

API를 사용하여 트레이닝을 위한 실험 실행을 만듭니다. 이 튜토리얼에서는 엔진, MLInessions 및 **실험******&#x200B;끝점에 중점을 **둡니다** . 다음 차트에서는 세 가지 요소 간의 관계를 간략히 설명하고 Run과 Model의 개념을 소개합니다.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE] &quot;Engine&quot;, &quot;MLInstance&quot;, &quot;MLService&quot;, &quot;Experiment&quot; 및 &quot;Model&quot;은 UI에서 다른 용어로 언급됩니다. UI에서 오는 경우 다음 표에 차이가 매핑됩니다.
> 
> | UI 용어 | API 용어 |
> --- | ---
> | 레서피 | 엔진 |
> | 모델 | MLInstance |
> | 교육 실행 | 실험 |
> | 서비스 | MLService |



### MLInstance 만들기

다음 요청을 사용하여 MLInstance를 만들 수 있습니다. API 튜토리얼을 사용하여 패키징된 레서피 가져오기에서 엔진을 만들 때 `{ENGINE_ID}` 반환된 [코드를 사용하게](./import-packaged-recipe-ui.md) 됩니다.

**요청**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.\
`{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명\
`{API_KEY}`:고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값\
`{JSON_PAYLOAD}`:MLInstance 구성 튜토리얼에서 사용하는 예는 다음과 같습니다.

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

>[!NOTE] In `{JSON_PAYLOAD}`the, we define parameters used for training and scoring in the `tasks` array. 은 `{ENGINE_ID}` 사용할 엔진의 ID이고 `tag` 필드는 인스턴스를 식별하는 데 사용되는 선택적 매개 변수입니다.

응답에는 만들어진 MLInstance를 `{INSTANCE_ID}` 나타내는 값이 포함됩니다. 구성이 다른 여러 모델 MLInestas를 만들 수 있습니다.

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

`{ENGINE_ID}`:MLInstance가 만들어지는 엔진을 나타내는 이 ID입니다.\
`{INSTANCE_ID}`:MLInstance를 나타내는 ID입니다.

### 실험 만들기

실험 방법은 데이터 과학자가 트레이닝 동안 고성능의 모델에 도달하기 위해 사용합니다. 데이터 세트, 기능, 학습 매개 변수 및 하드웨어를 변경하는 것이 여러 가지 실험입니다. 다음은 실험 만들기의 예입니다.

**요청**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명\
`{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.\
`{API_KEY}`:고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값\
`{JSON_PAYLOAD}`:만든 개체를 실험해 보십시오. 튜토리얼에서 사용하는 예는 다음과 같습니다.

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`:MLInstance를 나타내는 ID입니다.

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

`{EXPERIMENT_ID}`:방금 만든 실험을 나타내는 ID입니다.
`{INSTANCE_ID}`:MLInstance를 나타내는 ID입니다.

### 예약된 교육 실험 만들기

예약된 실험은 API 호출을 통해 각 단일 실험 실행을 만들 필요가 없도록 사용됩니다. 대신 Experiment 생성 중에 필요한 모든 매개 변수를 제공하며 각 실행이 주기적으로 생성됩니다.

예약된 실험 만들기를 나타내려면 요청 본문에 `template` 섹션을 추가해야 합니다. 에서 `template`실행을 예약하는 데 필요한 모든 매개 변수(예: `tasks`작업, 예약된 실행 시간 `schedule`표시)가 포함됩니다.

**요청**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명\
`{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.\
`{API_KEY}`:고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값\
`{JSON_PAYLOAD}`:게시할 데이터 세트입니다. 튜토리얼에서 사용하는 예는 다음과 같습니다.

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

실험(Experiment)을 만들 `{JSON_PAYLOAD}`때 본문에는 `mlInstanceId` 또는 `mlInstanceQuery` 매개 변수가 포함되어야 합니다. 이 예에서 예약된 Experiment는 20분마다 `cron` 매개 변수에 설정된 실행을 `startTime` Experiment에서 Experiment `endTime`까지 호출합니다.

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

`{EXPERIMENT_ID}`:실험을 나타내는 ID입니다.\
`{INSTANCE_ID}`:MLInstance를 나타내는 ID입니다.


### 트레이닝을 위한 실험 실행 만들기

Experiment 엔티티가 만들어지면 아래 호출을 사용하여 교육 실행을 만들고 실행할 수 있습니다. 요청 본문에 트리거할 `{EXPERIMENT_ID}` 항목을 `mode` 입력하고 상태를 표시합니다.

**요청**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`:타깃팅할 실험에 해당하는 ID입니다. 이것은 실험을 만들 때 응답에서 찾을 수 있습니다.\
`{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명\
`{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.\
`{API_KEY}`:고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값\
`{JSON_PAYLOAD}`:교육 실행을 만들려면 본문에 다음을 포함해야 합니다.

```JSON
{
    "mode":"Train"
}
```

다음 `tasks` 배열을 포함하여 구성 매개 변수를 재정의할 수도 있습니다.

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

아래의 `{EXPERIMENT_RUN_ID}` 및 구성을 알려주는 다음 응답을 받게 `tasks`됩니다.

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
`{EXPERIMENT_ID}`:실험 실행이 적용되는 실험을 나타내는 ID입니다.

### 실험 실행 상태 검색

실험 실행의 상태를 로 쿼리할 수 `{EXPERIMENT_RUN_ID}`있습니다.

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`:실험을 나타내는 ID입니다.\
`{EXPERIMENT_RUN_ID}`:실험 실행을 나타내는 ID입니다.\
`{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.\
`{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명\
`{API_KEY}`:고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값

**응답**

GET 호출은 아래와 같이 `state` 매개 변수의 상태를 제공합니다.

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
`{EXPERIMENT_ID}`:실험 실행이 적용되는 실험을 나타내는 ID입니다.

주 외에 다른 `DONE` 주들은 다음과 같습니다.
- `PENDING`
- `RUNNING`
- `FAILED`

자세한 내용은 `tasklogs` 매개 변수 아래에서 세부 로그를 확인할 수 있습니다.

### 교육된 모델 읽어들이기

트레이닝 중에 위의 트레이닝 모델을 만들기 위해 다음의 요청을 합니다.

**요청**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`:타깃팅할 실험 실행에 해당하는 ID입니다. 이것은 실험 실행을 만들 때 응답에서 찾을 수 있습니다.\
`{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.\
`{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명

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

`{MODEL_ID}`:모델에 해당하는 ID입니다.\
`{EXPERIMENT_ID}`: 실험 실행의 실험에 해당하는 ID입니다.\
`{EXPERIMENT_RUN_ID}`:실험 실행에 해당하는 ID입니다.

### 예약된 실험 중지 및 삭제

예약된 Experiment의 실행을 중지하려면 DELETE 요청을 `endTime`Experiment에 쿼리하여 `{EXPERIMENT_ID}`

**요청**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: 실험에 해당하는 ID입니다.\
`{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.\
`{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명

>[!NOTE] API 호출에서는 새 Experiment 실행을 만들 수 없습니다. 하지만 이미 실행 중인 실험 실행의 실행을 중지하지 않습니다.

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

이 자습서에서는 API를 사용하여 엔진, 실험, 예약된 실험 실행 및 트레이닝된 모델을 만드는 방법을 살펴보았습니다. 다음 [연습에서는](./score-model-api.md)성과가 가장 높은 트레이닝된 모델을 사용하여 새로운 데이터 세트를 채점함으로써 예측을 하게 됩니다.