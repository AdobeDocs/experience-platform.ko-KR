---
keywords: Experience Platform;모델 게시;데이터 과학 Workspace;인기 주제;sensei 머신 러닝 api
solution: Experience Platform
title: Sensei 머신 러닝 API를 사용하는 Publish as a Service
type: Tutorial
description: 이 튜토리얼에서는 Sensei 머신 러닝 API를 사용하여 모델을 서비스로 게시하는 프로세스에 대해 설명합니다.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 1%

---

# [!DNL Sensei Machine Learning API]을(를) 사용하여 모델을 서비스로 Publish

이 자습서에서는 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)을(를) 사용하여 모델을 서비스로 게시하는 프로세스에 대해 설명합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform 데이터 과학 Workspace에 대한 작업 이해가 필요합니다. 이 자습서를 시작하기 전에 [Data Science Workspace 개요](../home.md)에서 서비스에 대한 높은 수준의 소개를 검토하십시오.

이 자습서와 함께 따르려면 기존 ML 엔진, ML 인스턴스 및 실험이 있어야 합니다. API에서 만드는 방법에 대한 단계는 [패키지된 레시피 가져오기](./import-packaged-recipe-api.md)에 대한 자습서를 참조하십시오.

마지막으로, 이 자습서를 시작하기 전에 개발자 안내서의 [시작하기](../api/getting-started.md) 섹션에서 이 자습서 전체에서 사용되는 필수 헤더를 포함하여 [!DNL Sensei Machine Learning] API를 성공적으로 호출하기 위해 알아야 할 중요한 정보를 검토하십시오.

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

### 주요 용어

다음 표에서는 이 자습서에서 사용되는 몇 가지 일반적인 용어를 간략하게 설명합니다.

| 용어 | 정의 |
| --- | --- |
| **기계 학습 인스턴스(ML 인스턴스)** | 특정 데이터, 매개 변수 및 [!DNL Sensei] 코드를 포함하는 특정 테넌트에 대한 [!DNL Sensei] 엔진의 인스턴스입니다. |
| **실험** | 교육 실험 실행, 채점 실험 실행 또는 둘 다를 실행하기 위한 umbrella 엔티티입니다. |
| **예약된 실험** | 사용자 정의 일정에 의해 관리되는 교육 또는 채점 실험 실행의 자동화를 설명하는 용어입니다. |
| **실험 실행** | 교육 또는 채점 실험의 특정 인스턴스. 특정 실험의 여러 실험 실행은 교육 또는 채점에 사용되는 데이터 세트 값이 다를 수 있습니다. |
| **훈련된 모델** | 검증, 평가 및 최종 모델에 도달하기 전에 기능 엔지니어링을 실험하고 프로세스를 통해 생성된 머신 러닝 모델입니다. |
| **게시된 모델** | 교육, 유효성 검사 및 평가 후에 최종 버전 모델이 도착했습니다. |
| **기계 학습 서비스(ML 서비스)** | API 끝점을 사용하여 교육 및 채점에 대한 온디맨드 요청을 지원하기 위해 서비스로 배포된 ML 인스턴스. 훈련된 기존 실험 실행을 사용하여 ML 서비스를 만들 수도 있습니다. |

## 기존 교육 실험 실행 및 예약된 채점으로 ML 서비스 만들기

교육 실험 실행을 ML 서비스로 게시할 때 POST 요청의 페이로드에 채점 실험 실행에 대한 세부 정보를 제공하여 채점을 예약할 수 있습니다. 그 결과 채점에 대해 예약된 실험 개체가 생성됩니다.

**API 형식**

```http
POST /mlServices
```

**요청**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `mlInstanceId` | 기존 ML 인스턴스 식별, ML 서비스를 만드는 데 사용되는 교육 실험 실행은 이 특정 ML 인스턴스에 해당해야 합니다. |
| `trainingExperimentId` | ML 인스턴스 식별에 해당하는 실험 식별. |
| `trainingExperimentRunId` | ML 서비스 게시에 사용되는 특정 교육 실험 실행. |
| `scoringDataSetId` | 예약된 채점 실험 실행에 사용될 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행 채점에 사용될 데이터 필터링의 시간(분)을 나타내는 정수 값입니다. 예를 들어 값 `10080`은(는) 각 예약된 채점 실험 실행에 대해 지난 10080분 또는 168시간의 데이터가 사용됨을 의미합니다. `0` 값은 데이터를 필터링하지 않으며 데이터 집합 내의 모든 데이터는 채점에 사용됩니다. |
| `scoringSchedule` | 예약된 채점 실험 실행에 대한 세부 정보를 포함합니다. |
| `scoringSchedule.startTime` | 채점을 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 채점을 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행을 평가할 간격을 나타내는 크론 값. |

