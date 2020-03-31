---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: 피쳐 파이프라인 만들기
topic: Tutorial
translation-type: tm+mt
source-git-commit: b9b0578a43182650b3cfbd71f46bcb817b3b0cda

---


# 피쳐 파이프라인 만들기

Adobe Experience Platform을 사용하면 Sensei Machine Learning Framework 런타임(이하 &quot;런타임&quot;이라 한다)을 통해 기능 엔지니어링의 규모에 맞게 사용자 정의 기능 파이프라인을 구축 및 생성할 수 있습니다.

이 문서에서는 기능 파이프라인에서 발견되는 다양한 클래스에 대해 설명하고 PySpark 및 Spark에서 모델 작성 SDK를 사용하여 사용자 정의 기능 파이프라인을 만드는 [단계별](./sdk.md) 자습서를 제공합니다.

이 자습서에서는 다음 단계를 다룹니다.
- [Feature Pipeline 클래스 구현](#implement-your-feature-pipeline-classes)
   - [구성 파일에서 변수 정의](#define-variables-in-the-configuration-json-file)
   - [DataLoader를 사용하여 입력 데이터 준비](#prepare-the-input-data-with-dataloader)
   - [DatasetTransformer를 사용하여 데이터 세트 변환](#transform-a-dataset-with-datasettransformer)
   - [Feature PipelineFactory를 사용하여 데이터 기능 엔지니어링](#engineer-data-features-with-featurepipelinefactory)
   - [DataSaver를 사용하여 기능 데이터 세트 저장](#store-your-feature-dataset-with-datasaver)
   - [응용 프로그램 파일에서 구현된 클래스 이름을 지정합니다](#specify-your-implemented-class-names-in-the-application-file)
- [이진 객체 작성](#build-the-binary-artifact)
- [API를 사용하여 피쳐 파이프라인 엔진 생성](#create-a-feature-pipeline-engine-using-the-api)

## 기능 파이프라인 클래스

다음 표에서는 기능 파이프라인을 빌드하기 위해 확장해야 하는 기본 개요 클래스에 대해 설명합니다.

| 개요 클래스 | 설명 |
| -------------- | ----------- |
| DataLoader | DataLoader 클래스는 입력 데이터 검색을 위한 구현을 제공합니다. |
| DatasetTransformer | DatasetTransformer 클래스는 입력 데이터 집합을 변형하는 구현을 제공합니다. DatasetTransformer 클래스를 제공하지 않고 FeaturePipelineFactory 클래스 내에서 기능 엔지니어링 로직을 구현하도록 선택할 수 있습니다. |
| FeaturePipelineFactory | FeaturePipelineFactory 클래스는 기능 엔지니어링을 수행하기 위해 일련의 Spark Transformers로 구성된 Spark Pipeline을 만듭니다. FeaturePipelineFactory 클래스를 제공하지 않고 DatasetTransformer 클래스 내에서 기능 엔지니어링 로직을 구현할 수 있습니다. |
| DataSaver | DataSaver 클래스는 기능 데이터 세트 저장을 위한 논리를 제공합니다. |

Feature Pipeline 작업이 시작되면 Runtime은 먼저 DataLoader를 실행하여 입력 데이터를 DataFrame으로 로드한 다음 DatasetTransformer 또는 FeaturePipelineFactory 또는 둘 다를 실행하여 DataFrame을 수정합니다. 마지막으로, 결과 기능 데이터 세트는 DataSaver를 통해 저장됩니다.

다음 순서도는 런타임의 실행 순서를 보여줍니다.

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Feature Pipeline 클래스 구현

다음 섹션에서는 기능 파이프라인에 대한 필수 클래스 구현에 대한 세부 사항과 예제를 제공합니다.

### 구성 JSON 파일에서 변수 정의

구성 JSON 파일은 키-값 쌍으로 구성되며 런타임 동안 나중에 정의할 변수를 지정할 수 있도록 고안되었습니다. 이러한 키-값 쌍은 입력 데이터 집합 위치, 출력 데이터 집합 ID, 테넌트 ID, 열 머리글 등과 같은 속성을 정의할 수 있습니다.

다음 예에서는 구성 파일 내에 있는 키-값 쌍을 보여 줍니다. 예제를 확장하여 자세한 내용을 봅니다.


**구성 JSON 예**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
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



매개 변수로 정의된 모든 클래스 메서드를 통해 구성 JSON에 액세스할 `configProperties` 수 있습니다. 예:

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### DataLoader를 사용하여 입력 데이터 준비

DataLoader는 입력 데이터의 검색 및 필터링을 담당합니다. DataLoader의 구현은 추상 클래스를 `DataLoader` 확장하고 추상 메서드를 재정의해야 합니다 `load`.

다음 예제에서는 ID로 플랫폼 데이터 세트를 검색하고 이를 DataFrame으로 반환합니다. 여기서 데이터 세트 ID(`datasetId`)는 구성 파일에서 정의된 속성입니다. 각 예제를 확장하여 세부 사항을 봅니다.


**PySpark 예**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Spark 예**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```



### DatasetTransformer를 사용하여 데이터 세트 변환

DatasetTransformer는 입력 DataFrame을 변형하기 위한 논리를 제공하고 새로운 파생된 DataFrame을 반환합니다. 이 클래스는 FeaturePipelineFactory와 함께 작업하거나, 단독 기능 엔지니어링 구성 요소로 작업하거나, 이 클래스를 구현하지 않도록 선택할 수 있습니다.

다음 예제에서는 DatasetTransformer 클래스를 확장합니다. 각 예제를 확장하여 세부 사항을 봅니다.


**PySpark 예**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Spark 예**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### Feature PipelineFactory를 사용하여 데이터 기능 엔지니어링

Feature PipelineFactory를 사용하면 Spark Pipeline을 통해 일련의 Spark Transformers를 정의 및 연결함으로써 기능 엔지니어링 로직을 구현할 수 있습니다. 이 클래스는 DatasetTransformer와 함께 작업하거나 단독 기능 엔지니어링 구성 요소로 작업하거나 이 클래스를 구현하지 않도록 선택할 수 있습니다.

다음 예제에서는 FeaturePipelieFactory 클래스를 확장하고 Spark Pipeline에서 여러 단계로 구성된 Spark Transformers를 구현합니다. 각 예제를 확장하여 세부 사항을 봅니다.


**PySpark 예**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Spark 예**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### DataSaver를 사용하여 기능 데이터 세트 저장

DataSaver는 결과 기능 데이터 세트를 스토리지 위치에 저장할 책임이 있습니다. DataSaver를 구현하려면 개요 클래스를 `DataSaver` 확장하고 추상 방법을 무시해야 합니다 `save`.

다음 예에서는 데이터를 ID로 플랫폼 데이터 세트에 저장하는 DataSaver 클래스를 확장합니다. 여기서 데이터 세트 ID(`featureDatasetId`) 및 테넌트 ID(`tenantId`)는 구성 파일에서 정의된 속성입니다. 각 예제를 확장하여 세부 사항을 봅니다.


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




**Spark 예**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### 응용 프로그램 파일에서 구현된 클래스 이름을 지정합니다

Feature Pipeline 클래스가 정의 및 구현되었으므로 애플리케이션 파일에서 클래스 이름을 지정해야 합니다.

다음 예제에서는 구현된 클래스 이름을 지정합니다. 예제를 확장하여 자세한 내용을 봅니다.


**PySpark 예**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Spark 예**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## 이진 객체 작성

이제 Feature Pipeline 클래스가 구현되었으므로 이를 작성하여 바이너리 객체에 컴파일한 다음 API 호출을 통해 Feature Pipeline을 생성하는 데 사용할 수 있습니다.

**PySpark**

PySpark Feature Pipeline을 만들려면 모델 작성 SDK의 `setup.py` 루트 디렉토리에 있는 Python 스크립트를 실행합니다.

>[!NOTE] PySpark 기능 파이프라인을 만들려면 Python 3을 컴퓨터에 설치해야 합니다.

```shell
python3 setup.py bdist_egg
```

피쳐 파이프라인을 성공적으로 작성하면 `.egg` `/dist` 디렉토리에 가공물이 생성되며, 이 가공물은 피쳐 파이프라인을 생성하는 데 사용됩니다.

**Spark**

Spark Feature Pipeline을 빌드하려면 모델 작성 SDK의 루트 디렉토리에서 다음 콘솔 명령을 실행하십시오.

>[!NOTE] Spark Feature Pipeline을 만들려면 시스템에 Scala 및 sbt가 설치되어 있어야 합니다.

```shell
mvn clean install
```

피쳐 파이프라인을 성공적으로 작성하면 `.jar` `/dist` 디렉토리에 가공물이 생성되며, 이 가공물은 피쳐 파이프라인을 생성하는 데 사용됩니다.

## API를 사용하여 피쳐 파이프라인 엔진 생성

이제 Feature Pipeline을 제작하여 바이너리 객체를 만들었으므로 Sensei Machine Learning API를 사용하여 Feature Pipeline Engine을 [만들 수 있습니다](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts). Feature Pipeline Engine을 성공적으로 생성하면 응답 본문의 일부로 엔진 ID가 제공되므로 다음 단계를 계속하기 전에 이 값을 저장해야 합니다.

## 다음 단계

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

이 문서를 읽음으로써 모델 작성 SDK를 사용하여 피쳐 파이프라인을 작성하고 이진 객체를 빌드한 다음 해당 객체를 사용하여 API 호출을 통해 Feature Pipeline Engine을 생성했습니다. 이제 새로 만든 엔진을 사용하여 [피쳐 파이프라인 모델을](../api/mlinstances.md#create-an-mlinstance) 만들고 데이터 세트 변형과 데이터 기능 축적을 시작할 수 있습니다.