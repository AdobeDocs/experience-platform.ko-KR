---
keywords: Experience Platform;Data Science Workspace;popular topics
solution: Experience Platform
title: 레서피 및 노트북 마이그레이션 가이드
topic: Tutorial
translation-type: tm+mt
source-git-commit: f2a7300d4ad75e3910abbdf2ecc2946a2dfe553c
workflow-type: tm+mt
source-wordcount: '3459'
ht-degree: 0%

---


# 레서피 및 노트북 마이그레이션 가이드

>[!NOTE]
>Python/R을 사용한 노트북과 조리법은 영향을 받지 않습니다. 마이그레이션은 PySpark/Spark(2.3) 레시피 및 노트북에만 적용됩니다.

다음 안내서에서는 기존 레서피 및 전자 필기장을 마이그레이션하는 데 필요한 단계 및 정보에 대해 간략하게 설명합니다.

- [레서피 마이그레이션 가이드](#recipe-migration)
- [노트북 마이그레이션 가이드](#notebook-migration)

## 레서피 마이그레이션 가이드 {#recipe-migration}

최근 데이터 과학 작업 공간이 변경되어 기존 Spark 및 PySpark 레시피가 업데이트되어야 합니다. 다음 워크플로우를 사용하여 레시피 전환을 지원합니다.

- [Spark 마이그레이션 가이드](#spark-migration-guide)
   - [데이터 세트를 읽고 쓰는 방법 수정](#read-write-recipe-spark)
   - [샘플 레서피 다운로드](#download-sample-spark)
   - [문서 파일 추가](#add-dockerfile-spark)
   - [종속성 확인](#change-dependencies-spark)
   - [Docker 스크립트 준비](#prepare-docker-spark)
   - [docker로 레시피 만들기](#create-recipe-spark)
- [PySpark 마이그레이션 가이드](#pyspark-migration-guide)
   - [데이터 세트를 읽고 쓰는 방법 수정](#pyspark-read-write)
   - [샘플 레서피 다운로드](#pyspark-download-sample)
   - [문서 파일 추가](#pyspark-add-dockerfile)
   - [Docker 스크립트 준비](#pyspark-prepare-docker)
   - [docker로 레시피 만들기](#pyspark-create-recipe)

## Spark 마이그레이션 가이드 {#spark-migration-guide}

빌드 단계에서 생성된 레서피 아티팩트는 이제 .jar 바이너리 파일이 포함된 Docker 이미지입니다. 또한 플랫폼 SDK를 사용하여 데이터 세트를 읽고 쓰는 데 사용되는 구문이 변경되었으며 레서피 코드를 수정해야 합니다.

다음 비디오는 Spark 레서피에 필요한 변경 사항을 이해하는 데 도움이 되도록 만들어졌습니다.

>[!VIDEO](https://video.tv.adobe.com/v/33243)

### 데이터 세트 읽기 및 쓰기(Spark) {#read-write-recipe-spark}

Docker 이미지를 만들기 전에 아래 섹션에 설명된 대로 플랫폼 SDK에서 데이터 세트를 읽고 쓸 수 있는 예제를 검토하십시오. 기존 레서피를 변환하는 경우 플랫폼 SDK 코드를 업데이트해야 합니다.

#### 데이터 세트 읽기

이 섹션에서는 데이터 세트를 읽는 데 필요한 변경 사항에 대해 설명하고 Adobe에서 제공하는 [helper.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/helper/Helper.scala) 예제를 사용합니다.

**데이터 세트를 읽는 오래된 방법**

```scala
 var df = sparkSession.read.format("com.adobe.platform.dataset")
    .option(DataSetOptions.orgId, orgId)
    .option(DataSetOptions.serviceToken, serviceToken)
    .option(DataSetOptions.userToken, userToken)
    .option(DataSetOptions.serviceApiKey, apiKey)
    .load(dataSetId)
```

**데이터 세트를 읽는 새로운 방법**

Spark 레서피에 대한 업데이트를 통해 다양한 값을 추가하고 변경해야 합니다. 첫째, `DataSetOptions` 더 이상 사용되지 않습니다. Replace `DataSetOptions` with `QSOption`. 또한 새 매개 `option` 변수가 필요합니다. 둘 다 `QSOption.mode` 가 `QSOption.datasetId` 필요하다. 마지막으로, `orgId` 그리고 `serviceApiKey` 로 `imsOrg` 그리고 `apiKey`변경해야 합니다. 데이터 집합 읽기에 대한 비교는 다음 예를 검토하십시오.

```scala
import com.adobe.platform.query.QSOption
var df = sparkSession.read.format("com.adobe.platform.query")
  .option(QSOption.userToken", {userToken})
  .option(QSOption.serviceToken, {serviceToken})
  .option(QSOption.imsOrg, {orgId})
  .option(QSOption.apiKey, {apiKey})
  .option(QSOption.mode, "interactive")
  .option(QSOption.datasetId, {dataSetId})
  .load()
```

>[!TIP]
> 쿼리가 10분 이상 실행되는 경우 대화형 모드가 시간 초과됩니다. 데이터 크기가 몇 GB 이상인 경우 &quot;일괄 처리&quot; 모드로 전환하는 것이 좋습니다. 배치 모드는 시작하는 데 시간이 오래 걸리지만 더 큰 데이터 세트를 처리할 수 있습니다.

#### 데이터 세트에 쓰기

이 섹션에서는 Adobe에서 제공하는 [ScoringDataSaver.scala 예제를 사용하여 데이터 세트를](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/ScoringDataSaver.scala) 작성하는 데 필요한 변경 사항에 대해 간략하게 설명합니다.

**데이터 세트를 작성하는 오래된 방법**

```scala
df.write.format("com.adobe.platform.dataset")
    .option(DataSetOptions.orgId, orgId)
    .option(DataSetOptions.serviceToken, serviceToken)
    .option(DataSetOptions.userToken, userToken)
    .option(DataSetOptions.serviceApiKey, apiKey)
    .save(scoringResultsDataSetId)
```

**데이터 세트를 작성하는 새로운 방법**

Spark 레서피에 대한 업데이트를 통해 다양한 값을 추가하고 변경해야 합니다. 첫째, `DataSetOptions` 더 이상 사용되지 않습니다. Replace `DataSetOptions` with `QSOption`. 또한 새 매개 `option` 변수가 필요합니다. `QSOption.datasetId` 가 필요하며 `{dataSetId}` 인(in)을 로드할 필요성을 `.save()`대체합니다. 마지막으로, `orgId` 그리고 `serviceApiKey` 로 `imsOrg` 그리고 `apiKey`변경해야 합니다. 데이터 세트 작성에 대한 비교는 다음 예를 참조하십시오.

```scala
import com.adobe.platform.query.QSOption
df.write.format("com.adobe.platform.query")
  .option(QSOption.userToken", {userToken})
  .option(QSOption.serviceToken, {serviceToken})
  .option(QSOption.imsOrg, {orgId})
  .option(QSOption.apiKey, {apiKey})
  .option(QSOption.datasetId, {dataSetId})
  .save()
```

### Package Docker 기반 소스 파일(Spark) {#package-docker-spark}

먼저 레시피가 있는 디렉토리로 이동합니다.

다음 섹션에서는 [Data Science Workspace 공용 Github 저장소에서 찾을 수 있는 새로운 Scala Retail 판매 레시피를 사용합니다](https://github.com/adobe/experience-platform-dsw-reference).

### 샘플 레시피 다운로드(Spark) {#download-sample-spark}

샘플 레서피에는 기존 레서피로 복사해야 하는 파일이 포함되어 있습니다. 모든 샘플 레시피가 포함된 공용 Github를 복제하려면 터미널에 다음을 입력합니다.

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Scala 레시피는 다음 디렉토리에 있습니다 `experience-platform-dsw-reference/recipes/scala/retail`.

### Dockerfile(Spark) 추가 {#add-dockerfile-spark}

문서 기반 워크플로우를 사용하려면 레서피 폴더에 새 파일이 필요합니다. 의 레서피 폴더에서 Dockerfile을 복사하여 붙여넣습니다 `experience-platform-dsw-reference/recipes/scala/Dockerfile`. 선택적으로 아래 코드를 복사하여 새 파일에 붙여넣을 수도 있습니다 `Dockerfile`.

>[!IMPORTANT]
> 아래에 표시된 예제 jar 파일은 레시피 jar 파일 이름으로 `ml-retail-sample-spark-*-jar-with-dependencies.jar` 교체되어야 합니다.

```scala
FROM adobe/acp-dsw-ml-runtime-spark:0.0.1

COPY target/ml-retail-sample-spark-*-jar-with-dependencies.jar /application.jar
```

### 종속성 변경(Spark) {#change-dependencies-spark}

기존 레서피를 사용하는 경우 종속성에 대한 변경 사항이 pom.xml 파일에 필요합니다. 모델-authoring-sdk 종속성 버전을 2.0.0으로 변경합니다. 그런 다음, pom 파일의 Spark 버전을 2.4.3으로 업데이트하고 Scala 버전은 2.11.12로 업데이트합니다.

```json
<groupId>com.adobe.platform.ml</groupId>
<artifactId>authoring-sdk_2.11</artifactId>
<version>2.0.0</version>
<classifier>jar-with-dependencies</classifier>
```

### Docker 스크립트 준비(Spark) {#prepare-docker-spark}

Spark 레서피는 더 이상 바이너리 결함을 사용하지 않으며 대신 Docker 이미지를 빌드해야 합니다. 아직 설치하지 않은 경우 Docker를 [다운로드하여 설치합니다](https://www.docker.com/products/docker-desktop).

제공된 스칼라 샘플 레시피에서 스크립트 `login.sh` 를 찾아 위치 `build.sh` 를 확인할 수 `experience-platform-dsw-reference/recipes/scala/` 있습니다. 이러한 파일을 복사하여 기존 레서피에 붙여넣을 수 있습니다.

이제 폴더 구조가 다음 예제와 비슷해야 합니다(새로 추가된 파일이 강조 표시됨).

![폴더 구조](./images/migration/scala-folder.png)

다음 단계는 [패키지 소스 파일을 레서피](./models-recipes/package-source-files-recipe.md) 자습서로 따르는 것입니다. 이 자습서에는 Scala(Spark) 레서피용 도커 이미지를 만드는 방법에 대한 개요를 설명하는 섹션이 있습니다. 완료되면 Azure 컨테이너 레지스트리에서 해당 이미지 URL과 함께 Docker 이미지가 제공됩니다.

### 레서피 만들기(Spark) {#create-recipe-spark}

레시피를 만들려면 먼저 [패키지 소스 파일](./models-recipes/package-source-files-recipe.md) 자습서를 완료하고 문서 이미지 URL을 준비하도록 해야 합니다. UI 또는 API를 사용하여 레서피를 만들 수 있습니다.

UI를 사용하여 레시피를 만들려면 Scala용 패키지된 레서피(UI) [](./models-recipes/import-packaged-recipe-ui.md) 가져오기 자습서를 따릅니다.

API를 사용하여 레시피를 만들려면 Scala용 패키지 [레서피(API)](./models-recipes/import-packaged-recipe-api.md) 가져오기 자습서를 따릅니다.

## PySpark 마이그레이션 가이드 {#pyspark-migration-guide}

빌드 단계에서 생성된 레서피 아티팩트는 이제 .egg 바이너리 파일이 포함된 Docker 이미지입니다. 또한 플랫폼 SDK를 사용하여 데이터 세트를 읽고 쓰는 데 사용되는 구문이 변경되었으며 레서피 코드를 수정해야 합니다.

다음 비디오는 PySpark 레서피에 필요한 변경 사항을 이해하는 데 도움이 되도록 디자인되었습니다.

>[!VIDEO](https://video.tv.adobe.com/v/33048?learn=on&quality=12)

### 데이터 세트 읽기 및 쓰기(PySpark) {#pyspark-read-write}

Docker 이미지를 만들기 전에 아래 섹션에 설명된 대로 플랫폼 SDK에서 데이터 세트를 읽고 쓸 수 있는 예제를 검토하십시오. 기존 레서피를 변환하는 경우 플랫폼 SDK 코드를 업데이트해야 합니다.

#### 데이터 세트 읽기

이 섹션에서는 Adobe에서 제공하는 helper.py [예를 사용하여 데이터 세트를](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/pyspark/pysparkretailapp/helper.py) 읽는 데 필요한 변경 사항에 대해 설명합니다.

**데이터 세트를 읽는 오래된 방법**

```python
dataset_options = get_dataset_options(spark.sparkContext)
pd = spark.read.format("com.adobe.platform.dataset") 
  .option(dataset_options.serviceToken(), service_token) 
  .option(dataset_options.userToken(), user_token) 
  .option(dataset_options.orgId(), org_id) 
  .option(dataset_options.serviceApiKey(), api_key)
  .load(dataset_id)
```

**데이터 세트를 읽는 새로운 방법**

Spark 레서피에 대한 업데이트를 통해 다양한 값을 추가하고 변경해야 합니다. 첫째, `DataSetOptions` 더 이상 사용되지 않습니다. Replace `DataSetOptions` with `qs_option`. 또한 새 매개 `option` 변수가 필요합니다. 둘 다 `qs_option.mode` 가 `qs_option.datasetId` 필요하다. 마지막으로, `orgId` 그리고 `serviceApiKey` 로 `imsOrg` 그리고 `apiKey`변경해야 합니다. 데이터 집합 읽기에 대한 비교는 다음 예를 검토하십시오.

```python
qs_option = spark_context._jvm.com.adobe.platform.query.QSOption
pd = sparkSession.read.format("com.adobe.platform.query") 
  .option(qs_option.userToken, {userToken}) 
  .option(qs_option.serviceToken, {serviceToken}) 
  .option(qs_option.imsOrg, {orgId}) 
  .option(qs_option.apiKey, {apiKey}) 
  .option(qs_option.mode, "interactive") 
  .option(qs_option.datasetId, {dataSetId}) 
  .load()
```

>[!TIP]
> 쿼리가 10분 이상 실행되는 경우 대화형 모드가 시간 초과됩니다. 데이터 크기가 몇 GB 이상인 경우 &quot;일괄 처리&quot; 모드로 전환하는 것이 좋습니다. 배치 모드는 시작하는 데 시간이 오래 걸리지만 더 큰 데이터 세트를 처리할 수 있습니다.

#### 데이터 세트에 쓰기

이 섹션에서는 Adobe에서 제공하는 [data_saver.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/pyspark/pysparkretailapp/data_saver.py) 예를 사용하여 데이터 세트를 작성하는 데 필요한 변경 사항에 대해 설명합니다.

**데이터 세트를 작성하는 오래된 방법**

```python
df.write.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, orgId)
  .option(DataSetOptions.serviceToken, serviceToken)
  .option(DataSetOptions.userToken, userToken)
  .option(DataSetOptions.serviceApiKey, apiKey)
  .save(scoringResultsDataSetId)
```

**데이터 세트를 작성하는 새로운 방법**

PySpark 레서피에 대한 업데이트를 통해 많은 값을 추가하고 변경해야 합니다. 첫째, `DataSetOptions` 더 이상 사용되지 않습니다. Replace `DataSetOptions` with `qs_option`. 또한 새 매개 `option` 변수가 필요합니다.  `qs_option.datasetId` 가 필요하며 `{dataSetId}` in을 로드할 필요성을 `.save()` 대체합니다. 마지막으로, `orgId` 그리고 `serviceApiKey` 로 `imsOrg` 그리고 `apiKey`변경해야 합니다. 데이터 집합 읽기에 대한 비교는 다음 예를 검토하십시오.

```python
qs_option = spark_context._jvm.com.adobe.platform.query.QSOption
scored_df.write.format("com.adobe.platform.query") 
  .option(qs_option.userToken, {userToken}) 
  .option(qs_option.serviceToken, {serviceToken}) 
  .option(qs_option.imsOrg, {orgId}) 
  .option(qs_option.apiKey, {apiKey}) 
  .option(qs_option.datasetId, {dataSetId}) 
  .save()
```

### Package Docker 기반 소스 파일(PySpark) {#pyspark-package-docker}

먼저 레시피가 있는 디렉토리로 이동합니다.

이 예를 들어 새로운 PySpark 소매 영업 레서피가 사용되고 [데이터 과학 작업 공간 공용 Github 저장소에서 찾을 수 있습니다](https://github.com/adobe/experience-platform-dsw-reference).

### 샘플 레서피 다운로드(PySpark) {#pyspark-download-sample}

샘플 레서피에는 기존 레서피로 복사해야 하는 파일이 포함되어 있습니다. 모든 샘플 레시피가 포함된 공용 Github를 복제하려면 터미널에 다음을 입력합니다.

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

PySpark 레시피는 다음 디렉토리에 있습니다 `experience-platform-dsw-reference/recipes/pyspark`.

### Dockerfile(PySpark) 추가 {#pyspark-add-dockerfile}

문서 기반 워크플로우를 사용하려면 레서피 폴더에 새 파일이 필요합니다. 의 레서피 폴더에서 Dockerfile을 복사하여 붙여넣습니다 `experience-platform-dsw-reference/recipes/pyspark/Dockerfile`. 또한 아래 코드를 복사하여 붙여 넣고 새 파일을 만들 수도 있습니다 `Dockerfile`.

>[!IMPORTANT]
> 아래 표시된 예제 egg 파일은 조리법의 egg 파일 이름으로 대체되어야 `pysparkretailapp-*.egg` 합니다.

```scala
FROM adobe/acp-dsw-ml-runtime-pyspark:0.0.1
RUN mkdir /recipe

COPY . /recipe

RUN cd /recipe && \
    ${PYTHON} setup.py clean install && \
    rm -rf /recipe

RUN cp /databricks/conda/envs/${DEFAULT_DATABRICKS_ROOT_CONDA_ENV}/lib/python3.6/site-packages/pysparkretailapp-*.egg /application.egg
```

### Docker 스크립트 준비(PySpark) {#pyspark-prepare-docker}

PySpark 레시피는 더 이상 바이너리 결함을 사용하지 않으며 대신 Docker 이미지를 만들어야 합니다. 아직 설치하지 않은 경우 Docker를 다운로드하여 [설치합니다](https://www.docker.com/products/docker-desktop).

제공된 PySpark 샘플 레시피에서 스크립트 `login.sh` 를 찾아 위치 `build.sh` 를 확인할 수 `experience-platform-dsw-reference/recipes/pyspark` 있습니다. 이러한 파일을 복사하여 기존 레서피에 붙여넣을 수 있습니다.

이제 폴더 구조가 다음 예제와 비슷해야 합니다(새로 추가된 파일이 강조 표시됨).

![폴더 구조](./images/migration/folder.png)

이제 Docker 이미지를 사용하여 레시피를 작성할 수 있습니다. 다음 단계는 [패키지 소스 파일을 레서피](./models-recipes/package-source-files-recipe.md) 자습서로 따르는 것입니다. 이 자습서에는 PySpark(Spark 2.4) 레서피용 도커 이미지를 만드는 방법에 대한 개요를 설명하는 섹션이 있습니다. 완료되면 Azure 컨테이너 레지스트리에서 해당 이미지 URL과 함께 Docker 이미지가 제공됩니다.

### 레서피 만들기(PySpark) {#pyspark-create-recipe}

레시피를 만들려면 먼저 [패키지 소스 파일](./models-recipes/package-source-files-recipe.md) 자습서를 완료하고 문서 이미지 URL을 준비하도록 해야 합니다. UI 또는 API를 사용하여 레서피를 만들 수 있습니다.

UI를 사용하여 레시피를 만들려면 PySpark에 대한 패키지화된 레서피(UI) [](./models-recipes/import-packaged-recipe-ui.md) 가져오기 자습서를 따릅니다.

API를 사용하여 레시피를 만들려면 PySpark용 패키지 [레서피(API)](./models-recipes/import-packaged-recipe-api.md) 가져오기 자습서를 따릅니다.

## 노트북 마이그레이션 가이드 {#notebook-migration}

JupiterLab 노트북의 최근 변경 사항을 적용하려면 기존 PySpark 및 Spark 2.3 노트북을 2.4로 업데이트해야 합니다. 이러한 변경 사항을 통해 JupiterLab Launcher가 새로운 스타터 노트북으로 업데이트되었습니다. 전자 필기장을 변환하는 방법에 대한 단계별 가이드를 보려면 다음 안내서 중 하나를 선택하십시오.

- [PySpark 2.3 - 2.4 마이그레이션 안내서](#pyspark-notebook-migration)
- [Spark 2.3에서 Spark 2.4(Scala) 마이그레이션 가이드](#spark-notebook-migration)

다음 비디오는 JupiterLab 노트북에 필요한 변경 사항을 이해하는 데 도움이 되도록 설계되었습니다.

>[!VIDEO](https://video.tv.adobe.com/v/33444?quality=12&learn=on)

## PySpark 2.3-2.4 노트북 마이그레이션 안내서 {#pyspark-notebook-migration}

PySpark 2.4가 JupiterLab 노트북에 도입되면서 PySpark 2.4가 탑재된 새로운 Python 노트북이 PySpark 3 커널 대신 Python 3 커널을 사용하고 있다. 즉, PySpark 2.3에서 실행되는 기존 코드는 PySpark 2.4에서 지원되지 않습니다.

>[!IMPORTANT] PySpark 2.3은 더 이상 사용되지 않으며 이후 릴리스에서 제거되도록 설정됩니다. 기존의 모든 예는 PySpark 2.4 예로 대체되도록 설정됩니다.

기존 PySpark 3(Spark 2.3) 노트북을 Spark 2.4로 변환하려면 아래에 나와 있는 예제를 따르십시오.

### 커널

PySpark 3(Spark 2.4) 노트북에서는 PySpark 3(Spark 2.3 - 더 이상 사용되지 않음) 노트북에 사용되는 가치 없는 PySpark 커널 대신 Python 3 커널을 사용합니다.

JupiterLab UI에서 커널을 확인하거나 변경하려면 노트북 오른쪽 상단 내비게이션 막대에 있는 커널 버튼을 선택합니다. 사전 정의된 실행 노트북 중 하나를 사용하는 경우 커널이 미리 선택됩니다. 아래 예제는 PySpark 3(Spark 2.4) *집선* 노트북 스타터를 사용합니다.

![커널](./images/migration/pyspark-migration/check-kernel.png)

드롭다운 메뉴를 선택하면 사용 가능한 커넬 목록이 열립니다.

![커널](./images/migration/pyspark-migration/kernel-click.png)

![커널 드롭다운](./images/migration/pyspark-migration/select-kernel.png)

PySpark 3(Spark 2.4) 노트북의 경우 Python 3 커널을 선택하고 **선택** 단추를 클릭하여 확인합니다.

![커널 확인](./images/migration/pyspark-migration/confirm-kernel.png)

## sparkSession 초기화 중

모든 Spark 2.4 노트북에서는 새로운 상용구 코드로 세션을 초기화해야 합니다.

<table>
  <th>노트북</th>
  <th>PySpark 3(Spark 2.3 - 더 이상 사용되지 않음)</th>
  <th>PySpark 3(Spark 2.4)</th>
  <tr>
  <th>커널</th>
  <td align="center">PySpark 3</td>
  <td align="center">Python 3</td>
  </tr>
  <tr>
  <th>코드</th>
  <td>
  <pre class="JSON language-JSON hljs">
  spark
</pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
spark.sql 가져오기 SparkSessionsspark = SparkSession.builder.getOrCreate()
</pre>
  </td>
  </tr>
</table>

다음 이미지는 PySpark 2.3 및 PySpark 2.4의 구성 차이점을 강조 표시합니다. 이 예에서는 JupiterLab Launcher에서 제공하는 *집선* 시작 노트북을 사용합니다.

**2.3에 대한 구성 예(더 이상 사용되지 않음)**

![config 1](./images/migration/pyspark-migration/2.3-config.png)![config 2](./images/migration/pyspark-migration/2.3-config-import.png)

**2.4에 대한 구성 예**

![config 3](./images/migration/pyspark-migration/2.4-config.png)

## %dataset 매직 사용 {#magic}

Spark 2.4가 도입되면서 `%dataset` 새로운 PySpark 3(Spark 2.4) 노트북(Python 3 커널)에서 사용자 정의 마법을 사용할 수 있게 되었습니다.

**사용**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**설명**

Python 노트북(Python 3 커널)에서 데이터 세트를 읽거나 쓰는 사용자 정의 데이터 과학 작업 공간 매직 명령입니다.

- **{action}**: 데이터 세트에 대해 수행할 작업 유형입니다. 두 가지 작업을 &quot;읽기&quot; 또는 &quot;쓰기&quot;로 사용할 수 있습니다.
- **—datasetId {id}**: 데이터를 읽거나 쓸 수 있도록 데이터 집합의 ID를 제공하는 데 사용됩니다. 이것은 필수 인수입니다.
- **—dataFrame {df}**: 판다들의 데이터 프레임 이것은 필수 인수입니다.
   - 작업이 &quot;읽기&quot;인 경우 {df}는 데이터 집합 읽기 작업의 결과를 사용할 수 있는 변수입니다.
   - 작업이 &quot;write&quot;이면 이 데이터 프레임 {df}이(가) 데이터 세트에 기록됩니다.
- **—mode(선택 사항)**: 허용되는 매개 변수는 &quot;batch&quot; 및 &quot;interactive&quot;입니다. 기본적으로 모드는 &quot;interactive&quot;로 설정됩니다. 대량의 데이터를 읽을 때는 &quot;일괄 처리&quot; 모드를 사용하는 것이 좋습니다.

**예**

- **예제**&#x200B;보기: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **쓰기 예**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

## LocalContext에서 데이터 프레임으로 로드

Spark 2.4가 도입됨에 따라 [`%dataset`](#magic) 맞춤형 기능이 제공됩니다. 다음 예에서는 PySpark(Spark 2.3) 및 PySpark(Spark 2.4) 노트북에서 데이터 프레임을 로드하기 위한 주요 차이점을 강조 표시합니다.

**PySpark 3 사용(Spark 2.3 - 더 이상 사용되지 않음) - PySpark 3 커널**

```python
dataset_options = sc._jvm.com.adobe.platform.dataset.DataSetOptions
pd0 = spark.read.format("com.adobe.platform.dataset")
  .option(dataset_options.orgId(), "310C6D375BA5248F0A494212@AdobeOrg")
  .load("5e68141134492718af974844")
```

**PySpark 3 사용(Spark 2.4) - Python 3 커널**

```python
%dataset read --datasetId 5e68141134492718af974844 --dataFrame pd0
```

| 요소 | 설명 |
| ------- | ----------- |
| pd0 | 사용하거나 만들 판다의 데이터 프레임 개체의 이름입니다. |
| [%dataset](#magic) | Python3 커널의 데이터 액세스를 위한 사용자 정의 기능 |

다음 이미지는 PySpark 2.3 및 PySpark 2.4의 데이터 로드 시 주요 차이점을 강조 표시합니다. 이 예에서는 JupiterLab Launcher에서 제공하는 *Aggregation* 시작 노트북을 사용합니다.

**PySpark 2.3에서 데이터 로드(루마 데이터 세트) - 더 이상 사용되지 않음**

![로드 1](./images/migration/pyspark-migration/2.3-load.png)

**PySpark 2.4에서 데이터 로드(루마 데이터 세트)**

PySpark 3(Spark 2.4)을 사용하면 로딩 시 `sc = spark.sparkContext` 정의할 수 있습니다.

![로드 1](./images/migration/pyspark-migration/2.4-load.png)

**PySpark 2.3에서 Experience Cloud Platform 데이터 로드 - 더 이상 사용되지 않음**

![로드 2](./images/migration/pyspark-migration/2.3-load-alt.png)

**PySpark 2.4에서 Experience Cloud 플랫폼 데이터 로드**

PySpark 3(Spark 2.4)을 사용하면 더 이상 `org_id` 정의할 `dataset_id` 필요가 없습니다. 또한 데이터 세트 `df = spark.read.format` 를 손쉽게 읽고 쓸 수 [`%dataset`](#magic) 있는 맞춤형 마법으로 대체되었습니다.

![로드 2](./images/migration/pyspark-migration/2.4-load-alt.png)

| 요소 | description |
| ------- | ----------- |
| [%dataset](#magic) | Python3 커널의 데이터 액세스를 위한 사용자 정의 기능 |

>[!TIP] —mode를 `interactive` or로 설정할 수 `batch`있습니다. —mode의 기본값은 입니다 `interactive`. 대량의 데이터를 읽을 때는 `batch` 모드를 사용하는 것이 좋습니다.

## 로컬 데이터 프레임 만들기

PySpark 3(Spark 2.4) 스파크링은 `%%` 더 이상 지원되지 않습니다. 다음 작업은 더 이상 활용할 수 없습니다.

- `%%help`
- `%%info`
- `%%cleanup`
- `%%delete`
- `%%configure`
- `%%local`

다음 표에서는 스파크매직 쿼리를 변환하는 데 필요한 변경 사항에 대해 `%%sql` 설명합니다.

<table>
  <th>노트북</th>
  <th>PySpark 3(Spark 2.3 - 더 이상 사용되지 않음)</th>
  <th>PySpark 3(Spark 2.4)</th>
  <tr>
  <th>커널</th>
  <td align="center">PySpark 3</td>
  <td align="center">Python 3</td>
  </tr>
  <tr>
  <th>코드</th>
      <td>
         <pre class="JSON language-JSON hljs">%sql -o dfselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs"> %%sql -o df -n limiselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs">%%sql -o df -qselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs"> %%sql -o df -r fractionselect * from sparkdf
</pre>
      </td>
      <td>
         <pre class="JSON language-JSON hljs">
df = spark.sql(" SELECT * FROM sparkdf")
</pre>
         <pre class="JSON language-JSON hljs">
df = spark.sql(" SELECT * FROM sparkdf LIMIT")
</pre>
         <pre class="JSON language-JSON hljs">
df = spark.sql(" SELECT * FROM sparkdf LIMIT")
</pre>
         <pre class="JSON language-JSON hljs">
sample_df = df.sample(fraction)
</pre>
      </td>
   </tr>
</table>

>[!TIP] 대체, 이중 분수 또는 긴 시드가 있는 부울 값과 같은 선택적 시드 샘플을 지정할 수도 있습니다.

다음 이미지는 PySpark 2.3 및 PySpark 2.4에서 로컬 데이터 프레임을 만들기 위한 주요 차이점을 강조 표시합니다. 이 예에서는 JupiterLab Launcher에서 제공하는 *집계* 시작 전자 필기장을 사용합니다.

**로컬 데이터 프레임 PySpark 2.3 만들기 - 더 이상 사용되지 않음**

![데이터 프레임 1](./images/migration/pyspark-migration/2.3-dataframe.png)

**로컬 데이터 프레임 PySpark 2.4 만들기**

PySpark 3(Spark 2.4) `%%sql` Spark는 더 이상 지원되지 않으며 다음과 같이 대체되었습니다.

![데이터 프레임 2](./images/migration/pyspark-migration/2.4-dataframe.png)

## 데이터 세트에 쓰기

Spark 2.4가 도입되면서 데이터 세트를 [`%dataset`](#magic) 보다 깔끔하게 작성할 수 있는 맞춤형 기능이 제공됩니다. 데이터 세트에 쓰려면 다음 Spark 2.4 예를 사용하십시오.

**PySpark 3 사용(Spark 2.3 - 더 이상 사용되지 않음) - PySpark 3 커널**

```python
userToken = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.USER_TOKEN")
serviceToken = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.SERVICE_TOKEN")
serviceApiKey = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.SERVICE_API_KEY")

dataset_options = sc._jvm.com.adobe.platform.dataset.DataSetOptions

pd0.write.format("com.adobe.platform.dataset")
  .option(dataset_options.orgId(), "310C6D375BA5248F0A494212@AdobeOrg")
  .option(dataset_options.userToken(), userToken)
  .option(dataset_options.serviceToken(), serviceToken)
  .option(dataset_options.serviceApiKey(), serviceApiKey)
  .save("5e68141134492718af974844")
```

**PySpark 3 사용(Spark 2.4) - Python 3 커널**

```python
%dataset write --datasetId 5e68141134492718af974844 --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

| 요소 | description |
| ------- | ----------- |
| pd0 | 사용하거나 만들 판다의 데이터 프레임 개체의 이름입니다. |
| [%dataset](#magic) | Python3 커널의 데이터 액세스를 위한 사용자 정의 기능 |

>[!TIP] —mode를 `interactive` or로 설정할 수 `batch`있습니다. —mode의 기본값은 입니다 `interactive`. 대량의 데이터를 읽을 때는 `batch` 모드를 사용하는 것이 좋습니다.

다음 이미지는 PySpark 2.3 및 PySpark 2.4의 플랫폼에 데이터를 다시 작성하기 위한 주요 차이점을 강조 표시합니다. 이 예에서는 JupiterLab Launcher에서 제공하는 *집계* 시작 노트북을 사용합니다.

**Platform PySpark 2.3으로 데이터 다시 쓰기 - 가치 하락**

![dataframe 1](./images/migration/pyspark-migration/2.3-write.png)![dataframe 1](./images/migration/pyspark-migration/2.3-write-2.png)![dataframe 1](./images/migration/pyspark-migration/2.3-write-3.png)

**Platform PySpark 2.4로 데이터 다시 쓰기**

PySpark 3(Spark 2.4)을 사용하면 사용자 요구에 맞게 변경 가능한 기능 `%dataset` 을 통해 `userToken`, `serviceToken``serviceApiKey`및 `.option`같은 값을 정의할 필요가 없습니다. 또한 더 이상 정의할 `orgId` 필요가 없습니다.

![dataprame 2](./images/migration/pyspark-migration/2.4-write.png)![dataframe 2](./images/migration/pyspark-migration/2.4-write-2.png)

## Spark 2.3에서 Spark 2.4(Scala) 노트북 마이그레이션 가이드 {#spark-notebook-migration}

Spark 2.4가 JupiterLab 노트북에 새롭게 도입되면서 기존 Spark(Spark 2.3) 노트북에서 Spark 커널 대신 커널을 사용하고 있습니다. 즉, Spark(Spark 2.3)에서 실행되는 기존 코드는 Scala(Spark 2.4)에서 지원되지 않습니다. 또한 모든 새로운 Spark 노트북에는 JupiterLab launcher에서 Scala(Spark 2.4)를 사용해야 합니다.

>[!IMPORTANT] Spark(Spark 2.3)는 더 이상 사용되지 않으며 이후 릴리스에서 제거되도록 설정됩니다. 기존의 모든 예는 Scala(Spark 2.4) 예로 대체되도록 설정됩니다.

기존 Spark (Spark 2.3) 노트북을 Scala(Spark 2.4)로 변환하려면 아래 설명된 예를 따르십시오.

## 커널

Scala(Spark 2.4) 노트북에서는 Spark(Spark 2.3 - 더 이상 사용되지 않음) 노트북에 사용되는 가치 없는 Spark 커널 대신 Scala Kernel을 사용합니다.

JupiterLab UI에서 커널을 확인하거나 변경하려면 노트북 오른쪽 상단 내비게이션 막대에 있는 커널 버튼을 선택합니다. 커널 *선택* 팝업 창이 나타납니다. 사전 정의된 실행 노트북 중 하나를 사용하는 경우 커널이 미리 선택됩니다. 아래 예제는 JupiterLab Launcher의 Scala *Clustering* 노트북을 사용합니다.

![커널](./images/migration/spark-scala/scala-kernel.png)

드롭다운 메뉴를 선택하면 사용 가능한 커넬 목록이 열립니다.

![커널 드롭다운](./images/migration/spark-scala/select-dropdown.png)

![커널](./images/migration/spark-scala/dropdown.png)

Scala(Spark 2.4) 전자 필기장의 경우 Scala 커널 을 선택하고 **선택** 단추를 클릭하여 확인합니다.

![커널 확인](./images/migration/spark-scala/select.png)

## SparkSession 초기화 {#initialize-sparksession-scala}

모든 Scala(Spark 2.4) 노트북에서는 다음 상용구 코드로 세션을 초기화해야 합니다.

<table>
  <th>노트북</th>
  <th>Spark(Spark 2.3 - 더 이상 사용되지 않음)</th>
  <th>스칼라(Spark 2.4)</th>
  <tr>
  <th>커널</th>
  <td align="center">Spark</td>
  <td align="center">Scala</td>
  </tr>
  <tr>
  <th>코드</th>
  <td align="center">
  코드 필요 없음
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
import org.apache.spark.sql.{ SparkSession }val spark = SparkSession .builder() .master("local") .getOrCreate()
</pre>
  </td>
  </tr>
</table>

아래의 Scala(Spark 2.4) 이미지는 Spark 2.3 Spark 커널 및 Spark 2.4 Scala 커널을 사용하여 sparkSession을 초기화하면 주요 차이점을 강조 표시합니다. 이 예에서는 JupiterLab *Launcher에서* 제공하는 클러스터링 시작 노트북을 사용합니다.

**Spark(Spark 2.3 - 더 이상 사용되지 않음)**

Spark(Spark 2.3 - 가치 하락) - 스파크 커널을 사용하므로 Spark를 정의할 필요가 없습니다.

**스칼라(Spark 2.4)**

Scala 커널과 함께 Spark 2.4를 사용하려면 읽기 `val spark` 또는 쓰기 `SparkSesson` 를 위해 정의 및 가져와야 합니다.

![spark 가져오기 및 정의](./images/migration/spark-scala/start-session.png)

## 쿼리 데이터

Scala(Spark 2.4) `%%` 스파크마치는 더 이상 지원되지 않습니다. 다음 작업은 더 이상 활용할 수 없습니다.

- `%%help`
- `%%info`
- `%%cleanup`
- `%%delete`
- `%%configure`
- `%%local`

다음 표에서는 스파크매직 쿼리를 변환하는 데 필요한 변경 사항에 대해 `%%sql` 설명합니다.

<table>
  <th>노트북</th>
  <th>Spark(Spark 2.3 - 더 이상 사용되지 않음)</th>
  <th>스칼라(Spark 2.4)</th>
  <tr>
  <th>커널</th>
  <td align="center">Spark</td>
  <td align="center">Scala</td>
  </tr>
  <tr>
  <th>코드</th>
    <td>
       <pre class="JSON language-JSON hljs">
%sql -o dfselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -n limiselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -qselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -r fractionselect * from sparkdf
</pre>
      </td>
      <td>
         <pre class="JSON language-JSON hljs">
val df = spark.sql(" SELECT * FROM sparkdf")
</pre>
         <pre class="JSON language-JSON hljs">
val df = spark.sql(" SELECT * FROM sparkdf LIMIT")
</pre>
         <pre class="JSON language-JSON hljs">
val df = spark.sql(" SELECT * FROM sparkdf LIMIT")
</pre>
         <pre class="JSON language-JSON hljs">
val sample_df = df.sample(fraction) </pre>
      </td>
   </tr>
</table>

아래의 Scala(Spark 2.4) 이미지는 Spark 2.3 Spark 커널 및 Spark 2.4 Scala를 사용하여 쿼리를 작성할 때 중요한 차이점을 강조 표시합니다. 이 예에서는 JupiterLab *Launcher에서* 제공하는 클러스터링 시작 노트북을 사용합니다.

**Spark(Spark 2.3 - 더 이상 사용되지 않음)**

Spark(Spark 2.3 - 더 이상 사용되지 않음) 노트북에서는 Spark 커널을 사용합니다. 스파크 커널은 스파크카를 지원하고 `%%sql` 사용합니다.

![](./images/migration/spark-scala/sql-2.3.png)

**스칼라(Spark 2.4)**

Scala 커널은 더 이상 스파크마직을 지원하지 `%%sql` 않습니다. 기존 스파크매직 코드를 변환해야 합니다.

![spark 가져오기 및 정의](./images/migration/spark-scala/sql-2.4.png)

## 데이터 세트 읽기 {#notebook-read-dataset-spark}

Spark 2.3에서는 데이터를 읽거나 코드 셀에서 원시 값을 사용하는 데 사용되는 `option` 값에 대한 변수를 정의해야 했습니다. Scala에서 값을 선언 및 반환하는 데 사용할 수 있으므로 변수 `sys.env("PYDASDK_IMS_USER_TOKEN")` 를 정의할 필요가 없습니다 `var userToken`. 아래의 Scala(Spark 2.4) 예제 `sys.env` 에서 데이터 세트를 읽는 데 필요한 모든 값을 정의하고 반환하는 데 사용됩니다.

**Spark 사용(Spark 2.3 - 더 이상 사용되지 않음) - Spark Kernel**

```scala
import com.adobe.platform.dataset.DataSetOptions
var df1 = spark.read.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, "310C6D375BA5248F0A494212@AdobeOrg")
  .option(DataSetOptions.batchId, "dbe154d3-197a-4e6c-80f8-9b7025eea2b9")
  .load("5e68141134492718af974844")
```

**Scala 사용(Spark 2.4) - Scala Kernel**

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
  .option("ims-org", sys.env("IMS_ORG_ID"))
  .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
  .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()
```

| 요소를 생성하지 않습니다 | description |
| ------- | ----------- |
| df1 | 데이터를 읽고 쓰는 데 사용되는 판다데이터 프레임을 나타내는 변수입니다. |
| user-token | 을 사용하여 자동으로 반입되는 사용자 토큰입니다 `sys.env("PYDASDK_IMS_USER_TOKEN")`. |
| 서비스 토큰 | 를 사용하여 자동으로 반입되는 서비스 토큰입니다 `sys.env("PYDASDK_IMS_SERVICE_TOKEN")`. |
| ims-org | 를 사용하여 자동으로 가져오는 ims-org ID입니다 `sys.env("IMS_ORG_ID")`. |
| api-key | 를 사용하여 자동으로 가져오는 api 키 `sys.env("PYDASDK_IMS_CLIENT_ID")`. |

아래 이미지는 Spark 2.3 및 Spark 2.4를 사용하여 데이터를 로드할 때 중요한 차이점을 강조 표시합니다. 이 예에서는 JupiterLab Launcher에서 제공하는 *클러스터링* 시작 노트북을 사용합니다.

**Spark(Spark 2.3 - 더 이상 사용되지 않음)**

Spark(Spark 2.3 - 더 이상 사용되지 않음) 노트북에서는 Spark 커널을 사용합니다. 다음 두 셀에서는 날짜 범위(2019-3-21, 2019-3-29)에서 지정된 데이터 세트 ID를 사용하여 데이터 세트를 로드하는 예를 보여 줍니다.

![spark 2.3 로드 중](./images/migration/spark-scala/load-2.3.png)

**스칼라(Spark 2.4)**

Scala(Spark 2.4) 노트북에서는 첫 번째 코드 셀에서 강조 표시된 대로 설정 시 더 많은 값이 필요한 Scala 커널을 사용합니다. 또한 더 많은 값 `var mdata` 을 `option` 입력해야 합니다. 이 전자 필기장에는 SparkSession을 [초기화하기](#initialize-sparksession-scala) 위해 이전에 언급된 코드가 `var mdata` 코드 셀 내에 포함되어 있습니다.

![spark 2.4 로드 중](./images/migration/spark-scala/load-2.4.png)

>[!TIP] Scala에서는 값 `sys.env()` 을 선언하고 반환하는 데 사용할 수 있습니다 `option`. 이렇게 하면 변수가 한 번만 사용된다는 사실을 알고 있으면 변수를 정의할 필요가 없습니다. 다음 예제에서는 위 예제 `val userToken` 를 가져와서 내에 있는 줄을 선언합니다 `option`.
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## 데이터 세트에 쓰기

데이터 세트를 [읽는 것과](#notebook-read-dataset-spark)유사하게 데이터 세트에 기록하려면 아래 예제에 나와 있는 추가 `option` 값이 필요합니다. Scala에서 값을 선언 및 반환하는 데 사용할 수 있으므로 변수 `sys.env("PYDASDK_IMS_USER_TOKEN")` 를 정의할 필요가 없습니다 `var userToken`. 아래의 Scala 예에서 `sys.env` 는 데이터 세트에 쓰는 데 필요한 모든 값을 정의하고 반환하는 데 사용됩니다.

**Spark 사용(Spark 2.3 - 더 이상 사용되지 않음) - Spark Kernel**

```scala
import com.adobe.platform.dataset.DataSetOptions

var userToken = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.USER_TOKEN").get
var serviceToken = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.SERVICE_TOKEN").get
var serviceApiKey = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.SERVICE_API_KEY").get

df1.write.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, "310C6D375BA5248F0A494212@AdobeOrg")
  .option(DataSetOptions.userToken, userToken)
  .option(DataSetOptions.serviceToken, serviceToken)
  .option(DataSetOptions.serviceApiKey, serviceApiKey)
  .save("5e68141134492718af974844")
```

**Scala 사용(Spark 2.4) - Scala Kernel**

```scala
import org.apache.spark.sql.{Dataset, SparkSession}

val spark = SparkSession.builder().master("local").getOrCreate()

df1.write.format("com.adobe.platform.query")
  .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
  .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
  .option("ims-org", sys.env("IMS_ORG_ID"))
  .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| 요소를 생성하지 않습니다 | description |
| ------- | ----------- |
| df1 | 데이터를 읽고 쓰는 데 사용되는 판다데이터 프레임을 나타내는 변수입니다. |
| user-token | 을 사용하여 자동으로 반입되는 사용자 토큰입니다 `sys.env("PYDASDK_IMS_USER_TOKEN")`. |
| 서비스 토큰 | 를 사용하여 자동으로 반입되는 서비스 토큰입니다 `sys.env("PYDASDK_IMS_SERVICE_TOKEN")`. |
| ims-org | 를 사용하여 자동으로 가져오는 ims-org ID입니다 `sys.env("IMS_ORG_ID")`. |
| api-key | 를 사용하여 자동으로 가져오는 api 키 `sys.env("PYDASDK_IMS_CLIENT_ID")`. |