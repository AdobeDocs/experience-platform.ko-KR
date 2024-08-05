---
keywords: Experience Platform; 자습서; 기능 파이프라인; 데이터 과학 작업 영역; 인기 있는 항목
title: 모델 작성 SDK를 사용하여 기능 파이프라인 만들기
type: Tutorial
description: Adobe Experience Platform 사용하면 사용자 정의 기능 파이프라인을 빌드 및 생성하여 Sensei Machine Learning Framework Runtime을 통해 대규모로 기능 엔지니어링을 수행할 수 있습니다. 이 문서에서는 기능 파이프라인에 있는 다양한 클래스에 대해 설명하고 PySpark에서 모델 작성 SDK를 사용하여 사용자 지정 기능 파이프라인을 만들기 위한 단계별 자습서를 제공합니다.
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# 모델 작성 SDK를 사용하여 기능 파이프라인 생성

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

>[!IMPORTANT]
>
> 기능 파이프라인은 현재 API를 통해서만 사용할 수 있습니다.

Adobe Experience Platform을 사용하면 Sensei Machine Learning Framework 런타임(이하 &quot;런타임&quot;이라 함)을 통해 규모에 맞게 기능 엔지니어링을 수행할 수 있는 사용자 지정 기능 파이프라인을 작성하고 만들 수 있습니다.

