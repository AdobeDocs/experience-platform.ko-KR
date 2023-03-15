---
keywords: Experience Platform;개발자 안내서;SDK;모델 작성;Data Science Workspace;인기 항목;테스트
solution: Experience Platform
title: 모델 작성 SDK
description: 모델 작성 SDK를 사용하면 Adobe Experience Platform Data Science Workspace에서 사용할 수 있는 사용자 정의 머신 러닝 레서피 및 기능 파이프라인을 개발하고 PySpark 및 Spark(Scala)에서 구현 가능한 템플릿을 제공할 수 있습니다.
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 1%

---

# 모델 작성 SDK

모델 작성 SDK를 사용하면 다음에서 사용할 수 있는 사용자 지정 머신 러닝 레서피 및 기능 파이프라인을 개발할 수 있습니다. [!DNL Adobe Experience Platform] 데이터 과학 작업 영역, 구현 가능한 템플릿 제공 [!DNL PySpark] 및 [!DNL Spark (Scala)].

이 문서에서는 모델 작성 SDK 내에 있는 다양한 클래스에 대한 정보를 제공합니다.

## DataLoader {#dataloader}

DataLoader 클래스는 원시 입력 데이터의 검색, 필터링 및 반환과 관련된 모든 항목을 캡슐화합니다. 입력 데이터의 예로는 교육, 채점 또는 기능 엔지니어링을 위한 데이터가 있습니다. 데이터 로더는 추상 클래스를 확장합니다. `DataLoader` 및 은(는) abstract 메서드를 재정의해야 합니다. `load`.

**PySparc**

다음 표에서는 PySpark 데이터 로더 클래스의 추상 메서드에 대해 설명합니다.

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
                <p>플랫폼 데이터를 Pandas DataFrame으로 로드하고 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성 맵</li>
                    <li><code>spark</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**스파크**

