---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: SDK 개발자 가이드
topic: Overview
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---


# SDK 개발자 가이드

모델 작성 SDK를 사용하면 PySpark 및 Spark에서 구현 가능한 템플릿을 제공하여 [!DNL Adobe Experience Platform] 데이터 과학 작업 공간에서 사용할 수 있는 맞춤형 머신 러닝 레서피 및 기능 파이프라인을 개발할 수 있습니다.

이 문서에서는 모델 작성 SDK 내에 있는 다양한 클래스에 대한 정보를 제공합니다.

## DataLoader {#dataloader}

DataLoader 클래스는 원시 입력 데이터의 검색, 필터링 및 반환과 관련된 모든 것을 캡슐화합니다. 입력 데이터의 예로는 트레이닝, 점수 지정 또는 기능 엔지니어링 등이 있습니다. 데이터 로더는 추상 클래스를 확장하고 추상 메서드 `DataLoader` 를 재정의해야 합니다 `load`.

**PySpark**

다음 표에서는 PySpark Data Loader 클래스의 개요 메서드를 설명합니다.

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
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>Pendans DataFrame으로 플랫폼 데이터 로드 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성 맵</li>
                    <li><code class=" language-undefined">spark</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

다음 표에서는 Spark Data Loader 클래스의 개요 메서드를 설명합니다.

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
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>플랫폼 데이터를 DataFrame으로 로드 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성 맵</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 플랫폼 데이터 세트에서 데이터 로드 {#load-data-from-a-platform-dataset}

다음 예제에서는 Platform 데이터를 ID로 검색하고 DataFrame을 반환합니다. 여기서 데이터 세트 ID(`datasetId`)는 구성 파일에서 정의된 속성입니다.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

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
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
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

## DataSaver {#datasaver}

DataSaver 클래스는 점수 지정 또는 기능 엔지니어링 등 출력 데이터를 저장하는 것과 관련된 모든 것을 캡슐화합니다. 데이터 보호자는 추상 클래스를 확장하고 추상 메서드 `DataSaver` 를 무시해야 합니다 `save`.

**PySpark**

다음 표에서는 PySpark 데이터 보호기 클래스의 개요 방법을 설명합니다.

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
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>출력 데이터를 DataFrame으로 수신하여 플랫폼 데이터 세트에 저장</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성 맵</li>
                    <li><code class=" language-undefined">dataframe</code>: DataFrame 형식으로 저장할 데이터</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

다음 표에서는 Spark Data Saver 클래스의 개요 방법을 설명합니다.

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
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>출력 데이터를 DataFrame으로 수신하여 플랫폼 데이터 세트에 저장</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성 맵</li>
                    <li><code class=" language-undefined">dataFrame</code>: DataFrame 형식으로 저장할 데이터</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 플랫폼 데이터 세트에 데이터 저장 {#save-data-to-a-platform-dataset}

플랫폼 데이터 세트에 데이터를 저장하려면 구성 파일에서 속성을 제공하거나 정의해야 합니다.

- 데이터를 저장할 유효한 플랫폼 데이터 집합 ID
- 조직에 속하는 테넌트 ID

다음 예제에서는 데이터 세트(`prediction`)를 플랫폼 데이터 세트에 저장합니다. 여기서 데이터 세트 ID(`datasetId`) 및 테넌트 ID(`tenantId`)는 구성 파일 내에서 정의된 속성입니다.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
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

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
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

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## 데이터 세트 변환기 {#datasettransformer}

DatasetTransformer 클래스는 데이터 집합의 구조를 수정 및 변환합니다. Sensei 기계 학습 런타임은 이 구성 요소를 정의할 필요가 없으며 사용자의 요구 사항에 따라 구현됩니다.

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
                <p><i>abstract</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>데이터 세트를 입력으로 가져와 새로운 파생 데이터 세트를 출력합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성 맵</li>
                    <li><code class=" language-undefined">dataset</code>: 변환용 입력 데이터 집합</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

다음 표에서는 Spark 데이터 세트 변환기 클래스의 추상적인 방법을 설명합니다.

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
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>데이터 세트를 입력으로 가져와 새로운 파생 데이터 세트를 출력합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성 맵</li>
                    <li><code class=" language-undefined">dataset</code>: 변환용 입력 데이터 집합</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

FeaturePipelineFactory 클래스에는 피쳐 추출 알고리즘이 포함되어 있으며 피쳐 파이프라인의 시작 단계부터 끝까지의 단계가 정의됩니다.

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
                <p><i>abstract</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>일련의 Spark Transformers가 포함된 Spark Pipeline을 만들어 다시 전송</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성 맵</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개 변수 맵 검색 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

다음 표에서는 Spark FeaturePipelineFactory의 클래스 메서드에 대해 설명합니다.

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
                <p><i>abstract</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>여러 개의 트랜스포머가 포함된 파이프라인 생성 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성 맵</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개 변수 맵 검색 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

PipelineFactory 클래스는 트레이닝 로직과 알고리즘이 Spark Pipeline 형식으로 정의되는 모델 트레이닝 및 점수에 대한 메서드 및 정의를 캡슐화합니다.

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
                <p><i>abstract</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>모델 트레이닝 및 점수에 대한 로직과 알고리즘이 포함된 스파크 파이프라인 만들기 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>모델을 교육할 로직과 알고리즘이 포함된 사용자 지정 파이프라인을 반환합니다. Spark Pipeline을 사용하는 경우 이 메서드는 필요하지 않습니다</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">dataframe</code>: 트레이닝 입력을 위한 기능 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>교육된 모델을 사용하여 점수를 매기고 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">dataframe</code>: 점수 지정을 위한 데이터 세트 입력</li>
                    <li><code class=" language-undefined">model</code>: 채점하는 데 사용되는 트레이닝된 모델</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개 변수 맵 검색 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

다음 표에서는 Spark PipelineFactory의 클래스 메서드에 대해 설명합니다.

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
                <p><i>abstract</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>모델 트레이닝 및 점수부여에 대한 로직과 알고리즘이 포함된 파이프라인 생성 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>구성 속성에서 매개 변수 맵 검색 및 반환</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark 세션</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

MLEvaluator 클래스는 평가 지표를 정의하고 교육 및 데이터 세트를 테스트하는 메서드를 제공합니다.

**PySpark**

다음 표에서는 PySpark MLEvaluator의 클래스 메서드를 설명합니다.

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
                <p><i>abstract</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>입력 데이터 세트를 교육 및 테스트 하위 세트로 분할</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">dataframe</code>: 분할할 입력 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>교육된 모델을 평가하고 평가 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: 자체 참조</li>
                    <li><code class=" language-undefined">dataframe</code>: 교육 및 테스트 데이터로 구성된 DataFrame</li>
                    <li><code class=" language-undefined">model</code>: 훈련된 모델</li>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

다음 표에서는 Spark MLEvaluator의 클래스 메서드를 설명합니다.

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
                <p><i>abstract</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>입력 데이터 세트를 교육 및 테스트 하위 세트로 분할</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">data</code>: 분할할 입력 데이터 세트</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>교육된 모델을 평가하고 평가 결과를 반환합니다.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: 구성 속성</li>
                    <li><code class=" language-undefined">model</code>: 훈련된 모델</li>
                    <li><code class=" language-undefined">data</code>: 교육 및 테스트 데이터로 구성된 DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>