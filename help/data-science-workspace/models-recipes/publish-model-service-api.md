---
keywords: Experience Platform;모델 게시;데이터 과학 작업 공간;인기 항목;sensei 기계 학습 api
solution: Experience Platform
title: Sensei Machine Learning API를 사용하여 서비스로 모델 게시
type: Tutorial
description: 이 자습서에서는 Sensei 기계 학습 API를 사용하여 모델을 서비스로 게시하는 프로세스에 대해 설명합니다.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# 를 사용하여 모델을 서비스로 게시 [!DNL Sensei Machine Learning API]

이 자습서에서는 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## 시작하기

이 자습서에서는 Adobe Experience Platform Data Science Workspace에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 [Data Science Workspace 개요](../home.md) 서비스에 대한 높은 수준의 소개입니다.

이 자습서를 따르려면 기존 ML 엔진, ML 인스턴스 및 실험이 있어야 합니다. API에서 이러한 코드를 만드는 방법에 대한 단계는 [패키지된 레시피 가져오기](./import-packaged-recipe-api.md).

마지막으로 이 자습서를 시작하기 전에 [시작하기](../api/getting-started.md) 개발자 가이드의 섹션을 참조하십시오. [!DNL Sensei Machine Learning] 이 자습서 전체에서 사용되는 필수 헤더를 포함한 API입니다.

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

### 주요 용어

다음 표에서는 이 자습서에서 사용되는 몇 가지 일반적인 용어를 설명합니다.

| 용어 | 정의 |
| --- | --- |
| **기계 학습 인스턴스(ML 인스턴스)** | 의 인스턴스 [!DNL Sensei] 특정 데이터, 매개 변수 및 [!DNL Sensei] 코드가 있어야 합니다. |
| **실험** | 교육 실험 실행, 점수 실험 실행 또는 둘 모두를 보유하는 우산 엔티티. |
| **예약된 실험** | 사용자 정의 스케줄로 제어되는 교육 또는 점수 실험 실행 자동화를 설명하는 용어입니다. |
| **실험 실행** | 교육 또는 채점 실험 의 특정 인스턴스. 특정 경험의 여러 실험 실행은 교육 또는 점수에 사용되는 데이터 세트 값에서 다를 수 있습니다. |
| **숙련된 모델** | 검증, 평가 및 최종 모델에 도착하기 전에 실험 및 기능 엔지니어링 프로세스에 의해 생성된 기계 학습 모델입니다. |
| **게시된 모델** | 교육, 검증 및 평가 후에 완성되고 버전이 지정된 모델이 나타납니다. |
| **기계 학습 서비스(ML 서비스)** | API 종단점을 사용하여 교육 및 점수에 대한 온디맨드 요청을 지원하기 위해 서비스로 배포되는 ML 인스턴스. 기존의 숙련된 실험 실행을 사용하여 ML 서비스를 만들 수도 있습니다. |

## 기존 교육 실험 실행 및 예약된 점수를 사용하여 ML 서비스 만들기

교육 실험 실행을 ML 서비스로 게시하면 점수 계산 실험 실행 POST 요청의 페이로드에 대한 세부 정보를 제공하여 점수 책정을 예약할 수 있습니다. 이렇게 하면 점수부여 예약된 실험 엔티티가 생성됩니다.

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
| `mlInstanceId` | 기존 ML 인스턴스 ID인 ML 서비스를 만드는 데 사용되는 교육 실험 실행은 이 특정 ML 인스턴스에 해당해야 합니다. |
| `trainingExperimentId` | ML 인스턴스 식별에 해당하는 실험 식별 |
| `trainingExperimentRunId` | ML 서비스 게시에 사용할 특정 교육 실험 실행 |
| `scoringDataSetId` | 식별은 예약된 점수 실험 실행에 사용할 특정 데이터 세트를 나타냅니다. |
| `scoringTimeframe` | 실험 실행 점수에 사용할 데이터 필터링에 대한 분을 나타내는 정수 값입니다. 예를 들어 값 `10080` 는 지난 10080 분 또는 168시간의 데이터가 예약된 각 점수 실험 실행에 사용됩니다. 값 `0` 는 데이터를 필터링하지 않고 데이터 세트 내의 모든 데이터를 점수 책정에 사용합니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 사항을 포함합니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값입니다. |

