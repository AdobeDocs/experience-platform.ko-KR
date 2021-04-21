---
keywords: Experience Platform;모델 게시;데이터 과학 작업 공간;인기 항목;sensei 기계 학습 api
solution: Experience Platform
title: Sensei Machine Learning API를 사용하여 모델을 서비스로 게시
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 Sensei Machine Learning API를 사용하여 모델을 서비스로 게시하는 프로세스를 다룹니다.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# [!DNL Sensei Machine Learning API]

이 자습서에서는 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)을(를) 사용하여 모델을 서비스로 게시하는 프로세스에 대해 설명합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform Data Science Workspace에 대해 자세히 알아야 합니다. 이 자습서를 시작하기 전에 [데이터 과학 작업 공간 개요](../home.md)에서 서비스에 대한 수준 높은 소개를 확인하십시오.

이 튜토리얼을 따라 하려면 기존 ML 엔진, ML 인스턴스 및 실험 버전이 있어야 합니다. API에서 이러한 항목을 만드는 방법에 대한 자세한 내용은 [패키징된 레서피 가져오기](./import-packaged-recipe-api.md)의 자습서를 참조하십시오.

마지막으로 이 자습서를 시작하기 전에 [!DNL Sensei Machine Learning] API를 성공적으로 호출하기 위해 이 자습서에 사용된 필수 헤더를 포함하여,  API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보는 개발자 안내서의 [시작하기](../api/getting-started.md) 섹션을 검토하십시오.

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

### 주요 용어

다음 표에서는 이 자습서에서 사용되는 몇 가지 일반적인 용어에 대해 설명합니다.

| 용어 | 정의 |
--- | ---
| **기계 학습 인스턴스(ML 인스턴스)** | 특정 데이터, 매개 변수 및 [!DNL Sensei] 코드를 포함하는 특정 테넌트에 대한 [!DNL Sensei] 엔진 인스턴스입니다. |
| **실험** | 교육 실험 실행, 채점 실험 실행 또는 둘 다를 실행하기 위한 우산 엔티티. |
| **예약된 실험** | 사용자 정의 일정에 따라 제어되는 교육 또는 점수 실험 실행의 자동화를 설명하는 용어입니다. |
| **실험 실행** | 트레이닝 또는 채점 실험의 특정 인스턴스. 특정 실험에서의 다중 실험 실행은 교육 또는 점수화에 사용되는 데이터 세트 값마다 다를 수 있습니다. |
| **트레이닝된 모델** | 검증되고 평가 및 완료된 모델에 도달하기 전에 실험 및 기능 엔지니어링 프로세스에 의해 만들어진 기계 학습 모델입니다. |
| **게시된 모델** | 종결 및 버전 관리 모델이 트레이닝, 유효성 검사 및 평가 후 도착했습니다. |
| **기계 학습 서비스(ML 서비스)** | API 끝점을 사용한 트레이닝 및 점수 지정 요청에 대한 주문형 요청을 지원하기 위해 서비스로 배포된 ML 인스턴스입니다. 또한 기존 트레이닝된 실험 실행을 사용하여 ML 서비스를 만들 수 있습니다. |

## 기존 교육 실험 실행 및 예약된 점수를 사용하여 ML 서비스 만들기

교육 실험 실행을 ML 서비스로 게시하면 점수 지정 실험 실행에 대한 세부 정보를 제공하여 점수 지정 일정을 예약할 수 있습니다. POST 요청의 페이로드를 참조하십시오. 그러면 점수를 매길 예약된 실험 엔티티가 생성됩니다.

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
| `mlInstanceId` | 기존 ML 인스턴스 ID인 ML 서비스를 만드는 데 사용되는 교육 실험 실행은 이 특정 ML 인스턴스와 일치해야 합니다. |
| `trainingExperimentId` | ML 인스턴스 ID에 해당하는 ID를 실험해 봅니다. |
| `trainingExperimentRunId` | ML 서비스를 게시하는 데 사용할 특정 교육 실험 실행 |
| `scoringDataSetId` | 예약된 점수 실험 실행에 사용할 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행에 사용할 데이터를 필터링하는 시간을 나타내는 정수 값입니다. 예를 들어 `10080` 값은 과거 10080분 또는 168시간이 예약된 각 실험 실행에 사용됨을 의미합니다. `0` 값은 데이터를 필터링하지 않으며 데이터 세트 내의 모든 데이터가 점수를 매기는데 사용됩니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 정보가 들어 있습니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값입니다. |

**응답**

성공적인 응답은 해당 점수 지정 실험에 대한 고유 `id` 및 `scoringExperimentId` 등 새로 만든 ML 서비스의 세부 정보를 반환합니다.


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

특정 사용 사례와 요구 사항에 따라, ML 인스턴스를 사용하여 ML 서비스를 만드는 것은 트레이닝 일정 및 실험 실행 점수 지정 측면에서 유연합니다. 이 자습서에서는 다음과 같은 특정 사례를 살펴봅니다.

