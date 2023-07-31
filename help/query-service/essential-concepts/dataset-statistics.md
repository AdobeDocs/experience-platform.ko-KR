---
title: 데이터 세트 통계 계산
description: 이 문서에서는 SQL 명령을 사용하여 Azure ADLS(데이터 레이크 저장소) 데이터 세트에 대한 열 수준 통계를 계산하는 방법을 설명합니다.
source-git-commit: 02b0939ee8fe92580402a78c7ebb5a250902d01c
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# 데이터 세트 통계 계산

이제 의 열 수준 통계를 계산할 수 있습니다. [!DNL Azure Data Lake Storage] (ADLS) 데이터 세트 `COMPUTE STATISTICS` 및 `SHOW STATISTICS` 명령. 데이터 세트 통계를 계산하는 SQL 명령은 `ANALYZE TABLE` 명령입니다. 에 대한 전체 세부 정보 `ANALYZE TABLE` 명령은에서 찾을 수 있습니다. [SQL 참조 설명서](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>계산된 통계는 세션 수준 지속성이 있는 임시 테이블에 저장됩니다. 해당 세션 중에 언제든지 계산 결과에 액세스할 수 있습니다. 서로 다른 PSQL 세션에서 액세스할 수 없습니다.

를 사용하여 계산된 통계를 보려면 `ANALYZE TABLE COMPUTE STATISTICS` 명령에서 별칭 이름 또는 통계 ID에 대해 SELECT 쿼리를 사용할 수 있습니다. 전체 데이터 세트, 데이터 세트의 하위 집합, 모든 열 또는 열의 하위 집합으로 통계 분석의 범위를 제한할 수도 있습니다.

>[!IMPORTANT]
>
>다음 `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, 및 `SHOW STATISTICS` 명령은 data warehouse 테이블에서 지원되지 않습니다. 에 대한 이러한 확장 `ANALYZE TABLE` 명령은 현재 ADLS 테이블에 대해서만 지원됩니다. 자세한 내용은 [테이블 분석 섹션](../sql/syntax.md#analyze-table) SQL 구문 안내서의

이 안내서는 ADLS 데이터 세트의 열 통계를 계산할 수 있도록 쿼리를 구조화하는 데 도움이 됩니다. 이 명령을 사용하면 SQL 쿼리를 사용하여 PSQL 클라이언트를 통해 세션에서 생성된 통계를 볼 수 있습니다.

## 통계 계산 {#compute-statistics}

추가 구문이 `ANALYZE TABLE` 다음 작업을 수행할 수 있는 명령 **데이터 집합 하위 집합 및 특정 열에 대한 통계 계산**. 데이터 세트 통계를 계산하려면 다음을 사용해야 합니다 `ANALYZE TABLE <tableName> COMPUTE STATISTICS` 포맷.

>[!IMPORTANT]
>
>기본 동작은 다음에 대한 통계를 계산합니다. **전체 데이터 세트** 및 **모든 열**. 모든 열에 대한 통계를 계산하려면 쿼리 형식을 사용합니다 `ANALYZE TABLE COMPUTE STATISTICS`. 다음을 수행함: **아님** 사용 권장 `COMPUTE STATISTICS` 데이터 세트 크기가 매우 클 수 있으므로(잠재적으로 페타바이트급의 데이터) ADLS 데이터 세트에 필터를 사용하지 않는 명령입니다. 대신 항상 를 사용하여 analyze 명령을 실행하는 것을 고려해야 합니다. `FILTERCONTEXT` 지정한 열 목록. 의 섹션을 참조하십시오. [분석된 열 제한](#limit-included-columns) 및 [필터 조건 추가](#filter-condition) 을 참조하십시오.

아래에 표시된 예에서는 다음에 대한 통계를 계산합니다. `adc_geometric` 데이터 세트 및 대상 **모두** 데이터 집합에 있는 열입니다.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>다음 `COMPUTE STATISTICS` 명령은 배열 또는 맵 데이터 형식을 지원하지 않습니다. 다음을 설정할 수 있습니다. `skip_stats_for_complex_datatypes` 입력 데이터 프레임에 배열 및 맵 데이터 형식이 있는 열이 있는 경우 알림을 받거나 오류 발생에 대한 플래그입니다. 기본적으로 플래그는 true로 설정됩니다. 알림 또는 오류를 활성화하려면 다음 명령을 사용합니다. `SET skip_stats_for_complex_datatypes = false`.

## 별칭 이름 만들기 {#alias-name}

계산 결과는 많은 양의 데이터일 수 있으므로 콘솔 출력에서 직접 계산된 데이터를 반환하기에는 무리가 있습니다. 별칭 이름은 선택 사항이지만 통계를 계산할 때 모범 사례로 사용하는 것이 좋습니다. SQL 쿼리의 결과를 설명적으로 참조하려면 문에 별칭 이름을 입력합니다. 또는 자동으로 생성된 `Statistics ID` 가 생성되고 계산된 정보를 저장하는 데 사용됩니다.

아래 예제는 출력 계산된 통계를 `alias_name` 나중에 참조할 수 있도록 쿼리에 사용된 별칭 이름은 `ANALYZE TABLE` 명령이 실행되었습니다.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

위의 예제에 대한 출력은 다음과 같습니다. `SUCCESSFULLY COMPLETED, alias_name`. 콘솔 출력은 분석 테이블 통계 계산 명령에 대한 응답에 통계를 표시하지 않습니다. 자세한 결과를 보려면 별칭 이름 또는 통계 ID에 대해 SELECT 쿼리를 사용해야 합니다.

## 계산된 통계의 출력 보기 {#view-output-of-computed-statistics}

미리 별칭 이름을 제공하지 않으면 Query Service에서 자동으로 `Statistics ID` 형식을 따르는 `<tableName_stats_{incremental_number}>`. 별칭 이름을 지정하면 `Statistics ID` 열.

의 출력 예 `COMPUTE STATISTICS` 쿼리는 다음과 같습니다.

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

그런 다음 **계산된 통계를 직접 쿼리** 를 참조하여 `Statistics ID`. 아래의 예제 문을 사용하여 와 함께 사용할 경우 출력을 전체적으로 볼 수 있습니다. `Statistics ID` 또는 별칭 이름입니다.

```sql
SELECT * FROM adc_geometric_stats_1; 
```

계산된 통계 출력은 아래 예와 비슷할 수 있습니다.

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
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

## 통계 분석 메타데이터 표시 {#show-statistics}

다음을 사용할 수 있습니다. `SHOW STATISTICS` 세션에서 생성된 모든 임시 통계 테이블의 메타데이터를 표시하는 명령입니다. 이 명령은 통계 분석의 범위를 구체화하는 데 도움이 될 수 있습니다.

의 출력 예 `SHOW STATISTICS` 아래에 이 표시됩니다.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

메타데이터 열 이름에 대한 설명은 아래에 나와 있습니다.

| 열 이름 | 설명 |
|---|---|
| `statsId` | 이 ID는에서 생성한 임시 통계 테이블을 참조합니다. `COMPUTE STATISTICS` 명령입니다. |
| `tableName` | 분석에 사용된 원래 테이블. |
| `columnSet` | 분석을 위해 특별히 선택한 열 목록. 빈 값은 모든 열이 분석되었음을 나타냅니다. 의 섹션을 참조하십시오. [열 제한](#limit-included-columns) 추가 정보. |
| `filterContext` | 분석에 적용된 필터 목록. |
| `timestamp` | 특정 기간에 초점을 맞추기 위해 데이터 분석에 적용되는 모든 시간 순 필터. 다음을 참조하십시오. [타임스탬프 필터 조건 섹션](#filter-condition) 을 참조하십시오. |

통계 ID 또는 별칭 이름을 사용하여 해당 세션 내에서 언제든지 SELECT 문을 사용하여 계산된 통계를 조회할 수 있습니다. 통계 ID 및 생성된 통계는 이 특정 세션에만 유효하며 다른 PSQL 세션에서 액세스할 수 없습니다. 계산된 통계는 현재 지속되지 않습니다. 방법에 대한 섹션 참조 [계산된 통계의 출력 보기](#view-output-of-computed-statistics) 을 참조하십시오.

## 포함된 열 제한 {#limit-included-columns}

분석에 초점을 맞추기 위해 이름별로 특정 데이터 세트 열을 참조하여 특정 데이터 세트 열에 대한 통계를 계산할 수 있습니다. 사용 `FOR COLUMNS (<col1>, <col2>)` 특정 열을 대상으로 하는 구문 아래 예제는 열에 대한 통계를 계산합니다  `commerce`, `id`, 및 `timestamp` 데이터 세트용 `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

루트 레벨 또는 중첩된 열에 대한 통계를 계산할 수 있습니다. 다음 예제에서는 이러한 참조를 보여 줍니다.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## 타임스탬프 필터 조건 추가 {#filter-condition}

연대기를 기반으로 열을 중점적으로 분석하기 위해 타임스탬프 필터 조건을 추가할 수 있습니다. 이 조건은 이전 데이터를 필터링하거나 특정 기간에 데이터 분석을 집중하는 데 사용할 수 있습니다. 다음 `FILTERCONTEXT` 명령은 제공한 필터 조건을 기반으로 데이터 집합 하위 집합에 대한 통계를 계산합니다.

아래 예에서 통계는 데이터 세트의 모든 열에 대해 계산됩니다 `tableName`: 열 타임스탬프에 지정된 범위 내의 값이 있는 경우 `2023-04-01 00:00:00` 및 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

열 제한과 필터를 결합하여 데이터 세트 열에 대한 특정 계산 쿼리를 만들 수 있습니다. 예를 들어 다음 쿼리는 열에 대한 통계를 계산합니다 `commerce`, `id`, 및 `timestamp` 데이터 세트용 `tableName`: 열 타임스탬프에 지정된 범위 내의 값이 있는 경우 `2023-04-01 00:00:00` 및 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## 다음 단계 {#next-steps}

이제 이 문서를 읽으면 SQL 쿼리를 사용하여 ADLS 데이터 집합에서 열 수준 통계를 생성하는 방법을 더 잘 이해할 수 있습니다. 다음을 읽는 것이 좋습니다. [SQl 구문 안내서](../sql/syntax.md) Adobe Experience Platform 쿼리 서비스의 추가 기능을 살펴보십시오.
