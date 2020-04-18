---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 패키지된 레서피(API) 가져오기
topic: Tutorial
translation-type: tm+mt
source-git-commit: ebf7c883ce89fdf8b0d468ab21d1c3a1ba8aca06

---


# 패키지된 레서피(API) 가져오기

이 자습서는 Sensei [Machine Learning API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 사용하여 [사용자](../api/engines.md)인터페이스의 레서피라고도 하는 엔진을 만듭니다.

시작하기 전에 Adobe Experience Platform Data Science Workspace에서 서로 다른 용어를 사용하여 API 및 UI 내의 유사한 요소를 참조하는 것이 중요합니다. API 용어는 이 자습서 전체에서 사용되며 다음 표에서는 상관 관계 용어에 대해 대략적으로 설명합니다.

| UI 용어 | API 용어 |
| ---- | ---- |
| 레서피 | [엔진](../api/engines.md) |
| 모델 | [MLInstance](../api/mlinstances.md) |
| 트레이닝 및 평가 | [실험](../api/experiments.md) |
| 서비스 | [MLService](../api/mlservices.md) |

엔진은 특정 문제를 해결하기 위한 기계 학습 알고리즘과 논리를 포함합니다. 아래 다이어그램에서는 데이터 과학 작업 영역의 API 작업 과정을 보여주는 시각화를 제공합니다. 이 자습서는 기계 학습 모델의 두뇌인 엔진을 만드는 데 중점을 둡니다.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 시작하기

이 자습서에서는 이진 가공물이나 Docker URL 형식의 패키지된 레서피 파일이 필요합니다. 소스 [파일을 Recipe 튜토리얼로 패키징하여](./package-source-files-recipe.md) 패키지된 Recipe 파일을 만들거나 직접 제공합니다.

- 이진 아티팩트(더 이상 사용되지 않음):이진 아티팩트(예: JAR, EGG)를 사용하여 엔진을 만듭니다.
- `{DOCKER_URL}`:지능형 서비스의 Docker 이미지에 대한 URL 주소입니다.

이 자습서에서는 플랫폼 API를 [성공적으로 호출하려면 Adobe Experience Platform에 대한 인증 자습서를](../../tutorials/authentication.md) 완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- `{ACCESS_TOKEN}`:인증 후에 제공된 특정 베어러 토큰 값입니다.
- `{IMS_ORG}`:고유한 Adobe Experience Platform 통합에 포함된 IMS 조직 자격 증명
- `{API_KEY}`:고유한 Adobe Experience Platform 통합에 있는 특정 API 키 값

## 엔진 만들기

API 요청의 일부로 포함할 패키지된 레서피 파일의 형식에 따라, 엔진은 다음 두 가지 방법 중 하나를 통해 만들어집니다.

- [Docker URL을 사용하여 엔진 만들기](#create-an-engine-with-a-docker-url)
- [이진 가공물로 엔진 만들기(더 이상 사용되지 않음)](#create-an-engine-with-a-binary-artifact-deprecated)

### Docker URL을 사용하여 엔진 만들기

Docker 컨테이너에 저장된 패키지된 Recipe 파일이 있는 엔진을 만들려면 패키지된 Recipe 파일에 Docker URL을 제공해야 합니다.

>[!CAUTION]
> Python 또는 R을 사용하는 경우 아래 요청을 사용하십시오. PySpark 또는 Scala를 사용하는 경우 Python/R 예제 아래에 있는 PySpark/Scala 요청 예제를 사용합니다.

**API 형식**

```http
POST /engines
```

**Python/R 요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 속성 | 설명 |
| -------  | ----------- |
| `engine.name` | 엔진에 대해 원하는 이름입니다. 이 엔진에 해당하는 레서피는 이 값을 상속하여 Data Science Workspace 사용자 인터페이스에 레서피 이름으로 표시합니다. |
| `engine.description` | 엔진에 대한 선택적 설명입니다. 이 엔진에 해당하는 레서피는 이 값을 상속하여 레서피 설명으로 데이터 과학 작업 공간 사용자 인터페이스에 표시합니다. 설명을 제공하지 않기로 선택한 경우 이 속성을 제거하지 마십시오. 이 값은 빈 문자열이어야 합니다. |
| `engine.type` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지가 개발되는 언어에 해당합니다. 엔진을 만들기 위해 Docker URL이 제공되면 `type` , `Python``R`, `PySpark`(Scala) `Spark` 또는 `Tensorflow`이 표시됩니다. |
| `artifacts.default.image.location` | 여기 `{DOCKER_URL}` 가시면 됩니다 전체 Docker URL에는 다음 구조가 있습니다. `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker 이미지 파일의 추가 이름입니다. 이 속성을 제거하지 마십시오. 추가 Docker 이미지 파일 이름을 제공하지 않기로 선택한 경우 이 값이 빈 문자열이 되도록 하십시오. |
| `artifacts.default.image.executionType` | 이 엔진의 실행 유형입니다. 이 값은 Docker 이미지가 개발되는 언어에 해당합니다. 엔진을 만들기 위해 Docker URL이 제공되면 `executionType` , `Python``R`, `PySpark`(Scala) `Spark` 또는 `Tensorflow`이 표시됩니다. |

**PySpark 요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
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
| `type` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지가 &quot;PySpark&quot;를 기반으로 구축된 언어에 해당합니다. |
| `mlLibrary` | PySpark 및 Scala 레시피용 엔진을 만들 때 필요한 필드입니다. |
| `artifacts.default.image.location` | Docker URL 파섹 |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지가 &quot;Spark&quot;를 기반으로 구축된 언어에 해당합니다. |

**Request Scala**

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
| `type` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지가 &quot;Spark&quot;를 기반으로 구축된 언어에 해당합니다. |
| `mlLibrary` | PySpark 및 Scala 레시피용 엔진을 만들 때 필요한 필드입니다. |
| `artifacts.default.image.location` | Docker URL 파섹 |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 Docker 이미지가 &quot;Spark&quot;를 기반으로 구축된 언어에 해당합니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 엔진의 세부 사항이 포함된 페이로드를 반환합니다. 다음 예제는 Python 엔진에 대한 응답입니다. 제공된 POST를 기준으로 `executionType` 및 `type` 키가 변경됩니다.

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

성공적인 응답은 새로 만든 엔진에 대한 정보가 포함된 JSON 페이로드를 보여줍니다. 이 `id` 키는 고유한 엔진 식별자를 나타내며 다음 자습서에서 MLInstance를 만들어야 합니다. 다음 단계를 계속하기 전에 엔진 식별자가 저장되었는지 확인합니다.

## 다음 단계

API를 사용하여 엔진을 만들었으며 고유한 엔진 식별자를 응답 본문의 일부로 받았습니다. 다음 자습서에서는 API를 사용하여 모델을 [만들고, 교육하고, 평가하는 방법을 배울 때 이 엔진 식별자를 사용할 수 있습니다](./train-evaluate-model-api.md).

### 이진 가공물로 엔진 만들기(더 이상 사용되지 않음)

<!-- Will need to remove binary artifact documentation once the old flags are turned off -->

>[!CAUTION]
> 이진 가공물은 이전 PySpark 및 Spark 레시피에서 사용됩니다. 이제 Data Science Workspace에서 모든 레서피에 대한 Docker URL을 지원합니다. 이 업데이트를 사용하면 이제 모든 엔진이 Docker URL을 사용하여 만들어집니다. 이 [문서의 Docker URL 섹션을](#create-an-engine-with-a-docker-url) 참조하십시오. 이진 객체는 후속 릴리스에서 제거되도록 설정됩니다.

로컬 패키지 `.jar` 또는 `.egg` 이진 객체를 사용하여 엔진을 만들려면 로컬 파일 시스템의 이진 객체 파일에 대한 절대 경로를 제공해야 합니다. 터미널 환경에서 바이너리 결함을 포함하는 디렉토리로 이동한 다음 절대 경로에 대해 `pwd` Unix 명령을 실행합니다.

다음 호출은 이진 가공물이 있는 엔진을 만듭니다.

**API 형식**

```http
POST /engines
```

**요청**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine PySpark",
        "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
        "type": "PySpark"
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file/pysparkretailapp-0.1.0-py3.7.egg'
```

| 속성 | 설명 |
| -------  | ----------- |
| `engine.name` | 엔진에 대해 원하는 이름입니다. 이 엔진에 해당하는 레서피는 이 값을 상속하여 Data Science Workspace 사용자 인터페이스에 레서피 이름으로 표시합니다. |
| `engine.description` | 엔진에 대한 선택적 설명입니다. 이 엔진에 해당하는 레서피는 이 값을 상속하여 레서피 설명으로 데이터 과학 작업 공간 사용자 인터페이스에 표시합니다. 설명을 제공하지 않기로 선택한 경우 이 속성을 제거하지 마십시오. 이 값은 빈 문자열이어야 합니다. |
| `engine.type` | 엔진의 실행 유형입니다. 이 값은 이진 아티팩트가 개발된 언어에 해당합니다. 이진 객체를 업로드하여 엔진을 만들 `type` 때 는 `Spark` 또는 `PySpark`입니다. |
| `defaultArtifact` | 엔진을 만드는 데 사용되는 이진 객체 파일의 절대 경로입니다. 파일 경로 `@` 앞에 포함해야 합니다. |

**응답**

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine PySpark",
    "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
    "type": "PySpark",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://some-storage-location.net/some-path/your-uploaded-binary-artifact.egg",
                "name": "pysparkretailapp-0.1.0-py3.7.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

성공적인 응답은 새로 만든 엔진에 대한 정보가 포함된 JSON 페이로드를 보여줍니다. 이 `id` 키는 고유한 엔진 식별자를 나타내며 다음 자습서에서 MLInstance를 만들어야 합니다. [다음 단계를](#next-steps)계속하기 전에 엔진 식별자가 저장되었는지 확인합니다.