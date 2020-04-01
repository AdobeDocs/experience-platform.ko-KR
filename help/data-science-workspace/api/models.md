---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 모델
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# 모델

모델은 비즈니스 사용 사례를 해결하기 위해 내역 데이터 및 구성을 사용하여 교육되는 기계 학습 레서피의 한 예입니다.

## 모델 목록 검색

/models에 대한 단일 GET 요청을 수행하여 모든 모델에 속한 모델 세부 사항 목록을 검색할 수 있습니다. 기본적으로 이 목록은 가장 오래된 생성된 모델에서 자체적으로 순서를 지정하고 결과를 25로 제한합니다. 일부 쿼리 매개 변수를 지정하여 결과를 필터링하도록 선택할 수 있습니다. 사용 가능한 쿼리 목록은 자산 검색을 [위한](./appendix.md#query)쿼리 매개 변수의 부록 섹션을 참조하십시오.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 각 모델 고유 식별자(`id`)를 포함하여 모델의 세부 사항이 포함된 페이로드를 반환합니다.

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
| `modelArtifactUri` | 모델이 저장되는 위치를 나타내는 URI입니다. URI는 모델의 `name` 값으로 끝납니다. |
| `experimentId` | 유효한 실험 ID입니다. |
| `experimentRunId` | 유효한 실험 실행 ID입니다. |

## 특정 모델 검색

단일 GET 요청을 수행하고 요청 경로에서 유효한 모델 ID를 제공하여 특정 모델에 속한 모델 세부 사항 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에서 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 자산 검색을 [위한](./appendix.md#query)쿼리 매개 변수의 부록 섹션을 참조하십시오.

**API 형식**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 교육되었거나 게시된 모델의 식별자입니다. |
| `{EXPERIMENT_RUN_ID}` | 실험 실행의 식별자입니다. |

**요청**

다음 요청에는 쿼리가 포함되어 있고 동일한 experimentRunID({EXPERIMENT_RUN_ID})를 공유하는 교육 모델 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 모델 고유 식별자(`id`)를 포함하여 모델의 세부 사항이 포함된 페이로드를 반환합니다.

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
        "count": 1
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 모델에 해당하는 ID입니다. |
| `modelArtifactUri` | 모델이 저장되는 위치를 나타내는 URI입니다. URI는 모델의 `name` 값으로 끝납니다. |
| `experimentId` | 유효한 실험 ID입니다. |
| `experimentRunId` | 유효한 실험 실행 ID입니다. |

## ID로 모델 업데이트

요청 경로에 대상 모델의 ID가 포함된 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공하여 기존 모델을 업데이트할 수 있습니다.

>[!TIP] 이 PUT 요청의 성공을 보장하기 위해, 먼저 ID로 모델을 검색하기 위한 GET 요청을 수행하는 것이 좋습니다. 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청의 페이로드로 적용합니다.

**API 형식**

```http
PUT /models/{MODEL_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 교육되었거나 게시된 모델의 식별자입니다. |

**요청**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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

성공적인 응답은 Experiment의 업데이트된 세부 사항이 포함된 페이로드를 반환합니다.

```json
{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## ID로 모델 삭제

요청 경로에 대상 모델의 ID를 포함하는 삭제 요청을 수행하여 단일 모델을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /models/{MODEL_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MODEL_ID}` | 교육되었거나 게시된 모델의 식별자입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 모델의 삭제를 확인하는 200 상태가 포함된 페이로드를 반환합니다.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```
