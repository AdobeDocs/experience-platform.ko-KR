---
keywords: Experience Platform;홈;인기 항목;데이터 액세스;spark sdk;데이터 액세스 api;spark 레서피;읽기 spark;쓰기
solution: Experience Platform
title: 데이터 과학 작업 공간에서 Spark를 사용하여 데이터 액세스
topic-legacy: tutorial
type: Tutorial
description: 다음 문서에는 Data Science Workspace에서 사용할 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예가 나와 있습니다.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 데이터 과학 작업 공간에서 Spark를 사용하여 데이터 액세스

다음 문서에는 Data Science Workspace에서 사용할 Spark를 사용하여 데이터에 액세스하는 방법에 대한 예가 나와 있습니다. JupiterLab 전자 필기장을 사용하여 데이터에 액세스하는 방법에 대한 자세한 내용은 [JupiterLab 전자 필기장 데이터 액세스](../jupyterlab/access-notebook-data.md) 설명서를 참조하십시오.

## 시작하기

[!DNL Spark]을(를) 사용하려면 `SparkSession`에 추가해야 하는 성능 최적화가 필요합니다. 또한 데이터 세트를 읽고 쓰기 위해 나중에 `configProperties`을 설정할 수도 있습니다.

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

Spark를 사용하면 두 가지 읽기 모드를 사용할 수 있습니다.인터랙티브한 기능과 일괄 처리 기능을 제공합니다.

대화형 모드는 [!DNL Query Service]에 대한 JDBC(Java Database Connectivity) 연결을 만들고 자동으로 `DataFrame`로 변환되는 일반 JDBC `ResultSet`을 통해 결과를 가져옵니다. 이 모드는 내장 [!DNL Spark] 메서드 `spark.read.jdbc()`와 비슷하게 작동합니다. 이 모드는 작은 데이터 집합에만 사용됩니다. 데이터 세트에 5백만 행이 넘는 경우 일괄 처리 모드로 전환하는 것이 좋습니다.

일괄 처리 모드는 [!DNL Query Service]의 COPY 명령을 사용하여 공유 위치에 쪽모이 세공 항목 결과 집합을 생성합니다. 이러한 Portable 파일을 추가로 처리할 수 있습니다.

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

마찬가지로, 일괄 처리 모드에서 데이터 세트를 읽는 예도 아래에 나와 있습니다.

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

DISTINCT 절을 사용하면 모든 개별 값을 행/열 수준에서 가져와 응답에서 모든 중복 값을 제거할 수 있습니다.

`distinct()` 함수를 사용하는 예는 아래에 볼 수 있습니다.

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE 절

[!DNL Spark] SDK에서는 두 가지 필터링 방법을 사용할 수 있습니다.SQL 표현식 사용 또는 조건을 필터링하여

이러한 필터링 기능을 사용하는 예는 다음과 같습니다.

#### SQL 식

```scala
df.where("age > 15")
```

#### 필터링 조건

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY 절

ORDER BY 절을 사용하면 수신한 결과를 특정 순서(오름차순 또는 내림차순)의 지정된 열로 정렬할 수 있습니다. [!DNL Spark] SDK에서 이 작업은 `sort()` 함수를 사용하여 수행됩니다.

`sort()` 함수를 사용하는 예는 아래에 볼 수 있습니다.

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT 절

LIMIT 절을 사용하면 데이터 세트에서 수신한 레코드 수를 제한할 수 있습니다.

`limit()` 함수를 사용하는 예는 아래에 볼 수 있습니다.

```scala
df = df.limit(100)
```

## 데이터 세트에 쓰기

`configProperties` 매핑을 사용하면 `QSOption`을 사용하여 Experience Platform의 데이터 세트에 쓸 수 있습니다.

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

Adobe Experience Platform Data Science Workspace는 위의 코드 샘플을 사용하여 데이터를 읽고 작성하는 Scala(Spark) 레서피 샘플을 제공합니다. 데이터에 액세스하기 위해 Spark를 사용하는 방법에 대한 자세한 내용은 [Data Science Workspace Scala GitHub 리포지토리](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)을 참조하십시오.