**응답**

응답이 성공하면 해당 채점 실험에 대한 고유한 `id` 및 `scoringExperimentId`을(를) 포함하여 새로 만든 ML 서비스의 세부 정보가 반환됩니다.


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## 기존 ML 인스턴스에서 ML 서비스 만들기

특정 사용 사례 및 요구 사항에 따라 ML 인스턴스로 ML 서비스를 만들면 교육 일정 조정 및 실험 실행 채점 측면에서 유연합니다. 이 튜토리얼에서는 다음과 같은 특정 사례를 살펴봅니다.

- [예약된 교육은 필요하지 않지만, 예약된 채점이 필요합니다.](#ml-service-with-scheduled-experiment-for-scoring)
- [교육 및 채점 모두에 대해 예약된 실험 실행이 필요합니다.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

ML 서비스는 교육 또는 채점 실험 예약 없이 ML 인스턴스를 사용하여 만들 수 있습니다. 이러한 ML 서비스는 일반적인 실험 개체 및 교육 및 채점을 위한 단일 실험 실행을 만듭니다.

### 채점을 위한 실험이 예약된 ML 서비스 {#ml-service-with-scheduled-experiment-for-scoring}

점수에 대해 예약된 실험 실행이 있는 ML 인스턴스를 게시하여 ML 서비스를 만들 수 있으며, 이는 교육을 위한 일반 실험 엔티티를 만듭니다. 교육 실험 실행이 생성되며 모든 예약된 채점 실험 실행에 사용됩니다. ML 서비스를 만드는 데 필요한 `mlInstanceId`, `trainingDataSetId` 및 `scoringDataSetId`이(가) 있고 올바른 값인지 확인하십시오.

**API 형식**

```http
POST /mlServices
```

**요청**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON 키 | 설명 |
| --- | --- |
| `mlInstanceId` | ML 서비스를 만드는 데 사용되는 ML 인스턴스를 나타내는 기존 ML 인스턴스 식별. |
| `trainingDataSetId` | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별 |
| `trainingTimeframe` | 교육 실험에 사용될 데이터 필터링에 걸리는 시간을 나타내는 정수 값입니다. 예를 들어 값 `"10080"`은(는) 지난 10080분 또는 168시간의 데이터가 교육 실험 실행에 사용됨을 의미합니다. `"0"` 값은 데이터를 필터링하지 않으며 데이터 집합 내의 모든 데이터가 교육에 사용됩니다. |
| `scoringDataSetId` | 예약된 채점 실험 실행에 사용될 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행 채점에 사용될 데이터 필터링의 시간(분)을 나타내는 정수 값입니다. 예를 들어 값 `"10080"`은(는) 각 예약된 채점 실험 실행에 대해 지난 10080분 또는 168시간의 데이터가 사용됨을 의미합니다. `"0"` 값은 데이터를 필터링하지 않으며 데이터 집합 내의 모든 데이터는 채점에 사용됩니다. |
| `scoringSchedule` | 예약된 채점 실험 실행에 대한 세부 정보를 포함합니다. |
| `scoringSchedule.startTime` | 채점을 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 채점을 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행을 평가할 간격을 나타내는 크론 값. |

**응답**

성공적인 응답은 새로 생성된 ML 서비스의 세부 정보를 반환합니다. 여기에는 각각 해당 교육 및 채점 실험에 대한 `trainingExperimentId` 및 `scoringExperimentId`과(와) 서비스의 고유한 `id`이(가) 포함됩니다.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### 교육 및 채점을 위한 예약된 실험이 포함된 ML 서비스 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

교육 및 채점 실험 실행이 예약된 기존 ML 인스턴스를 ML 서비스로 게시하려면 교육 및 채점 일정을 모두 제공해야 합니다. 이 구성의 ML 서비스가 생성되면 교육 및 채점 모두에 대해 예약된 실험 엔티티도 생성됩니다. 교육 및 채점 일정이 동일하지 않아도 됩니다. 채점 작업 실행 중에 예약된 교육 실험 실행에서 생성된 최신 교육 모델을 가져와 예약된 채점 실행에 사용합니다.

**API 형식**

```http
POST /mlServices
```

**요청**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON 키 | 설명 |
| --- | --- |
| `mlInstanceId` | ML 서비스를 만드는 데 사용되는 ML 인스턴스를 나타내는 기존 ML 인스턴스 식별. |
| `trainingDataSetId` | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별 |
| `trainingTimeframe` | 교육 실험에 사용될 데이터 필터링에 걸리는 시간을 나타내는 정수 값입니다. 예를 들어 값 `"10080"`은(는) 지난 10080분 또는 168시간의 데이터가 교육 실험 실행에 사용됨을 의미합니다. `"0"` 값은 데이터를 필터링하지 않으며 데이터 집합 내의 모든 데이터가 교육에 사용됩니다. |
| `scoringDataSetId` | 예약된 채점 실험 실행에 사용될 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행 채점에 사용될 데이터 필터링의 시간(분)을 나타내는 정수 값입니다. 예를 들어 값 `"10080"`은(는) 각 예약된 채점 실험 실행에 대해 지난 10080분 또는 168시간의 데이터가 사용됨을 의미합니다. `"0"` 값은 데이터를 필터링하지 않으며 데이터 집합 내의 모든 데이터는 채점에 사용됩니다. |
| `trainingSchedule` | 예약된 교육 실험 실행에 대한 세부 정보를 포함합니다. |
| `scoringSchedule` | 예약된 채점 실험 실행에 대한 세부 정보를 포함합니다. |
| `scoringSchedule.startTime` | 채점을 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 채점을 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행을 평가할 간격을 나타내는 크론 값. |

**응답**

성공적인 응답은 새로 생성된 ML 서비스의 세부 정보를 반환합니다. 여기에는 서비스의 고유한 `id`과(와) 해당 교육 및 채점 실험의 `trainingExperimentId` 및 `scoringExperimentId`이(가) 각각 포함됩니다. 아래 예제 응답에서 `trainingSchedule` 및 `scoringSchedule`이(가) 있으면 교육 및 채점을 위한 실험 엔터티가 예약된 실험임을 나타냅니다.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## ML 서비스 조회 {#retrieving-ml-services}

`/mlServices`에 `GET` 요청을 하고 경로에 ML 서비스의 고유한 `id`을(를) 제공하여 기존 ML 서비스를 조회할 수 있습니다.

**API 형식**

```http
GET /mlServices/{SERVICE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SERVICE_ID}` | 조회 중인 ML 서비스의 고유한 `id`입니다. |

**요청**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 ML 서비스의 세부 정보를 반환합니다.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>다른 ML 서비스를 검색하면 키-값 쌍이 더 많거나 적은 응답이 반환될 수 있습니다. 위의 응답은 예약된 교육 및 채점 실험 실행 ](#ml-service-with-scheduled-experiments-for-training-and-scoring)이(가) 모두 있는 [ML 서비스를 나타냅니다.


## 교육 또는 채점 예약

이미 게시된 ML 서비스에 대한 채점 및 교육을 예약하려면 `/mlServices`에 `PUT` 요청으로 기존 ML 서비스를 업데이트하여 예약할 수 있습니다.

**API 형식**

```http
PUT /mlServices/{SERVICE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SERVICE_ID}` | 업데이트하는 ML 서비스의 고유한 `id`입니다. |

**요청**

다음 요청은 각각의 `startTime`, `endTime` 및 `cron` 키와 함께 `trainingSchedule` 및 `scoringSchedule` 키를 추가하여 기존 ML 서비스에 대한 교육 및 채점을 예약합니다.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>기존의 예약된 교육 및 채점 작업에서 `startTime`을(를) 수정하지 마십시오. `startTime`을(를) 수정해야 하는 경우 동일한 모델을 게시하고 교육 및 채점 작업의 일정을 다시 설정하는 것이 좋습니다.

**응답**

성공적인 응답은 업데이트된 ML 서비스의 세부 정보를 반환합니다.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```
