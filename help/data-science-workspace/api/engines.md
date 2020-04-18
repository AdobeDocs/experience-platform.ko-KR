---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 엔진
topic: Developer guide
translation-type: tm+mt
source-git-commit: 2940f69d193ff8a4ec6ad4a58813b5426201ef45

---


# 엔진

엔진은 데이터 과학 작업 영역의 머신 러닝 모델을 위한 토대입니다. 특정 문제를 해결하는 머신 러닝 알고리즘, 기능 엔지니어링 수행 기능 파이프라인 또는 두 가지 모두를 포함합니다.

## Docker 레지스트리 검색

>[!TIP]
>Docker URL이 없는 경우 소스 파일을 [레서피](../models-recipes/package-source-files-recipe.md) 자습서로 패키징하여 Docker 호스트 URL 만들기에 대한 단계별 연습을 참조하십시오.

Docker 호스트 URL, 사용자 이름 및 암호를 포함하여 패키지된 레서피 파일을 업로드하려면 Docker 레지스트리 자격 증명이 필요합니다. 다음 GET 요청을 수행하여 이 정보를 조회할 수 있습니다.

**API 형식**

```http
GET /engines/dockerRegistry
```

**요청**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 Docker URL(`host`), 사용자 이름(`username`) 및 암호(`password`)를 포함하여 Docker 레지스트리의 세부 정보가 포함된 페이로드를 반환합니다.

