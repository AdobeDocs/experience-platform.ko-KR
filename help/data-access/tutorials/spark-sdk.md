---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api
solution: Experience Platform
title: 안전한 Spark Data Access SDK
topic: tutorial
type: Tutorial
description: Secure Spark Data Access SDK는 Adobe Experience Platform에서 데이터 세트를 읽고 쓸 수 있는 소프트웨어 개발 키트입니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# 보안 [!DNL Spark Data Access] SDK

보안 [!DNL Spark][!DNL Data Access] SDK는 Adobe Experience Platform에서 데이터 세트를 읽고 쓸 수 있는 소프트웨어 개발 키트입니다.

## 시작하기

보안 [SDK를 호출하기 위해 값에 액세스하려면](../../tutorials/authentication.md) 인증 [!DNL Spark] 자습서를 [!DNL Data Access] 완료해야 합니다.

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. SDK를 [!DNL Spark] 사용하려면 작업이 수행할 샌드박스의 이름과 ID가 필요합니다.

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

## 환경 설정

SDK에서는 [!DNL Spark] 환경 변수 또는 데이터 소스 옵션에 자격 증명을 제공해야 합니다.

| 변수 | 값 |
| -------- | ----- | 
| `SERVICE_TOKEN` | 서비스 인증 토큰입니다. |
| `SERVICE_API_KEY` | 서비스 API 키. 일반적으로 IMS 클라이언트 ID와 동일합니다. |
| `ORG_ID` | ID `{IMS_ORG}` 값. |
| `USER_TOKEN` | 가치 `{ACCESS_TOKEN}` 를 |

기타 구성 매개 변수는 다음과 같습니다.

| 변수 | 값 |
| -------- | ----- |
| `ENVIRONMENT_NAME` | 연결하려는 환경입니다. &quot;dev&quot;, &quot;stage&quot; 또는 &quot;prod&quot; 중 하나일 수 있습니다. |
| `SANDBOX_NAME` | 연결할 샌드박스의 이름입니다. |

또는 아래 예에서 보듯이 위 `ENVIRONMENT_NAME`의 환경 변수 중 하나 `QSOption`를 아래 예에서 설정할 수 있습니다.

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## 설치

SDK를 [!DNL Spark] 사용하려면 성능 최적화가 필요합니다. 이 경우 SDK에 추가해야 합니다 `SparkSession`. 다음 방법 중 하나를 사용하여 적용할 수 있습니다.

현재 SparkSession에 바로 적용할 수 있습니다.

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

SparkSession 생성 전 또는 SparkSession 생성 시 다음 회의를 설정합니다.

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## 데이터 세트 읽기

SDK는 다음 두 가지 읽기 모드를 지원합니다. [!DNL Spark] 인터랙티브한 컨텐츠와 일괄 처리

대화형 모드는 JDBC(Java Database Connectivity)에 대한 연결을 생성하고 자동으로 JDBC [!DNL Query Service] 로 변환되는 일반 JDBC `ResultSet` 를 통해 결과를 가져옵니다 `DataFrame`. 이 모드는 내장 [!DNL Spark] 메서드와 유사하게 작동합니다 `spark.read.jdbc()`. 이 모드는 작은 데이터 집합에만 사용되며 인증에 사용자 토큰만 필요합니다.

일괄 처리 모드는 [!DNL Query Service]의 COPY 명령을 사용하여 공유 위치에서 쪽모이 세공 나무 결과 세트를 생성합니다. 이러한 Partiented 파일은 추가로 처리할 수 있습니다. 이 모드에서는 `acp.foundation.catalog.credentials` 범위를 가진 사용자 토큰과 서비스 토큰이 모두 필요합니다.

대화형 모드에서 데이터 세트를 읽는 예는 아래에 나와 있습니다.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

마찬가지로, 일괄 처리 모드에서 데이터 세트를 읽는 예는 아래에 나와 있습니다.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
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

SDK는 데이터 집합 작성을 지원합니다. [!DNL Spark] 사용자는 먼저 새 데이터 세트에 쓰기 위해 이전 데이터 세트를 검색해야 합니다.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
