---
keywords: Experience Platform;개발자 안내서;엔드포인트;데이터 과학 작업 공간;인기 항목;mlservices;sensei 기계 학습 api
solution: Experience Platform
title: MLSservices API 끝점
description: MLService는 이전에 개발된 모델에 액세스하고 재사용할 수 있는 기능을 조직에 제공하는 게시된 숙련된 모델입니다. MLServices의 주요 기능은 교육 및 채점을 일정에 따라 자동화하는 기능입니다. 예약된 교육 실행은 모델의 효율성과 정확성을 유지하는 데 도움이 되지만, 예약된 점수 실행에서는 새로운 통찰력이 일관되게 생성됩니다.
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# MLSservices 끝점

MLService는 이전에 개발된 모델에 액세스하고 재사용할 수 있는 기능을 조직에 제공하는 게시된 숙련된 모델입니다. MLServices의 주요 기능은 교육 및 채점을 일정에 따라 자동화하는 기능입니다. 예약된 교육 실행은 모델의 효율성과 정확성을 유지하는 데 도움이 되지만, 예약된 점수 실행에서는 새로운 통찰력이 일관되게 생성됩니다.

자동 교육 및 점수 표는 시작 타임스탬프, 종료 타임스탬프 및 다음과 같이 표시되는 빈도로 정의됩니다 [cron 식](https://en.wikipedia.org/wiki/Cron). 스케줄은 [mlsService 만들기](#create-an-mlservice) 또는 [기존 MLService 업데이트](#update-an-mlservice).

## MLS 서비스 만들기 {#create-an-mlservice}

POST 요청 및 서비스 이름과 유효한 MLInstance ID를 제공하는 페이로드를 수행하여 MLSservice를 만들 수 있습니다. MLService를 만드는 데 사용되는 MLInstance는 기존 교육 실험이 필요하지 않지만 해당 실험 ID 및 교육 실행 ID를 제공하여 기존 훈련 모델로 MLService를 만들도록 선택할 수 있습니다.

**API 형식**

```http
POST /mlServices
```

**요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | MLService에 대해 원하는 이름입니다. 이 MLService에 해당하는 서비스는 서비스 갤러리 UI에 표시할 이 값을 서비스 이름으로 상속합니다. |
| `description` | MLS 서비스에 대한 선택적 설명입니다. 이 MLService에 해당하는 서비스는 서비스 갤러리 UI에 표시될 이 값을 서비스 설명으로 상속합니다. |
| `mlInstanceId` | 유효한 MLInstance ID입니다. |
| `trainingDataSetId` | 제공되는 경우 MLInstance의 기본 데이터 세트 ID를 무시하는 교육 데이터 세트 ID입니다. MLService를 만드는 데 사용되는 MLInstance에서 교육 데이터 세트를 정의하지 않는 경우 적절한 교육 데이터 세트 ID를 제공해야 합니다. |
| `trainingExperimentId` | 선택적으로 제공할 수 있는 실험 ID입니다. 이 값을 제공하지 않으면 MLService를 만들면 MLInstance의 기본 구성을 사용하여 새 실험도 생성됩니다. |
| `trainingExperimentRunId` | 선택적으로 제공할 수 있는 교육 실행 ID입니다. 이 값을 제공하지 않으면 MLService를 만들면 MLInstance의 기본 교육 매개 변수를 사용하여 교육 실행도 생성 및 실행됩니다. |
| `trainingSchedule` | 자동 교육 실행에 대한 일정입니다. 이 속성이 정의된 경우 MLService는 예약된 대로 교육 실행을 자동으로 수행합니다. |
| `trainingSchedule.startTime` | 예약된 교육 실행이 시작되는 타임스탬프입니다. |
| `trainingSchedule.endTime` | 예약된 교육이 실행되는 타임스탬프가 종료됩니다. |
| `trainingSchedule.cron` | 자동화된 교육 실행 빈도를 정의하는 cron 식. |
| `scoringSchedule` | 자동 점수 실행에 대한 일정입니다. 이 속성이 정의된 경우 MLSservice는 예약된 기준에 따라 점수 실행을 자동으로 수행합니다. |
| `scoringSchedule.startTime` | 예약된 점수 실행이 시작되는 타임스탬프입니다. |
| `scoringSchedule.endTime` | 예약된 점수 실행이 끝나는 타임스탬프입니다. |
| `scoringSchedule.cron` | 자동 점수 실행의 빈도를 정의하는 크론 표현식입니다. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 만든 MLSservice의 세부 정보가 포함된 페이로드를 반환합니다`id`), 교육을 위한 실험 ID(`trainingExperimentId`), 점수를 위한 실험 ID(`scoringExperimentId`) 및 입력 교육 데이터 세트 ID(`trainingDataSetId`).

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## MLServices 목록 검색 {#retrieve-a-list-of-mlservices}

단일 GET 요청을 수행하여 MLSservices 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 [자산 검색을 위한 쿼리 매개 변수](./appendix.md#query).

**API 형식**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETER}` | 다음 중 하나 [사용 가능한 쿼리 매개 변수](./appendix.md#query) 결과를 필터링하는 데 사용됩니다. |
| `{VALUE}` | 이전 쿼리 매개 변수의 값입니다. |

**요청**

다음 요청에는 쿼리가 포함되어 있고 동일한 MLInstance ID(`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 MLSservices 목록 및 해당 MLService ID(`{MLSERVICE_ID}`), 교육을 위한 실험 ID(`{TRAINING_ID}`), 점수를 위한 실험 ID(`{SCORING_ID}`) 및 입력 교육 데이터 세트 ID(`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## 특정 MLService 검색 {#retrieve-a-specific-mlservice}

요청 경로에 원하는 MLService ID를 포함하는 GET 요청을 수행하여 특정 실험의 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: 유효한 MLService ID입니다.

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 요청된 MLSservice의 세부 정보가 포함된 페이로드가 반환됩니다.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## MLS 서비스 업데이트 {#update-an-mlservice}

요청 경로에서 Target MLService의 ID를 포함하는 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공하여 기존 MLService를 업데이트할 수 있습니다.

>[!TIP]
>
>이 PUT 요청의 성공을 보장하기 위해 먼저 GET 요청을 수행하십시오로서 [id로 MLS 서비스 검색](#retrieve-a-specific-mlservice). 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청의 페이로드로 적용합니다.

**API 형식**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: 유효한 MLService ID입니다.

**요청**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**응답**

성공적인 응답은 MLService의 업데이트된 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## MLService 삭제

요청 경로에서 target MLService의 ID를 포함하는 DELETE 요청을 수행하여 단일 MLService를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MLSERVICE_ID}` | 유효한 MLService ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLService deletion was successful"
}
```

## MLInstance ID로 MLServices 삭제

MLInstance ID를 쿼리 매개 변수로 지정하는 DELETE 요청을 수행하여 특정 MLInstance에 속하는 모든 MLServices를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MLINSTANCE_ID}` | 유효한 MLInstance ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLServices deletion was successful"
}
```
