---
keywords: Experience Platform;개발자 가이드;SDK;모델 작성;데이터 과학 작업 공간;인기 있는 주제;테스트
solution: Experience Platform
title: 모델 작성 SDK
topic-legacy: Overview
description: 모델 제작 SDK를 사용하면 Adobe Experience Platform Data Science Workspace에서 사용할 수 있는 맞춤형 머신 러닝 레서피 및 기능 파이프라인을 개발할 수 있으며 PySpark 및 Spark(Scala)에서 구현 가능한 템플릿을 제공할 수 있습니다.
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 1%

---

# 모델 작성 SDK

모델 작성 SDK를 사용하면 [!DNL PySpark] 및 [!DNL Spark (Scala)]에서 구현 가능한 템플릿을 제공하여 [!DNL Adobe Experience Platform] 데이터 과학 작업 공간에서 사용할 수 있는 사용자 정의 기계 학습 레서피 및 기능 파이프라인을 개발할 수 있습니다.

이 문서에서는 모델 작성 SDK 내에 있는 다양한 클래스에 대한 정보를 제공합니다.

## DataLoader {#dataloader}

DataLoader 클래스는 원시 입력 데이터의 검색, 필터링 및 반환과 관련된 모든 내용을 캡슐화합니다. 입력 데이터의 예로는 트레이닝, 점수 지정 또는 기능 엔지니어링 등이 있습니다. 데이터 로더는 추상 클래스 `DataLoader`을(를) 확장하고 추상 메서드 `load`을(를) 재정의해야 합니다.

**PySpark**

다음 표에서는 PySpark Data Loader 클래스의 추상 메서드에 대해 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>Pendas DataFrame으로 플랫폼 데이터 로드 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성 맵</li>
                    <li><code>spark</code>:Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

다음 표에서는 [!DNL Spark] Data Loader 클래스의 추상 메서드에 대해 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>플랫폼 데이터를 DataFrame으로 로드 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성 맵</li>
                    <li><code>sparkSession</code>:Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### [!DNL Platform] 데이터 세트 {#load-data-from-a-platform-dataset}에서 데이터 로드

다음 예제에서는 ID로 [!DNL Platform] 데이터를 검색하고 DataFrame을 반환합니다. 여기서 데이터 세트 ID(`datasetId`)는 구성 파일에서 정의된 속성입니다.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

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

        # return as DataFrame
        return pd
