---
keywords: Experience Platform;개발자 안내서;엔드포인트;Data Science Workspace;인기 주제;엔진;sensei 머신 러닝 api
solution: Experience Platform
title: 엔진 API 엔드포인트
description: 엔진은 데이터 과학 작업 영역에서 머신 러닝 모델을 위한 기초입니다. 여기에는 특정 문제를 해결하는 머신 러닝 알고리즘, 기능 엔지니어링을 수행하는 기능 파이프라인 또는 둘 다가 포함됩니다.
exl-id: 7c670abd-636c-47d8-bd8c-5ce0965ce82f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 3%

---

# 엔진 엔드포인트

엔진은 데이터 과학 작업 영역에서 머신 러닝 모델을 위한 기초입니다. 여기에는 특정 문제를 해결하는 머신 러닝 알고리즘, 기능 엔지니어링을 수행하는 기능 파이프라인 또는 둘 다가 포함됩니다.

## Docker 레지스트리 조회

>[!TIP]
>
>도커 URL이 없는 경우 다음을 방문하십시오. [소스 파일을 레시피에 패키징](../models-recipes/package-source-files-recipe.md) 도커 호스트 URL 만들기에 대한 단계별 연습에 대한 자습서입니다.

Docker 호스트 URL, 사용자 이름 및 암호를 포함하여 패키지된 레서피 파일을 업로드하려면 Docker 레지스트리 자격 증명이 필요합니다. 다음 GET 요청을 수행하여 이 정보를 조회할 수 있습니다.

**API 형식**

```https
GET /engines/dockerRegistry
```

**요청**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 도커 URL( )을 포함한 도커 레지스트리의 세부 사항이 포함된 페이로드를 반환합니다`host`), 사용자 이름(`username`) 및 암호(`password`).

>[!NOTE]
>
>Docker 암호는 `{ACCESS_TOKEN}` 이(가) 업데이트되었습니다.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 도커 URL을 사용하여 엔진 만들기 {#docker-image}

여러 부분 양식의 도커 이미지를 참조하는 도커 URL과 메타데이터를 제공하는 동안 POST 요청을 수행하여 엔진을 만들 수 있습니다.

**API 형식**

```https
POST /engines
```

**Python/R 요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 속성 | 설명 |
| --- | --- |
| `name` | 원하는 엔진 이름. 이 엔진에 해당하는 레시피는 레시피의 이름으로 UI에 표시될 이 값을 상속합니다. |
| `description` | 엔진에 대한 선택적 설명. 이 엔진에 해당하는 레시피는 레시피의 설명으로 UI에 표시될 이 값을 상속합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 해당 값을 빈 문자열로 설정하십시오. |
| `type` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 구축된 언어에 해당하며 &quot;Python&quot;, &quot;R&quot; 또는 &quot;Tensorflow&quot;일 수 있습니다. |
| `algorithm` | 머신 러닝 알고리즘의 유형을 지정하는 문자열. 지원되는 알고리즘 유형에는 &quot;Classification&quot;, &quot;Regression&quot; 또는 &quot;Custom&quot;이 포함됩니다. |
| `artifacts.default.image.location` | 도커 URL에 의해 연결된 도커 이미지의 위치입니다. |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 구축된 언어에 해당하며 &quot;Python&quot;, &quot;R&quot; 또는 &quot;Tensorflow&quot;일 수 있습니다. |

**PySpark/Scala 요청**

PySpark 레시피를 요청할 때 `executionType` 및 `type` 은(는) &quot;PySpark&quot;입니다. Scala 레시피를 요청할 때 `executionType` 및 `type` 은(는) &quot;Spark&quot;입니다. 다음 Scala 레시피 예제에서는 Spark를 사용합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | 원하는 엔진 이름. 이 엔진에 해당하는 레시피는 레시피의 이름으로 UI에 표시될 이 값을 상속합니다. |
| `description` | 엔진에 대한 선택적 설명. 이 엔진에 해당하는 레시피는 레시피의 설명으로 UI에 표시될 이 값을 상속합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 해당 값을 빈 문자열로 설정하십시오. |
| `type` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 빌드되는 언어에 해당합니다. 이 값은 Spark 또는 PySpark로 설정할 수 있습니다. |
| `mlLibrary` | PySpark 및 Scala 레시피의 엔진을 만들 때 필요한 필드입니다. 이 필드는 (으)로 설정해야 합니다. `databricks-spark`. |
| `artifacts.default.image.location` | 도커 이미지의 위치입니다. Azure ACR 또는 공개(인증되지 않음) Dockerhub만 지원됩니다. |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 빌드되는 언어에 해당합니다. &quot;Spark&quot; 또는 &quot;PySpark&quot;일 수 있습니다. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 생성된 엔진의 세부 사항이 포함된 페이로드를 반환합니다`id`). 다음 예제 응답은 Python 엔진에 대한 것입니다. 모든 엔진 응답은 다음 형식을 따릅니다.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
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
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## 도커 URL을 사용하여 기능 파이프라인 엔진 생성 {#feature-pipeline-docker}

