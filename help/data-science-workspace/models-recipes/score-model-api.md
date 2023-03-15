---
keywords: Experience Platform;모델 점수 매기기;Data Science Workspace;인기 주제;sensei 머신 러닝 api
solution: Experience Platform
title: Sensei 머신 러닝 API를 사용하여 모델 점수 매기기
type: Tutorial
description: 이 자습서에서는 Sensei 머신 러닝 API를 활용하여 실험 및 실험 실행을 만드는 방법을 보여줍니다.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# 를 사용하여 모델에 점수 매기기 [!DNL Sensei Machine Learning API]

이 자습서에서는 API를 활용하여 실험 및 실험 실행을 만드는 방법을 보여줍니다. Sensei 머신 러닝 API의 모든 엔드포인트 목록은 을 참조하십시오. [이 문서](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## 채점에 대해 예약된 실험 만들기

교육을 위해 예약된 실험과 마찬가지로, 채점을 위해 예약된 실험을 만드는 것도 `template` section을 body 매개 변수에 추가합니다. 또한 `name` 필드 아래 `tasks` 본문에는 가 로 설정되어 있습니다. `score`.

다음은에서 시작하여 20분마다 실행되는 실험을 만드는 예제입니다 `startTime` 까지 실행됩니다. `endTime`.

**요청**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.\
`{JSON_PAYLOAD}`: 전송할 실험 실행 개체. 자습서에서 사용하는 예는 다음과 같습니다.

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`: MLInstance를 나타내는 ID입니다.\
`{MODEL_ID}`: 훈련된 모델을 나타내는 ID입니다.

다음은 예약된 실험을 만든 후의 응답입니다.

**응답**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`: 실험을 나타내는 ID입니다.\
`{INSTANCE_ID}`: MLInstance를 나타내는 ID입니다.


### 채점을 위한 실험 실행 만들기

이제 훈련된 모델을 사용하여 채점을 위한 실험 실행을 만들 수 있습니다. 값 `modelId` 매개 변수는 `id` 위의 GET 모델 요청에서 매개 변수가 반환되었습니다.

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

`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.\
`{EXPERIMENT_ID}`: 타깃팅할 실험에 해당하는 ID입니다. 이는 실험을 생성할 때 응답에서 찾을 수 있습니다.\
`{JSON_PAYLOAD}`: 게시할 데이터. 자습서에서 사용하는 예는 다음과 같습니다.

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`: 모델에 해당하는 ID.

실험 실행 만들기의 응답은 다음과 같습니다.

**응답**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`: 실행 중인 실험에 해당하는 ID입니다.\
`{EXPERIMENT_RUN_ID}`: 방금 만든 실험 실행에 해당하는 ID입니다.


### 예약된 실험 실행에 대한 실험 실행 상태 검색

예약된 실험에 대한 실험 실행을 가져오려면 쿼리가 아래에 표시됩니다.

**요청**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: 실행 중인 실험에 해당하는 ID입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.\
`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 IMS 조직 자격 증명입니다.

특정 실험에 대해 여러 실험 실행이 있기 때문에, 반환되는 응답에는 실행 ID 배열이 있습니다.

**응답**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: 실험 실행에 해당하는 ID입니다.\
`{EXPERIMENT_ID}`: 실행 중인 실험에 해당하는 ID입니다.

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
