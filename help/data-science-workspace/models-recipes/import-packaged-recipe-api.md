---
keywords: Experience Platform;패키지된 레시피 가져오기;Data Science Workspace;인기 주제;레시피;api;sensei machine learning;엔진 만들기
solution: Experience Platform
title: Sensei 머신 러닝 API를 사용하여 패키지된 레시피 가져오기
type: Tutorial
description: 이 자습서에서는 Sensei 머신 러닝 API를 사용하여 사용자 인터페이스에서 레시피라고도 하는 엔진을 만듭니다.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 2%

---

# Sensei 머신 러닝 API를 사용하여 패키지된 레시피 가져오기

이 튜토리얼에서는 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 다음을 만들려면: [엔진](../api/engines.md)사용자 인터페이스에서 레시피라고도 합니다.

시작하기 전에 Adobe Experience Platform을 참고하십시오 [!DNL Data Science Workspace] 에서는 API 및 UI 내의 유사한 요소를 지칭하기 위해 다른 용어를 사용합니다. API 용어는 이 자습서 전체에서 사용되며 다음 표에서 상관 관계를 설명합니다.

| UI 용어 | API 용어 |
| ---- | ---- |
| 레시피 | [엔진](../api/engines.md) |
| 모델 | [MLInstance](../api/mlinstances.md) |
| 교육 및 평가 | [실험](../api/experiments.md) |
| 서비스 | [MLSservice](../api/mlservices.md) |

엔진은 특정 문제를 해결하기 위한 기계 학습 알고리즘과 논리를 포함합니다. 아래 다이어그램은에서 API 워크플로를 보여주는 시각화를 제공합니다. [!DNL Data Science Workspace]. 이 자습서에서는 머신 러닝 모델의 두뇌인 엔진 을 만드는 데 중점을 둡니다.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 시작하기

이 자습서에서는 도커 URL 형태로 패키지된 레시피 파일이 필요합니다. 다음 [소스 파일을 레시피에 패키징](./package-source-files-recipe.md) 패키지된 레시피 파일을 만들거나 직접 제공하는 튜토리얼입니다.

- `{DOCKER_URL}`: 지능형 서비스의 도커 이미지에 대한 URL 주소입니다.

이 자습서를 사용하려면 다음을 완료해야 합니다. [Adobe Experience Platform에 대한 인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을(를) 성공적으로 호출하기 위해 [!DNL Platform] API. 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

- `{ACCESS_TOKEN}`: 인증 후 제공된 특정 전달자 토큰 값입니다.
- `{ORG_ID}`: 고유한 Adobe Experience Platform 통합에서 찾은 조직 자격 증명입니다.
- `{API_KEY}`: 고유한 Adobe Experience Platform 통합에서 찾은 특정 API 키 값.

## 엔진 만들기

엔진은 /engines 끝점에 POST 요청을 하여 만들 수 있습니다. 작성된 엔진은 API 요청의 일부로 포함되어야 하는 패키지된 레시피 파일의 양식을 기반으로 구성됩니다.

### 도커 URL을 사용하여 엔진 만들기 {#create-an-engine-with-a-docker-url}

Docker 컨테이너에 저장된 패키지된 레시피 파일이 있는 엔진을 만들려면 패키지된 레시피 파일에 도커 URL을 제공해야 합니다.

>[!CAUTION]
>
> 을 사용하는 경우 [!DNL Python] 또는 아래 요청을 사용하십시오. PySpark 또는 Scala를 사용하는 경우 Python/R 예제 아래에 있는 PySpark/Scala 요청 예제를 사용합니다.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `engine.name` | 원하는 엔진 이름. 이 엔진에 해당하는 레시피는에 표시될 이 값을 상속합니다. [!DNL Data Science Workspace] 사용자 인터페이스를 레시피의 이름으로 사용하십시오. |
| `engine.description` | 엔진에 대한 선택적 설명. 이 엔진에 해당하는 레시피는에 표시될 이 값을 상속합니다. [!DNL Data Science Workspace] 사용자 인터페이스를 레시피의 설명으로 사용합니다. 이 속성을 제거하지 마십시오. 설명을 제공하지 않도록 선택하는 경우 이 값을 빈 문자열로 둡니다. |
| `engine.type` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 개발되는 언어에 해당합니다. 엔진을 만들기 위해 도커 URL이 제공되면 `type` 다음 중 하나 `Python`, `R`, `PySpark`, `Spark` (Scala) 또는 `Tensorflow`. |
| `artifacts.default.image.location` | 사용자 `{DOCKER_URL}` 여기 로 이동합니다. 전체 도커 URL의 구조는 다음과 같습니다. `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | 도커 이미지 파일의 추가 이름입니다. 추가 도커 이미지 파일 이름을 제공하지 않도록 선택하는 경우 이 속성을 제거하지 말고 이 값을 빈 문자열로 둡니다. |
| `artifacts.default.image.executionType` | 이 엔진의 실행 유형입니다. 이 값은 도커 이미지가 개발되는 언어에 해당합니다. 엔진을 만들기 위해 도커 URL이 제공되면 `executionType` 다음 중 하나 `Python`, `R`, `PySpark`, `Spark` (Scala) 또는 `Tensorflow`. |

**PySpark 요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | 원하는 엔진 이름. 이 엔진에 해당하는 레시피는 레시피의 이름으로 UI에 표시될 이 값을 상속합니다. |
| `description` | 엔진에 대한 선택적 설명. 이 엔진에 해당하는 레시피는 레시피의 설명으로 UI에 표시될 이 값을 상속합니다. 이 속성은 필수입니다. 설명을 제공하지 않으려면 해당 값을 빈 문자열로 설정하십시오. |
| `type` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 &quot;PySpark&quot;에 빌드되는 언어에 해당합니다. |
| `mlLibrary` | PySpark 및 Scala 레시피의 엔진을 만들 때 필요한 필드입니다. |
| `artifacts.default.image.location` | 도커 URL에 의해 연결된 도커 이미지의 위치입니다. |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 &quot;Spark&quot;에 빌드되는 언어에 해당합니다. |

**Scala 요청**

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
| `type` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 &quot;Spark&quot;에 빌드되는 언어에 해당합니다. |
| `mlLibrary` | PySpark 및 Scala 레시피의 엔진을 만들 때 필요한 필드입니다. |
| `artifacts.default.image.location` | 도커 URL에 의해 연결된 도커 이미지의 위치입니다. |
| `artifacts.default.image.executionType` | 엔진의 실행 유형입니다. 이 값은 도커 이미지가 &quot;Spark&quot;에 빌드되는 언어에 해당합니다. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 생성된 엔진의 세부 사항이 포함된 페이로드를 반환합니다`id`). 다음 예제 응답은 [!DNL Python] 엔진. 다음 `executionType` 및 `type` 제공된 POST에 따라 키가 변경됩니다.

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

성공적인 응답은 새로 생성된 엔진에 대한 정보와 함께 JSON 페이로드를 보여 줍니다. 다음 `id` 키는 고유한 엔진 식별자를 나타내며 다음 튜토리얼에서 MLInstance를 만드는 데 필요합니다. 다음 단계를 계속하기 전에 엔진 식별자가 저장되었는지 확인하십시오.

## 다음 단계 {#next-steps}

API를 사용하여 엔진을 만들었고 고유한 엔진 식별자가 응답 본문의 일부로 가져왔습니다. 방법을 배울 때 다음 자습서에서 이 엔진 식별자를 사용할 수 있습니다. [API를 사용하여 모델 만들기, 교육 및 평가](./train-evaluate-model-api.md).
