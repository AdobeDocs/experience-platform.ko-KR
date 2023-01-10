---
keywords: Experience Platform;개발자 안내서;엔드포인트;데이터 과학 작업 공간;인기 항목;모델;sensei 기계 학습 api
solution: Experience Platform
title: 모델 API 끝점
description: 모델은 비즈니스 사용 사례를 해결하기 위해 이전 데이터 및 구성을 사용하여 교육되는 기계 학습 레서피의 예입니다.
exl-id: e66119a9-9552-497c-9b3a-b64eb3b51fcf
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 모델 끝점

모델은 비즈니스 사용 사례를 해결하기 위해 이전 데이터 및 구성을 사용하여 교육되는 기계 학습 레서피의 예입니다.

## 모델 목록 검색

/models에 대한 단일 GET 요청을 수행하여 모든 모델에 속하는 모델 세부 사항 목록을 검색할 수 있습니다. 기본적으로 이 목록은 가장 오래된 작성 모델에서 순서대로 정렬되며 결과를 25로 제한합니다. 일부 쿼리 매개 변수를 지정하여 결과를 필터링하도록 선택할 수 있습니다. 사용 가능한 쿼리 목록은 [자산 검색을 위한 쿼리 매개 변수](./appendix.md#query).

**API 형식**

```http
GET /models
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 각 모델 고유 식별자(`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 모델에 해당하는 ID입니다. |
| `modelArtifactUri` | 모델이 저장되는 위치를 나타내는 URI입니다. URI는 `name` 모델에 대한 값입니다. |
| `experimentId` | 유효한 실험 ID입니다. |
| `experimentRunId` | 올바른 실험 실행 ID입니다. |

## 특정 모델 검색

단일 GET 요청을 수행하고 요청 경로에 유효한 모델 ID를 제공하여 특정 모델에 속하는 모델 세부 사항 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 [자산 검색을 위한 쿼리 매개 변수](./appendix.md#query).

**API 형식**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 훈련되었거나 게시된 모델의 식별자입니다. |
| `{EXPERIMENT_RUN_ID}` | 실험 실행의 식별자입니다. |

**요청**

다음 요청에는 쿼리가 포함되어 있으며 동일한 experimentRunID({EXPERIMENT_RUN_ID})를 공유하는 교육된 모델 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 모델 고유 식별자( )를 포함하여 모델의 세부 정보가 포함된 페이로드가 반환됩니다`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 모델에 해당하는 ID입니다. |
| `modelArtifactUri` | 모델이 저장되는 위치를 나타내는 URI입니다. URI는 `name` 모델에 대한 값입니다. |
| `experimentId` | 유효한 실험 ID입니다. |
| `experimentRunId` | 올바른 실험 실행 ID입니다. |

## 사전 생성된 모델 등록 {#register-a-model}

에 POST 요청을 작성하여 미리 생성된 모델을 등록할 수 있습니다 `/models` 엔드포인트. 모델을 등록하려면 `modelArtifact` 파일 및 `model` 속성 값은 요청 본문에 포함해야 합니다.

**API 형식**

```http
POST /models
```

**요청**

다음 POST에는 `modelArtifact` 파일 및 `model` 필요한 속성 값입니다. 이러한 값에 대한 자세한 내용은 아래 표를 참조하십시오.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `modelArtifact` | 포함할 전체 모델 객체의 위치입니다. |
| `model` | 만들어야 하는 Model 개체의 양식 데이터입니다. |

**응답**

성공적으로 응답하면 모델 고유 식별자( )를 포함하여 모델의 세부 정보가 포함된 페이로드가 반환됩니다`id`).

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 모델에 해당하는 ID입니다. |
| `modelArtifactUri` | 모델이 저장되는 위치를 나타내는 URI입니다. URI는 `id` 값 을 참조하십시오. |

## ID별 모델 업데이트

요청 경로에서 대상 모델의 ID를 포함하는 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공하여 기존 모델을 업데이트할 수 있습니다.

>[!TIP]
>
>이 PUT 요청의 성공을 보장하기 위해, 먼저 ID로 모델을 검색하도록 GET 요청을 수행하는 것이 좋습니다. 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청의 페이로드로 적용합니다.

**API 형식**

```http
PUT /models/{MODEL_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 훈련되었거나 게시된 모델의 식별자입니다. |

**요청**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**응답**

성공적인 응답은 실험에서 업데이트된 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## ID별 모델 삭제

요청 경로에 대상 모델의 ID를 포함하는 DELETE 요청을 수행하여 단일 모델을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /models/{MODEL_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 훈련되었거나 게시된 모델의 식별자입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 모델의 삭제를 확인하는 200 상태가 포함된 페이로드가 반환됩니다.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## 모델에 대한 새 코드 변환 만들기 {#create-transcoded-model}

코드 변환은 한 인코딩의 디지털 대 디지털 직접 변환입니다. 를 제공하여 모델에 대한 새 코드 변환을 만듭니다 `{MODEL_ID}` 그리고 `targetFormat` 새 출력을 입력하려는 경우

**API 형식**

```http
POST /models/{MODEL_ID}/transcodings
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 훈련되었거나 게시된 모델의 식별자입니다. |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**응답**

성공적인 응답은 코드 변환 정보와 함께 JSON 개체가 포함된 페이로드를 반환합니다. 여기에는 전송 고유 식별자(`id`)에서 사용할 수 있습니다. [특정 코드 변환 모델 검색](#retrieve-transcoded-model).

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## 모델의 전송 목록 검색 {#retrieve-transcoded-model-list}

를 사용하여 GET 요청을 수행하여 모델에서 수행된 전송 목록을 검색할 수 있습니다 `{MODEL_ID}`.

**API 형식**

```http
GET /models/{MODEL_ID}/transcodings
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 훈련되었거나 게시된 모델의 식별자입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 모델에서 수행된 각 코드 변환 목록과 함께 json 개체가 포함된 페이로드를 반환합니다. 각 코드 변환 모델은 고유한 식별자(`id`).

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## 특정 코드 변환 모델 검색 {#retrieve-transcoded-model}

로 GET 요청을 수행하여 특정 코드 변환 모델을 검색할 수 있습니다 `{MODEL_ID}` 및 코드 변환된 모델의 id입니다.

**API 형식**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 훈련되었거나 게시된 모델의 고유 식별자입니다. |
| `{TRANSCODING_ID}` | 코드 변환된 모델의 고유 식별자입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 트랜스코딩된 모델의 데이터와 함께 JSON 개체가 포함된 페이로드를 반환합니다.

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```
