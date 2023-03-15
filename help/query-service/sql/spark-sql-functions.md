---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;spark sql;Spark sql;spark;spark sql 함수;함수;
solution: Experience Platform
title: 쿼리 서비스의 Spark SQL 함수
description: 이 설명서에는 SQL 기능을 확장하는 Spark SQL 함수에 대한 정보가 포함되어 있습니다.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '3866'
ht-degree: 0%

---

# [!DNL Spark] SQL 함수

Adobe Experience Platform Query Service는 SQL 기능을 확장하기 위한 몇 가지 내장 Spark SQL 기능을 제공합니다. 이 문서에서는 쿼리 서비스에서 지원하는 Spark SQL 함수를 나열합니다.

구문, 사용 방법 및 예를 포함하여 함수에 대한 자세한 내용은 [Spark SQL 함수 설명서](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>외부 설명서의 모든 기능이 지원되는 것은 아닙니다.

## 수학 및 통계 연산자 및 함수 {#math}

| 연산자/함수 | 설명 |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | 두 숫자의 나머지 반환 |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | 두 숫자를 곱합니다 |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | 두 숫자를 추가합니다. |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | 두 숫자를 뺍니다. |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | 두 숫자를 나눕니다. |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | 입력의 절대값 반환 |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | 역 코사인 값 반환 |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | HyperLogLog에 의한 예상 카디널리티를 반환합니다++ |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | 주어진 백분율로 대략적인 백분위수 값 반환 |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | 역 사인 값 반환 |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | 역탄젠트 값 반환 |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | 양의 x축 평면과 좌표로 지정된 점 사이의 각도 반환 |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | 평균 값 반환 |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | 세제곱근 반환 |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) 또는 [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | 입력한 값보다 크지 않은 가장 작은 정수 반환 |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | 한 베이스에서 다른 베이스로 변환 |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | 숫자 사이의 피어슨 계수 반환 |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | 코사인 값 반환 |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | 쌍곡코사인 값 반환 |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | 코탄젠트 값 반환 |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | 값 그룹의 값 순위 반환 |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | 오일러 숫자 반환 |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | 값의 거듭제곱으로 e 반환 |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | e에서 1을 뺀 값의 거듭제곱 반환 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | 값의 계승 반환 |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | 값보다 작지 않은 가장 큰 정수 반환 |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | 모든 매개 변수 중 가장 큰 값을 반환합니다. |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | 주어진 두 값의 빗변 반환 |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | 그룹에서 첨도 값 반환 |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | 모든 매개 변수 중 가장 작은 값을 반환합니다. |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | 값의 자연 로그 반환 |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | 값의 로그 반환 |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | 밑이 10인 값의 로그 반환 |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | 값에 1을 더한 로그 반환 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | 밑이 2인 값의 로그 반환 |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | 표현식의 최대값 반환 |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | 값에서 계산된 평균을 반환합니다. |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | 표현식의 최소값 반환 |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | 단조롭게 증가하는 ID 반환 |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | 부정된 값 반환 |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | 값의 백분율 순위 반환 |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | 지정된 백분율로 정확한 백분위수 반환 |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | 주어진 백분율로 대략적인 백분위수를 반환합니다. |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | pi 반환 |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | 두 값 사이의 양의 모듈로 반환 |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | 양수 값 반환 |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | 첫 번째 값을 두 번째 값의 거듭제곱으로 반환합니다. |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | 값을 라디안으로 변환 |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | 0과 1 사이의 난수를 반환합니다. |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | 임의 값 반환 |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | 가장 가까운 double 값 반환 |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | 가장 가까운 반올림된 값 반환 |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | 숫자 기호 반환 |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | 값의 사인 반환 |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | 값의 쌍곡사인 반환 |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | 값의 제곱근 반환 |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | 값의 표준 편차 반환 |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | 값의 모집단 표준 편차 반환 |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | 값의 샘플 표준 편차 반환 |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | 값의 합계 반환 |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | 값의 탄젠트 반환 |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | 값의 쌍곡탄젠트 반환 |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | 계산된 모집단 변량 반환 |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | 계산된 샘플 분산 반환 |

### 논리 연산자 및 함수 {#logical-operators}

| 연산자/함수 | 설명 |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) 또는 [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | 논리적 아님 |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | 미만 |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | 작거나 같음 |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | 같음 |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | 보다 큼 |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | 크거나 같음 |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | 비트 전용 또는 |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | 비트 OR |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | 비트 아님 |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | 일반 요소 반환 |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | 표현식이 true인지 어설션 |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | 표현식이 true로 평가되면 두 번째 표현식을 반환합니다. 그렇지 않으면 세 번째 표현식을 반환합니다. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | 표현식이 null이면 두 번째 표현식을 반환합니다. 그렇지 않으면 첫 번째 표현식을 반환합니다. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | 첫 번째 표현식이 후속 표현식 중 하나이면 true를 반환합니다. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | 값이 숫자가 아닌 경우 true 반환 |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | 값이 null이 아니면 true 반환 |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | 값이 null이면 true 반환 |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | 숫자가 아닌 경우 첫 번째 표현식 반환, 그렇지 않은 경우 두 번째 표현식 반환 |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | 논리적 또는 |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | 를 사용하여 비교할 분기 조건을 작성할 수 있습니다. |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | XPath 표현식이 true로 평가되거나 일치하는 노드가 발견되면 true를 반환합니다. |

### 날짜/시간 함수 {#datetime-functions}

| 함수 | 설명 |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | 일자에 월 추가 |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | 일자에 일 추가 |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | 날짜 형식 수정 |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | 날짜에서 일 빼기 |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | 지정한 단위로 잘린 날짜 반환 |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | 일자 간 차이값(일) 반환 |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day), [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | 날짜를 반환합니다. |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | 요일 반환(1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | 일(한 해 기준) 반환 |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | 날짜를 Unix 시간으로 반환 |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | 날짜를 UTC 시간으로 반환 |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | 입력 시간 반환 |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | 날짜가 속한 달의 말일을 반환합니다. |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | 입력 시간(분) 반환 |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | 입력 월 반환 |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | 다음 기간 사이의 개월 수 |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | 입력보다 1일 늦게 반환 |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | 입력의 사분기를 반환합니다. |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | 문자열의 초 반환 |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | 문자열을 날짜로 변환합니다. **참고:** 문자열 **필수** 형식이어야 합니다. `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | 문자열을 타임스탬프로 변환합니다. **참고:** 문자열 **필수** 형식이어야 합니다. `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | 문자열을 Unix 타임스탬프로 변환합니다. |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | 문자열을 UTC 타임스탬프로 변환 |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | 날짜 자르기 |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Unix 타임스탬프 반환 |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | 요일 (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | 지정된 일자의 주를 반환합니다. |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | 문자열의 연도 반환 |

### 배열 {#arrays}

| 함수 | 설명 |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | 지정된 요소로 배열을 만듭니다. |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | 배열에 값이 포함되어 있는지 확인합니다. |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | 배열에서 중복 값 제거 |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | 첫 번째 배열에 있는 요소의 배열을 반환하지만 두 번째 배열은 반환하지 않습니다. |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | 두 배열의 교차를 반환합니다. |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | 두 배열을 함께 연결 |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | 배열의 최대값 반환 |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | 배열의 최소값 반환 |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | 요소의 1부터 시작하는 위치 반환 |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | 요소와 동일한 모든 요소를 제거합니다. |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | 계산 시간 값을 포함하는 배열 만들기 |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | 배열 정렬 |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | 중복 없이 어레이를 함께 결합합니다. |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | 지정된 배열의 값을 지정된 인덱스의 원래 컬렉션 값과 결합합니다. |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | 배열 크기 반환 |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | 위치에 요소 반환 |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | 배열의 요소를 여러 행으로 구분(null 제외) |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | 배열의 요소를 null을 포함하여 여러 행으로 구분 |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | 배열의 1부터 시작하는 위치를 반환합니다. |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | 배열 배열 병합 |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | null을 제외하고 구조체 배열을 테이블로 구분 |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | null을 포함하여 별도의 구조체 배열을 테이블로 |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | 배열의 요소를 null을 제외하고 위치가 있는 여러 행으로 구분 |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | 배열의 요소 반전 |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | 배열의 임의 순열 반환 |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | 배열 하위 집합 |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | 주어진 순서로 배열을 정렬합니다. |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | 함수를 적용하기 전에 두 배열을 단일 배열로 병합합니다. |

### 데이터 유형 캐스팅 함수 {#datatype-casting}

| 함수 | 설명 |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | 데이터 유형을 bigint로 변경 |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | 데이터 형식을 이진으로 변경 |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | 데이터 유형을 부울로 변경 |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | 데이터 형식을 지정된 형식으로 변경합니다. |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | 데이터 유형을 날짜로 변경 |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | 데이터 형식을 십진수로 변경 |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | 데이터 유형을 double로 변경 |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | 데이터 형식을 float으로 변경 |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | 데이터 유형을 int로 변경 |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | 데이터 유형을 smallint로 변경 |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | 문자열에서 맵 만들기 |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | 데이터 유형을 문자열로 변경 |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | 구조 만들기 |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | 데이터 유형을 tinyint로 변경 |

### 변환 및 서식 함수 {#conversion}

| 함수 | 설명 |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | 숫자(ASCII) 값 반환 |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | 인수를 base64 문자열로 변경합니다. |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | 인수를 이진 값으로 변경합니다. |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | 비트 길이 반환 |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | ASCII 문자 반환 |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | 문자열 길이 반환 |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | 순환 중복 검사 값 반환 |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | 라디안을 도로 변환 |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | 숫자 형식 변경 |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | JSON에서 데이터 가져오기 |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | 해시 값 반환 |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | 인수를 16진수 값으로 변환 |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | 문자열을 제목 케이스로 변경합니다. |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | 문자열을 모두 소문자로 변경합니다. |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | 문자열의 왼쪽에 패드 달기 |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | 맵 만들기 |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | 배열에서 맵 만들기 |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | 구조체 배열에서 맵 만들기 |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | md5 값 반환 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | 문자열의 오른쪽에 패드 추가 |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | 후행 공백 제거 |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | SHA1 값 반환 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | SHA2 값 반환 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Soundex 코드 반환 |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | 값을 행으로 구분 |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | 하위 문자열 반환 |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | JSON 문자열 반환 |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | 문자열 내의 값 바꾸기 |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | 선행 및 후행 문자 제거 |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | 문자열을 모두 대문자로 변경합니다. |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | base64 문자열을 이진으로 변환 |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | 16진수를 바이너리로 변환 |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | UUID 반환 |

### 데이터 평가 {#data-evaluation}

| 함수 | 설명 |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | null이 아닌 첫 번째 인수 반환 |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | 고유하지 않은 요소 목록 반환 |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | 고유 요소 집합 반환 |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | 연결 |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | 분리자와 연결 |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | 행의 총 개수 반환 |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | 문자 집합을 사용하여 디코딩 |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | 반환 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)번째 입력 |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | 문자 집합을 사용하여 인코딩 |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | 첫 번째 값 반환 |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | 열이 그룹화되었는지 보여 줍니다. |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | 그룹화 수준 반환 |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | 문자 발생에 대한 1부터 시작하는 인덱스 반환 |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | JSON 입력에서 튜플 반환 |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | 오프셋 이전 값 반환 |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | 마지막 값 반환 |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | 첫 번째 반환 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) 자 |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | 문자열의 길이 반환 |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | 문자열 간 Levenshtein 거리 반환 |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | 하위 문자열의 첫 번째 발생 위치 반환 |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | 맵 연결 |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | 맵의 키 반환 |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | 맵 값 반환 |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | 행을 분할 영역으로 분할 |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | true인 경우 null 반환 |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | null인 경우 값 반환 |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | null이 아닌 경우 값 반환 |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | URL의 일부 추출 |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | 값의 순위 계산 |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | 정규 표현식과 일치하는 것을 추출합니다 |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | 정규 표현식과 일치하는 것을 대체합니다. |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | 반복하는 문자열 반환 |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | 문자열의 모든 인스턴스 바꾸기 |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | 다차원 롤업 만들기 |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | 고유한 행 번호 할당 |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | JSON 스키마 반환 |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | 문자열을 단어 배열로 분할합니다. |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | 요소 배열 생성 |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | 부호 있는 비트 시프트 왼쪽 |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | 부호 있는 비트 시프트 오른쪽 |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | 부호 없는 비트 시프트 오른쪽 |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | 배열 크기 반환 |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | 다음을 사용하여 문자열 반환 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) 공백 |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | 문자열 분할 |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | 하위 문자열의 인덱스 반환 |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | 창 |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | XML 노드 구문 분석 |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | XML 노드를 double로 구문 분석 |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | 부동 소수점에 대한 XML 노드 구문 분석 |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | 정수에 대한 XML 노드 구문 분석 |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | XML 노드를 길게 구문 분석 |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | 짧은 정수에 대한 XML 노드 구문 분석 |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | 문자열에 대한 XML 노드 구문 분석 |

### 현재 정보 {#current-information}

| 함수 | 설명 |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | 현재 데이터베이스를 반환합니다. |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | 현재 날짜 반환 |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | 현재 타임스탬프 반환 |

### 고차 함수 {#higher-order}

| 함수 | 설명 |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | 배열의 요소 변형 |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | 요소가 있는지 확인 |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | 입력 배열 필터링 |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | 모든 요소에 이진 연산자 적용 |