**응답**

성공적인 응답은 고유한 ML 서비스를 포함하여 새로 만든 ML 서비스의 세부 사항을 반환합니다 `id` 그리고 `scoringExperimentId` 해당 점수 실험


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

특정 사용 사례 및 요구 사항에 따라 ML 인스턴스로 ML 서비스를 만드는 것은 교육 일정 및 실험 실행 점수 책정 측면에서 유연합니다. 이 튜토리얼은 다음과 같은 특정 사례를 다룹니다.

- [예정된 트레이닝은 필요하지 않지만 예약된 점수가 필요합니다.](#ml-service-with-scheduled-experiment-for-scoring)
- [교육 및 점수 모두에 대해 예약된 실험 실행이 필요합니다.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

ML 서비스는 교육 또는 점수 실험 예약을 하지 않고 ML 인스턴스를 사용하여 만들 수 있습니다. 이러한 ML 서비스는 일반 실험 개체를 만들고, 교육 및 점수를 위한 단일 실험 실행을 만듭니다.

### 점수를 위한 예약된 실험이 있는 ML 서비스 {#ml-service-with-scheduled-experiment-for-scoring}

채점용으로 예약된 실험 실행으로 ML 인스턴스를 게시하여 ML 서비스를 만들 수 있으며, 이 경우 교육을 위한 일반 실험 개체가 생성됩니다. 교육 실험 실행이 생성되고 모든 예약된 점수 실험 실행에 사용됩니다. 다음을 확인합니다. `mlInstanceId`, `trainingDataSetId`, 및 `scoringDataSetId` ML 서비스를 만드는 데 필요하며, ML 서비스가 존재하며 유효한 값입니다.

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
| `mlInstanceId` | ML 서비스를 만드는 데 사용되는 ML 인스턴스를 나타내는 기존 ML 인스턴스 ID입니다. |
| `trainingDataSetId` | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별 |
| `trainingTimeframe` | 교육 실험에 사용할 데이터 필터링에 대한 분을 나타내는 정수 값입니다. 예를 들어 값 `"10080"` 는 지난 10080 분 또는 168시간의 데이터가 교육 실험 실행에 사용됨을 의미합니다. 값 `"0"` 는 데이터를 필터링하지 않으며 데이터 집합 내의 모든 데이터가 교육에 사용됩니다. |
| `scoringDataSetId` | 식별은 예약된 점수 실험 실행에 사용할 특정 데이터 세트를 나타냅니다. |
| `scoringTimeframe` | 실험 실행 점수에 사용할 데이터 필터링에 대한 분을 나타내는 정수 값입니다. 예를 들어 값 `"10080"` 는 지난 10080 분 또는 168시간의 데이터가 예약된 각 점수 실험 실행에 사용됩니다. 값 `"0"` 는 데이터를 필터링하지 않고 데이터 세트 내의 모든 데이터를 점수 책정에 사용합니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 사항을 포함합니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값입니다. |

**응답**

성공적인 응답은 새로 만든 ML 서비스의 세부 정보를 반환합니다. 여기에는 서비스의 고유한 기능이 포함됩니다 `id`뿐만 아니라 `trainingExperimentId` 및 `scoringExperimentId` 해당 교육 및 채점 실험용으로 각각 제공됩니다.

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

### 교육 및 점수를 위한 예약된 실험이 포함된 ML 서비스 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

예약된 교육 및 점수 실험 실행과 함께 기존 ML 인스턴스를 ML 서비스로 게시하려면 교육 및 점수 일정을 모두 제공해야 합니다. 이 구성의 ML 서비스를 만들면 교육 및 점수 둘 다에 대해 예약된 실험 엔티티가 생성됩니다. 교육 및 점수 지정 일정이 동일할 필요는 없습니다. 점수부여 작업 실행 중에 스케줄링된 훈련 실험 실행으로 생성된 최신 훈련 모델을 가져와 스케줄링된 점수부여 실행에 사용합니다.

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
| `mlInstanceId` | ML 서비스를 만드는 데 사용되는 ML 인스턴스를 나타내는 기존 ML 인스턴스 ID입니다. |
| `trainingDataSetId` | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별 |
| `trainingTimeframe` | 교육 실험에 사용할 데이터 필터링에 대한 분을 나타내는 정수 값입니다. 예를 들어 값 `"10080"` 는 지난 10080 분 또는 168시간의 데이터가 교육 실험 실행에 사용됨을 의미합니다. 값 `"0"` 는 데이터를 필터링하지 않으며 데이터 집합 내의 모든 데이터가 교육에 사용됩니다. |
| `scoringDataSetId` | 식별은 예약된 점수 실험 실행에 사용할 특정 데이터 세트를 나타냅니다. |
| `scoringTimeframe` | 실험 실행 점수에 사용할 데이터 필터링에 대한 분을 나타내는 정수 값입니다. 예를 들어 값 `"10080"` 는 지난 10080 분 또는 168시간의 데이터가 예약된 각 점수 실험 실행에 사용됩니다. 값 `"0"` 는 데이터를 필터링하지 않고 데이터 세트 내의 모든 데이터를 점수 책정에 사용합니다. |
| `trainingSchedule` | 예약된 교육 실험 실행에 대한 세부 정보를 포함합니다. |
| `scoringSchedule` | 예약된 점수 실험 실행에 대한 세부 사항을 포함합니다. |
| `scoringSchedule.startTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.endTime` | 점수를 시작할 시기를 나타내는 날짜/시간입니다. |
| `scoringSchedule.cron` | 실험 실행에 점수를 매길 간격을 나타내는 크론 값입니다. |

**응답**

성공적인 응답은 새로 만든 ML 서비스의 세부 정보를 반환합니다. 여기에는 서비스의 고유한 기능이 포함됩니다 `id`뿐만 아니라 `trainingExperimentId` 및 `scoringExperimentId` 해당 교육 및 채점 실험 중에서 각각 선택합니다. 아래 예제 응답에는 `trainingSchedule` 및 `scoringSchedule` 교육 및 점수에 대한 실험 엔티티가 예약된 실험임을 나타냅니다.

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

기존 ML 서비스를 만들기 위해 `GET` 요청 `/mlServices` 고유한 `id` 경로에 있는 ML 서비스의 매개 변수 값을 나타냅니다.

**API 형식**

```http
GET /mlServices/{SERVICE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SERVICE_ID}` | 고유 `id` 조회하고 있는 ML 서비스 중 |

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
>다른 ML 서비스를 검색하면 하나 이상의 키-값 쌍이 있는 응답을 반환할 수 있습니다. 위의 응답은 [예약된 교육 및 점수 테스트 실행이 모두 포함된 ML 서비스](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## 교육 또는 점수 책정 예약

이미 게시된 ML 서비스에 대한 점수 및 교육을 예약하려는 경우 기존 ML 서비스를 `PUT` 요청 시 `/mlServices`.

**API 형식**

```http
PUT /mlServices/{SERVICE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SERVICE_ID}` | 고유 `id` 업데이트하려는 ML 서비스의 HTML 서비스 중 하나를 선택합니다. |

**요청**

다음 요청은 기존 ML 서비스에 대한 교육 및 점수를 예약하며, `trainingSchedule` 및 `scoringSchedule` 해당 `startTime`, `endTime`, 및 `cron` 키.

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
>수정 안 함 `startTime` 기존 예약된 교육 및 점수 책정 작업 만약 `startTime` 수정해야 합니다. 동일한 모델을 게시하고 교육 및 점수 작업 일정을 조정하십시오.

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
