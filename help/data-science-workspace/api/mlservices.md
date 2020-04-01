---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 서비스
topic: Developer guide
translation-type: tm+mt
source-git-commit: dabeee04dd6ec2bbdd37a6987efcb54b285df7ca

---


# MLServices

MLService는 이전에 개발된 모델에 액세스하고 재사용할 수 있는 기능을 조직에 제공하는 교육된 게시된 모델입니다. MLServices의 주요 기능은 트레이닝 및 점수의 일정을 자동화하는 기능입니다. 예약된 트레이닝 실행은 모델의 효율성과 정확성을 유지하는 데 도움이 되지만, 예약된 점수 실행은 새로운 인사이트를 일관되게 생성할 수 있습니다.

자동화된 트레이닝 및 점수 지정 일정은 시작 타임스탬프, 종료 타임스탬프 및 <a href="https://en.wikipedia.org/wiki/Cron" target="_blank">cron 표현식으로</a>표시되는 빈도로 정의됩니다. MLService를 [만들 때 예약을](#create-an-mlservice) 정의하거나 기존 MLService를 [업데이트하여 적용할 수 있습니다](#update-an-mlservice).

## MLService 만들기

POST 요청과 서비스 이름과 유효한 MLInstance ID를 제공하는 페이로드를 수행하여 MLService를 만들 수 있습니다. MLService를 만드는 데 사용되는 MLInstance는 기존 교육 실험을 가질 필요는 없지만 해당 실험 ID 및 교육 실행 ID를 제공하여 기존의 교육 모델을 사용하여 MLService를 만들 수도 있습니다.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "trainingDataSetId": "{DATASET_ID}",
        "trainingExperimentId": "{TRAINING_ID}",
        "trainingExperimentRunId": "{RUN_ID}",
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
| `name` | MLService에 대해 원하는 이름입니다. 이 MLService에 해당하는 서비스는 서비스 갤러리 UI에 서비스의 이름으로 표시할 이 값을 상속합니다. |
| `description` | MLService에 대한 선택적 설명입니다. 이 MLService에 해당하는 서비스는 서비스의 설명으로 서비스 갤러리 UI에 표시할 이 값을 상속합니다. |
| `mlInstanceId` | 유효한 MLInstance ID입니다. |
| `trainingDataSetId` | 제공된 경우 MLInstance의 기본 데이터 집합 ID를 무시하는 교육 데이터 집합 ID입니다. MLService를 만드는 데 사용된 MLInstance가 교육 데이터 집합을 정의하지 않으면 적절한 교육 데이터 집합 ID를 제공해야 합니다. |
| `trainingExperimentId` | 선택적으로 제공할 수 있는 실험 ID입니다. 이 값이 제공되지 않으면 MLService를 만들면 MLInstance의 기본 구성을 사용하여 새 Experiment가 생성됩니다. |
| `trainingExperimentRunId` | 선택적으로 제공할 수 있는 교육 실행 ID입니다. 이 값이 제공되지 않으면 MLService를 만들면 MLInstance의 기본 교육 매개 변수를 사용하여 교육 실행도 만들고 실행됩니다. |
| `trainingSchedule` | 자동화된 트레이닝 일정이 실행됩니다. 이 속성이 정의된 경우 MLService는 예약된 대로 교육 실행을 자동으로 수행합니다. |
| `trainingSchedule.startTime` | 예약된 교육 실행이 시작되는 타임스탬프 |
| `trainingSchedule.endTime` | 예약된 교육이 종료되는 타임스탬프 |
| `trainingSchedule.cron` | 자동화된 교육 실행 빈도를 정의하는 cron 식입니다. |
| `scoringSchedule` | 자동 점수 실행 일정 이 속성이 정의된 경우 MLService는 예약된 기준으로 점수 실행을 자동으로 수행합니다. |
| `scoringSchedule.startTime` | 예약된 점수 실행이 시작되는 타임스탬프. |
| `scoringSchedule.endTime` | 예약된 점수 실행이 끝날 타임스탬프. |
| `scoringSchedule.cron` | 자동화된 점수 실행 빈도를 정의하는 cron 표현식. |

**응답**

성공적인 응답은 고유 식별자(`id`), 교육 실험 ID(`trainingExperimentId`), 점수 지정 실험 ID(`scoringExperimentId`), 입력 교육 데이터 집합 ID(`trainingDataSetId`)를 포함하여 새로 만든 MLService의 세부 사항이 포함된 페이로드를 반환합니다.

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
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

## MLServices 목록 검색

단일 GET 요청을 수행하여 MLSerservices 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에서 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 자산 검색을 [위한](./appendix.md#query)쿼리 매개 변수의 부록 섹션을 참조하십시오.

**API 형식**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETER}` | 결과를 필터링하는 데 사용되는 [사용 가능한 쿼리 매개 변수](./appendix.md#query) 중 하나입니다. |
| `{VALUE}` | 이전 쿼리 매개 변수의 값입니다. |

**요청**

다음 요청에는 쿼리가 포함되어 있고 동일한 MLInstance ID(`{MLINSTANCE_ID}`)를 공유하는 MLSerservices 목록을 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId=={MLINSTANCE_ID}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 MLService ID(`{MLSERVICE_ID}`), 교육 실험 ID(`{TRAINING_ID}`), 점수 지정 실험 ID(`{SCORING_ID}`), 입력 교육 데이터 세트 ID(`{DATASET_ID}`)를 포함하여 MLServices 및 세부 사항을 반환합니다.

```json
{
    "children": [
        {
            "id": "{MLSERVICE_ID}",
            "name": "A service created in UI",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "trainingExperimentId": "{TRAINING_ID}",
            "trainingDataSetId": "{DATASET_ID}",
            "scoringExperimentId": "{SCORING_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId=={MLINSTANCE_ID},deleted==false",
        "count": 1
    }
}
```

## 특정 MLService 검색

요청 경로에 원하는 MLService ID를 포함하는 GET 요청을 수행하여 특정 실험 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:유효한 MLService ID입니다.

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 MLService의 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## MLService 업데이트

요청 경로에 대상 MLService ID가 포함된 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공하여 기존 MLService를 업데이트할 수 있습니다.

>[!TIP] 이 PUT 요청의 성공을 보장하기 위해, 먼저 ID로 MLService를 [검색하기 위한 GET 요청을 수행하는 것이 좋습니다](#retrieve-a-specific-mlservice). 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청의 페이로드로 적용합니다.

**API 형식**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:유효한 MLService ID입니다.

**요청**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "trainingExperimentId": "{TRAINING_ID}",
        "trainingDataSetId": "{DATASET_ID}",
        "scoringExperimentId": "{SCORING_ID}",
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
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
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

요청 경로에 대상 MLService의 ID를 포함하는 DELETE 요청을 수행하여 단일 MLService를 삭제할 수 있습니다.

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
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{MLSERVICE_ID}` | 유효한 MLService ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