```

**Spark(Scala)**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## 데이터 보호기 {#datasaver}

DataSaver 클래스는 점수 지정 또는 기능 엔지니어링 등 출력 데이터를 저장하는 것과 관련된 모든 것을 캡슐화합니다. 데이터 보호자는 추상 클래스 `DataSaver`을(를) 확장하고 추상 메서드 `save`을(를) 재정의해야 합니다.

**PySpark**

다음 표에서는 [!DNL PySpark] 데이터 세이버 클래스의 추상 메서드를 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>출력 데이터를 DataFrame으로 수신하여 플랫폼 데이터 세트에 저장</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성 맵</li>
                    <li><code>dataframe</code>:DataFrame 형식으로 저장할 데이터</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

다음 표에서는 [!DNL Spark] 데이터 세이버 클래스의 추상 메서드를 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>출력 데이터를 DataFrame으로 수신하여 플랫폼 데이터 세트에 저장</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성 맵</li>
                    <li><code>dataFrame</code>:DataFrame 형식으로 저장할 데이터</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 데이터를 [!DNL Platform] 데이터 세트 {#save-data-to-a-platform-dataset}에 저장

데이터를 [!DNL Platform] 데이터 세트에 저장하려면 구성 파일에서 속성을 제공하거나 정의해야 합니다.

- 데이터를 저장할 유효한 [!DNL Platform] 데이터 집합 ID
- 조직에 속하는 테넌트 ID

다음 예제에서는 데이터 세트 ID(`datasetId`) 및 테넌트 ID(`tenantId`)가 구성 파일 내에 정의된 속성인 [!DNL Platform] 데이터 세트에 데이터(`prediction`)를 저장합니다.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**Spark(Scala)**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## DatasetTransformer {#datasettransformer}

DatasetTransformer 클래스는 데이터 세트의 구조를 수정 및 변환합니다. [!DNL Sensei Machine Learning Runtime]은(는) 이 구성 요소를 정의할 필요가 없으며 사용자의 요구 사항에 따라 구현됩니다.

기능 파이프라인과 관련하여 데이터 세트 변환기는 기능 파이프라인 팩터리와 함께 사용하여 기능 엔지니어링 데이터를 준비할 수 있습니다.

**PySpark**

다음 표에서는 PySpark 데이터 세트 변환기 클래스의 클래스 메서드를 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>데이터 세트를 입력으로 가져와 새로운 파생 데이터 세트를 출력합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성 맵</li>
                    <li><code>dataset</code>:변환용 입력 데이터 집합</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

다음 표에서는 [!DNL Spark] 데이터 세트 변환기 클래스의 추상 메서드를 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>데이터 세트를 입력으로 가져와 새로운 파생 데이터 세트를 출력합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성 맵</li>
                    <li><code>dataset</code>:변환용 입력 데이터 집합</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

FeaturePipelineFactory 클래스에는 기능 추출 알고리즘이 포함되어 있으며 피쳐 파이프라인의 시작 단계부터 완료 단계까지 정의합니다.

**PySpark**

다음 표에서는 PySpark FeaturePipelineFactory의 클래스 메서드에 대해 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>일련의 Spark Transformers가 포함된 Spark Pipeline을 만들고 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성 맵</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개 변수 맵 검색 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>sparkSession</code>:Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

다음 표에서는 [!DNL Spark] FeaturePipelineFactory의 클래스 메서드에 대해 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>createPipeline(configProperties)</code></p>
                <p>여러 개의 트랜스포머가 포함된 파이프라인 생성 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성 맵</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개 변수 맵 검색 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>sparkSession</code>:Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

PipelineFactory 클래스는 트레이닝 로직과 알고리즘이 [!DNL Spark] 파이프라인 형태로 정의된 모델 트레이닝 및 점수에 대한 메서드 및 정의를 캡슐화합니다.

**PySpark**

다음 표에서는 PySpark PipelineFactory의 클래스 메서드에 대해 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(self, configProperties)</code></p>
                <p>모델 트레이닝 및 점수부여 논리 및 알고리즘이 포함된 스파크 파이프라인 만들기 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>모델을 교육할 로직과 알고리즘이 포함된 사용자 지정 파이프라인을 반환합니다. Spark Pipeline을 사용하는 경우 이 메서드는 필요하지 않습니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>dataframe</code>:트레이닝 입력을 위한 기능 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>트레이닝된 모델을 사용하여 점수를 매기고 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>dataframe</code>:채점을 위한 데이터 세트 입력</li>
                    <li><code>model</code>:채점하는 데 사용되는 트레이닝된 모델</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개 변수 맵 검색 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>sparkSession</code>:Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

다음 표에서는 [!DNL Spark] PipelineFactory의 클래스 메서드에 대해 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(configProperties)</code></p>
                <p>모델 트레이닝 및 점수부여에 대한 로직과 알고리즘이 포함된 파이프라인 만들기 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개 변수 맵 검색 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>sparkSession</code>:Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

MLEvaluator 클래스는 평가 지표를 정의하고 교육 및 데이터 세트를 테스트하는 메서드를 제공합니다.

**PySpark**

다음 표에서는 PySpark LEvaluator의 클래스 메서드를 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>입력 데이터 세트를 교육 및 테스트 하위 세트로 분할</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>dataframe</code>:분할할 입력 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>교육된 모델을 평가하고 평가 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:자체 참조</li>
                    <li><code>dataframe</code>:교육 및 테스트 데이터로 구성된 DataFrame</li>
                    <li><code>model</code>:훈련된 모델</li>
                    <li><code>configProperties</code>:구성 속성</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

다음 표에서는 [!DNL Spark] MLEvaluator의 클래스 메서드를 설명합니다.

<table>
    <thead>
        <tr>
            <th>방법 및 설명</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(configProperties, data)</code></p>
                <p>입력 데이터 세트를 교육 및 테스트 하위 세트로 분할</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>data</code>:분할할 입력 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>교육된 모델을 평가하고 평가 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:구성 속성</li>
                    <li><code>model</code>:훈련된 모델</li>
                    <li><code>data</code>:교육 및 테스트 데이터로 구성된 DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
