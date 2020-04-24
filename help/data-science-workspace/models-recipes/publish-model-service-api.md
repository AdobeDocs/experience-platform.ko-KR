---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 모델을 서비스로 게시(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# 모델을 서비스로 게시(API)

## 전제 조건

- 이 자습서에 [따라](../../tutorials/authentication.md) API 호출 작업을 시작할 수 있습니다.
이제 튜토리얼에서 다음 정보를 확인하십시오.
   - `{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.
   - `{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명
   - `{API_KEY}`:고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값
- 이 자습서에서는 기존 ML 엔진, ML 인스턴스 및 실험 엔티티가 필요합니다. ML 엔진, [ML 인스턴스](./import-packaged-recipe-api.md) 또는 실험 엔티티 만들기에 대한 이 자습서를 참조하십시오.
- 이 튜토리얼에서 언급한 API 끝점과 요청에 대한 자세한 내용은 전체 Sensei Machine [Learning API를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## 주요 용어

이 자습서에서 사용되는 몇 가지 일반적인 용어:

| 용어 | 정의 |
--- | ---
| **기계 학습 인스턴스(ML 인스턴스)** | 특정 데이터, 매개 변수 및 Sensei 코드로 구성된 특정 테넌트의 Sensei 엔진 인스턴스인 개념 개체 |
| **실험** | 교육 실험 실행, 점수 지정 실험 실행 또는 둘 다를 실행하기 위한 우산 엔티티. |
| **예약된 실험** | 사용자 정의 일정에 의해 제어되는 교육 또는 점수 실험 실행의 자동화를 설명하는 용어입니다. |
| **실험 실행** | 교육 또는 채점 테스트의 특정 인스턴스. 특정 실험에서의 다중 실험 실행은 트레이닝 또는 점수부여에 사용되는 데이터 세트 값에서 다를 수 있습니다. |
| **교육된 모델** | 검증되고 평가 및 최종 모델을 제공하기 전에 실험 및 기능 엔지니어링 프로세스에 의해 만들어진 기계 학습 모델입니다. |
| **게시된 모델** | 종결 및 버전 관리 모델이 트레이닝, 유효성 검사 및 평가 후 도착했습니다. |
| **ML(Machine Learning Service)** | 종단점을 통한 트레이닝 및 점수 지정 요청 시 지원을 위해 서비스로 배포된 ML 인스턴스. 또한 ML 서비스는 기존의 트레이닝된 실험 실행을 사용하여 만들 수 있습니다. |


## API 워크플로우

이 자습서에서는 ML 서비스 만들기, 검색 및 업데이트에 대해 살펴봅니다.

## 기존 트레이닝 실행 및 예약된 점수 지정으로 ML 서비스 만들기

교육 실험 실행을 ML 서비스로 게시할 때 {JSON_PAYLOAD}에서 점수 지정 실험 실행에 대한 세부 정보를 제공하여 점수 `scoringSchedule` 매기기를 예약할 수 있습니다. 그러면 점수에 대해 예약된 실험 엔티티가 생성됩니다. 해당 값이 `mlInstanceId`, `trainingExperimentId``trainingExperimentRunId`및 `scoringDataSetId`존재하며 유효한 값인지 확인합니다.

시작하려면 `POST` 요청을 `/mlServices`하십시오. 다음은 샘플 curl 명령입니다.

**요청**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` :고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값
- `{IMS_ORG}` : IMS 조직 ID 파섹
- `{ACCESS_TOKEN}` :인증 후에 제공된 특정 베어러 토큰 값입니다.
- `{JSON_PAYLOAD}` :다음은 JSON 페이로드 형식의 예입니다.

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` :기존 ML 인스턴스 ID인 ML 서비스를 만드는 데 사용되는 교육 실험 실행은 이 특정 ML 인스턴스에 해당되어야 합니다.
- `trainingExperimentId` :ML 인스턴스 ID에 해당하는 ID를 실험해 봅니다.
- `trainingExperimentRunId` :ML 서비스를 게시하는 데 사용할 특정 교육 실험 실행
- `scoringDataSetId` :예약된 점수 실험 실행에 사용할 특정 데이터 세트를 참조하는 ID입니다.
- `scoringTimeframe` :실험 실행에 사용할 데이터 필터링에 대한 시간을 나타내는 정수 값. 예를 들어 값이 `"10080"` 있으면 지난 10080분 또는 168시간의 데이터가 예약된 점수 실험 실행에 사용됩니다. 값은 데이터를 필터링하지 `"0"` 않으며 데이터 세트 내의 모든 데이터를 채점하는 데 사용합니다.
- `scoringSchedule` :예약된 점수 지정 실험 실행에 대한 세부 사항이 포함되어 있습니다.
- `startTime` : 정의.
- `endTime` : 정의.
- `cron` : 정의.

**응답**

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

JSON 응답에서 해당 값이 `scoringExperimentId` 있는 키는 요청에 제공한 실험 일정과 함께 새로운 점수 지정 실험이 생성되었음을 `POST` 제안합니다. 응답의 `id` 키는 생성된 ML 서비스를 고유하게 식별합니다.

## 기존 ML 인스턴스에서 ML 서비스 만들기

특정 사용 사례와 요구 사항에 따라, ML 인스턴스를 사용하여 ML 서비스를 만드는 것은 트레이닝 일정 및 실험 실행 점수 지정 측면에서 유연합니다. 이 자습서에서는 다음과 같은 특정 사례를 살펴봅니다.

- [예약된 교육이 필요하지 않지만 예약된 점수가 필요합니다.](#ml-service-with-scheduled-experiment-for-scoring)
- [트레이닝 및 점수 모두에 대해 예약된 실험 실행이 필요합니다.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

교육 또는 채점 실험을 예약하지 않고도 ML 인스턴스를 사용하여 ML 서비스를 만들 수 있습니다. 이러한 ML 서비스는 일반적인 실험 실체와 트레이닝과 점수 매기기를 위한 단일 실험 실행을 만듭니다.

### 점수 매기기로 예약된 ML 서비스 {#ml-service-with-scheduled-experiment-for-scoring}

채점용으로 예약된 실험 실행을 사용하여 ML 인스턴스를 게시하여 ML 서비스를 만들면 일반 교육 실험 개체가 생성됩니다. 생성된 교육 실험 실행은 예약된 모든 점수 지정 실험 실행에 사용됩니다. ML 서비스 생성에 `mlInstanceId`필요한 XML `trainingDataSetId``scoringDataSetId` Service가 존재하며 유효한 값인지 확인합니다.

시작하려면 `POST` 요청을 `/mlServices`하십시오. 다음은 샘플 curl 명령입니다.

**요청**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` :고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값
- `{IMS_ORG}` : IMS 조직 ID 파섹
- `{ACCESS_TOKEN}` :인증 후에 제공된 특정 베어러 토큰 값입니다.
- `{JSON_PAYLOAD}` :다음은 JSON 페이로드 형식의 예입니다.

```JSON
{
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
}
```

| JSON 키 | 설명 |
| --- | --- |
| **`mlInstanceId`** | ML 서비스를 만드는 데 사용되는 ML 인스턴스를 나타내는 기존 ML 인스턴스 ID입니다. |
| **`trainingDataSetId`** | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별. |
| **`trainingTimeframe`** | 교육 실험에 사용할 데이터 필터링에 대한 시간을 나타내는 정수 값. 예를 들어 값이 `"10080"` 이면 지난 10080분 또는 168시간의 데이터가 교육 실험 실행에 사용됩니다. 값은 데이터를 필터링하지 `"0"` 않으며 데이터 세트 내의 모든 데이터가 교육에 사용됩니다. |
| **`scoringDataSetId`** | 예약된 점수 실험 실행에 사용할 특정 데이터 세트를 참조하는 ID입니다. |
| **`scoringTimeframe`** | 실험 실행에 사용할 데이터 필터링에 대한 시간을 나타내는 정수 값. 예를 들어 값이 `"10080"` 있으면 지난 10080분 또는 168시간의 데이터가 예약된 점수 실험 실행에 사용됩니다. 값은 데이터를 필터링하지 `"0"` 않으며 데이터 세트 내의 모든 데이터를 채점하는 데 사용합니다. |
| **`scoringSchedule`** | 예약된 점수 지정 실험 실행에 대한 세부 사항이 포함되어 있습니다. |

**응답**

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

응답에서 키 `JSON` 및 `trainingExperimentId` `scoringExperimentId` 제안은 이 ML 서비스에 대해 새로운 트레이닝 및 점수 지정 실체가 생성되었음을 나타냅니다. 객체가 존재하면 실험 실행 일정 `scoringSchedule` 점수에 대한 세부 사항이 표시됩니다. 응답의 `id` 키는 방금 만든 ML 서비스를 나타냅니다.

### 트레이닝 및 채점용 시험 일정이 잡힌 ML 서비스 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

예약된 트레이닝 및 점수 지정 실험 실행을 사용하여 기존 ML 인스턴스를 ML 서비스로 게시하려면 교육 및 점수 지정 일정을 모두 제공해야 합니다. 이 구성의 ML 서비스가 생성되면 교육 및 점수 모두에 대해 예약된 실험 엔티티도 생성됩니다. 교육 및 점수 지정 일정은 동일할 필요는 없습니다. 점수 지정 작업 실행 동안 예약된 교육 실험 실행으로 제작된 최신 교육 모델이 가져와 예약된 점수 책정기에 사용됩니다.

ML 서비스를 만들려면 추가할 ML 서비스 개체를 `POST` 나타내는 `/mlServices` ML 서비스 개체로 요청을 `{JSON_PAYLOAD}` 수행하십시오. 가 `mlInstanceId`, `trainingDataSetId`및 `scoringDataSetId` 존재하며 유효한 값인지 확인합니다.

**요청**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` :고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값
- `{IMS_ORG}` : IMS 조직 ID 파섹
- `{ACCESS_TOKEN}` :인증 후에 제공된 특정 베어러 토큰 값입니다.
- `{JSON_PAYLOAD}` :다음은 JSON 페이로드 형식의 예입니다.

```JSON
{
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
}
```

| JSON 키 | 설명 |
| --- | --- |
| **`mlInstanceId`** | ML 서비스를 만드는 데 사용되는 ML 인스턴스를 나타내는 기존 ML 인스턴스 ID입니다. |
| **`trainingDataSetId`** | 교육 실험에 사용할 특정 데이터 세트를 참조하는 식별. |
| **`trainingTimeframe`** | 교육 실험에 사용할 데이터 필터링에 대한 시간을 나타내는 정수 값. 예를 들어 값이 `"10080"` 이면 지난 10080분 또는 168시간의 데이터가 교육 실험 실행에 사용됩니다. 값은 데이터를 필터링하지 `"0"` 않으며 데이터 세트 내의 모든 데이터가 교육에 사용됩니다. |
| **`scoringDataSetId`** | 예약된 점수 실험 실행에 사용할 특정 데이터 세트를 참조하는 ID입니다. |
| **`scoringTimeframe`** | 실험 실행에 사용할 데이터 필터링에 대한 시간을 나타내는 정수 값. 예를 들어 값이 `"10080"` 있으면 지난 10080분 또는 168시간의 데이터가 예약된 점수 실험 실행에 사용됩니다. 값은 데이터를 필터링하지 `"0"` 않으며 데이터 세트 내의 모든 데이터를 채점하는 데 사용합니다. |
| **`trainingSchedule`** | 예약된 교육 실험 실행에 대한 세부 사항을 포함합니다. |
| **`scoringSchedule`** | 예약된 점수 지정 실험 실행에 대한 세부 사항이 포함되어 있습니다. |

**응답**

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

응답 본문에 `trainingExperimentId` 및 `scoringExperimentId` 를 추가하면 트레이닝과 점수 모두에 대해 실험 개체가 생성됩니다. 위에 언급된 `trainingSchedule` 교육 및 점수 지정 실험 엔티티가 예약된 실험임을 `scoringSchedule` 표시하고 제안합니다. 응답의 `id` 키는 방금 만든 ML 서비스를 나타냅니다.

## ML 서비스 검색 {#retrieving-ml-services}

기존 ML 서비스를 검색하는 것은 종단점에 대한 `GET` 요청을 하는 것만큼 간단합니다 `/mlServices` . 검색하려는 특정 ML 서비스에 대한 ML 서비스 ID가 있어야 합니다.

**요청**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` :고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값
- `{IMS_ORG}` : IMS 조직 ID 파섹
- `{ACCESS_TOKEN}` :인증 후에 제공된 특정 베어러 토큰 값입니다.

**응답**

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

JSON 응답은 ML 서비스 개체를 나타냅니다. 이 개체는 ML 서비스를 만들 때의 응답과 같습니다. 서로 다른 ML 서비스를 검색하면 키-값 쌍보다 많거나 적은 수의 응답이 반환될 수 있습니다. 위의 응답은 예약된 트레이닝과 점수 [지정 실험 실행을 모두 포함하는 ML 서비스의 표현입니다](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## 트레이닝 또는 점수 지정 예약

이미 게시된 ML 서비스에 대한 채점 및 트레이닝을 예약하려는 경우 `PUT` 요청을 통해 기존 ML 서비스를 업데이트하면 `/mlServices`됩니다. 업데이트하려는 ML 서비스 ID가 있어야 합니다. 참조용으로 업데이트할 ML [서비스를](#retrieving-ml-services) 검색하는 것은 유용한 첫 번째 단계일 수 있습니다.

**요청**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` :업데이트할 ML 서비스를 참조하는 고유 ID입니다.
- `{API_KEY}` :고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값
- `{IMS_ORG}` : IMS 조직 ID 파섹
- `{ACCESS_TOKEN}` :인증 후에 제공된 특정 베어러 토큰 값입니다.
- `{JSON_PAYLOAD}` :다음은 JSON 페이로드 형식의 예입니다.

```JSON
{
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
}
```

트레이닝 및 점수 예약은 해당 키, `trainingSchedule` 키, `scoringSchedule` 키와 함께 `startTime`및 `endTime`키를 추가하여 수행할 수 `cron` 있습니다.

>[!NOTE] 이 `PUT` 요청을 통해 기존의 예약된 실험 실행으로 서비스를 수정할 `mlServices` 수 있습니다. 예약된 **기존 트레이닝 및 점수 지정 작업을 수정하지 마십시오** `startTime` . 수정해야 `startTime` 하는 경우 동일한 모델을 게시하고 교육 및 점수 지정 작업의 일정을 조정하십시오.

**응답**

응답은 `{JSON_PAYLOAD}` 가 되지만 개체에 추가 `id`, `created`및 `updated` 키가 있습니다.

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
