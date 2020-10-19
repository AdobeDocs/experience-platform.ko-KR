---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: Spark를 사용하여 데이터 액세스
topic: tutorial
type: Tutorial
description: 다음 문서에는 Data Science Workspace에서 사용할 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예제가 나와 있습니다.
translation-type: tm+mt
source-git-commit: e1035f3d1ad225a0892c5f97ca51618cd6b47412
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Spark를 사용하여 데이터 액세스

다음 문서에는 Data Science Workspace에서 사용할 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예제가 나와 있습니다. JupiterLab 전자 필기장을 사용하여 데이터에 액세스하는 방법에 대한 자세한 내용은 [JupiterLab 노트북 데이터 액세스](../jupyterlab/access-notebook-data.md) 설명서를 참조하십시오.

## 시작하기

을 [!DNL Spark] 사용하려면 성능 최적화가 필요합니다. 이 경우 성능 최적화가 `SparkSession`필요합니다. 또한 나중에 데이터 세트 `configProperties` 를 읽고 쓸 수 있도록 설정할 수도 있습니다.

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

Spark를 사용하면 두 가지 읽기 모드를 사용할 수 있습니다.인터랙티브한 컨텐츠와 일괄 처리

대화형 모드는 JDBC(Java Database Connectivity)에 대한 연결을 생성하고 자동으로 JDBC [!DNL Query Service] 로 변환되는 일반 JDBC `ResultSet` 를 통해 결과를 가져옵니다 `DataFrame`. 이 모드는 내장 [!DNL Spark] 메서드와 유사하게 작동합니다 `spark.read.jdbc()`. 이 모드는 작은 데이터 세트에 대해서만 사용됩니다. 데이터 세트에 5백만 행이 넘는 경우 일괄 처리 모드로 전환하는 것이 좋습니다.

일괄 처리 모드는 [!DNL Query Service]의 COPY 명령을 사용하여 공유 위치에서 쪽모이 세공 나무 결과 세트를 생성합니다. 이러한 Partiented 파일은 추가로 처리할 수 있습니다.

대화형 모드에서 데이터 세트를 읽는 예는 아래에 나와 있습니다.

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

마찬가지로, 일괄 처리 모드에서 데이터 세트를 읽는 예는 아래에 나와 있습니다.

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

DISTINCT 절을 사용하면 모든 고유한 값을 행/열 수준에서 가져와 응답에서 모든 중복 값을 제거할 수 있습니다.

함수 사용 예는 아래에 `distinct()` 나와 있습니다.

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE 절

SDK에서는 두 가지 필터링 방법을 사용할 수 있습니다. [!DNL Spark] SQL 표현식 사용 또는 조건을 필터링합니다.

다음은 이러한 필터링 기능을 사용하는 예입니다.

#### SQL 식

```scala
df.where("age > 15")
```

#### 필터링 조건

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY 절

ORDER BY 절을 사용하면 수신한 결과를 특정 순서(오름차순 또는 내림차순)의 지정된 열로 정렬할 수 있습니다. SDK에서 [!DNL Spark] 이 작업은 `sort()` 함수를 사용하여 수행됩니다.

함수 사용 예는 아래에 `sort()` 나와 있습니다.

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT 절

LIMIT 절을 사용하면 데이터 세트에서 수신한 레코드 수를 제한할 수 있습니다.

함수 사용 예는 아래에 `limit()` 나와 있습니다.

```scala
df = df.limit(100)
```

## 데이터 세트에 쓰기

매핑을 사용하여 Experience Platform의 데이터 세트에 쓸 수 `configProperties` 있습니다 `QSOption`.

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

Adobe Experience Platform 데이터 과학 작업 공간에서는 위 코드 샘플을 사용하여 데이터를 읽고 쓸 수 있는 Scala(Spark) 레서피 샘플을 제공합니다. Spark를 사용하여 데이터에 액세스하는 방법에 대한 자세한 내용은 [Data Science Workspace Scala GitHub 리포지토리를 참조하십시오](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).