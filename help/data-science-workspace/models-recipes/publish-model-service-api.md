---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics;sensei machine learning api
solution: Experience Platform
title: 모델을 서비스로 게시(API)
topic: tutorial
type: Tutorial
description: 이 자습서에서는 Sensei Machine Learning API를 사용하여 모델을 서비스로 게시하는 프로세스에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 1%

---


# 모델을 서비스로 게시(API)

이 자습서에서는 모델을 서비스를 사용하여 서비스로 게시하는 프로세스에 대해 설명합니다 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## 시작하기

이 자습서에서는 Adobe Experience Platform 데이터 과학 작업 공간에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 [데이터 과학 작업 공간 개요를](../home.md) 검토하여 서비스에 대한 자세한 내용을 살펴보십시오.

이 튜토리얼을 따라 하려면 기존 ML 엔진, ML 인스턴스 및 실험 버전이 있어야 합니다. API에서 이러한 항목을 만드는 방법에 대한 단계는 패키지된 레시피 [가져오기에 대한 자습서를 참조하십시오](./import-packaged-recipe-api.md).

마지막으로, 이 자습서를 시작하기 전에 개발자 안내서의 [시작하기](../api/getting-started.md) 섹션 [!DNL Sensei Machine Learning] 에서 API를 성공적으로 호출하기 위해 이 자습서 전체에 사용된 필수 헤더를 포함하여, 알아야 하는 중요한 정보가 필요하면 이자습서를 참조하십시오.

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

### 주요 용어

다음 표에서는 이 자습서에서 사용되는 몇 가지 일반적인 용어에 대해 설명합니다.

| 용어 | 정의 |
--- | ---
| **기계 학습 인스턴스(ML 인스턴스)** | 특정 데이터, 매개 변수 및 [!DNL Sensei] [!DNL Sensei] 코드를 포함하는 특정 테넌트에 대한 엔진 인스턴스입니다. |
| **실험** | 교육 실험 실행, 점수 지정 실험 실행 또는 둘 모두를 보유하는 상위 엔티티. |
| **실험 예약** | 사용자 정의 일정에 의해 제어되는 교육 또는 점수 실험 실행의 자동화를 설명하는 용어입니다. |
| **실험 실행** | 트레이닝 또는 채점 실험의 특정 인스턴스. 특정 실험에서의 다중 실험 실행은 교육 또는 점수 지정에 사용되는 데이터 세트 값에서 다를 수 있습니다. |
| **교육된 모델** | 검증된 모델에 도달하기 전에 실험 및 기능 엔지니어링 프로세스에 의해 만들어진 기계 학습 모델입니다. |
| **게시된 모델** | 종결 및 버전 관리 모델이 트레이닝, 유효성 검사 및 평가 후 도착했습니다. |
| **기계 학습 서비스(ML 서비스)** | API 종단점을 사용한 트레이닝 및 점수에 대한 온디맨드 요청을 지원하기 위해 서비스로 배포된 ML 인스턴스입니다. 또한 기존 트레이닝된 실험 실행을 사용하여 ML 서비스를 만들 수 있습니다. |

## 기존 트레이닝 실험 실행 및 예약된 점수를 사용하여 ML 서비스 만들기

교육 실험 실행을 ML 서비스로 게시하면 점수 지정 실험 실행에 POST 요청의 페이로드를 세부적으로 제공하여 점수 지정 일정을 예약할 수 있습니다. 그러면 점수에 대해 예약된 실험 엔티티가 생성됩니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}'
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
--- | ---
| `mlInstanceId` | 기존 ML 인스턴스 ID인 ML 서비스를 만드는 데 사용되는 교육 실험 실행은 이 특정 ML 인스턴스에 해당되어야 합니다. |
| `trainingExperimentId` | ML 인스턴스 식별에 해당하는 실험 식별 |
| `trainingExperimentRunId` | ML 서비스를 게시하는 데 사용할 특정 교육 실험 실행 |
| `scoringDataSetId` | 예약된 점수 실험 실행에 사용될 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행에 사용할 데이터를 필터링하는 시간을 나타내는 정수 값. 예를 들어 값이 `10080` 지난 10080분 또는 168시간의 데이터를 각 예약된 점수 실험 실행에 사용합니다. 값 `0` 은 데이터를 필터링하지 않으며 데이터 세트 내의 모든 데이터는 점수 지정에 사용됩니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 사항을 포함합니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값. |