이 문서에서는 기능 파이프라인에 있는 다양한 클래스에 대해 설명하고, PySpark에서 모델 작성 SDK](./sdk.md)를 사용하여 [사용자 지정 기능 파이프라인을 만들기 위한 단계별 튜토리얼 기능을 제공합니다.

피쳐 파이프라인이 실행될 때 발생하는 작업 과정 유형은 다음과 같습니다.

1. 레서피 기능은 데이터 세트를 파이프라인에 로드합니다.
2. 기능 변환은 데이터 세트에서 수행되며 Adobe Experience Platform에 다시 기록됩니다.
3. 변환된 데이터는 교육 교육을 위해 로드됩니다.
4. 기능 파이프라인은 Gradient Boosting Regressor를 선택한 모델로 사용하여 단계를 정의합니다.
5. 파이프라인은 교육 데이터 피팅에 사용되며 학습된 모델이 만들어집니다.
6. 모델은 점수 매기기 데이터 세트 로 변환됩니다.
7. 그런 다음 출력의 관심 열이 선택되고 관련 데이터와 함께 다시 [!DNL Experience Platform] 저장됩니다.

## 시작하기

조직에서 레서피 기능을 실행하려면 다음이 필요합니다.
- 입력 데이터 세트.
- 데이터 세트의 스키마.
- 변환된 스키마와 해당 스키마를 기반으로 하는 빈 데이터 세트.
- 출력 스키마 및 해당 스키마를 기반으로 하는 빈 데이터 세트.

위의 모든 데이터 세트를 UI 에 [!DNL Platform] 업로드해야 합니다. 이를 설정하려면 Adobe Systems 제공 [부트스트랩 스크립트를](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap) 사용하십시오.

## 기능 파이프라인 클래스

다음 표에서는 기능 파이프라인을 빌드하기 위해 확장해야 하는 기본 추상 클래스에 대해 설명합니다.

| 추상 클래스 | 설명 |
| -------------- | ----------- |
| DataLoader | DataLoader 클래스는 입력 데이터 검색을 위한 구현 기능을 제공합니다. |
| 데이터 세트 트랜스포머 | DatasetTransformer 클래스는 입력 데이터 세트를 변환하는 구현을 제공합니다. DatasetTransformer 클래스를 제공하지 않도록 선택하고 대신 FeaturePipelineFactory 클래스 내에서 기능 엔지니어링 논리를 구현할 수 있습니다. |
| FeaturePipelineFactory | FeaturePipelineFactory 클래스는 기능 엔지니어링을 수행하기 위해 일련의 Spark 변환기로 구성된 Spark 파이프라인을 빌드합니다. FeaturePipelineFactory 클래스를 제공하지 않도록 선택하고 대신 DatasetTransformer 클래스 내에서 기능 엔지니어링 논리를 구현할 수 있습니다. |
| 데이터 세이버 | DataSaver 클래스는 기능 데이터 세트 저장에 대한 논리를 제공합니다. |

Feature Pipeline 작업이 시작되면 런타임은 먼저 DataLoader를 실행하여 입력 데이터를 DataFrame으로 로드한 다음 DatasetTransformer, FeaturePipelineFactory 또는 둘 다를 실행하여 DataFrame을 수정합니다. 마지막으로 결과 기능 데이터 세트 DataSaver를 통해 저장됩니다.

다음 순서도는 런타임의 실행 순서를 보여 줍니다.

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Feature Pipeline 클래스 구현 {#implement-your-feature-pipeline-classes}

다음 섹션에서는 기능 파이프라인에 필요한 클래스를 구현하는 방법에 대한 세부 정보와 예를 제공합니다.

### 구성 JSON 파일에서 변수 정의 {#define-variables-in-the-configuration-json-file}

구성 JSON 파일은 키-값 쌍으로 구성되며 런타임 중에 나중에 정의할 변수를 지정하기 위한 것입니다. 이러한 키-값 쌍은 입력 데이터 세트 위치, 출력 데이터 세트 ID, 테넌트 ID, 열 헤더 등과 같은 속성을 정의할 수 있습니다.

다음 예제에서는 구성 파일 내에 있는 키-값 쌍을 보여 줍니다.

**구성 JSON 예제**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```

매개 변수로 정의하는 `config_properties` 클래스 메서드를 통해 구성 JSON에 액세스할 수 있습니다. 예:

**파이스파크**

```python
dataset_id = str(config_properties.get(dataset_id))
```

보다 심층적인 [구성 예는 Data Science 작업 영역에서 제공하는 pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) 파일을 참조하십시오.

### DataLoader를 사용하여 입력 데이터 준비 {#prepare-the-input-data-with-dataloader}

DataLoader는 입력 데이터를 검색하고 필터링합니다. DataLoader 구현 시 추상 클래스를 `DataLoader` 확장하고 추상 메서드를 `load`재정의해야 합니다.

다음 예제에서는 ID로 데이터 세트 검색 [!DNL Platform] 하여 DataFrame으로 반환하며, 여기서 데이터 세트 ID(`dataset_id`)는 구성 파일에 정의된 속성입니다.

**PySpark 예제**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

    query_options = get_query_options(spark.sparkContext)

    pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
        .option(query_options.userToken(), user_token) \
        .option(query_options.serviceToken(), service_token) \
        .option(query_options.imsOrg(), org_id) \
        .option(query_options.apiKey(), api_key) \
        .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
        .option(query_options.datasetId(), dataset_id) \
        .load()
    pd.show()

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### DatasetTransformer로 데이터 세트 변환 {#transform-a-dataset-with-datasettransformer}

DatasetTransformer는 입력 DataFrame을 변환하기 위한 논리를 제공하고 새로 파생된 DataFrame을 반환합니다. 이 클래스는 FeaturePipelineFactory와 함께 작동하거나, 유일한 기능 엔지니어링 구성 요소로 작동하거나, 이 클래스를 구현하지 않도록 선택할 수 있습니다.

다음 예제에서는 DatasetTransformer 클래스를 확장합니다.

**PySpark 예제**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### FeaturePipelineFactory를 사용하여 데이터 기능 엔지니어링 {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory를 사용하면 Spark Pipeline을 통해 일련의 Spark Transformer를 정의하고 함께 연결하여 기능 엔지니어링 논리를 구현 할 수 있습니다. 이 클래스는 DatasetTransformer와 함께 작동하거나, 유일한 기능 엔지니어링 구성 요소로 작동하거나, 이 클래스를 구현하지 않도록 선택할 수 있습니다.

다음 예제에서는 FeaturePipelineFactory 클래스를 확장합니다.

**PySpark 예**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### DataSaver로 기능 데이터 세트 저장 {#store-your-feature-dataset-with-datasaver}

DataSaver는 결과 기능 데이터 세트를 저장소 위치에 저장하는 역할을 합니다. DataSaver 구현은 추상 클래스 `DataSaver`을(를) 확장하고 추상 메서드 `save`을(를) 재정의해야 합니다.

다음 예제에서는 데이터를 ID별로 [!DNL Platform] 데이터 집합으로 저장하는 DataSaver 클래스를 확장합니다. 여기서 데이터 집합 ID(`featureDatasetId`) 및 테넌트 ID(`tenantId`)는 구성에 정의된 속성입니다.

**PySpark 예**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```


### 애플리케이션 파일에 구현된 클래스 이름을 지정합니다 {#specify-your-implemented-class-names-in-the-application-file}

이제 기능 파이프라인 클래스가 정의되고 구현되었으므로 애플리케이션 YAML 파일에서 클래스 이름을 지정해야 합니다.

다음 예제에서는 구현된 클래스 이름을 지정합니다.

**PySpark 예제**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## API를 사용하여 기능 파이프라인 엔진 만들기 {#create-feature-pipeline-engine-api}

이제 기능 파이프라인을 작성했으므로 API에서 기능 파이프라인 끝점을 호출하기 위해 Docker 이미지를 만들어야 합니다 [!DNL Sensei Machine Learning] . 기능 파이프라인 끝점을 호출하려면 Docker 이미지 URL 이 필요합니다.

>[!TIP]
>
>Docker URL가 없는 경우 Docker 호스트 URL 만드는 방법에 대한 단계별 연습을 위해 패키지 원본 파일을 레서피](../models-recipes/package-source-files-recipe.md) 튜토리얼로 방문[.

필요에 따라 다음 Postman 컬렉션 을 사용하여 기능 파이프라인 API 작업 과정 완료를 지원할 수도 있습니다.

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### 기능 파이프라인 엔진 만들기 {#create-engine-api}

Docker 이미지 위치가 있으면 에 대한 POST 를 수행하여 API를 [!DNL Sensei Machine Learning] 사용하여 기능 파이프라인 엔진을](../api/engines.md#feature-pipeline-docker) 만들 수 있습니다[`/engines`. 기능 파이프라인 엔진을 생성하면 엔진 고유 식별자(`id`)가 제공됩니다. 계속하기 전에 이 값을 저장하십시오.

### 인스턴스 만들기 {#create-mlinstance}

새로 만든 `engineID`을(를) 사용하여 `/mlInstance` 끝점에 대한 POST 요청을 만들어 [MLIstance를 만들고](../api/mlinstances.md#create-an-mlinstance)해야 합니다. 성공적인 응답은 다음 API 호출에 사용된 고유 식별자(`id`)를 포함하여 새로 생성된 MLInstance의 세부 정보가 포함된 페이로드를 반환합니다.

### 실험 만들기 {#create-experiment}

다음, 실험을](../api/experiments.md#create-an-experiment) 만들어야 합니다[. 실험을 만들려면 MLIstance 고유 식별자(`id`)가 있어야 하며 `/experiment` 끝점에 대한 POST 요청을 수행해야 합니다. 성공적인 응답은 다음 API 호출에 사용된 고유 식별자(`id`)를 포함하여 새로 만들어진 실험의 세부 정보가 포함된 페이로드를 반환합니다.

### 실험 실행 기능 파이프라인 작업 지정 {#specify-feature-pipeline-task}

실험을 만든 후에는 실험의 모드를 `featurePipeline`(으)로 변경해야 합니다. 모드를 변경하려면 `EXPERIMENT_ID`을(를) 사용하여 [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring)에 추가 POST을 하고 본문에서 `{ "mode":"featurePipeline"}`을(를) 전송하여 기능 파이프라인 실험 실행을 지정하십시오.

완료되면 `/experiments/{EXPERIMENT_ID}`에게 [실험 상태를 검색](../api/experiments.md#retrieve-specific)하도록 GET을 요청하고 실험 상태가 업데이트될 때까지 기다립니다.

### 실험 실행 교육 작업 지정 {#training}

다음, 교육 실행 작업을](../api/experiments.md#experiment-training-scoring) 지정해야 [합니다. 본문에 POST `experiments/{EXPERIMENT_ID}/runs` 하고 mode를 로 `train` 설정하고 교육 매개 변수가 포함된 작업 배열을 보냅니다. 성공적인 응답은 요청된 실험의 세부 사항이 포함된 페이로드를 반환합니다.

완료되면 `/experiments/{EXPERIMENT_ID}`에게 [실험 상태를 검색](../api/experiments.md#retrieve-specific)하도록 GET을 요청하고 실험 상태가 업데이트될 때까지 기다립니다.

### 실험 실행 채점 작업 지정 {#scoring}

>[!NOTE]
>
> 이 단계를 완료하려면 실험과 연결된 성공적인 교육 실행이 하나 이상 있어야 합니다.

교육 실행이 성공하면 점수 실행 작업을](../api/experiments.md#experiment-training-scoring) 지정해야 [합니다. 에 `experiments/{EXPERIMENT_ID}/runs` 대한 POST 및 본문에서 속성을 &quot;score&quot;로 설정합니다 `mode` . 채점 실험 실행이 시작됩니다.

완료되면 `/experiments/{EXPERIMENT_ID}`에게 [실험 상태를 검색](../api/experiments.md#retrieve-specific)하도록 GET을 요청하고 실험 상태가 업데이트될 때까지 기다립니다.

채점이 완료되면 기능 파이프라인이 작동되어야 합니다.

## 다음 단계 {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

이 문서를 읽은 후에는 모델 작성 SDK를 사용하여 기능 파이프라인을 작성하고 도커 이미지를 만든 다음 도커 이미지 URL을 사용하여 [!DNL Sensei Machine Learning] API를 사용하여 기능 파이프라인 모델을 만들었습니다. 이제 [[!DNL Sensei Machine Learning API]](../api/getting-started.md)을(를) 사용하여 데이터 집합을 계속 변환하고 데이터 기능을 규모에 맞게 추출할 준비가 되었습니다.
