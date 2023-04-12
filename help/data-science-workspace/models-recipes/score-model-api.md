---
keywords: Experience Platform;모델 점수 책정;데이터 과학 작업 공간;인기 항목;sensei 기계 학습 api
solution: Experience Platform
title: Sensei 기계 학습 API를 사용하여 모델 점수 책정
type: Tutorial
description: 이 자습서에서는 Sensei 기계 학습 API를 활용하여 실험 및 실험 실행을 만드는 방법을 보여줍니다.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# 를 사용하여 모델 점수 책정 [!DNL Sensei Machine Learning API]

이 자습서에서는 API를 활용하여 실험 및 실험 실행을 만드는 방법을 보여줍니다. Sensei 기계 학습 API의 모든 엔드포인트 목록은 다음을 참조하십시오. [이 문서](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## 점수에 대한 예약된 실험 만들기

교육을 위한 예약된 실험과 유사하게, 점수에 대해 예약된 실험을 만드는 것도 다음을 포함하여 수행됩니다 `template` 섹션에 본문 매개 변수를 추가합니다. 또한 `name` 아래의 필드 `tasks` 에서는 가 `score`.

다음은 부터 20분마다 실행되는 실험을 만드는 예입니다 `startTime` 다음 기간 동안 실행됩니다. `endTime`.

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

`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 조직 자격 증명입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 베어러 토큰 값입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값입니다.\
`{JSON_PAYLOAD}`: 보낼 실험 실행 개체입니다. 자습서에서 사용하는 예는 다음과 같습니다.

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


### 점수를 위한 실험 실행 만들기

이제 숙련된 모델로 채점하기 위한 실험 실행을 만들 수 있습니다. 의 값 `modelId` 매개 변수는 `id` 위의 GET 모델 요청에서 반환된 매개 변수입니다.

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

`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 조직 자격 증명입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 베어러 토큰 값입니다.\
`{API_KEY}`: 고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값입니다.\
`{EXPERIMENT_ID}`: 타겟팅할 실험에 해당하는 ID입니다. 실험을작성할 때 응답에서 찾을 수 있습니다.\
`{JSON_PAYLOAD}`: 게시할 데이터입니다. 자습서에서 사용하는 예제는 다음과 같습니다.

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

`{MODEL_ID}`: 모델에 해당하는 ID입니다.

실험 실행 생성의 응답은 다음과 같습니다.

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

예약된 실험에 대해 실험 실행을 가져오려면 다음과 같은 쿼리가 표시됩니다.

**요청**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: 실행 중인 실험에 해당하는 ID입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 베어러 토큰 값입니다.\
`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 조직 자격 증명입니다.

특정 실험에 대해 여러 개의 실험 실행이 있으므로 반환된 응답에는 실행 ID의 배열이 있습니다.

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

예약된 실험 실행 전에 실행을 중지하려면 `endTime`에 DELETE 요청을 쿼리하여 수행할 수 있습니다. `{EXPERIMENT_ID}`

**요청**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: 실험에 해당하는 ID입니다.\
`{ACCESS_TOKEN}`: 인증 후 제공된 특정 베어러 토큰 값입니다.\
`{ORG_ID}`: 고유한 Adobe Experience Platform 통합에 있는 조직 자격 증명입니다.

>[!NOTE]
>
>API 호출을 사용하면 새 실험 실행 만들기가 비활성화됩니다. 그러나 이미 실행 중인 실험 실행의 실행을 중지하지는 않습니다.

다음은 실험이 성공적으로 삭제되었음을 알리는 응답입니다.

**응답**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```