>[!NOTE]
>Docker 암호는 업데이트될 때마다 `{ACCESS_TOKEN}` 변경됩니다.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 문서 URL을 사용하여 엔진 만들기 {#docker-image}

여러 부분으로 된 양식에서 Docker 이미지를 참조하는 Docker URL과 메타데이터를 제공하는 동안 POST 요청을 수행하여 엔진을 만들 수 있습니다.

**API 형식**

```http
POST /engines
```

**Python/R 요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 속성 | 설명 |
| --- | --- |
| `name` | 엔진에 대해 원하는 이름입니다. 이 엔진에 해당하는 레서피는 이 값을 상속하여 레서피 이름으로 UI에 표시합니다. |
| `description` | 엔진에 대한 선택적 설명입니다. 이 엔진에 해당하는 레시피는 레서피의 설명으로 UI에 표시할 이 값을 상속합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 값을 빈 문자열로 설정합니다. |
| `type` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지가 내장된 언어에 해당하며 &quot;Python&quot;, &quot;R&quot; 또는 &quot;Tensorflow&quot;가 될 수 있습니다. |
| `algorithm` | 기계 학습 알고리즘의 유형을 지정하는 문자열. 지원되는 알고리즘 유형에는 &quot;분류&quot;, &quot;회귀&quot; 또는 &quot;사용자 지정&quot;이 포함됩니다. |
| `artifacts.default.image.location` | Docker URL 파섹 |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지가 내장된 언어에 해당하며 &quot;Python&quot;, &quot;R&quot; 또는 &quot;Tensorflow&quot;가 될 수 있습니다. |

**PySpark/Scala 요청**

PySpark 레시피를 요청할 때 `executionType` 및 `type` &quot;PySpark&quot;는 Scala 레시피를 요청할 때 `executionType` 및 `type` 는 &quot;Spark&quot;입니다. 다음 Scala 레시피 예제에서는 Spark를 사용합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 엔진에 대해 원하는 이름입니다. 이 엔진에 해당하는 레서피는 이 값을 상속하여 레서피 이름으로 UI에 표시합니다. |
| `description` | 엔진에 대한 선택적 설명입니다. 이 엔진에 해당하는 레시피는 레서피의 설명으로 UI에 표시할 이 값을 상속합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 값을 빈 문자열로 설정합니다. |
| `type` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지를 기반으로 하는 언어에 해당합니다. 이 값은 Spark 또는 PySpark로 설정할 수 있습니다. |
| `mlLibrary` | PySpark 및 Scala 레시피용 엔진을 만들 때 필요한 필드입니다. 이 필드는 로 설정해야 합니다 `databricks-spark`. |
| `artifacts.default.image.location` | Docker 이미지의 위치입니다. Azure ACR 또는 공개(인증되지 않은) Dockerhub만 지원됩니다. |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지를 기반으로 하는 언어에 해당합니다. &quot;Spark&quot; 또는 &quot;PySpark&quot;일 수 있습니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 엔진의 세부 사항이 포함된 페이로드를 반환합니다. 다음 예제는 Python 엔진에 대한 응답입니다. 모든 엔진 응답은 다음 형식을 따릅니다.

```json
{
    "id": "{ENGINE_ID}",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## 엔진 목록 검색

단일 GET 요청을 수행하여 엔진 목록을 검색할 수 있습니다. 결과를 필터링하는 데 도움이 되도록 요청 경로에서 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 자산 검색을 [위한](./appendix.md#query)쿼리 매개 변수의 부록 섹션을 참조하십시오.

**API 형식**

```http
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 엔진 및 세부 사항 목록을 반환합니다.

```json
{
    "children": [
        {
            "id": "{ENGINE_ID}",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "{ENGINE_ID}",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "{ENGINE_ID}",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### 특정 엔진 검색 {#retrieve-specific}

요청 경로에서 원하는 엔진의 ID를 포함하는 GET 요청을 수행하여 특정 엔진의 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
GET /engines/{ENGINE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ENGINE_ID}` | 기존 엔진의 ID입니다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 원하는 엔진의 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "{ENGINE_ID}",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/{ENGINE_ID}/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## 엔진 업데이트

요청 경로에서 대상 엔진의 ID를 포함하는 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공하여 기존 엔진을 수정 및 업데이트할 수 있습니다.

>[!NOTE] 이 PUT 요청의 성공을 보장하기 위해, 먼저 ID로 엔진을 [검색하기 위한 GET 요청을 수행하는 것이 좋습니다](#retrieve-specific). 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청의 페이로드로 적용합니다.

다음 샘플 API 호출은 처음 이러한 속성을 갖는 동안 엔진의 이름과 설명을 업데이트합니다.

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**API 형식**

```http
PUT /engines/{ENGINE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ENGINE_ID}` | 기존 엔진의 ID입니다. |

**요청**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**응답**

성공적인 응답은 엔진의 업데이트된 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "{ENGINE_ID}",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## 엔진 삭제

요청 경로에서 대상 엔진의 ID를 지정하는 동안 DELETE 요청을 수행하여 엔진을 삭제할 수 있습니다. 엔진을 삭제하면 해당 MLInestas에 속한 실험 및 실험 실행을 포함하여 해당 엔진을 참조하는 모든 MLInestas가 삭제됩니다.

**API 형식**

```http
DELETE /engines/{ENGINE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ENGINE_ID}` | 기존 엔진의 ID입니다. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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
    "detail": "Engine deletion was successful"
}
```

## 더 이상 사용되지 않는 요청

>[!IMPORTANT]
>이진 객체는 더 이상 지원되지 않으며 나중에 제거되도록 설정됩니다. 새로운 PySpark 및 Scala 레시피가 이제 [도커 이미지](#docker-image) 예제를 따라 엔진을 만들어야 합니다.

## 이진 객체를 사용하여 엔진 만들기 - 더 이상 사용되지 않음

메타 데이터 및 객체의 경로를 여러 부분으로 된 양식에서 제공하는 동안 POST 요청을 수행하여 로컬 `.jar` 또는 `.egg` 이진 객체를 사용하여 엔진을 만들 수 있습니다.

**API 형식**

```http
POST /engines
```

**요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "algorithm": "Classification",
        "type": "PySpark",
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file.egg'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 엔진에 대해 원하는 이름입니다. 이 엔진에 해당하는 레서피는 이 값을 상속하여 레서피 이름으로 UI에 표시합니다. |
| `description` | 엔진에 대한 선택적 설명입니다. 이 엔진에 해당하는 레시피는 레서피의 설명으로 UI에 표시할 이 값을 상속합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 값을 빈 문자열로 설정합니다. |
| `algorithm` | 기계 학습 알고리즘의 유형을 지정하는 문자열. 지원되는 알고리즘 유형에는 &quot;분류&quot;, &quot;회귀&quot; 또는 &quot;사용자 지정&quot;이 포함됩니다. |
| `type` | 엔진의 실행 유형입니다. 이 값은 바이너리 아티팩트가 내장되어 있는 언어에 해당하며 &quot;PySpark&quot; 또는 &quot;Spark&quot;가 될 수 있습니다. |


**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 엔진의 세부 사항이 포함된 페이로드를 반환합니다.

```json
{
    "id": "{ENGINE_ID}",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## 이진 객체를 사용하여 피쳐 파이프라인 엔진 생성 - 더 이상 사용되지 않음

>[!IMPORTANT]
>이진 객체는 더 이상 지원되지 않으며 나중에 제거되도록 설정됩니다.

POST 요청을 수행하는 동안 여러 부분으로 된 양식에서 해당 메타데이터와 객체의 경로를 제공하여 로컬 `.jar` 또는 `.egg` 바이너리 객체를 사용하여 피쳐 파이프라인 엔진을 생성할 수 있습니다. PySpark 또는 Spark Engine은 코어 수 또는 메모리 양과 같은 컴퓨팅 리소스를 지정할 수 있습니다. 자세한 내용은 PySpark 및 [Spark 리소스 구성의](./appendix.md#resource-config) 부록 섹션을 참조하십시오.

**API 형식**

```http
POST /engines
```

**요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "Feature Pipeline Engine",
        "description": "A feature pipeline Engine",
        "algorithm":"fp",
        "type": "PySpark"
    }' \
    -F 'featurePipelineOverrideArtifact=@path/to/binary/artifact/feature_pipeline.egg' \
    -F 'defaultArtifact=@path/to/binary/artifact/feature_pipeline.egg'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 엔진에 대해 원하는 이름입니다. 이 엔진에 해당하는 레서피는 이 값을 상속하여 레서피 이름으로 UI에 표시합니다. |
| `description` | 엔진에 대한 선택적 설명입니다. 이 엔진에 해당하는 레시피는 레서피의 설명으로 UI에 표시할 이 값을 상속합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 값을 빈 문자열로 설정합니다. |
| `algorithm` | 기계 학습 알고리즘의 유형을 지정하는 문자열. 이 값을 &quot;fp&quot;로 설정하여 이 생성을 피쳐 파이프라인 엔진으로 지정합니다. |
| `type` | 엔진의 실행 유형입니다. 이 값은 바이너리 아티팩트가 내장되어 있는 언어에 해당하며 &quot;PySpark&quot; 또는 &quot;Spark&quot;가 될 수 있습니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 엔진의 세부 사항이 포함된 페이로드를 반환합니다.

```json
{
    "id": "{ENGINE_ID}",
    "name": "Feature Pipeline Engine",
    "description": "A feature pipeline Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```
