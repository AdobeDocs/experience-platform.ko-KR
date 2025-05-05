---
title: 데이터 세트 통계 계산
description: 이 문서에서는 SQL 명령을 사용하여 Azure ADLS(데이터 레이크 저장소) 데이터 세트에 대한 열 수준 통계를 계산하는 방법을 설명합니다.
exl-id: 66f11cd4-b115-40b8-ba8a-c4bb3606bbbf
source-git-commit: 37aeff5131b9f67dbc99f6199918403e699478c8
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# 데이터 세트 통계 계산

이제 `COMPUTE STATISTICS` SQL 명령을 사용하여 [!DNL Azure Data Lake Storage] (ADLS) 데이터 세트에 대한 열 수준 통계를 계산할 수 있습니다. 데이터 집합 통계를 계산하는 SQL 명령은 `ANALYZE TABLE` 명령의 확장입니다. `ANALYZE TABLE` 명령에 대한 전체 세부 정보는 [SQL 참조 설명서](../sql/syntax.md#analyze-table)에서 찾을 수 있습니다.

>[!NOTE]
>
>계산된 통계는 세션 수준 지속성이 있는 임시 테이블에 저장됩니다. 해당 세션 중에 언제든지 계산 결과에 액세스할 수 있습니다. 서로 다른 PSQL 세션에서 액세스할 수 없습니다.

`ANALYZE TABLE COMPUTE STATISTICS` 명령으로 계산된 통계를 보려면 별칭 이름 또는 통계 ID에 SELECT 쿼리를 사용할 수 있습니다. 전체 데이터 세트, 데이터 세트의 하위 집합, 모든 열 또는 열의 하위 집합으로 통계 분석의 범위를 제한할 수도 있습니다.

>[!IMPORTANT]
>
>`COMPUTE STATISTICS`, `FILTERCONTEXT` 및 `FOR COLUMNS` 명령은 가속화된 저장소 테이블에서 지원되지 않습니다. `ANALYZE TABLE` 명령에 대한 이러한 확장은 현재 ADLS 테이블에서만 지원됩니다. 자세한 내용은 SQL 구문 안내서의 [테이블 분석 섹션](../sql/syntax.md#analyze-table)을 참조하십시오.

이 안내서는 ADLS 데이터 세트의 열 통계를 계산할 수 있도록 쿼리를 구조화하는 데 도움이 됩니다. 이 명령을 사용하면 SQL 쿼리를 사용하여 PSQL 클라이언트를 통해 세션에서 생성된 통계를 볼 수 있습니다.

## 통계 계산 {#compute-statistics}

`ANALYZE TABLE` 명령에 추가 구문이 추가되어 데이터 집합 하위 집합 및 특정 열에 대한 통계를 **계산할 수 있습니다**. 데이터 집합 통계를 계산하려면 `ANALYZE TABLE <tableName> COMPUTE STATISTICS` 형식을 사용해야 합니다.

>[!IMPORTANT]
>
>기본 동작은 **전체 데이터 세트** 및 **모든 열**&#x200B;에 대한 통계를 계산합니다. 모든 열에 대한 통계를 계산하려면 쿼리 형식 `ANALYZE TABLE COMPUTE STATISTICS`을(를) 사용합니다. ADLS 데이터 집합의 크기가 매우 클 수 있으므로(잠재적으로 페타바이트급 데이터) ADLS 데이터 집합에 필터 없이 `COMPUTE STATISTICS` 명령을 사용하는 것이 **권장되지**&#x200B;않습니다. 대신 항상 `FILTERCONTEXT`과(와) 지정한 열 목록을 사용하여 analyze 명령을 실행해야 합니다. 자세한 내용은 [분석된 열 제한](#limit-included-columns) 및 [필터 조건 추가](#filter-condition)에 대한 섹션을 참조하십시오.

아래에 표시된 예제에서는 `adc_geometric` 데이터 집합 및 데이터 집합의 **all** 열에 대한 통계를 계산합니다.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` 명령은 배열 또는 맵 데이터 형식을 지원하지 않습니다. 입력 데이터 프레임에 배열 및 맵 데이터 형식의 열이 있는 경우 알림을 받거나 오류를 발생하도록 `skip_stats_for_complex_datatypes` 플래그를 설정할 수 있습니다. 기본적으로 플래그는 true로 설정됩니다. 알림 또는 오류를 사용하려면 다음 명령을 사용하십시오. `SET skip_stats_for_complex_datatypes = false`.

## 별칭 이름 만들기 {#alias-name}

계산 결과는 많은 양의 데이터일 수 있으므로 콘솔 출력에서 직접 계산된 데이터를 반환하기에는 무리가 있습니다. 별칭 이름은 선택 사항이지만 통계를 계산할 때 모범 사례로 사용하는 것이 좋습니다. SQL 쿼리의 결과를 설명적으로 참조하려면 문에 별칭 이름을 입력합니다. 또는 자동으로 생성된 `Statistics ID`을(를) 생성하여 계산된 정보를 저장하는 데 사용합니다.

아래 예제에서는 나중에 참조할 수 있도록 출력 계산 통계를 `alias_name`에 저장합니다. 쿼리에 사용된 별칭 이름은 `ANALYZE TABLE` 명령을 실행하는 즉시 참조할 수 있습니다.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

위의 예제에 대한 출력은 `SUCCESSFULLY COMPLETED, alias_name`입니다. 콘솔 출력은 분석 테이블 통계 계산 명령에 대한 응답에 통계를 표시하지 않습니다. 자세한 결과를 보려면 별칭 이름 또는 통계 ID에 대해 SELECT 쿼리를 사용해야 합니다.

## 계산된 통계의 출력 보기 {#view-output-of-computed-statistics}

미리 별칭 이름을 제공하지 않으면 쿼리 서비스에서 `<tableName_stats_{incremental_number}>`의 형식을 따르는 `Statistics ID`에 대한 이름을 자동으로 생성합니다. 별칭 이름을 지정하면 `Statistics ID` 열에 나타납니다.

`COMPUTE STATISTICS` 쿼리의 출력 예는 다음과 같습니다.

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

그런 다음 `Statistics ID`을(를) 참조하여 **계산된 통계를 직접 쿼리**&#x200B;할 수 있습니다. 아래 예제 문을 사용하면 `Statistics ID` 또는 별칭 이름과 함께 사용할 때 출력을 모두 볼 수 있습니다.

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

`SHOW STATISTICS` 명령을 사용하여 세션에서 생성된 모든 임시 통계에 대한 메타데이터를 표시할 수 있습니다. 이 명령은 통계 분석의 범위를 구체화하는 데 도움이 될 수 있습니다.

`SHOW STATISTICS`의 출력 예는 아래에 나와 있습니다.

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
| `statsId` | 이 ID는 `COMPUTE STATISTICS` 명령으로 생성된 임시 통계 테이블을 참조합니다. |
| `tableName` | 분석에 사용된 원래 테이블. |
| `columnSet` | 분석을 위해 특별히 선택한 열 목록. 빈 값은 모든 열이 분석되었음을 나타냅니다. 자세한 내용은 [열 제한](#limit-included-columns)에 대한 섹션을 참조하십시오. |
| `filterContext` | 분석에 적용된 필터 목록. |
| `timestamp` | 특정 기간에 초점을 맞추기 위해 데이터 분석에 적용되는 모든 시간 순 필터. 자세한 내용은 [타임스탬프 필터 조건 섹션](#filter-condition)을 참조하십시오. |

통계 ID 또는 별칭 이름을 사용하여 해당 세션 내에서 언제든지 SELECT 문을 사용하여 계산된 통계를 조회할 수 있습니다. 통계 ID 및 생성된 통계는 이 특정 세션에만 유효하며 다른 PSQL 세션에서 액세스할 수 없습니다. 계산된 통계는 현재 지속되지 않습니다. 자세한 내용은 [계산된 통계의 출력을 보는 방법](#view-output-of-computed-statistics)에 대한 섹션을 참조하십시오.

## 포함된 열 제한 {#limit-included-columns}

분석에 초점을 맞추기 위해 이름별로 특정 데이터 세트 열을 참조하여 특정 데이터 세트 열에 대한 통계를 계산할 수 있습니다. 특정 열을 대상으로 지정하려면 `FOR COLUMNS (<col1>, <col2>)` 구문을 사용하십시오. 아래 예제에서는 데이터 세트 `tableName`에 대한 열 `commerce`, `id` 및 `timestamp`에 대한 통계를 계산합니다.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

루트 레벨 또는 중첩된 열에 대한 통계를 계산할 수 있습니다. 다음 예제에서는 이러한 참조를 보여 줍니다.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## 타임스탬프 필터 조건 추가 {#filter-condition}

연대기를 기반으로 열을 중점적으로 분석하기 위해 타임스탬프 필터 조건을 추가할 수 있습니다. 이 조건은 이전 데이터를 필터링하거나 특정 기간에 데이터 분석을 집중하는 데 사용할 수 있습니다. `FILTERCONTEXT` 명령은 제공한 필터 조건을 기반으로 데이터 집합 하위 집합에 대한 통계를 계산합니다.

아래 예에서 통계는 데이터 집합 `tableName`의 모든 열에 대해 계산되며, 열 타임스탬프에는 지정된 범위 `2023-04-01 00:00:00`과(와) `2023-04-05 00:00:00` 사이의 값이 있습니다.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

열 제한과 필터를 결합하여 데이터 세트 열에 대한 특정 계산 쿼리를 만들 수 있습니다. 예를 들어 다음 쿼리는 데이터 집합 `tableName`의 열 `commerce`, `id` 및 `timestamp`에 대한 통계를 계산합니다. 여기서 열 타임스탬프에는 지정된 범위 `2023-04-01 00:00:00`과(와) `2023-04-05 00:00:00` 사이의 값이 있습니다.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## 다음 단계 {#next-steps}

이제 이 문서를 읽으면 SQL 쿼리를 사용하여 ADLS 데이터 집합에서 열 수준 통계를 생성하는 방법을 더 잘 이해할 수 있습니다. Adobe Experience Platform 쿼리 서비스의 더 많은 기능을 검색하려면 [SQl 구문 안내서](../sql/syntax.md)를 읽는 것이 좋습니다.