- [예약된 교육이 필요하지 않지만 예약된 점수가 필요합니다.](#ml-service-with-scheduled-experiment-for-scoring)
- [교육 및 점수 모두에 대해 예약된 실험 실행이 필요합니다.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

교육 또는 채점 실험을 예약하지 않고도 ML 인스턴스를 사용하여 ML 서비스를 만들 수 있습니다. 이러한 ML 서비스는 일반적인 실험 실체와 트레이닝과 점수를 위한 단일 실험 실행을 만듭니다.

### {#ml-service-with-scheduled-experiment-for-scoring} 점수를 매기기로 예약된 ML 서비스

채점용으로 예약된 실험 실행을 포함하는 ML 인스턴스를 게시하여 ML 서비스를 만들 수 있습니다. 이 경우 일반적인 교육 실험 엔티티를 만들 수 있습니다. 교육 실험 실행이 생성되고 모든 예약된 점수 실험 실행에 사용됩니다. ML 서비스를 만드는 데 필요한 `mlInstanceId`, `trainingDataSetId` 및 `scoringDataSetId`가 있고 해당 서비스가 존재하며 유효한 값인지 확인하십시오.

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
| `trainingDataSetId` | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별. |
| `trainingTimeframe` | 교육 실험에 사용할 데이터 필터링 시간을 나타내는 정수 값입니다. 예를 들어 `"10080"` 값은 지난 10080분 또는 168시간이 교육 실험 실행에 사용됨을 의미합니다. `"0"` 값은 데이터를 필터링하지 않습니다. 데이터 세트 내의 모든 데이터는 교육에 사용됩니다. |
| `scoringDataSetId` | 예약된 점수 실험 실행에 사용할 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행에 사용할 데이터를 필터링하는 시간을 나타내는 정수 값입니다. 예를 들어 `"10080"` 값은 과거 10080분 또는 168시간이 예약된 각 실험 실행에 사용됨을 의미합니다. `"0"` 값은 데이터를 필터링하지 않으며 데이터 세트 내의 모든 데이터가 점수를 매기는데 사용됩니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 정보가 들어 있습니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값입니다. |

**응답**

성공적으로 응답하면 새로 만든 ML 서비스의 세부 정보가 반환됩니다. 여기에는 각각 해당 교육 및 채점 실험용 `trainingExperimentId` 및 `scoringExperimentId`뿐만 아니라 서비스의 고유한 `id`도 포함됩니다.

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

### 교육 및 채점 {#ml-service-with-scheduled-experiments-for-training-and-scoring}에 대한 예약된 실험과 함께 ML 서비스

예약된 트레이닝 및 점수 지정 실험 실행이 있는 ML 서비스로 기존 ML 인스턴스를 게시하려면 교육 및 점수 지정 일정을 모두 제공해야 합니다. 이 구성의 ML 서비스가 생성되면 교육 및 점수 모두에 대해 예약된 실험 엔티티도 생성됩니다. 교육 및 채점 일정이 동일할 필요는 없습니다. 점수 지정 작업 실행 중에 예약된 교육 실험 실행에 의해 생성된 최신 교육 모델을 가져와 예약된 점수 책정기에 사용합니다.

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
| `trainingDataSetId` | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별. |
| `trainingTimeframe` | 교육 실험에 사용할 데이터 필터링 시간을 나타내는 정수 값입니다. 예를 들어 `"10080"` 값은 지난 10080분 또는 168시간이 교육 실험 실행에 사용됨을 의미합니다. `"0"` 값은 데이터를 필터링하지 않습니다. 데이터 세트 내의 모든 데이터는 교육에 사용됩니다. |
| `scoringDataSetId` | 예약된 점수 실험 실행에 사용할 특정 데이터 세트를 참조하는 식별. |
| `scoringTimeframe` | 실험 실행에 사용할 데이터를 필터링하는 시간을 나타내는 정수 값입니다. 예를 들어 `"10080"` 값은 과거 10080분 또는 168시간이 예약된 각 실험 실행에 사용됨을 의미합니다. `"0"` 값은 데이터를 필터링하지 않으며 데이터 세트 내의 모든 데이터가 점수를 매기는데 사용됩니다. |
| `trainingSchedule` | 예약된 교육 실험 실행에 대한 세부 사항을 포함합니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 정보가 들어 있습니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값입니다. |

**응답**

성공적으로 응답하면 새로 만든 ML 서비스의 세부 정보가 반환됩니다. 여기에는 서비스의 고유한 `id`뿐만 아니라 해당 교육 및 채점 실험의 `trainingExperimentId` 및 `scoringExperimentId`도 각각 포함됩니다. 아래 예제 응답에서 `trainingSchedule` 및 `scoringSchedule`의 존재 여부에 따라 교육 및 채점용 실험 엔티티가 예약된 실험임을 알 수 있습니다.

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

## ML 서비스 {#retrieving-ml-services} 조회

`GET` 요청을 `/mlServices`에 만들고 경로에 ML 서비스의 고유한 `id`를 제공하여 기존 ML 서비스를 조회할 수 있습니다.

**API 형식**

```http
GET /mlServices/{SERVICE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SERVICE_ID}` | 찾고 있는 ML 서비스의 고유한 `id`. |

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
>다른 ML 서비스를 검색하면 키-값 쌍 이상의 응답이 반환될 수 있습니다. 위의 응답은 예약된 교육과 점수 지정 실험 실행](#ml-service-with-scheduled-experiments-for-training-and-scoring)이 모두 포함된 [ML 서비스의 표현입니다.


## 트레이닝 또는 점수 지정 예약

이미 게시된 ML 서비스에 대한 채점 및 트레이닝을 예약하려면 `/mlServices`의 `PUT` 요청과 함께 기존 ML 서비스를 업데이트하면 됩니다.

**API 형식**

```http
PUT /mlServices/{SERVICE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SERVICE_ID}` | 업데이트하는 ML 서비스의 고유한 `id`. |

**요청**

다음 요청은 해당 `startTime`, `endTime` 및 `cron` 키에 `trainingSchedule` 및 `scoringSchedule` 키를 추가하여 기존 ML 서비스에 대한 트레이닝과 점수를 예약합니다.

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
>기존의 예약된 교육 및 점수 지정 작업에서 `startTime`을(를) 수정하지 마십시오. `startTime`을(를) 수정해야 하는 경우 동일한 모델을 게시하고 교육 및 점수 지정 작업의 일정을 다시 잡는 것이 좋습니다.

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
