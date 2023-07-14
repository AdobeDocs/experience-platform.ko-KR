---
title: 데이터 세트 통계 계산
description: 이 문서에서는 SQL 명령을 사용하여 Azure ADLS(데이터 레이크 저장소) 데이터 세트에 대한 열 수준 통계를 계산하는 방법을 설명합니다.
source-git-commit: c7bc395038906e27449c82c518bd33ede05c5691
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# 데이터 세트 통계 계산

이제 의 열 수준 통계를 계산할 수 있습니다. [!DNL Azure Data Lake Storage] (ADLS) 데이터 세트 `COMPUTE STATISTICS` 및 `SHOW STATISTICS` 명령. 데이터 세트 통계를 계산하는 SQL 명령은 `ANALYZE TABLE` 명령입니다. 에 대한 전체 세부 정보 `ANALYZE TABLE` 명령은에서 찾을 수 있습니다. [SQL 참조 설명서](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>현재 생성된 통계는 해당 세션에만 유효하며 세션 간에는 지속되지 않습니다. 서로 다른 PSQL 세션에서 액세스할 수 없습니다.

포함 `SHOW STATISTICS FOR <alias_name>` 명령을 실행하면 다음을 사용하여 계산된 통계를 볼 수 있습니다. `ANALYZE TABLE COMPUTE STATISTICS` 명령입니다. 이제 이러한 명령의 조합을 통해 전체 데이터 세트, 데이터 세트의 하위 집합, 모든 열 또는 열의 하위 집합에 대한 열 통계를 계산할 수 있습니다.

>[!IMPORTANT]
>
>다음 `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, 및 `SHOW STATISTICS` 명령은 data warehouse 테이블에서 지원되지 않습니다. 에 대한 이러한 확장 `ANALYZE TABLE` 명령은 현재 ADLS 테이블에 대해서만 지원됩니다. 자세한 내용은 [테이블 분석 섹션](../sql/syntax.md#analyze-table) SQL 구문 안내서의

이 안내서는 ADLS 데이터 세트의 열 통계를 계산할 수 있도록 쿼리를 구조화하는 데 도움이 됩니다. 이 명령을 사용하면 SQL 쿼리를 사용하여 PSQL 클라이언트를 통해 세션에서 생성된 통계를 볼 수 있습니다.

## 통계 계산 {#compute-statistics}

추가 구문이 `ANALYZE TABLE` 다음을 수행할 수 있는 명령 **데이터 집합 하위 집합 및 특정 열에 대한 통계 계산**. 이렇게 하려면 다음을 사용해야 합니다 `ANALYZE TABLE <tableName> COMPUTE STATISTICS` 포맷.

>[!IMPORTANT]
>
>기본 동작은 다음에 대한 통계를 계산합니다. **전체 데이터 세트** 및 **모든 열**. 모든 열에 대한 통계를 계산하려면 쿼리 형식을 사용합니다 `ANALYZE TABLE COMPUTE STATISTICS`. 다음을 수행함: **아님** 데이터 세트의 크기가 매우 클 수 있으므로(잠재적으로 페타바이트급의 데이터) ADLS 데이터 세트에서 이 함수를 사용하는 것이 좋습니다. 대신 항상 를 사용하여 analyze 명령을 실행하는 것을 고려해야 합니다. `FILTERCONTEXT` 지정한 열 목록. 의 섹션을 참조하십시오. [분석된 열 제한](#limit-included-columns) 및 [필터 조건 추가](#filter-condition) 을 참조하십시오.

아래에 표시된 예에서는 다음에 대한 통계를 계산합니다. `adc_geometric` 데이터 세트 및 대상 **모두** 데이터 집합에 있는 열입니다.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` 는 배열 또는 맵 데이터 유형을 지원하지 않습니다. 다음을 설정할 수 있습니다. `skip_stats_for_complex_datatypes` 입력 데이터 프레임에 배열 및 맵 데이터 형식이 있는 열이 있는 경우 알림을 받거나 오류 발생에 대한 플래그. 기본적으로 플래그는 true로 설정됩니다. 알림 또는 오류를 활성화하려면 다음 명령을 사용합니다. `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

콘솔 출력은 분석 테이블 통계 계산 명령에 대한 응답으로 통계를 표시하지 않습니다. 대신 콘솔에는 의 단일 행 열이 표시됩니다 `Statistics ID` 결과를 참조할 수 있는 범용 고유 식별자. 다음을 선택할 수도 있습니다. **에서 바로 쿼리`Statistics ID`**. 을(를) 성공적으로 완료하면 `COMPUTE STATISTICS` 질의, 결과는 다음과 같이 표시됩니다.

```console
| Statistics ID    | 
| ---------------- |
| adc_geometric_stats_1 |
(1 row)
```

다음을 참조하여 통계 출력을 직접 쿼리할 수 있습니다. `Statistics ID` 아래에 표시된 대로:

```sql
SELECT * FROM adc_geometric_stats_1; 
```

이 문을 사용하면 와 함께 사용할 때 SHOW STATISTICS 명령과 유사한 방식으로 출력을 볼 수 있습니다. `Statistics ID`.

SHOW STATISTICS 명령을 실행하여 세션 내에서 계산된 모든 통계 목록을 볼 수 있습니다. SHOW STATISTICS 명령의 출력 예는 아래에 나와 있습니다.

```console
statsId | tableName | columnSet | filterContext | timestamp
-----------+---------------+-----------+---------------------------------------+---------------
adc_geometric_stats_1 |adc_geometric | (age) | | 25/06/2023 09:22:26
demo_table_stats_1 | demo_table | (*) | ((age > 25)) | 25/06/2023 12:50:26
```

<!-- Commented out until the <alias_name> feature is released.

To see the output, you must use the `SHOW STATISTICS` command. Instructions on [how to show the statistics](#show-statistics) are provided later in the document. 

-->

## 포함된 열 제한 {#limit-included-columns}

이름별로 참조하여 특정 데이터 세트 열에 대한 통계를 계산할 수 있습니다. 사용 `FOR COLUMNS (<col1>, <col2>)` 특정 열을 대상으로 하는 구문 아래 예제는 열에 대한 통계를 계산합니다  `commerce`, `id`, 및 `timestamp` 데이터 세트용 `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

루트 레벨 또는 중첩된 열에 대한 통계를 계산할 수 있습니다. 다음 예제에서는 이러한 참조를 보여 줍니다.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## 타임스탬프 필터 조건 추가 {#filter-condition}

타임스탬프 필터 조건을 추가하여 열의 분석에 집중할 수 있습니다. 이를 사용하여 이전 데이터를 필터링하거나 특정 기간에 데이터 분석을 집중시킬 수 있습니다. 다음 `FILTERCONTEXT` 명령은 제공한 필터 조건을 기반으로 데이터 집합 하위 집합에 대한 통계를 계산합니다.

아래 예에서 통계는 데이터 세트의 모든 열에 대해 계산됩니다 `tableName`: 열 타임스탬프에 지정된 범위 내의 값이 있는 경우 `2023-04-01 00:00:00` 및 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

열 제한과 필터를 결합하여 데이터 세트 열에 대한 특정 계산 쿼리를 만들 수 있습니다. 예를 들어 다음 쿼리는 열에 대한 통계를 계산합니다 `commerce`, `id`, 및 `timestamp` 데이터 세트용 `tableName`: 열 타임스탬프에 지정된 범위 내의 값이 있는 경우 `2023-04-01 00:00:00` 및 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

<!-- Commented out until the <alias_name> feature is released.
## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. 
-->

<!-- Commented out until the <alias_name> feature is released.

## Show the statistics {#show-statistics}

The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  

Even with a filter condition and a column list, the computation can target a large amount of data. Query Service generates a universally unique identifier for the statistics ID to store this calculated information. You can then use this statistics ID to look up the computed statistics with the `SHOW STATISTICS` command at any time within that session. 

The statistics ID and the statistics generated are only valid for this particular session and cannot be accessed across different PSQL sessions. The computed statistics are not currently persistent. To display the statistics, use the command seen below.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

An output might look similar to the example below. 

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(12 rows)
```

-->

## 다음 단계 {#next-steps}

이제 이 문서를 읽으면 SQL 쿼리를 사용하여 ADLS 데이터 집합에서 열 수준 통계를 생성하는 방법을 더 잘 이해할 수 있습니다. 다음을 읽는 것이 좋습니다. [SQl 구문 안내서](../sql/syntax.md) Adobe Experience Platform 쿼리 서비스의 추가 기능을 살펴보십시오.