**응답**

성공적인 응답은 고유 및 해당 점수 실험 `id` 에 대한 세부 사항 `scoringExperimentId` 을 비롯하여 새로 만든 ML 서비스의 세부 사항을 반환합니다.


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

## 기존 ML 인스턴스에서 ML 서비스 생성

특정 사용 사례와 요구 사항에 따라, ML 인스턴스를 사용하여 ML 서비스를 만드는 것은 트레이닝 예약과 실험 실행을 평가하는 측면에서 유연합니다. 이 자습서는 다음과 같은 특정 사례를 살펴봅니다.

- [예약된 교육이 필요하지 않지만 예약된 점수가 필요합니다.](#ml-service-with-scheduled-experiment-for-scoring)
- [트레이닝과 점수 모두에 대해 예약된 실험 실행이 필요합니다.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

교육 또는 점수 지정 실험을 예약하지 않고도 ML 인스턴스를 사용하여 ML 서비스를 만들 수 있습니다. 이러한 ML 서비스는 일반 실험 실체뿐만 아니라 트레이닝과 채점용으로 단일 실험 실행을 만들 것입니다.

### 점수 매기기를 위한 ML 서비스 {#ml-service-with-scheduled-experiment-for-scoring}

채점용으로 예약된 실험 실행이 포함된 ML 인스턴스를 게시하여 ML 서비스를 만들 수 있습니다. 그러면 일반 실험 실체가 생성되어 트레이닝할 수 있습니다. 교육 실험 실행이 생성되고 모든 예약된 점수 실험 실행에 사용됩니다. ML 서비스 `mlInstanceId`를 만드는 데 필요한 `trainingDataSetId`값 `scoringDataSetId` 과 값이 있는지 확인합니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `mlInstanceId` | ML 서비스를 만드는 데 사용되는 ML 인스턴스를 나타내는 기존 ML 인스턴스 ID입니다. |
| `trainingDataSetId` | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별 |
| `trainingTimeframe` | 교육 실험에 사용할 데이터 필터링에 대한 시간을 나타내는 정수 값. 예를 들어, 값 `"10080"` 은 지난 10080분 또는 168시간의 데이터를 교육 실험 실행에 사용한다는 의미입니다. 값 `"0"` 은 데이터를 필터링하지 않으며 데이터 세트 내의 모든 데이터는 교육에 사용됩니다. |
| `scoringDataSetId` | 예약된 점수 실험 실행에 사용될 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행에 사용할 데이터를 필터링하는 시간을 나타내는 정수 값. 예를 들어 값이 `"10080"` 지난 10080분 또는 168시간의 데이터를 각 예약된 점수 실험 실행에 사용합니다. 값 `"0"` 은 데이터를 필터링하지 않으며 데이터 세트 내의 모든 데이터는 점수 지정에 사용됩니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 사항을 포함합니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값. |

**응답**

성공적인 응답은 새로 만든 ML 서비스의 세부 정보를 반환합니다. 여기에는 서비스의 고유한 기능 `id`과 해당 트레이닝 및 점수 실험 `trainingExperimentId` 에 대한 `scoringExperimentId` 및 해당 정보가 포함됩니다.

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

### 트레이닝 및 채점하기 위한 예약된 실험을 포함한 ML 서비스 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

예약된 교육 및 점수 실험 실행이 있는 ML 서비스로 기존 ML 인스턴스를 게시하려면 교육 및 점수 지정 일정을 모두 제공해야 합니다. 이 구성의 ML 서비스가 생성되면 교육 및 점수 모두에 대해 예약된 실험 엔티티가 생성됩니다. 교육 및 점수 지정 일정은 동일할 필요는 없습니다. 점수 지정 작업 실행 중, 예약된 교육 실험 실행에 의해 생성된 최신 교육 모델이 가져와 예약된 점수 책정기에 사용됩니다.

**API 형식**

```http
POST /mlServices
```

**요청**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `mlInstanceId` | ML 서비스를 만드는 데 사용되는 ML 인스턴스를 나타내는 기존 ML 인스턴스 ID입니다. |
| `trainingDataSetId` | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별 |
| `trainingTimeframe` | 교육 실험에 사용할 데이터 필터링에 대한 시간을 나타내는 정수 값. 예를 들어, 값 `"10080"` 은 지난 10080분 또는 168시간의 데이터를 교육 실험 실행에 사용한다는 의미입니다. 값 `"0"` 은 데이터를 필터링하지 않으며 데이터 세트 내의 모든 데이터는 교육에 사용됩니다. |
| `scoringDataSetId` | 예약된 점수 실험 실행에 사용될 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행에 사용할 데이터를 필터링하는 시간을 나타내는 정수 값. 예를 들어 값이 `"10080"` 지난 10080분 또는 168시간의 데이터를 각 예약된 점수 실험 실행에 사용합니다. 값 `"0"` 은 데이터를 필터링하지 않으며 데이터 세트 내의 모든 데이터는 점수 지정에 사용됩니다. |
| `trainingSchedule` | 예약된 교육 실험 실행에 대한 세부 사항을 포함합니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 사항을 포함합니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값. |

**응답**

성공적인 응답은 새로 만든 ML 서비스의 세부 정보를 반환합니다. 여기에는 서비스의 고유한 기능 `id`과 해당 트레이닝 및 채점 실험 `trainingExperimentId` 과 `scoringExperimentId` 가 각각 포함됩니다. 아래 예제 응답에서 교육 및 점수 `trainingSchedule` 를 위한 실험 엔티티가 예정된 실험임을 `scoringSchedule` 제안합니다.

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

경로에 ML 서비스의 고유한 기능을 제공하고 요청하여 기존 ML 서비스 `GET` `/mlServices` `id` 를 조회할 수 있습니다.

**API 형식**

```http
GET /mlServices/{SERVICE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SERVICE_ID}` | 원하는 ML 서비스 `id` 의 고유한 기능 |

**요청**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>다른 ML 서비스를 검색하면 키-값 쌍보다 많거나 적은 수의 응답이 반환될 수 있습니다. 위 응답은 예약된 트레이닝과 점수 지정 실험 실행 [](#ml-service-with-scheduled-experiments-for-training-and-scoring)기능이 있는 ML 서비스의 표현입니다.


## 트레이닝 또는 점수 지정 예약

이미 게시된 ML 서비스에 대한 채점 및 트레이닝을 예약하려는 경우 기존 ML 서비스를 `PUT` 요청과 함께 업데이트하면 됩니다 `/mlServices`.

**API 형식**

```http
PUT /mlServices/{SERVICE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SERVICE_ID}` | 업데이트하려는 ML 서비스 `id` 의 고유 |

**요청**

다음 요청은 해당, 키 및 키를 함께 추가하여 기존 ML 서비스 `trainingSchedule` 에 대한 교육 및 점수 `scoringSchedule` 를 `startTime`예약합니다 `endTime``cron` .

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>기존의 예약된 교육 및 점수 지정 작업 `startTime` 을 수정하지 마십시오. 수정할 `startTime` 경우 동일한 모델을 게시하고 교육 및 점수 지정 작업의 일정을 조정하십시오.

**응답**

성공적으로 응답하면 업데이트된 ML 서비스의 세부 정보가 반환됩니다.

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
