---
keywords: Experience Platform;홈;인기 항목;데이터 액세스;spark sdk;데이터 액세스 api;스파크 레서피;스파크 읽기;스파크 쓰기
solution: Experience Platform
title: Data Science Workspace에서 스파크를 사용하여 데이터 액세스
type: Tutorial
description: 다음 문서에는 Data Science Workspace에서 사용할 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예가 나와 있습니다.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Data Science Workspace에서 스파크를 사용하여 데이터 액세스

다음 문서에는 Data Science Workspace에서 사용할 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예가 나와 있습니다. JupiterLab 노트북을 사용하여 데이터에 액세스하는 방법에 대한 자세한 내용은 [JupiterLab 노트북 데이터 액세스](../jupyterlab/access-notebook-data.md) 설명서.

## 시작하기

사용 [!DNL Spark] 을(를) 추가하려면 성능 최적화가 필요합니다. `SparkSession`. 또한 `configProperties` 나중에 데이터 세트에 읽고 쓸 수 있습니다.

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

## 데이터 집합 읽기

Spark를 사용하는 동안 다음 두 가지 읽기 모드에 액세스할 수 있습니다. 인터랙티브한 구성 및 배치

대화형 모드에서는 Java 데이터베이스 연결(JDBC) 연결을 생성합니다 [!DNL Query Service] 일반 JDBC를 통해 결과를 가져옵니다. `ResultSet` 자동으로 `DataFrame`. 이 모드는 기본 제공 모드에서 작동합니다 [!DNL Spark] 메서드 `spark.read.jdbc()`. 이 모드는 작은 데이터 세트에 대해서만 사용됩니다. 데이터 세트에 500만 개의 행이 넘는 경우 일괄 처리 모드로 전환하는 것이 좋습니다.

일괄 처리 모드에서 [!DNL Query Service]공유 위치에 Parquet 결과 세트를 생성하기 위한 &#39;s COPY 명령. 이러한 Parquet 파일을 추가로 처리할 수 있습니다.

대화형 모드에서 데이터 세트를 읽는 예는 다음과 같습니다.

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

마찬가지로 배치 모드에서 데이터 세트를 읽는 예는 다음과 같습니다.

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

DISTINCT 절을 사용하면 행/열 레벨에서 모든 고유 값을 가져와 응답에서 모든 중복 값을 제거할 수 있습니다.

사용 예 `distinct()` 함수는

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE 절

다음 [!DNL Spark] SDK에서는 두 가지 필터링 방법을 사용할 수 있습니다. SQL 표현식을 사용하거나 조건을 필터링하여 사용합니다.

이러한 필터링 함수를 사용하는 예는 다음과 같습니다.

#### SQL 식

```scala
df.where("age > 15")
```

#### 필터링 조건

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY 절

ORDER BY 절을 사용하면 수신한 결과를 특정 순서(오름차순 또는 내림차순)로 지정된 열로 정렬할 수 있습니다. 에서 [!DNL Spark] SDK, 이 작업은 `sort()` 함수 위에 있어야 합니다.

사용 예 `sort()` 함수는

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT 절

LIMIT 절을 사용하면 데이터 집합에서 받은 레코드 수를 제한할 수 있습니다.

사용 예 `limit()` 함수는

```scala
df = df.limit(100)
```

## 데이터 집합에 쓰기

사용 `configProperties` 매핑을 사용하여 Experience Platform의 데이터 집합에 쓸 수 있습니다 `QSOption`.

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

Adobe Experience Platform Data Science Workspace에서는 위의 코드 샘플을 사용하여 데이터를 읽고 쓰는 Scala(Spark) 레서피 샘플을 제공합니다. 데이터 액세스에 Spark를 사용하는 방법에 대해 자세히 알아보려면 [Data Science Workspace Scala GitHub 저장소](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
