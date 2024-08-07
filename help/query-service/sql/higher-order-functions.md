---
title: 고차 함수로 배열 관리 및 데이터 유형 매핑
description: Query Service에서 배열을 관리하고 데이터 형식을 고차 함수로 매핑하는 방법에 대해 알아봅니다. 예제는 일반적인 사용 사례와 함께 제공됩니다.
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: d2bc580ba1cacdfab45bdc6356c630a63e7d0f6e
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# 고차 함수로 배열 관리 및 데이터 유형 매핑

이 안내서를 사용하여 상위 함수가 배열 및 맵과 같은 복잡한 데이터 형식을 처리하는 방법에 대해 알아보십시오. 이러한 함수를 사용하면 배열을 분해하고 함수를 수행한 다음 결과를 결합할 필요가 없습니다. 고차 함수는 복잡한 중첩 구조, 배열, 맵 및 다양한 사용 사례를 특징으로 하는 시계열 데이터 세트 및 분석을 분석하거나 처리하는 데 특히 유용합니다.

다음 사용 사례 목록에는 고차 배열 및 맵 조작 함수의 예가 포함되어 있습니다.

## 변형을 사용하여 n까지 가격 합계를 조정합니다. {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

위의 코드 조각은 배열의 각 요소에 함수를 적용하고 변환된 요소의 새 배열을 반환합니다. 특히 `transform` 함수는 T 형식의 배열을 사용하고 각 요소를 T 형식에서 U 형식으로 변환합니다. 그런 다음 U 형식의 배열을 반환합니다. 실제 유형 T와 U는 변환 함수의 특정 용도에 따라 다릅니다.

`transform(array<T>, function<T, Int, U>): array<U>`

이 배열 변환 함수는 앞의 예제와 비슷하지만, 이 함수에는 두 개의 인수가 있습니다. 이 함수의 두 번째 인수는 변환되는 것 외에도 배열에 있는 요소의 인덱스도 받습니다.

**예**

아래의 SQL 예제에서는 이 사용 사례를 보여 줍니다. 쿼리는 지정된 테이블에서 제한된 행 집합을 검색하여 각 항목의 `priceTotal` 특성에 73을 곱하여 `productListItems` 배열을 변환합니다. 결과에는 `_id`, `productListItems` 및 변환된 `price_in_inr` 열이 포함됩니다. 선택은 특정 타임스탬프 범위를 기반으로 합니다.

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
 productListItems | price_in_inr
-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## 이(가) 존재하여 특정 SKU를 사용하는 제품이 존재하는지 여부 검색 {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

위의 코드 조각에서 `exists` 함수는 배열의 각 요소에 적용되며 부울 값을 반환합니다. 부울은 배열에 지정된 조건을 충족하는 요소가 하나 이상 있는지 여부를 나타냅니다. 이 경우 특정 SKU를 사용하는 제품이 존재하는지 확인합니다.

**예**

아래 SQL 예제에서 쿼리는 `geometrixxx_999_xdm_pqs_1batch_10k_rows` 테이블에서 `productListItems`을(를) 가져오고 `productListItems` 배열에서 SKU가 `123679`과(와) 같은 요소가 있는지 평가합니다. 그런 다음 특정 범위의 타임스탬프를 기반으로 결과를 필터링하고 최종 결과를 10개의 행으로 제한합니다.

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
productListItems
-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## 필터를 사용하여 SKU > 100000 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

이 함수는 각 요소를 부울 값으로 평가하는 주어진 조건을 기반으로 요소 배열을 필터링합니다. 그런 다음 조건이 true 값을 반환하는 요소만 포함하는 새 배열을 반환합니다.

**예**

아래 쿼리는 `productListItems` 열을 선택하고, SKU가 100000보다 큰 요소만 포함하도록 필터를 적용하고, 결과 집합을 특정 타임스탬프 범위 내의 행으로 제한합니다. 그런 다음 필터링된 배열은 출력에서 `_filter`(으)로 별칭이 지정됩니다.

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
productListItems | _filter
-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## 합계를 사용하여 특정 ID와 연결된 모든 제품 목록 항목의 SKU를 합하고 결과 합계를 두 배로 늘립니다. {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

이 집계 작업은 이진 연산자를 초기 상태와 배열의 모든 요소에 적용합니다. 또한 여러 값을 단일 상태로 줄입니다. 이 감소 후 최종 상태는 마무리 함수를 사용하여 최종 결과로 변환됩니다. finish 함수는 모든 배열 요소에 이진 연산자를 적용한 후 얻은 마지막 상태를 사용하고, 최종 결과를 생성하기 위해 이와 함께 어떤 작업을 수행합니다.

**예**

이 쿼리 예제는 지정된 타임스탬프 범위 내의 `productListItems` 배열에서 최대 SKU 값을 계산하고 결과를 두 배로 늘립니다. 출력에는 원본 `productListItems` 배열과 계산된 `max_value`이(가) 포함됩니다.

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
productListItems | max_value
-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## zip_with를 사용하여 제품 목록의 모든 항목에 시퀀스 번호를 지정합니다 {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

이 코드 조각은 두 배열의 요소를 하나의 새 배열로 결합합니다. 이 작업은 배열의 각 요소에 대해 독립적으로 수행되며 값의 쌍을 생성합니다. 배열 하나가 짧으면 긴 배열의 길이와 일치하도록 null 값이 추가됩니다. 이 문제는 함수가 적용되기 전에 발생합니다.

**예**

