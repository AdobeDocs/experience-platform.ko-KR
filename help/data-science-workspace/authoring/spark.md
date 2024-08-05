---
keywords: Experience Platform; 집; 인기 있는 주제; 데이터 액세스; 스파크 SDK; 데이터 액세스 API; 스파크 레서피; 스파크 읽기; Spark 쓰기
solution: Experience Platform
title: 데이터 과학 작업 영역 에서 Spark를 사용하여 데이터 액세스
type: Tutorial
description: 다음 문서에는 데이터 과학 작업 영역 에서 사용하기 위해 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예가 포함되어 있습니다.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 데이터 과학 작업 영역 에서 Spark를 사용하여 데이터 액세스

>[!NOTE]
>
>Data Science 작업 영역은(는) 더 이상 구매할 수 없습니다.
>
>이 설명서는 데이터 과학 작업 영역 이전에 사용 권한이 있는 기존 고객을 대상으로 합니다.

다음 문서에는 데이터 과학 작업 영역 에서 사용하기 위해 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예가 포함되어 있습니다. JupiterLab 노트북을 사용한 데이터 액세스에 대한 자세한 내용은 JupiterLab 노트북 데이터 액세스](../jupyterlab/access-notebook-data.md) 설명서를 방문 참조하십시오[.

## 시작하기

를 사용하려면 [!DNL Spark] .`SparkSession` 또한 나중에 데이터 세트를 읽고 쓸 수 있도록 설정할 `configProperties` 수도 있습니다.

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## 데이터 세트 읽기

Spark를 사용하는 동안 대화식 및 일괄 처리의 두 가지 읽기 모드에 액세스할 수 있습니다.

인터랙티브한 모드는 에 대한 [!DNL Query Service] `ResultSet` JDBC(Java Database Connectivity) 연결을 생성하고 자동으로 `DataFrame`. 이 모드는 내장 [!DNL Spark] 방법 `spark.read.jdbc()`과 유사하게 작동합니다. 이 모드는 작은 데이터 세트에만 사용할 수 있습니다. 데이터 세트 행이 5백만 개를 초과하는 경우 배치 모드로 전환하는 것이 좋습니다.

일괄 처리 모드는 의 COPY 명령을 사용하여 [!DNL Query Service]공유 위치에 Parquet 결과 집합을 생성합니다. 그런 다음 이러한 Parquet 파일을 추가로 처리할 수 있습니다.

대화형 모드에서 데이터 세트 읽기의 예는 다음과 같습니다.

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

마찬가지로 배치 모드에서 데이터 세트 읽기의 예는 아래에서 볼 수 있습니다.

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### 데이터 세트 SELECT 열

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT 절

DISTINCT 절을 사용하면 행/열 수준에서 모든 고유 값을 가져와서 응답에서 모든 중복 값을 제거할 수 있습니다.

함수 사용 `distinct()` 의 예는 다음과 같습니다.

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE 절

SDK에서는 [!DNL Spark] SQL 표현식을 사용하거나 조건을 필터링하는 두 가지 필터링 방법을 사용할 수 있습니다.

이러한 필터링 기능을 사용하는 예는 다음과 같습니다.

#### SQL 표현식

```scala
df.where("age > 15")
```

#### 조건 필터링

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY 절

ORDER BY 절을 사용하면 수신된 결과를 지정된 열을 기준으로 특정 순서(오름차순 또는 내림차순)로 정렬할 수 있습니다. [!DNL Spark] SDK에서 이 작업은 함수를 사용하여 `sort()` 수행됩니다.

함수 사용 `sort()` 의 예는 다음과 같습니다.

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT 절

LIMIT 절을 사용하면 데이터 세트 에서 받은 레코드 수를 제한할 수 있습니다.

함수 사용 `limit()` 의 예는 다음과 같습니다.

```scala
df = df.limit(100)
```

## 데이터 세트 쓰기

매핑을 `configProperties` 사용하면 를 사용하여 `QSOption`Experience Platform 의 데이터 세트 에 쓸 수 있습니다.

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## 다음 단계

Adobe Experience Platform Data Science 작업 영역는 위의 코드 샘플을 사용하여 데이터를 읽고 쓰는 Scala(Spark) 레서피 샘플을 제공합니다. Spark를 사용하여 데이터에 액세스하는 방법에 대해 자세히 알아보려면 Data Science 작업 영역 Scala GitHub 리포지토리](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)를 [검토하세요.
