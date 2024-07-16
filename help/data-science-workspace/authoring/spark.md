---
keywords: Experience Platform;홈;인기 항목;데이터 액세스;spark sdk;데이터 액세스 api;spark 레서피;spark 읽기;spark 쓰기
solution: Experience Platform
title: Data Science Workspace에서 Spark를 사용하여 데이터 액세스
type: Tutorial
description: 다음 문서에는 데이터 과학 Workspace에서 사용하기 위해 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예가 포함되어 있습니다.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Data Science Workspace에서 Spark를 사용하여 데이터 액세스

다음 문서에는 데이터 과학 Workspace에서 사용하기 위해 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예가 포함되어 있습니다. JupyterLab Notebooks를 사용하여 데이터에 액세스하는 방법에 대한 자세한 내용은 [JupyterLab Notebooks 데이터 액세스](../jupyterlab/access-notebook-data.md) 설명서를 참조하십시오.

## 시작하기

[!DNL Spark]을(를) 사용하려면 `SparkSession`에 추가해야 하는 성능 최적화가 필요합니다. 또한 나중에 `configProperties`을(를) 설정하여 데이터 세트를 읽고 쓸 수도 있습니다.

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

Spark를 사용하는 동안 대화식 및 일괄 처리, 이렇게 두 가지 읽기 모드에 액세스할 수 있습니다.

대화형 모드에서는 [!DNL Query Service]에 대한 JDBC(Java Database Connectivity) 연결을 만들고 `DataFrame`(으)로 자동 변환되는 일반 JDBC `ResultSet`을(를) 통해 결과를 가져옵니다. 이 모드는 기본 제공 [!DNL Spark] 메서드 `spark.read.jdbc()`과(와) 유사하게 작동합니다. 이 모드는 작은 데이터 세트에만 적용됩니다. 데이터 세트가 5백만 행을 초과하는 경우 배치 모드로 전환하는 것이 좋습니다.

일괄 처리 모드에서는 [!DNL Query Service]의 COPY 명령을 사용하여 공유 위치에 Parquet 결과 집합을 생성합니다. 그런 다음 이러한 Parquet 파일을 추가로 처리할 수 있습니다.

대화형 모드로 데이터 세트를 읽는 예는 다음에서 볼 수 있습니다.

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

마찬가지로 배치 모드에서 데이터 세트를 읽는 예는 아래에서 볼 수 있습니다.

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

### 데이터 세트에서 열 선택

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT 절

DISTINCT 절을 사용하면 행/열 수준에서 모든 고유 값을 가져와 응답에서 모든 중복 값을 제거할 수 있습니다.

`distinct()` 함수를 사용하는 예는 아래에서 확인할 수 있습니다.

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE 절

[!DNL Spark] SDK에서는 SQL 식을 사용하거나 조건을 통해 필터링하는 두 가지 필터링 방법을 사용할 수 있습니다.

이러한 필터링 함수를 사용하는 예는 아래에서 확인할 수 있습니다.

#### SQL 표현식

```scala
df.where("age > 15")
```

#### 필터링 조건

```scala
df.where("age" > 15 || "name" = "Steve")
```

### 항목별 순서

ORDER BY 절을 사용하면 수신된 결과를 지정된 열을 기준으로 특정 순서(오름차순 또는 내림차순)로 정렬할 수 있습니다. [!DNL Spark] SDK에서 이 작업은 `sort()` 함수를 사용하여 수행됩니다.

`sort()` 함수를 사용하는 예는 아래에서 확인할 수 있습니다.

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT 절

LIMIT 절을 사용하면 데이터 집합에서 받는 레코드 수를 제한할 수 있습니다.

`limit()` 함수를 사용하는 예는 아래에서 확인할 수 있습니다.

```scala
df = df.limit(100)
```

## 데이터 세트에 쓰기

`configProperties` 매핑을 사용하여 `QSOption`을(를) 사용하여 Experience Platform의 데이터 세트에 쓸 수 있습니다.

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

Adobe Experience Platform Data Science Workspace은 위의 코드 샘플을 사용하여 데이터를 읽고 쓰는 Scala(Spark) 레시피 샘플을 제공합니다. 데이터에 액세스하는 데 Spark를 사용하는 방법에 대해 자세히 알아보려면 [Data Science Workspace Scala GitHub 저장소](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)를 검토하십시오.