다음 표에서는 의 추상 메서드를 설명합니다. [!DNL Spark] 데이터 로더 클래스:

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
                    <li><code>configProperties</code>: 구성 속성 맵</li>
                    <li><code>sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 에서 데이터 로드 [!DNL Platform] 데이터 세트 {#load-data-from-a-platform-dataset}

다음 예제는 [!DNL Platform] ID별 데이터를 반환하고 데이터 세트 ID(`datasetId`)는 구성 파일에서 정의된 속성입니다.

**PySparc**

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

**스파크(Scala)**

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

DataSaver 클래스는 채점 또는 기능 엔지니어링의 데이터를 포함하여 출력 데이터 저장과 관련된 모든 항목을 캡슐화합니다. 데이터 저장자는 추상 클래스를 확장합니다. `DataSaver` 및 은(는) abstract 메서드를 재정의해야 합니다. `save`.

**PySparc**

다음 표에서는 의 추상 메서드를 설명합니다. [!DNL PySpark] Data Saver 클래스:

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
                <p>출력 데이터를 DataFrame으로 수신하여 Platform 데이터 세트에 저장합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성 맵</li>
                    <li><code>dataframe</code>: DataFrame 형태로 저장할 데이터</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**스파크(Scala)**

다음 표에서는 의 추상 메서드를 설명합니다. [!DNL Spark] Data Saver 클래스:

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
                <p>출력 데이터를 DataFrame으로 수신하여 Platform 데이터 세트에 저장합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: 구성 속성 맵</li>
                    <li><code>dataFrame</code>: DataFrame 형태로 저장할 데이터</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 에 데이터 저장 [!DNL Platform] 데이터 세트 {#save-data-to-a-platform-dataset}

에 데이터를 저장하려면 [!DNL Platform] 데이터 세트인 경우 구성 파일에 속성을 제공하거나 정의해야 합니다.

- 유효 [!DNL Platform] 데이터를 저장할 데이터 세트 ID
- 조직에 속한 테넌트 ID입니다

다음 예제에서는 데이터를 저장합니다(`prediction`)에 [!DNL Platform] 데이터 세트, 데이터 세트 ID(`datasetId`) 및 임차인 ID(`tenantId`)는 구성 파일 내에서 정의된 속성입니다.


**PySparc**

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

**스파크(Scala)**

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

## 데이터 집합 변환기 {#datasettransformer}

DatasetTransformer 클래스는 데이터 집합의 구조를 수정하고 변환합니다. 다음 [!DNL Sensei Machine Learning Runtime] 는 이 구성 요소를 정의할 필요가 없으며, 요구 사항에 따라 구현됩니다.

기능 파이프라인과 관련하여 데이터 세트 변환기를 기능 파이프라인 팩토리와 함께 사용하여 기능 엔지니어링을 위한 데이터를 준비할 수 있습니다.

**PySparc**

다음 표에서는 PySpark 데이터 세트 변환기 클래스의 클래스 메서드에 대해 설명합니다.

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
                <p><i>요약</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>데이터 세트를 입력으로 취하여 새로운 파생된 데이터 세트를 출력합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성 맵</li>
                    <li><code>dataset</code>: 변환을 위한 입력 데이터 세트</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**스파크(Scala)**

다음 표에서는 의 추상 메서드를 설명합니다. [!DNL Spark] 데이터 집합 변환기 클래스:

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
                <p>데이터 세트를 입력으로 취하여 새로운 파생된 데이터 세트를 출력합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: 구성 속성 맵</li>
                    <li><code>dataset</code>: 변환을 위한 입력 데이터 세트</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

FeaturePipelineFactory 클래스에는 기능 추출 알고리즘이 포함되어 있으며 처음부터 끝까지 기능 파이프라인의 단계를 정의합니다.

**PySparc**

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
                <p><i>요약</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>일련의 Spark 변환기가 포함된 Spark 파이프라인 생성 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성 맵</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>요약</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개변수 맵을 검색하고 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**스파크(Scala)**

다음 표에서는 [!DNL Spark] 기능 파이프라인 팩토리:

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
                <p><i>요약</i><br/><code>createPipeline(configProperties)</code></p>
                <p>일련의 변환기가 포함된 파이프라인 생성 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: 구성 속성 맵</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>요약</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개변수 맵을 검색하고 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

PipelineFactory 클래스는 모델 교육 및 점수에 대한 메서드와 정의를 캡슐화합니다. 여기서 교육 논리 및 알고리즘은 [!DNL Spark] 파이프라인.

**PySparc**

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
                <p><i>요약</i><br/><code>apply(self, configProperties)</code></p>
                <p>모델 교육 및 채점을 위한 논리 및 알고리즘이 포함된 Spark 파이프라인 생성 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>요약</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>모델을 교육하기 위한 논리 및 알고리즘이 포함된 사용자 지정 파이프라인을 반환합니다. Spark 파이프라인을 사용하는 경우에는 이 방법이 필요하지 않습니다</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>dataframe</code>: 교육 입력을 위한 기능 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>요약</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>훈련된 모델을 사용하여 점수를 매기고 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>dataframe</code>: 채점을 위한 입력 데이터 세트</li>
                    <li><code>model</code>: 채점에 사용되는 훈련된 모델</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>요약</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개변수 맵을 검색하고 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**스파크(Scala)**

다음 표에서는 [!DNL Spark] PipelineFactory:

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
                <p><i>요약</i><br/><code>apply(configProperties)</code></p>
                <p>모델 교육 및 채점에 대한 논리 및 알고리즘이 포함된 파이프라인 생성 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: 구성 속성</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>요약</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개변수 맵을 검색하고 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

MLEvaluator 클래스는 평가 지표를 정의하고 교육 및 테스트 데이터 세트를 결정하는 메서드를 제공합니다.

**PySparc**

다음 표에서는 PySpark MLEvaluator의 클래스 메서드에 대해 설명합니다.

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
                <p><i>요약</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>입력 데이터 세트를 교육 및 테스트 하위 집합으로 분할</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>dataframe</code>: 분할할 입력 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>요약</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>훈련된 모델을 평가하고 평가 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: 자체 참조</li>
                    <li><code>dataframe</code>: 교육 및 테스트 데이터로 구성된 DataFrame</li>
                    <li><code>model</code>: 훈련된 모델</li>
                    <li><code>configProperties</code>: 구성 속성</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**스파크(Scala)**

다음 표에서는 [!DNL Spark] MLEvaluator:

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
                <p><i>요약</i><br/><code>split(configProperties, data)</code></p>
                <p>입력 데이터 세트를 교육 및 테스트 하위 집합으로 분할</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>data</code>: 분할할 입력 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>요약</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>훈련된 모델을 평가하고 평가 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: 구성 속성</li>
                    <li><code>model</code>: 훈련된 모델</li>
                    <li><code>data</code>: 교육 및 테스트 데이터로 구성된 DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