다음 쿼리는 `zip_with` 함수를 사용하여 두 배열에서 값 쌍을 만듭니다. 이 작업은 `productListItems` 배열의 SKU 값을 `Sequence` 함수를 사용하여 생성된 정수 시퀀스에 추가하여 수행합니다. 원래 `productListItems` 열과 함께 결과가 선택되었으며 타임스탬프 범위에 따라 제한됩니다.

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
productListItems     | zip_with
---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## map_from_entries를 사용하여 제품 목록의 각 항목에 시퀀스 번호를 지정하고 최종 결과를 맵으로 얻습니다. {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

이 코드 조각은 키-값 쌍의 배열을 맵으로 변환합니다. 보다 조직적이고 효율적인 구조를 활용할 수 있는 키-값 쌍 데이터를 처리할 때 유용합니다.

**예**

다음 쿼리는 시퀀스 및 productListItems 배열에서 값 쌍을 만들고 map_from_entries를 사용하여 이 쌍을 맵으로 변환한 다음 새로 만든 map_from_entries 열과 함께 원래 productListItems 열을 선택합니다. 결과는 지정된 타임스탬프 범위를 기반으로 필터링되고 제한됩니다.

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## map_form_arrays를 사용하여 제품 목록의 항목에 시퀀스 번호를 할당하고 결과를 맵으로 반환합니다 {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

`map_form_arrays` 함수는 두 배열에서 쌍을 이루는 값을 사용하여 맵을 만듭니다.

>[!IMPORTANT]
>
>키에 null 요소가 없어야 합니다.

**예**

아래 SQL은 `Sequence` 함수를 사용하여 생성된 일련 번호이고 값이 `productListItems` 배열의 요소인 맵을 만듭니다. 쿼리는 `productListItems` 열을 선택하고 `Map_from_arrays` 함수를 사용하여 생성된 숫자 시퀀스 및 배열의 요소를 기반으로 맵을 만듭니다. 결과는 10개의 행으로 제한되며 타임스탬프 범위를 기반으로 필터링됩니다.

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## map_concat를 사용하여 두 맵을 단일 맵으로 연결합니다 {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

위 코드 조각의 `map_concat` 함수는 여러 맵을 인수로 사용하고 입력 맵의 모든 키-값 쌍을 결합하는 새 맵을 반환합니다. 이 함수는 여러 맵을 단일 맵으로 연결하고, 결과 맵에는 입력 맵의 모든 키-값 쌍이 포함됩니다.

**예**

아래의 SQL은 `productListItems`의 각 항목이 시퀀스 번호와 연결된 맵을 만듭니다. 이 맵은 특정 시퀀스 범위에서 키가 생성되는 다른 맵과 연결됩니다.

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## 추가 계산을 위해 ID 맵에서 &#39;AAID&#39;에 해당하는 값을 검색하려면 element_at를 사용합니다 {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

배열의 경우 코드 조각은 지정된 (1 기반) 인덱스의 요소 또는 맵의 키와 연결된 값을 반환합니다. 인덱스가 0 미만이면 마지막 요소부터 첫 번째 요소까지 액세스하고 인덱스가 배열의 길이를 초과하면 null을 반환합니다.

맵의 경우 지정된 키에 대한 값을 반환하거나 키가 맵에 포함되지 않은 경우 null을 반환합니다.

**예**

쿼리가 테이블 `geometrixxx_999_xdm_pqs_1batch_10k_rows`에서 `identitymap` 열을 선택하고 각 행에 대해 키 `AAID`과(와) 연결된 값을 추출합니다. 결과는 지정된 타임스탬프 범위 내에 있는 행으로 제한되며 쿼리는 출력을 10개 행으로 제한합니다.

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## ID 맵에서 카디널리티를 사용하여 ID 수 찾기 {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

이 코드 조각은 특정 배열 또는 맵의 크기를 반환하고 별칭을 제공합니다. 값이 null이면 -1을 반환합니다.

**예**

아래 쿼리는 `identitymap` 열을 검색하고 `Cardinality` 함수는 `identitymap` 내의 각 맵에서 요소의 수를 계산합니다. 결과는 10개의 행으로 제한되며 지정된 타임스탬프 범위를 기반으로 필터링됩니다.

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
                                                                  identitymap                                            |  size(identitymap) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## array_distinct를 사용하여 productListItems에서 개별 요소를 찾습니다. {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

위의 스니펫은 지정된 배열에서 중복 값을 제거합니다.

**예**

아래 쿼리는 `productListItems` 열을 선택하고 배열에서 중복된 항목을 제거하며 지정된 타임스탬프 범위를 기준으로 출력을 10행으로 제한합니다.

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**결과**

이 SQL의 결과는 아래에 표시된 결과와 유사합니다.

```console
productListItems     | array_distinct(productListItems)
---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### 추가적인 고차 함수 {#additional-higher-order-functions}

다음 상위 함수 예는 유사한 레코드 검색 사용 사례의 일부로 설명되어 있습니다. 각 기능의 사용 예제와 설명은 해당 문서의 각 섹션에 나와 있습니다.

[`transform` 함수 예제](../use-cases/retrieve-similar-records.md#length-adjustment)은(는) 제품 목록의 토큰화를 다룹니다.

[`filter` 함수 예제](../use-cases/retrieve-similar-records.md#filter-results)에서는 텍스트 데이터에서 관련 정보를 보다 정교하고 정확하게 추출하는 방법을 보여 줍니다.

[`reduce` 함수](../use-cases/retrieve-similar-records.md#higher-order-function-solutions)은(는) 다양한 분석 및 계획 프로세스에서 중추적 역할을 할 수 있는 누적 값 또는 합계를 도출하는 방법을 제공합니다.