POST 요청을 수행하면서 해당 메타데이터와 도커 이미지를 참조하는 도커 URL을 제공하여 기능 파이프라인 엔진을 생성할 수 있습니다.

**API 형식**

```https
POST /engines
```

**요청**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| 속성 | 설명 |
| --- | --- |
| `type` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 빌드되는 언어에 해당합니다. 이 값은 Spark 또는 PySpark로 설정할 수 있습니다. |
| `algorithm` | 사용 중인 알고리즘입니다. 이 값을 로 설정하십시오. `fp` (기능 파이프라인). |
| `name` | 피쳐 파이프라인 엔진에 대해 원하는 이름입니다. 이 엔진에 해당하는 레시피는 레시피의 이름으로 UI에 표시될 이 값을 상속합니다. |
| `description` | 엔진에 대한 선택적 설명. 이 엔진에 해당하는 레시피는 레시피의 설명으로 UI에 표시될 이 값을 상속합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 해당 값을 빈 문자열로 설정하십시오. |
| `mlLibrary` | PySpark 및 Scala 레시피의 엔진을 만들 때 필요한 필드입니다. 이 필드는 (으)로 설정해야 합니다. `databricks-spark`. |
| `artifacts.default.image.location` | 도커 이미지의 위치입니다. Azure ACR 또는 공개(인증되지 않음) Dockerhub만 지원됩니다. |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 빌드되는 언어에 해당합니다. &quot;Spark&quot; 또는 &quot;PySpark&quot;일 수 있습니다. |
| `artifacts.default.image.packagingType` | 엔진의 패키징 타입. 이 값은 다음으로 설정해야 합니다. `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | 사용자 `pipeline.json` 구성 파일 매개 변수. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 생성된 기능 파이프라인 엔진의 세부 사항이 포함된 페이로드를 반환합니다`id`). 다음 예제 응답은 PySpark 기능 파이프라인 엔진에 대한 것입니다.

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## 엔진 목록 검색

단일 GET 요청을 수행하여 엔진 목록을 검색할 수 있습니다. 결과를 필터링하기 위해 요청 경로에 쿼리 매개 변수를 지정할 수 있습니다. 사용 가능한 쿼리 목록은 의 부록 섹션을 참조하십시오. [자산 검색을 위한 쿼리 매개 변수](./appendix.md#query).

**API 형식**

```https
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답이 성공하면 엔진 목록과 세부 정보가 반환됩니다.

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
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
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
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
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
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

요청 경로에 원하는 엔진의 ID를 포함하는 GET 요청을 수행하여 특정 엔진의 세부 정보를 검색할 수 있습니다.

**API 형식**

```https
GET /engines/{ENGINE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ENGINE_ID}` | 기존 엔진의 ID. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 원하는 엔진의 세부 정보가 포함된 페이로드를 반환합니다.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
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
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## 엔진 업데이트

요청 경로에 대상 엔진의 ID를 포함하는 PUT 요청을 통해 속성을 덮어쓰고 업데이트된 속성이 포함된 JSON 페이로드를 제공하여 기존 엔진을 수정하고 업데이트할 수 있습니다.

>[!NOTE]
>
>이 PUT GET 요청의 성공을 보장하려면 먼저 다음 작업을 수행하는 것이 좋습니다. [ID로 엔진 검색](#retrieve-specific). 그런 다음 반환된 JSON 개체를 수정 및 업데이트하고 수정된 JSON 개체 전체를 PUT 요청에 대한 페이로드로 적용합니다.

다음 샘플 API 호출은 이러한 속성을 처음 사용하는 동안 엔진의 이름과 설명을 업데이트합니다.

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

```https
PUT /engines/{ENGINE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ENGINE_ID}` | 기존 엔진의 ID. |

**요청**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공한 응답은 엔진의 업데이트된 세부 사항이 포함된 페이로드를 반환합니다.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
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

요청 경로에서 대상 엔진의 ID를 지정하는 동안 DELETE 요청을 수행하여 엔진을 삭제할 수 있습니다. 엔진을 삭제하면 해당 MLInstance에 속하는 모든 실험 및 실험 실행을 포함하여 해당 엔진을 참조하는 모든 MLInstance가 계단식으로 삭제됩니다.

**API 형식**

```https
DELETE /engines/{ENGINE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ENGINE_ID}` | 기존 엔진의 ID. |

**요청**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
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
    "detail": "Engine deletion was successful"
}
```
