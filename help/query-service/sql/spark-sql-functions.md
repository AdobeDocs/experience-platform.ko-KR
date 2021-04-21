---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;Spark sql;spark sql;spark sql functions;functions;
solution: Experience Platform
title: 쿼리 서비스의 Spark SQL 함수
topic-legacy: spark sql functions
description: 이 설명서에는 SQL 기능을 확장하는 Spark SQL 함수에 대한 정보가 포함되어 있습니다.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '3893'
ht-degree: 1%

---

# [!DNL Spark] SQL 함수

Adobe Experience Platform 쿼리 서비스는 SQL 기능을 확장하기 위해 내장된 여러 Spark SQL 기능을 제공합니다. 이 문서에는 쿼리 서비스에서 지원되는 Spark SQL 함수가 나와 있습니다.

함수 구문, 사용 방법, 예 등 함수에 대한 자세한 내용은 [Spark SQL 함수 설명서](https://spark.apache.org/docs/latest/api/sql/index.html)를 참조하십시오.

>[!NOTE]
>
>외부 설명서의 일부 기능이 지원되지 않습니다.

## 카테고리

- [수학 및 통계 연산자 및 함수](#math)
- [논리 연산자](#logical-operators)
- [날짜/시간 함수](#datetime-functions)
- [어레이](#arrays)
- [데이터 유형 변환 함수](#datatype-casting)
- [변환 및 서식 지정 함수](#conversion)
- [데이터 평가](#data-evaluation)
- [현재 정보](#current-information)
- [높은 주문 함수](#higher-order)

## 수학 및 통계 연산자 및 함수 {#math}

| 연산자/함수 | 설명 |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_2) | 두 숫자 중 나머지 숫자를 반환합니다. |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_4) | 두 숫자를 곱합니다. |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | 두 숫자를 추가합니다. |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | 두 숫자 빼기 |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | 두 숫자 나누기 |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | 입력의 절대값을 반환합니다. |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | 역코사인 값을 반환합니다. |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | HyperLogLog++의 예상 기수를 반환합니다. |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | 주어진 백분율로 대략적인 백분위수 값을 반환합니다. |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | 역사인 값을 반환합니다. |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | 역접선 값을 반환합니다. |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | 양수 x축 평면과 좌표로 지정된 점 사이의 각도를 반환합니다. |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | 평균 값을 반환합니다. |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | 큐브 루트를 반환합니다. |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) 또는 [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | 입력 값보다 크지 않은 가장 작은 정수를 반환합니다. |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | 한 베이스에서 다른 베이스로 변환 |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | 숫자 사이의 피어슨 계수를 반환합니다. |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | 코사인 값을 반환합니다. |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | 쌍곡코사인 값을 반환합니다. |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | 컨텐츠 값을 반환합니다. |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | 값 그룹의 값 등급을 반환합니다. |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Euler의 번호를 반환합니다. |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | e를 값의 거듭제곱 반환 |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | e를 값 빼기 1의 거듭제곱으로 반환합니다. |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | 값의 조합을 반환합니다. |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | 값보다 작지 않은 가장 큰 정수를 반환합니다. |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | 모든 매개 변수의 가장 큰 값을 반환합니다. |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | 주어진 두 값의 가설을 반환합니다. |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | 그룹의 첨자 값을 반환합니다. |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | 모든 매개 변수의 가장 작은 값을 반환합니다. |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | 값의 자연 로그를 반환합니다. |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | 값의 로그를 반환합니다. |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | 값의 밑이 10인 로그를 반환합니다. |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | 값의 로그 더하기 1을 반환합니다. |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | 값의 밑이 2인 로그를 반환합니다. |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | 표현식의 최대값을 반환합니다. |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | 값에서 계산된 평균을 반환합니다. |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | 표현식의 최소값을 반환합니다. |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | 단색으로 증가하는 ID를 반환합니다. |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | 무효화된 값을 반환합니다. |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | 값의 백분율 등급을 반환합니다. |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | 지정된 백분율로 정확한 백분위수를 반환합니다. |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | 지정된 백분율로 대략적인 백분위수를 반환합니다. |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | pi 반환 |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | 두 값 사이의 양의 모듈을 반환합니다. |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | 양의 값을 반환합니다. |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | 두 번째 값의 성능에 첫 번째 값을 반환합니다. |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | 값을 라디안으로 변환합니다. |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | 0과 1 사이의 난수를 반환합니다. |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | 임의 값을 반환합니다. |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | 가장 가까운 이중 값을 반환합니다. |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | 가장 근접한 반올림값을 반환합니다. |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign),  [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | 숫자 기호를 반환합니다. |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | 값의 사인을 반환합니다. |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | 값의 쌍곡사인을 반환합니다. |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | 값의 제곱근을 반환합니다. |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | 값의 표준 편차를 반환합니다. |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | 값의 모집단 표준 편차를 반환합니다. |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | 값의 샘플 표준 편차를 반환합니다. |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | 값의 합계를 반환합니다. |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | 값의 탄젠트를 반환합니다. |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | 값의 쌍곡탄젠트를 반환합니다. |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | 계산된 인구 변화를 반환합니다. |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp),  [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | 계산된 샘플 변화를 반환합니다. |

### 논리 연산자 및 함수 {#logical-operators}

| 연산자/함수 | 설명 |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) 또는 [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | 논리 NOT |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | 보다 작음 |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | 작거나 같음 |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_10) | 같음 |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | 보다 큼 |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | 크거나 같음 |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | 비트 전용 또는 |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | 크거나 같음 |
| [`|`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | 비트 또는 |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | 비트 전송되지 않음 |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | 공통 요소를 반환합니다. |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | 표현식이 true인 경우 어설션 |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | 표현식이 true로 평가되면 두 번째 표현식을 반환합니다. 그렇지 않으면 세 번째 표현식을 반환합니다. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | 식이 null이면 두 번째 식을 반환합니다. 그렇지 않으면 첫 번째 표현식을 반환합니다. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | 다음 표현식에 첫 번째 표현식이 있으면 true를 반환합니다. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | 값이 숫자가 아닌 경우 true를 반환합니다. |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | 값이 null이 아니면 true를 반환합니다. |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | 값이 null이면 true를 반환합니다. |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | 숫자가 아닌 경우 첫 번째 표현식을 반환하고 두 번째 표현식을 반환합니다. |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | 논리 또는 |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | 비교할 분기 조건을 만드는 데 사용할 수 있는 시기 |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | XPath 표현식이 true로 평가되거나 일치하는 노드가 발견되면 true를 반환합니다. |

### 날짜/시간 함수 {#datetime-functions}

| 함수 | 설명 |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | 날짜에 월 추가 |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | 날짜에 일 추가 |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | 날짜 형식 수정 |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | 날짜로부터 일 빼기 |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | 지정된 단위로 잘린 날짜를 반환합니다. |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | 일 단위 날짜 간의 차이를 반환합니다. |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day),  [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | 해당 월의 날짜를 반환합니다. |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | 요일을 반환합니다(1-7). |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | 일 수를 반환합니다. |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Unix 시간으로 날짜를 반환합니다. |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | 날짜를 UTC 시간으로 반환합니다. |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | 입력 시간을 반환합니다. |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | 날짜가 속하는 월의 마지막 날을 반환합니다. |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | 입력 시간을 반환합니다. |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | 입력 월을 반환합니다. |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | 다음 사이의 개월 수 |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | 입력보다 늦은 첫 번째 날을 반환합니다. |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | 입력 분기를 반환합니다. |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | 문자열의 두 번째 값을 반환합니다. |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | 문자열을 날짜로 변환합니다. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | 문자열을 타임스탬프로 변환합니다. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | 문자열을 Unix 타임스탬프로 변환합니다. |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | 문자열을 UTC 타임스탬프로 변환합니다. |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | 날짜를 자릅니다. |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Unix 타임스탬프를 반환합니다. |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | 요일(0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | 지정된 날짜에 대한 연도의 주를 반환합니다. |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | 문자열의 연도를 반환합니다. |

### 배열 {#arrays}

| 함수 | 설명 |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | 지정된 요소가 있는 배열을 만듭니다. |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | 배열에 값이 포함되어 있는지 확인합니다. |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | 배열에서 중복 값을 제거합니다. |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | 첫 번째 배열에 있는 요소의 배열을 반환하지만 두 번째 배열은 반환합니다. |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | 두 배열의 교차를 반환합니다. |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | 두 개의 스토리지를 함께 연결 |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | 배열의 최대값을 반환합니다. |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | 배열의 최소 값을 반환합니다. |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | 요소의 1 기반 위치를 반환합니다. |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | 요소와 같은 모든 요소를 제거합니다. |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | 계산 시간이 포함된 배열을 만듭니다. |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | 배열을 정렬합니다. |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | 중복 없이 배열을 함께 결합합니다. |
| [`array_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Zip |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | 배열의 크기를 반환합니다. |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | 요소의 위치를 반환합니다. |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | 배열 요소를 여러 행으로 분리(null 제외) |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | 배열 요소를 null을 포함하여 여러 행으로 분리 |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | 배열의 1기반 위치를 반환합니다. |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | 배열 병합 |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | null을 제외하고 별도의 구조체 배열을 테이블로 지정합니다. |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | null을 포함하여 별도의 구조체 배열 |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | 배열 요소를 위치가 있는 여러 행으로 분리(null 제외) |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | 배열 요소를 null을 포함하여 위치가 있는 여러 행으로 분리 |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | 배열의 요소 반전 |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | 배열의 임의 순차를 반환합니다. |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | 배열의 하위 세트 |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | 순서가 지정된 배열 정렬 |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | 함수를 적용하기 전에 두 배열을 단일 배열로 병합합니다. |

### 데이터 형식 변환 함수 {#datatype-casting}

| 함수 | 설명 |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | 데이터 유형을 bigint로 변경 |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | 데이터 형식을 이진 형식으로 변경 |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | 데이터 유형을 부울로 변경 |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | 데이터 유형을 지정된 유형으로 변경 |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | 데이터 유형을 날짜로 변경 |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | 데이터 유형을 십진수로 변경 |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | 데이터 유형을 두 배로 변경 |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | 데이터 유형을 부동 항목으로 변경 |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | 데이터 유형을 int로 변경 |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | 데이터 유형을 smallint로 변경 |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | 문자열에서 맵 만들기 |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | 데이터 유형을 문자열로 변경 |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | 구조체 만들기 |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | 데이터 유형을 tinyint로 변경 |

### 변환 및 서식 함수 {#conversion}

| 함수 | 설명 |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | 숫자(ASCII) 값을 반환합니다. |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | base64 문자열로 인수 변경 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | 인수를 이진 값으로 변경 |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | 비트 길이를 반환합니다. |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char),  [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | ASCII 문자 반환 |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length),  [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | 문자열 길이를 반환합니다. |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | 순환 중복 검사 값을 반환합니다. |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | 라디안을 도로 변환 |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | 숫자 형식 변경 |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json),  [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | JSON에서 데이터 가져오기 |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | 해시 값을 반환합니다. |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | 인수를 16진수 값으로 변환 |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | 제목을 지정할 문자열을 변경합니다. |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase),  [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | 문자열을 모두 소문자로 변경합니다. |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | 문자열의 왼쪽에 패드를 넣습니다. |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | 지도 만들기 |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | 배열에서 지도 만들기 |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | 일련의 구조에서 지도 만들기 |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | md5 값 반환 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | 문자열의 오른쪽에 패드를 넣습니다. |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | 후행 공백 제거 |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha),  [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | SHA1 값 반환 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | SHA2 값 반환 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | 사운드 덱스 코드 반환 |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | 값을 행으로 구분 |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr),  [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | 하위 문자열 반환 |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | JSON 문자열을 반환합니다. |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | 문자열 내의 값 바꾸기 |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | 행간 및 후행 문자 제거 |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase),  [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | 문자열을 모두 대문자로 변경합니다. |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | base64 문자열을 바이너리로 변환 |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | 16진수를 이진 파일로 변환 |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | UUID 반환 |

### 데이터 평가 {#data-evaluation}

| 함수 | 설명 |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | null이 아닌 첫 번째 인수를 반환합니다. |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | 고유하지 않은 요소 목록 반환 |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | 고유한 요소 집합 반환 |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | 연결 |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | 구분 기호를 사용한 연결 |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | 행의 총 개수를 반환합니다. |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | 문자 집합을 사용하여 디코딩 |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)번째 입력을 반환합니다. |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | 문자 집합을 사용하여 인코딩 |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first),  [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | 첫 번째 값을 반환합니다. |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | 열을 그룹화했는지 여부를 나타냅니다. |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | 그룹화 수준을 반환합니다. |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | 문자 발생 1부터 시작하는 인덱스를 반환합니다. |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | JSON 입력에서 튜플을 반환합니다. |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag),  [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | 오프셋 앞에 값을 반환합니다. |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last),  [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | 마지막 값을 반환합니다. |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | 첫 번째 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) 문자를 반환합니다. |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | 문자열의 길이를 반환합니다. |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | 문자열 사이의 레벨 간격 거리를 반환합니다. |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate),  [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | 하위 문자열의 첫 번째 발생 위치를 반환합니다. |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | 지도 연결 |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | 지도 키 반환 |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | 지도 값 반환 |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | 행을 파티션으로 나누기 |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | true이면 null을 반환합니다. |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | null인 경우 값을 반환합니다. |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | null이 아닌 경우 값을 반환합니다. |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | URL의 일부를 추출합니다. |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | 값의 등급 계산 |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | regex와 일치하는 항목을 추출합니다. |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | regex와 일치하는 항목을 바꿉니다. |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | 반복되는 문자열을 반환합니다. |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | 문자열의 모든 인스턴스 바꾸기 |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | 다차원 롤업 만들기 |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | 고유 행 번호를 할당합니다. |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | JSON의 스키마를 반환합니다. |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | 문자열을 단어 배열로 분할 |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | 요소의 배열을 생성합니다. |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | 서명된 비트 시프트 왼쪽 |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | 서명된 비트 시프트 오른쪽 |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | 부호 없는 비트 시프트 오른쪽 |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | 배열의 크기를 반환합니다. |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) 공백이 있는 문자열 반환 |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | 문자열 분할 |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | 하위 문자열의 인덱스 반환 |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | 창 |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | XML 노드 구문 분석 |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double),  [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | XML 노드를 두 배로 구문 분석 |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | XML 노드에서 부동 소수점 |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | XML 노드에서 정수를 구문 분석합니다. |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | XML 노드를 오랫동안 구문 분석합니다. |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | XML 노드에서 짧은 정수를 구문 분석합니다. |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | XML 노드에서 문자열을 구문 분석합니다. |

### 현재 정보 {#current-information}

| 함수 | 설명 |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | 현재 데이터베이스를 반환합니다. |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | 현재 날짜를 반환합니다. |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp),  [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | 현재 타임스탬프를 반환합니다. |

### 높은 주문 함수 {#higher-order}

| 함수 | 설명 |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | 배열의 요소 변형 |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | 요소가 있는지 확인 |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | 입력 배열 필터링 |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | 모든 요소에 이진 연산자 적용 |
