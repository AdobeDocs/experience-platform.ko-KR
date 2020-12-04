---
keywords: Experience Platform;home;popular topics;query service;Query service;spark sql;Spark sql;spark;spark sql functions;functions;
solution: Experience Platform
title: Spark SQL 함수
topic: spark sql functions
description: 이 설명서에는 SQL 기능을 확장하는 내장 Spark SQL 기능을 제공하는 Spark SQL 도움말에 대한 정보가 포함되어 있습니다.
translation-type: tm+mt
source-git-commit: d0fa57effb45fad6934345323366ef45383bed01
workflow-type: tm+mt
source-wordcount: '5009'
ht-degree: 5%

---


# [!DNL Spark] SQL 함수

SQL [!DNL Spark] 도움말은 SQL 기능을 확장하는 내장 [!DNL Spark] SQL 기능을 제공합니다.

참조: [Spark SQL 함수 설명서](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE]
>
>외부 설명서의 일부 기능이 지원되지 않습니다.

## 카테고리

- [수학 및 통계 연산자 및 함수](#math)
- [논리 연산자](#logical-operators)
- [날짜/시간 함수](#datetime-functions)
- [집계 함수](#aggregate-functions)
- [스토리지 시스템](#arrays)
- [데이터 형식 캐스팅 함수](#datatype-casting)
- [변환 및 서식 기능](#conversion)
- [데이터 평가](#data-evaluation)
- [현재 정보](#current-information)
- [높은 주문 함수](#higher-order)

### 수학 및 통계 연산자 및 함수 {#math}

#### 모듈로

`expr1 % expr2`:나머지 값은 `expr1`/후에`expr2`반환합니다.

예

```sql
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### 곱하기

`expr1 * expr2`: 반환 `expr1`*`expr2`.

예:

```sql
> SELECT 2 * 3;
 6
```

#### 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에

`expr1 + expr2`: 반환 `expr1`+`expr2`.

예:

```sql
> SELECT 1 + 2;
 3
```

#### 빼기

`expr1 - expr2`: 반환 `expr1`-`expr2`.

예:

```sql
> SELECT 2 - 1;
 1
```

#### 나누기

`expr1 / expr2`: 반환 `expr1`/`expr2`. 항상 부동 소수점 나누기를 수행합니다.

예

```sql
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`:숫자 값의 절대값을 반환합니다.

예:

```sql
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`:을 사용하여 계산한 것처럼 의 역코사인(호 코사인)을 `expr`반환합니다 `java.lang.Math.acos`.

예

```sql
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### approx_percentives

`approx_percentile(col, percentage [, accuracy])`:지정된 백분율로 숫자 열의 대략적인 백분위수 값 `col` 을 반환합니다. 백분율 값은 0.0에서 1.0 사이여야 합니다. 매개 `accuracy` 변수(기본값:10000은 메모리 비용으로 근사 정확성을 제어하는 양의 숫자 리터럴입니다. 수익률이 높은 `accuracy` 경우 근사치의 상대적인 오류 `1.0/accuracy` 가 발생합니다. 배열 `percentage` 인 경우 백분율 배열의 각 값은 0.0에서 1.0 사이여야 합니다. 이 경우 지정된 백분율 배열에 있는 열의 대략적인 백분위수 배열 `col` 이 반환됩니다.

예

```sql
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`:아크 사인으로 알려진 역사인(아크 사인)을 계산 `expr`방식으로 반환합니다 `java.lang.Math.asin`.

예

```sql
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`:의 역탄젠트(호 탄젠트라고도 함)를 `expr`반환합니다. `java.lang.Math.atan`

예:

```sql
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`:평면의 양수 x축과 좌표(`exprX`,)에 의해 주어진 점 사이의 라디안 단위 각도 `exprY`를 계산대로 반환합니다 `java.lang.Math.atan2`.

인수:

`exprY`:Y축 좌표`exprX`:x축 좌표

예:

```sql
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`:그룹의 값에서 계산된 평균을 반환합니다.

#### 기수

`cardinality(expr)`:배열 또는 맵의 크기를 반환합니다. 이 함수는 입력한 내용이 null이고 true(기본값)로 설정되어 있으면 -1 `spark.sql.legacy.sizeOfNull` 을 반환합니다. false `spark.sql.legacy.sizeOfNull` 로 설정된 경우 함수는 null 입력에 대해 null을 반환합니다.

예

```sql
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`:의 큐브 루트를 반환합니다 `expr`.

예:

```sql
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`:보다 작지 않은 가장 작은 정수를 반환합니다 `expr`.

예

```sql
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### 천장

`ceiling(expr)`:보다 작지 않은 가장 작은 정수를 반환합니다 `expr`.

예

```sql
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`:변환 `num` `from_base` 을 `to_base`

예

```sql
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)`:숫자 쌍 집합 간의 상관 관계의 피어슨 계수를 반환합니다.

#### cos

`cos(expr)`:의 코사인(을 `expr`가 계산한 것처럼)을 `java.lang.Math.cos`반환합니다.

예:

```sql
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`:에 의해 계산되는 `expr`것처럼 쌍곡코사인을 반환합니다 `java.lang.Math.cosh`.

인수:
- `expr`:쌍곡각

예:

```
> SELECT cosh(0);
 1.0
```

#### 유아원

`cot(expr)`:에 의해 계산되는 `expr`것처럼 의 내용을 반환합니다 `1/java.lang.Math.cot`.

인수:
- `expr`:라디안 단위 각도

예:

```sql
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`:값 그룹의 값 순위를 계산합니다. 결과는 이전에 할당된 등급 값이 1에 추가됩니다. 함수 `rank`와 달리 등급 시퀀스에 간격이 `dense_rank` 생기지 않습니다.

#### e

`e()`:Euler의 번호를 반환합니다.

예:

```sql
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`:e를 강력한 기능으로 `expr`되돌립니다.

예:

```sql
> SELECT exp(0);
 1.0
```

#### exml

`expm1(expr)`:exp(`expr`) - 1을 반환합니다.

예:

```sql
> SELECT expm1(0);
 0.0
```

#### 계승

`factorial(expr)`:의 계수를 `expr`반환합니다. `expr` 은 [0.20입니다]. 그렇지 않으면 null입니다.

예:

```
> SELECT factorial(5);
 120
```

#### 바닥

`floor(expr)`:다음보다 크지 않은 가장 큰 정수를 반환합니다 `expr`.

예

```sql
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### 최고

`greatest(expr, ...)`:null 값을 건너뛰면서 모든 매개 변수의 최대값을 반환합니다.

예:

```sql
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### 후광

`hypot(expr1, expr2)`:sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>)를 반환합니다.

예:

```sql
> SELECT hypot(3, 4);
 5.0
```

#### 쿠토시스

`kurtosis(expr)`:그룹의 값에서 계산된 최대값 반환


#### 최소

`least(expr, ...)`:null 값을 건너뛰면서 모든 매개 변수의 최소 값을 반환합니다.

예:

```sql
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### 레벤슈테인

`levenshtein(str1, str2)`:주어진 두 문자열 사이의 Levenshtein 거리를 반환합니다.

예

```sql
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`:의 자연 로그(기본 e)를 `expr`반환합니다.

예:

```sql
> SELECT ln(1);
 0.0
```

#### 로그

`log(base, expr)`:와 함께 `expr` 로그를 `base`반환합니다.

예:

```sql
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`:밑이 10인 로그의 `expr` 로그를 반환합니다.

예:

```sql
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: 반환 `log(1 + expr)`.

예:

```sql
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`:밑이 2인 로그의 `expr` 로그를 반환합니다.

예:

```sql
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`:의 최대값을 반환합니다 `expr`.

#### mean

`mean(expr)`:그룹의 값에서 계산된 평균을 반환합니다.

#### min

`min(expr)`:최소값을 반환합니다 `expr`.

#### monthonically_increasing_id

`monotonically_increasing_id()`:단색으로 증가하는 64비트 정수를 반환합니다. 생성된 ID는 단조롭게 증가하고 고유하지만 연속되지 않습니다. 현재 구현은 파티션 ID를 상위 31비트에, 하위 33비트는 각 파티션 내의 레코드 수를 나타냅니다. 데이터 프레임의 파티션이 10억 개 미만이고 각 파티션의 레코드가 80억 개 미만이라는 가정입니다. 함수 결과가 파티션 ID에 따라 다르므로 이 함수는 결정적이지 않습니다.

#### negative

`negative(expr)`:무효화된 값 `expr`을 반환합니다.

예:

```sql
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()`:값 그룹에서 값의 백분율 등급을 계산합니다.

#### 백분위수

`percentile(col, percentage [, frequency])`:지정된 백분율로 숫자 열의 정확한 백분위수 값 `col` 을 반환합니다. 값은 0.0에서 1.0 사이여야 `percentage` 합니다. 이 값은 `frequency` 양의 필수 요소여야 합니다.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`:지정된 백분율로 숫자 열의 정확한 백분위수 값 배열 `col` 을 반환합니다. 백분율 배열의 각 값은 0.0에서 1.0 사이여야 합니다. 이 값은 양의 필수 요소여야 `frequency` 합니다.

#### percentage_approx

`percentile_approx(col, percentage [, accuracy])`:지정된 백분율로 숫자 열의 대략적인 백분위수 값 `col` 을 반환합니다. 값은 0.0에서 1.0 사이여야 `percentage` 합니다. `accuracy` 매개 변수(기본값:10000은 메모리 비용으로 근사 정확성을 제어하는 양의 숫자 리터럴입니다. 수익률이 높은 `accuracy` 경우 근사치의 상대적인 오류 `1.0/accuracy` 가 발생합니다. 배열 `percentage` `col` 이 되면 백분율 배열의 각 값은 0.0과 1.0 사이여야 합니다. 이 경우 지정된 백분율 배열에서 열의 대략적인 백분위수를 반환합니다.

예

```sql
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`:pi를 반환합니다.

예:

```sql
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`:mod의 양수 값을 `expr1` 반환합니다 `expr2`.

예

```sql
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### 긍정적

`positive(expr)`:양의 `expr`

#### 전쟁

`pow(expr1, expr2)`:힘 `expr1` 을 `expr2`높입니다

예:

```sql
> SELECT pow(2, 3);
 8.0
```

#### 전원

`power(expr1, expr2)`:힘 `expr1` 을 `expr2`높입니다

예

```sql
> SELECT power(2, 3);
 8.0
```

#### 방사성

`radians(expr)`:도를 라디안으로 변환합니다.

인수:

- `expr`:각도(도)

예:

```sql
> SELECT radians(180);
 3.141592653589793
```

#### 랜드

`rand([seed])`:(0, 1)에서 일관적으로 배포된 값(i.i.d.)을 가지는 독립적이고 동일하게 배포된 값의 임의 값을 반환합니다.

예

```sql
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE]
>
>이 함수는 일반적으로 결정적이지 않습니다.

#### randn

`randn([seed])`:표준 정규 분포에서 끌어들인 독립 및 동일하게 배포된(i.i.d.) 값이 있는 임의 값을 반환합니다.

예

```sql
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE]
>
>이 함수는 일반적으로 결정적이지 않습니다.

#### rint

`rint(expr)`:인수에 가장 근접한 값이고 수학 정수와 같은 이중 값을 반환합니다.

예

```sql
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`:HALF `expr` _UP `d` 반올림 모드를 사용하여 소수점 이하 자리로 반올림된 값을 반환합니다.

예:

```sql
> SELECT round(2.5, 0);
 3.0
```

#### sign

`sign(expr)`:-1.0, 0.0 또는 1.0을 `expr` 음수, 0 또는 양수로 반환합니다.

예:

```sql
> SELECT sign(40);
 1.0
```

#### 신호음

`signum(expr)`:-1.0, 0.0 또는 1.0을 `expr` 음수, 0 또는 양수로 반환합니다.

예:

```sql
> SELECT signum(40);
 1.0
```

#### 죄

`sin(expr)`:의 사인(을 `expr`로 계산하 `java.lang.Math.sin`는 것)을 반환합니다.

인수:

- `expr`:라디안 단위 각도

예:

```sql
> SELECT sin(0);
 0.0
```

#### sine

`sinh(expr)`:에 의해 계산되는 `expr`것처럼 쌍곡사인을 `java.lang.Math.sinh`반환합니다.

인수:

- `expr`:쌍곡각

예:

```sql
> SELECT sinh(0);
 0.0
```

#### 제곱근

`sqrt(expr)`:제곱근을 반환합니다 `expr`.

예:

```sql
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`:그룹의 값에서 계산된 샘플 표준 편차를 반환합니다.

#### stdev_pop

`sttdev_pop(expr)`:그룹 값에서 계산된 모집단 표준 편차를 반환합니다.

#### stdev_samp

`stddev_samp(expr)`:그룹의 값에서 계산된 샘플 표준 편차를 반환합니다.

#### sum

`sum(expr)`:그룹의 값에서 계산된 합계를 반환합니다.

#### 탄

`tan(expr)`:의 탄젠트를 `expr`를 계산 방식으로 반환합니다 `java.lang.Math.tan`.

인수:

- `expr`:라디안 단위 각도

예:

```sql
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`:에 의해 계산되는 `expr`것처럼 쌍곡탄젠트를 반환합니다 `java.lang.Math.tanh`.

인수:

- `expr`:쌍곡각

예:

```sql
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`:그룹의 값에서 계산된 인구 변화를 반환합니다.

#### Var_samp

`var_samp(expr)`:그룹의 값에서 계산된 샘플 분산을 반환합니다.

#### 차이

`variance(expr)`:그룹의 값에서 계산된 샘플 분산을 반환합니다.

### 논리 연산자 {#logical-operators}

#### 논리 NOT

`! expr`:논리적이지 않습니다.

#### 보다 작음

`expr1 < expr2`:보다 작으면 true `expr1` 를 반환합니다 `expr2`.

인수:

- `expr1, expr2`:두 표현식은 같은 유형이거나 일반 유형으로 캐스트할 수 있어야 하며, 순서를 지정할 수 있는 유형이어야 합니다. 예를 들어 맵 유형은 주문할 수 없으므로 지원되지 않습니다. 배열/구조체와 같은 복잡한 유형의 경우 필드의 데이터 유형을 오더할 수 있어야 합니다.

예

```sql
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### 작거나 같음

`expr1 <= expr2`:작거나 같은 경우 true `expr1` 를 반환합니다 `expr2`.

인수:

- `expr1, expr2`:두 표현식은 같은 유형이거나 일반적인 유형으로 캐스트할 수 있어야 하며, 순서를 지정할 수 있는 유형이어야 합니다. 예를 들어 맵 유형은 주문할 수 없으므로 지원되지 않습니다. 배열/구조체와 같은 복잡한 유형의 경우 필드의 데이터 유형을 오더할 수 있어야 합니다.

예

```sql
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### 같음

`expr1 = expr2`:같은 경우 true를 반환하거나 `expr1` 그렇지 않으면 false를 `expr2`반환합니다.

인수:

- `expr1, expr2`:두 표현식은 같은 유형이거나 일반 유형으로 캐스트할 수 있어야 하며 동일한 비교에 사용할 수 있는 유형이어야 합니다. 맵 유형은 지원되지 않습니다. 배열/구조체와 같은 복잡한 유형의 경우 필드의 데이터 유형을 오더할 수 있어야 합니다.

예

```sql
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### 보다 큼

`expr1 > expr2`:보다 큰 경우 true `expr1` 를 반환합니다 `expr2`.

인수:

- `expr1, expr2`:두 표현식은 같은 유형이거나 일반 유형으로 캐스트할 수 있어야 하며, 순서를 지정할 수 있는 유형이어야 합니다. 예를 들어 맵 유형은 주문할 수 없으므로 지원되지 않습니다. 배열/구조체와 같은 복잡한 유형의 경우 필드의 데이터 유형을 오더할 수 있어야 합니다.

예

```sql
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### 크거나 같음

`expr1 >= expr2`:크거나 `expr1` 같으면 true를 반환합니다 `expr2`.

인수:

- `expr1, expr2`:두 표현식은 같은 유형이거나 일반 유형으로 캐스트할 수 있어야 하며, 순서를 지정할 수 있는 유형이어야 합니다. 예를 들어 맵 유형은 주문할 수 없으므로 지원되지 않습니다. 배열/구조체와 같은 복잡한 유형의 경우 필드의 데이터 유형을 오더할 수 있어야 합니다.

예

```sql
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### 비트 전용 또는

`expr1 ^ expr2`:비트 독점 OR 및 `expr1` 의 결과를 반환합니다 `expr2`.

예:

```sql
> SELECT 3 ^ 5;
 2
```

#### 및

`expr1 and expr2`:논리 AND.

#### array_overlaps

`arrays_overlap(a1, a2)`:a1에 a2에도 있는 null이 아닌 요소 이상이 포함된 경우 true를 반환합니다. 배열에 공통 요소가 없고 두 요소가 모두 비어 있지 않고 둘 중 하나에 null 요소가 들어 있으면 null이 반환됩니다. 그렇지 않으면 false가 반환됩니다.

예:

```sql
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

이후:2.4.0

#### assert_true

`assert_true(expr)`:true가 아닌 경우 예외 `expr` 를 throw합니다.

예:

```sql
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`:true `expr1` 로 평가되면 반환 `expr2`;그렇지 않으면 반환됩니다 `expr3`.

예:

```sql
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### fifnull

`ifnull(expr1, expr2)`:null `expr2` 인 경우 또는 `expr1` 그렇지 않은 경우 `expr1` 반환합니다.

예:

```sql
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`:임의의 valN에 `expr` 등하는 경우 true를 반환합니다.

인수:
- `expr1, expr2, expr3, ...`:인수는 동일한 형식이어야 합니다.

예

```sql
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### 이스난

`isnan(expr)`:NaN이면 true `expr` 를 반환하고 그렇지 않으면 false를 반환합니다.

예:

```sql
> SELECT isnan(cast('NaN' as double));
 true
```

#### null이 아님

`isnotnull(expr)`:null이 `expr` 아니면 true를 반환하고, 그렇지 않으면 false를 반환합니다.

예

```sql
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`:null이면 true `expr` 를 반환하고 그렇지 않으면 false를 반환합니다.

예:

```sql
> SELECT isnull(1);
 false
```

#### nvl

`nanvl(expr1, expr2)`:NaN이 `expr1` 아닌 경우, 또는 다른 `expr2` 방법으로 반환합니다.

예:

```sql
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`:논리적이지 않습니다.

#### 또는

`expr1 or expr2`:논리적이거나

#### xpath_boolean

`xpath_boolean(xml, xpath)`:XPath 식이 true로 평가되거나 일치하는 노드가 발견되면 true를 반환합니다.

예:

```sql
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### 날짜/시간 함수 {#datetime-functions}

#### add_monds

`add_months(start_date, num_months)`:이후 날짜를 `num_months` 반환합니다 `start_date`.

예:

```sql
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

이후:1.5.0

#### date_add

`date_add(start_date, num_days)`:이후 날짜를 `num_days` 반환합니다 `start_date`.

예:

```sql
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

이후:1.5.0

#### date_format

`date_format(timestamp, fmt)`:날짜 형식 `timestamp` 으로 지정된 형식의 문자열 값으로 변환합니다 `fmt`.

예:

```sql
> SELECT date_format('2016-04-08', 'y');
 2016
```

이후:1.5.0

#### date_sub

`date_sub(start_date, num_days)`:이전 날짜를 `num_days` 반환합니다 `start_date`.

예:

```sql
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

이후:1.5.0

#### date_trunc

`date_trunc(fmt, ts)`:형식 모델에 의해 지정된 단위로 잘린 타임스탬프를 반환합니다 `fmt`. `fmt` should one of [&quot;YEAR&quot;, &quot;YYY&quot;, &quot;MON&quot;, &quot;MONTH&quot;, &quot;MM&quot;, &quot;DAY&quot;, &quot;DD&quot;, &quot;HOUR&quot;, &quot;MINUTES&quot;, &quot;SECOND&quot;, &quot;WEEK&quot;, &quot;QUARTERS&quot;]

예

```sql
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

이후:2.3.0

#### 날짜 편집

`datediff(endDate, startDate)`:부터 까지 일 수 `startDate` 를 반환합니다 `endDate`.

예

```sql
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

이후:1.5.0

#### 일

`day(date)`:날짜/타임스탬프의 월 날짜를 반환합니다.

예:

```sql
> SELECT day('2009-07-30');
 30
```

이후:1.5.0

#### 다류

`dayofmonth(date)`:날짜/타임스탬프의 월 날짜를 반환합니다.

예:

```sql
> SELECT dayofmonth('2009-07-30');
 30
```

이후:1.5.0

#### 다요프위크

`dayofweek(date)`:날짜/타임스탬프에 대한 요일을 반환합니다(1 = 일요일, 2 = 월요일, ..., 7 = 토요일).

예:

```sql
> SELECT dayofweek('2009-07-30');
 5
```

이후:2.3.0

#### 다요프년

`dayofyear(date)`:일/타임스탬프의 날짜를 반환합니다.

예:

```sql
> SELECT dayofyear('2016-04-09');
 100
```

이후:1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)`:지정된 값 `unix_time` 에서 반환합니다 `format`.

예:

```sql
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

이후:1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`:&#39;2017-07-14 02:40:00.0&#39;과 같은 타임스탬프를 UTC의 시간으로 해석하고 해당 시간을 지정된 시간대의 타임스탬프로 렌더링합니다. 예를 들어 &#39;GMT+1&#39;은 &#39;2017-07-14 03:40:00.0&#39;을 반환합니다.

예:

```sql
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

이후:1.5.0

#### 시간

`hour(timestamp)`:문자열/타임스탬프의 시간 구성 요소를 반환합니다.

예:

```sql
> SELECT hour('2009-07-30 12:58:59');
 12
```

이후:1.5.0

#### last_day

`last_day(date):` 날짜가 속하는 달의 마지막 날을 반환합니다.

예:

```sql
> SELECT last_day('2009-01-12');
 2009-01-31
```

이후:1.5.0

#### 분

`minute(timestamp)`:문자열/타임스탬프의 분 구성 요소를 반환합니다.

예:

```sql
> SELECT minute('2009-07-30 12:58:59');
 58
```

이후:1.5.0

#### 개월

`month(date)` 날짜/타임스탬프의 월 구성 요소를 반환합니다.

예:

```sql
> SELECT month('2016-07-30');
 7
```

이후:1.5.0

#### months_between

`months_between(timestamp1, timestamp2[, roundOff])`:보다 `timestamp1` 나중이면 `timestamp2`결과가 긍정적입니다. 및 `timestamp1` 가 같은 달 `timestamp2` 에 있거나 둘 다 월의 마지막 날이면, 하루 시간이 무시됩니다. 그렇지 않으면 월별 31일을 기준으로 차이가 계산되고 그렇지 않은 경우 8자리로 반올림됩니다 `roundOff=false`.

예

```sql
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

이후:1.5.0

#### next_day

`next_day(start_date, day_of_week)`:지정된 날짜보다 늦고 이름이 지정된 첫 번째 날짜 `start_date` 를 반환합니다.

예:

```sql
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

이후:1.5.0

#### 분기

`quarter(date)`:날짜 연도의 분기를 1에서 4 사이의 값으로 반환합니다.

예:

```sql
> SELECT quarter('2016-08-31');
 3
```

이후:1.5.0

#### second

`second(timestamp)`:문자열/타임스탬프의 두 번째 구성 요소를 반환합니다.

예:

```sql
> SELECT second('2009-07-30 12:58:59');
 59
```

이후:1.5.0

#### to_date

`to_date(date_str[, fmt])`:식을 날짜 `date_str` 로 구문 `fmt` 분석합니다. 잘못된 입력으로 null을 반환합니다. 기본적으로, 이 규칙을 생략하면 날짜 앞에 캐스팅 규칙을 `fmt` 따릅니다.

예

```sql
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

이후:1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`:식을 타임스탬프로 구문 `timestamp` 으로 `fmt` 분석합니다. 잘못된 입력으로 null을 반환합니다. 기본적으로, 이 매개 변수를 생략하면 타임스탬프로 캐스팅 규칙을 `fmt` 따릅니다.

예

```sql
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

이후:2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`:지정된 시간의 UNIX 타임스탬프를 반환합니다.

예:

```sql
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

이후:1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`:&#39;2017-07-14 02:40:00.0&#39;과 같은 타임스탬프를 지정된 시간대의 시간으로 해석하고 해당 시간을 UTC의 타임스탬프로 렌더링합니다. 예를 들어 &#39;GMT+1&#39;은 &#39;2017-07-14 01:40:00.0&#39;을 반환합니다.

예:

```sql
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

이후:1.5.0

#### trunc

`trunc(date, fmt)`:형식 모델에 의해 지정된 단위로 잘렸던 날짜의 시간 부분을 반환합니다 `fmt`. `fmt` 는 [&quot;year&quot;, &quot;yyyy&quot;, &quot;yy&quot;, &quot;mon&quot;, &quot;month&quot;, &quot;mm&quot; 중 하나입니다.]

예

```sql
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

이후:1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`:현재 또는 지정된 시간의 UNIX 타임스탬프를 반환합니다.

예

```sql
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

이후:1.5.0

#### 평일

`weekday(date)`:날짜/타임스탬프에 대한 요일을 반환합니다(0 = 월요일, 1 = 화요일, ..., 6 = 일요일).

예:

```sql
> SELECT weekday('2009-07-30');
 3
```

이후:2.4.0

#### week_of_year

`weekofyear(date)`:주어진 날짜의 연도의 주를 반환합니다. 한 주는 월요일에 시작하는 것으로 간주되며, 1주는 3일을 넘는 첫 번째 주가 됩니다.

예:

```sql
> SELECT weekofyear('2008-02-20');
 8
```

이후:1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`:When `expr1` = true이면 반환 `expr2`;else when `expr3` = true이면 반환 `expr4`;else 반환 `expr5`.

인수:

- `expr1`, `expr3`:분기 조건 표현식은 모두 부울 형식이어야 합니다.
- `expr2`, `expr4``expr5`:분기 값 표현식 및 기타 값 표현식은 모두 같은 유형이거나 공통 유형으로 강제 변환되어야 합니다.

예

```sql
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### 년

`year(date)`:날짜/타임스탬프의 연도 구성 요소를 반환합니다.

예:

```sql
> SELECT year('2016-07-30');
 2016
```

이후:1.5.0

### 집계 함수 {#aggregate-functions}

#### approx_count_distinct

`approx_count_distinct(expr[, relativeSD])`:예상 카디널리티를 HyperLogLog++로 반환합니다. `relativeSD` 허용되는 최대 예측 오류를 정의합니다.

### 스토리지 시스템 {#arrays}

#### 배열

`array(expr, ...)`:지정된 요소가 있는 배열을 반환합니다.

예:

```sql
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`:배열에 값이 포함되어 있으면 true를 반환합니다.

예:

```sql
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_distinct

`array_distinct(array)`:배열에서 중복 값을 제거합니다.

예:

```sql
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

이후:2.4.0

#### array_except

`array_except(array1, array2)`:중복 없이 in `array1` 과 not in `array2`의 요소 배열을 반환합니다.

예:

```sql
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

이후:2.4.0

#### array_intersect

`array_intersect(array1, array2)`:와 의 교차에서 중복 없이 요소 `array1` 의 배열을 `array2`반환합니다.

예:

```sql
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

이후:2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`:구분 기호 및 선택적 문자열을 사용하여 지정된 배열의 요소를 연결하여 null을 바꿉니다. 에 대해 값이 설정되지 않은 경우 `nullReplacement`모든 null 값이 필터링됩니다.

예

```sql
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

이후:2.4.0

#### array_max

`array_max(array)`:배열의 최대값을 반환합니다. null 요소는 건너뜁니다.

예:

```sql
> SELECT array_max(array(1, 20, null, 3));
 20
```

이후:2.4.0

#### array_min

`array_min(array)`:배열의 최소값을 반환합니다. null 요소는 건너뜁니다.

예:

```sql
> SELECT array_min(array(1, 20, null, 3));
 1
```

이후:2.4.0

#### array_position

`array_position(array, element)`:배열의 첫 번째 요소의 (1 기반) 인덱스를 반환합니다.

예:

```sql
> SELECT array_position(array(3, 2, 1), 1);
 3
```

이후:2.4.0

#### array_remove

`array_remove(array, element)`:배열에서 요소와 같은 요소를 모두 제거합니다.

예:

```sql
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

이후:2.4.0

#### array_repeat

`array_repeat(element, count)`:요소 카운트 시간이 포함된 배열을 반환합니다.

예:

```sql
> SELECT array_repeat('123', 2);
 ["123","123"]
```

이후:2.4.0

#### array_sort

`array_sort(array)`:입력 배열을 오름차순으로 정렬합니다. 입력 어레이의 요소는 주문할 수 있어야 합니다. 반환된 배열의 끝에 null 요소가 배치됩니다.

예:

```sql
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

이후:2.4.0

#### array_union

`array_union(array1, array2)`:중복되지 않고 `array1` 및 `array2`의 결합에 있는 요소의 배열을 반환합니다.

예:

```sql
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

이후:2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`:N-번째 구조체에 입력 배열의 모든 N 번째 값이 포함된 병합된 구조체 배열을 반환합니다.

예

```sql
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

이후:2.4.0

#### element_at

`element_at(array, index)`:지정된(1 기반) 인덱스에서 배열 요소를 반환합니다. if `index < 0`, accesses elements from the last to the first. 인덱스가 배열 길이를 초과하는 경우 NULL을 반환합니다.

`element_at(map, key)`:지정된 키에 대한 값을 반환하거나 키가 맵에 포함되지 않은 경우 NULL을 반환합니다.

예

```sql
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

이후:2.4.0

#### 분해

`explode(expr)`:배열 요소를 여러 행 `expr` 으로 분리하거나 맵 요소 `expr` 를 여러 행과 열로 구분합니다.

예

```sql
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_outer

`explode_outer(expr)`:배열 요소를 여러 행 `expr` 으로 분리하거나 맵 요소 `expr` 를 여러 행과 열로 구분합니다.

예:

```sql
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`:지정된 문자열(1 기반)의 인덱스(`str`)를 쉼표로 구분된 목록(`str_array`)으로 반환합니다. 문자열을 찾을 수 없거나 주어진 문자열(`str`)에 쉼표가 포함된 경우 0을 반환합니다.

예:

```sql
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### 분리

`flatten(arrayOfArrays)`:어레이 배열을 단일 어레이로 변환합니다.

예:

```sql
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

이후:2.4.0

#### 인라인

`inline(expr)`:일련의 구조를 테이블로 결합합니다.

예:

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_outer

`inline_outer(expr)`:일련의 구조를 테이블로 결합합니다.

예:

```sql
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### 폭발

`posexplode(expr)`:배열 요소를 위치를 사용하여 여러 행 `expr` 으로 분리하거나, 맵 요소를 위치가 있는 여러 행 및 열 `expr` 로 구분합니다.

예:

```sql
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### poexplode_outer

`posexplode_outer(expr)`:배열 요소를 위치를 사용하여 여러 행 `expr` 으로 분리하거나, 맵 요소를 위치가 있는 여러 행 및 열 `expr` 로 구분합니다.

예:

```sql
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### 반전

`reverse(array)`:요소 순서가 뒤바뀐 문자열 또는 배열을 반환합니다.

예

```sql
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

이후:1.5.0

>[!NOTE]
>
>어레이에 대한 rse 로직은 2.4.0부터 사용할 수 있습니다.

#### 셔플

`shuffle(array)`:지정된 배열의 임의 변이를 반환합니다.

예

```sql
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

이후:2.4.0

>[!NOTE]
>
>함수는 결정적이지 않습니다.

#### 슬라이스

`slice(x, start, length)`:인덱스 시작으로부터 시작(또는 start가 음수인 경우 끝부터 시작)되는 배열 x를 지정된 길이로 하위 설정합니다.

예

```sql
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

이후:2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`:배열 요소의 자연어 순서에 따라 입력 배열을 오름차순이나 내림차순으로 정렬합니다. Null 요소는 반환된 배열의 시작 부분에 오름차순 또는 반환된 배열의 끝에 내림차순으로 배치됩니다.

예

```sql
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`:주어진 두 배열을 요소 단위로 하나의 배열로 병합합니다. 하나의 배열이 더 짧은 경우 함수를 적용하기 전에 긴 배열의 길이와 일치하도록 끝에 null이 추가됩니다.

예

```sql
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

이후:2.4.0

### 데이터 형식 캐스팅 함수 {#datatype-casting}

#### bigint

`bigint(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `bigint`.

#### 이진

`binary(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `binary`.

#### 부울

`boolean(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `boolean`.

#### 캐스트

`cast(expr AS type)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `type`.

예:

```sql
> SELECT cast('10' as int);
 10
```

#### 날짜

`date(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `date`.

#### 소수

`decimal(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `decimal`.

#### 이중

`double(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `double`.

#### float

`float(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `float`.

#### int

`int(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `int`.

#### 지도

`map(key0, value0, key1, value1, ...)`:지정된 키/값 쌍으로 맵을 만듭니다.

예:

```sql
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### smalint

`smallint(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`:구분 기호를 사용하여 텍스트를 키/값 쌍으로 분할한 후 맵을 만듭니다. 기본 구분 기호는 &#39;,&#39;이고 `pairDelim` 는 &#39;:&#39;입니다 `keyValueDelim`.

예

```sql
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### string

`string(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `string`.

#### 구조체

`struct(col1, col2, col3, ...)`:주어진 필드 값이 있는 구조체를 만듭니다.

#### tinyint

`tinyint(expr)`:대상 데이터 유형 `expr` 에 값을 캐스팅합니다 `tinyint`.

### 변환 및 서식 기능 {#conversion}

#### ascii

`ascii(str)`:첫 번째 문자의 숫자 값을 반환합니다 `str`.

예

```sql
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`:인수를 바이너리에서 기본 64 문자열 `bin` 로 변환합니다.

예:

```sql
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)`:이진 형식으로 표시되는 긴 값의 문자열 표현 `expr` 을 반환합니다.

예

```sql
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`:문자열 데이터의 비트 길이 또는 이진 데이터의 비트 수를 반환합니다.

예:

```sql
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`:바이너리에 상응하는 ASCII 문자를 반환합니다 `expr`. n이 256보다 큰 경우 결과는 같습니다 `chr(n % 256)`.

예:

```sql
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`:문자열 데이터의 문자 길이 또는 바이너리 데이터의 바이트 수를 반환합니다. 문자열 데이터의 길이에는 후행 공백이 포함됩니다. 이진 데이터의 길이에는 이진 0이 포함됩니다.

예

```sql
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)`:문자열 데이터의 문자 길이 또는 바이너리 데이터의 바이트 수를 반환합니다. 문자열 데이터의 길이에는 후행 공백이 포함됩니다. 이진 데이터의 길이에는 이진 0이 포함됩니다.

예

```sql
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`:expr에 상응하는 바이너리가 있는 ASCII 문자를 반환합니다. n이 256보다 큰 경우 결과는 `chr(n % 256)`

예:

```sql
> SELECT chr(65);
 A
```

#### 도

`degrees(expr)`:라디안을 도로 변환합니다.

인수:
- `expr`:라디안 단위 각도

예:

```sql
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`:형식을 &#39;#,###,#### 등의 형식으로 지정합니다. `expr1`##&#39;, 소수점 이하 `expr2` 자리까지 반올림되었습니다. 0이면 결과 `expr2` 에 소수점 또는 분수 부분이 없습니다. `expr2` 또한 사용자가 지정한 형식을 수락합니다. MySQL과 같은 기능을 제공하기 위한 것입니다 `FORMAT`.

예

```sql
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`:주어진 and를 사용하여 구조체 값 `jsonStr` 을 반환합니다 `schema`.

예

```sql
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

이후:2.2.0

#### 해시

`hash(expr1, expr2, ...)`:인수의 해시 값을 반환합니다.

예:

```sql
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### 16진수

`hex(expr)`:16진수 `expr` 로 변환합니다.

예

```sql
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`:각 단어 `str` 의 첫 번째 문자를 대문자로 반환합니다. 다른 문자는 모두 소문자입니다. 단어는 공백으로 구분됩니다.

예:

```sql
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)`:모든 문자 `str` 가 소문자로 변경된 경우를 반환합니다.

예:

```sql
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)`:모든 문자 `str` 가 소문자로 변경된 경우를 반환합니다.

예:

```sql
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`:왼쪽 `str`으로 채워져 있는 값 `pad` 을 반환합니다 `len`. 보다 `str` 긴 경우 반환 `len`값이 `len` 문자로 단축됩니다.

예

```sql
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### 지도

`map(key0, value0, key1, value1, ...)`:지정된 키/값 쌍으로 맵을 만듭니다.

예:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)`:지정된 키/값 배열 쌍으로 맵을 만듭니다. 키의 요소는 null일 수 없습니다.

예:

```sql
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

이후:2.4.0

#### map_from_entries

`map_from_entries(arrayOfEntries)`:주어진 항목 배열에서 만든 맵을 반환합니다.

예:

```sql
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

이후:2.4.0

#### md5

`md5(expr)`:MD5 128비트 체크섬을 16진수 문자열로 반환합니다 `expr`.

예:

```sql
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`:오른쪽 `str`으로 채워져 있는 값 `pad` 을 반환합니다 `len`. 보다 `str` 긴 경우 반환 `len`값이 `len` 문자로 단축됩니다.

예

```sql
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### 트리밍

`rtrim(str)`:후행 공백 문자를 제거합니다 `str`.

`rtrim(trimStr, str)`:trim 문자열의 문자가 포함된 후행 문자열을 제거합니다 `str`.

인수:
- `str`:문자열 표현식
- `trimStr`:트리밍할 트리밍 문자열 문자입니다. 기본값은 단일 스페이스입니다

예

```sql
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### 샤

`sha(expr)`:해시 값을 `sha1` 16진수 문자열로 `expr`반환합니다.

예:

```sql
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`:해시 값을 `sha1` 16진수 문자열로 `expr`반환합니다.

예:

```sql
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`:SHA-2 제품군의 체크섬을 16진수 문자열로 반환합니다 `expr`. SHA-224, SHA-256, SHA-384 및 SHA-512가 지원됩니다. 비트 길이는 256과 같습니다.

예:

```sql
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### sounddex

`soundex(str)`:문자열의 Sounddex 코드를 반환합니다.

예:

```sql
> SELECT soundex('Miller');
 M460
```

#### 스택

`stack(n, expr1, ..., exprk)`:행들 `expr1`로, ... `exprk` 을 `n` 구분합니다.

예:

```sql
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`:길이가 길이이고 `str` 에서 시작하는 하위 문자열 `pos` 을 `len`반환하거나, 길이가 길이이고 다음으로 시작하는 바이트 배열 `pos` 의 하위 문자열을 반환합니다 `len`.

예

```sql
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### 하위 문자열

`substring(str, pos[, len])`:길이가 길이이고 `str` 에서 시작하는 하위 문자열 `pos` 을 `len`반환하거나, 길이가 길이이고 다음으로 시작하는 바이트 배열 `pos` 의 하위 문자열을 반환합니다 `len`.

예

```sql
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`:주어진 구조체 값이 있는 JSON 문자열을 반환합니다.

예

```sql
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

이후:2.2.0

#### 번역

`translate(input, from, to)`:문자열에 있는 문자를 문자열의 해당 문자로 바꾸어 문자열을 `input` `from` `to` 변환합니다.

예:

```sql
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`:선행 및 후행 공백 문자를 제거합니다 `str`.

`trim(BOTH trimStr FROM str)`:앞과 뒤 `trimStr` 문자를 제거합니다 `str`.

`trim(LEADING trimStr FROM str)`:행간 `trimStr` 문자를 제거합니다 `str`.

`trim(TRAILING trimStr FROM str)`:후행 `trimStr` 문자를 제거합니다 `str`.

인수:
- `str`:문자열 표현식
- `trimStr`:트리밍할 트리밍 문자열 문자이며 기본값은 단일 스페이스입니다
- `BOTH`, `FROM`:문자열 양끝에서 트리밍 문자열 문자를 지정하는 키워드입니다.
- `LEADING`, `FROM`:문자열 왼쪽 끝에서 트리밍 문자열 문자를 지정하는 키워드입니다
- `TRAILING`, `FROM`:문자열 오른쪽 끝에서 트리밍 문자열 문자를 지정하는 키워드입니다

예

```sql
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### 후부

`ucase(str)`:모든 문자 `str` 가 대문자로 변경된 경우를 반환합니다.

예:

```sql
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`:기본 64 문자열에서 바이너리로 인수 `str` 를 변환합니다.

예:

```sql
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### 16진수

`unhex(expr)`:16진수를 이진 `expr` 으로 변환합니다.

예:

```sql
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`:모든 문자 `str` 가 대문자로 변경된 경우를 반환합니다.

예:

```sql
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`:UUID(범용 고유 식별자) 문자열을 반환합니다. 이 값은 기본 UUID 36자 문자열로 반환됩니다.

예:

```sql
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE]
>
>함수는 결정적이지 않습니다.

### 데이터 평가 {#data-evaluation}

#### 코알스

`coalesce(expr1, expr2, ...)`:있을 경우 null이 아닌 첫 번째 인수를 반환합니다. 그렇지 않으면 null입니다.

예:

```sql
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_list

`collect_list(expr)`:고유하지 않은 요소 목록을 수집하고 반환합니다.

#### collect_set

`collect_set(expr)`:고유한 요소 집합을 수집하고 반환합니다.

#### concat

`concat(col1, col2, ..., colN)`:col1, col2, ..., colN의 연결을 반환합니다.

예

```sql
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE]
>
>`concat` 어레이에 대한 로직은 2.4.0부터 사용할 수 있습니다.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`:문자열 연결을 다음으로 `sep`반환합니다.

예:

```sql
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`:null을 포함하는 행을 포함하여 검색된 행의 총 수를 반환합니다.

`count(expr[, expr...])`:제공된 표현식이 모두 null이 아닌 행 수를 반환합니다.

`count(DISTINCT expr[, expr...])`:제공된 표현식이 고유하고 null이 아닌 행 수를 반환합니다.

#### crc32

`crc32(expr)`:중점 단위의 순환 중복 검사 값 `expr` 을 반환합니다.

예:

```sql
> SELECT crc32('Spark');
 1557323817
```

#### 디코딩

`decode(bin, charset)`:두 번째 인수 문자 집합을 사용하여 첫 번째 인수를 디코딩합니다.

예:

```sql
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)`:값이 2 `n`일 때 반환되는 숫자 입력(예: 값 `input2` ) `n` 을 반환합니다.

예:

```sql
> SELECT elt(1, 'scala', 'java');
 scala
```

#### 인코딩

`encode(str, charset)`:두 번째 인수 문자 집합을 사용하여 첫 번째 인수를 인코딩합니다.

예:

```sql
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`:행 그룹에 대한 첫 번째 값 `expr` 을 반환합니다. true `isIgnoreNull` 이면 null이 아닌 값만 반환합니다.

#### first_value

`first_value(expr[, isIgnoreNull])`:행 그룹에 대한 첫 번째 값 `expr` 을 반환합니다. true `isIgnoreNull` 이면 null이 아닌 값만 반환합니다.

#### get_json_object

`get_json_object(json_txt, path)`:json 개체를 추출합니다 `path`.

예:

```sql
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### 그룹화

<!-- was blank -->

#### grouping_id

<!-- was blank -->

#### instr

`instr(str, substr)`:에 있는 첫 번째 항목의 (1 기반) 인덱스 `substr` 를 `str`반환합니다.

예:

```sql
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`:함수 같은 튜브를 `get_json_object`반환하지만 여러 이름이 사용됩니다. 모든 입력 매개 변수와 출력 열 유형은 문자열입니다.

예:

```sql
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### 시차

`lag(input[, offset[, default]])`:창의 현재 행 앞 `input` 에 있는 행 `offset`의 값을 반환합니다. 기본값은 `offset` 1이고 기본값은 null `default` 입니다. 행 `input` 의 값이 null이면 `offset`null이 반환됩니다. 오프셋 행이 없는 경우(예: 오프셋이 1이면 창의 첫 번째 행에 이전 행이 없음) `default` 반환됩니다.

#### last

`last(expr[, isIgnoreNull])`:행 그룹에 대한 마지막 값 `expr` 을 반환합니다. true `isIgnoreNull` 이면 null이 아닌 값만 반환합니다.

#### last_value

`last_value(expr[, isIgnoreNull])`:행 그룹에 대한 마지막 값 `expr` 을 반환합니다. true `isIgnoreNull` 이면 null이 아닌 값만 반환합니다.

#### 리드

`lead(input[, offset[, default]])`:창의 현재 행 뒤 `input` 에 있는 행 `offset`의 값을 반환합니다. 기본값은 `offset` 1이고 기본값은 null `default` 입니다. 행 `input` 의 값이 null이면 `offset`null이 반환됩니다. 오프셋 행이 없는 경우(예: 오프셋이 1이면 창의 마지막 행에 후속 행이 없음), `default` 반환됩니다.


#### left

`left(str, len)`:문자열에서 가장 왼쪽 `len` (문자열 유형일 수`len` 있음)을 반환합니다 `str`. 0보다 `len` 작거나 같은 경우 결과는 빈 문자열입니다.

예:

```sql
> SELECT left('Spark SQL', 3);
 Spa
```

#### length

`length(expr)`:문자열 데이터의 문자 길이 또는 바이너리 데이터의 바이트 수를 반환합니다. 문자열 데이터의 길이에는 후행 공백이 포함됩니다. 이진 데이터의 길이에는 이진 0이 포함됩니다.

예

```sql
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### locate

`locate(substr, str[, pos])`:위치 `substr` 후 첫 번째 발생 `str` 의 위치를 반환합니다 `pos`. 주어진 값 `pos` 과 반환 값은 1입니다.

예

```sql
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`:지정된 모든 맵의 조합을 반환합니다.

예:

```sql
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

이후:2.4.0

#### map_keys

`map_keys(map)`:맵의 키가 포함된 순서가 없는 배열을 반환합니다.

예:

```sql
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`:맵의 값이 포함된 순서가 지정되지 않은 배열을 반환합니다.

예:

```sql
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)`:각 창 분할 영역에 대한 행을 1부터 `n` 최대 범위의 버킷으로 나눕니다 `n`.

#### 무효

`nullif(expr1, expr2)`:과 같은 경우 null을 `expr1` 반환하거나 `expr2``expr1` 그렇지 않은 경우 반환합니다.

예:

```sql
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`:null `expr2` 인 경우 또는 `expr1` 그렇지 않은 경우 `expr1` 반환합니다.

예:

```sql
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`:null이 `expr2` 아닌 경우 또는 `expr1` 그렇지 않은 경우 `expr3` 반환합니다.

예:

```sql
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`:URL에서 부분을 추출합니다.

예

```sql
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])`:위치 `substr` 후 첫 번째 발생 `str` 의 위치를 반환합니다 `pos`. 주어진 값 `pos` 과 반환 값은 1입니다.

예

```sql
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### 계급

`rank()`:값 그룹의 값 순위를 계산합니다. 그 결과 파티션의 순서에서 현재 행 앞에 하나 이상의 행이 있습니다. 이 값들은 시퀀스에서 간격을 생성합니다.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`:일치하는 그룹을 추출합니다 `regexp`.

예:

```sql
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`:일치하는 모든 하위 문자열 `str` 을 다음으로 `regexp` 바꿉니다 `rep`.

예:

```sql
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### 반복

`repeat(str, n)`:주어진 문자열 값을 n번 반복하는 문자열을 반환합니다.

예:

```sql
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`:모든 항목을 로 `search` 대체합니다 `replace`.

인수:
- `str`:문자열 표현식
- `search`:문자열 식입니다. 에서 `search` 를 찾을 수 없으면 `str`변경되지 `str` 않고 반환됩니다.
- `replace`:문자열 식입니다. 이 지정되지 `replace` 않았거나 빈 문자열인 경우, 제거되는 문자열이 아무것도 교체되지 않습니다 `str`.

예:

```sql
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### 롤업

<!-- was blank -->

#### row_number

`row_number()`:창 분할 영역 내의 행 순서에 따라 각 행에 고유한 순차적 번호를 할당합니다.

#### schema_of_json

`schema_of_json(json[, options])`:JSON 문자열의 DDL 형식으로 스키마를 반환합니다.

예:

```sql
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

이후:2.4.0

#### 문장

`sentences(str[, lang, country])`:일련의 단어 `str` 로 분할합니다.

예:

```sql
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### 시퀀스

`sequence(start, stop, step)`:시작부터 중지까지(포함) 요소 배열을 생성하여 단계별로 증가시킵니다. 반환된 요소의 유형은 인수 표현식 유형과 동일합니다.

지원되는 유형은 다음과 같습니다.byte, short, integer, long, date, timestamp.

`start` 및 `stop` 표현식은 동일한 유형으로 확인되어야 합니다. `start` 및 `stop` `step` 표현식이 &#39;date&#39; 또는 &#39;timestamp&#39; 유형으로 확인되는 경우 표현식이 &#39;interval&#39; 유형으로 확인되어야 합니다.그렇지 않으면 `start` 및 표현식과 동일한 유형으로 `stop` 결정됩니다.

인수:
- `start`:표현. 범위의 시작
- `stop`:표현. 범위(포함)의 끝입니다.
- `step`:선택적 표현식입니다. 범위의 단계입니다. 기본값 `step` 은 &#39;1&#39;이고 `start` 는 &#39;1&#39;이고, 그렇지 않으면 &#39; `stop`1&#39;입니다. 임시 시퀀스의 경우 각각 &#39;1&#39;일과 &#39;-1&#39;일입니다. 보다 `start` 큰 경우 `stop`음수여야 `step` 하며, 그 반대도 음수여야 합니다.

예

```sql
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval '1' month);
 [2018-01-01,2018-02-01,2018-03-01]
```

이후:2.4.0

#### 시프트

`shiftleft(base, expr)`:비트 왼쪽 시프트

예:

```sql
> SELECT shiftleft(2, 1);
 4
```

#### 시프트라이트

`shiftright(base, expr)`:비트(서명) 오른쪽 이동.

예:

```sql
> SELECT shiftright(4, 1);
 2
```

#### shiftrighttunsigned

`shiftrightunsigned(base, expr)`:비트 부호 없는 오른쪽 시프트.

예:

```sql
> SELECT shiftrightunsigned(4, 1);
 2
```

#### 크기

`size(expr)`:배열 또는 맵의 크기를 반환합니다. 이 함수는 입력한 내용이 null이고 true로 설정된 경우 -1 `spark.sql.legacy.sizeOfNull` 을 반환합니다. false `spark.sql.legacy.sizeOfNull` 로 설정된 경우 함수는 null 입력에 대해 null을 반환합니다. 기본적으로 매개 `spark.sql.legacy.sizeOfNull` 변수는 true로 설정됩니다.

예

```sql
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### 공간

`space(n)`:공백으로 구성된 문자열을 `n` 반환합니다.

예:

```sql
> SELECT concat(space(2), '1');
   1
```

#### split

`split(str, regex)`:일치하는 항목 `str` 을 기준으로 분할합니다 `regex`.

예:

```sql
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`:구분 기호가 나오기 `str` 전의 하위 문자열 `count` 을 반환합니다 `delim`. 긍정적인 경우 `count` 마지막 구분 기호(왼쪽에서 계산)의 왼쪽에 있는 모든 항목이 반환됩니다. 음수이면 마지막 구분 기호 오른쪽에 있는 모든 것(오른쪽에서 계산)이 반환됩니다. `count` 이 함수 `substring_index` 는 검색할 때 대/소문자 구분 일치를 수행합니다 `delim`.

예:

```sql
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### 창

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`:XPath 표현식과 일치하는 xml의 노드 내에 있는 값의 문자열 배열을 반환합니다.

예:

```sql
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_double

`xpath_double(xml, xpath)`:일치하는 값을 찾을 수 없는 경우 값 0을 반환하고, 일치하는 값이 발견되었지만 숫자가 아닌 경우에는 NaN을 반환합니다.

예:

```sql
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`:부동 값을 반환합니다. 일치하는 항목이 없으면 값 0을 반환하고, 일치하는 값이 있지만 값이 숫자가 아닌 경우에는 NaN을 반환합니다.

예:

```sql
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`:정수 값을 반환하거나 일치하는 값이 없거나 일치하는 값이 검색되었지만 숫자가 아닌 경우 값 0을 반환합니다.

예:

```sql
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`:긴 정수 값을 반환하거나 일치하는 값이 없거나 일치하는 값이 검색되었지만 숫자가 아닌 경우 값 0을 반환합니다.

예:

```sql
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`:일치하는 값을 찾을 수 없는 경우 값 0을 반환하고, 일치하는 값이 발견되었지만 숫자가 아닌 경우에는 NaN을 반환합니다.

예:

```sql
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`:짧은 정수 값을 반환하거나 일치하는 값이 없거나 일치하는 값이 검색되었지만 숫자가 아닌 경우 값 0을 반환합니다.

예:

```sql
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`:XPath 표현식과 일치하는 첫 번째 xml 노드의 텍스트 내용을 반환합니다.

예:

```sql
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### 현재 정보 {#current-information}

#### current_database

`current_database()`:현재 데이터베이스를 반환합니다.

예:

```sql
> SELECT current_database();
 default
```

#### current_date

`current_date()`:쿼리 평가가 시작될 때 현재 날짜를 반환합니다.

이후:1.5.0

#### current_timestamp

`current_timestamp()`:쿼리 평가 시작 시 현재 타임스탬프를 반환합니다.

이후:1.5.0

#### now

`now()`:쿼리 평가 시작 시 현재 타임스탬프를 반환합니다.

이후:1.5.0

### 높은 주문 함수 {#higher-order}

#### transform

`transform(array, lambdaExpression): array`

함수를 사용하여 배열의 요소를 변형합니다.

람다 함수에 두 개의 인수가 있는 경우 두 번째 인수는 요소의 인덱스를 의미합니다.

예:

```sql
> SELECT transform(array(1, 2, 3), x -> x + 1);
  [2,3,4]
> SELECT transform(array(1, 2, 3), (x, i) -> x + i);
  [1,3,5]
```


#### 존재

`exists(array, lambdaExpression returning Boolean): Boolean`

술어가 배열에 있는 하나 이상의 요소에 대해 보유하는지 테스트합니다.

예:

```sql
> SELECT exists(array(1, 2, 3), x -> x % 2 == 0);
  true
```

#### 필터

`filter(array, lambdaExpression returning Boolean): array`

주어진 조건자를 사용하여 입력 배열을 필터링합니다.

예:

```sql
> SELECT filter(array(1, 2, 3), x -> x % 2 == 1);
 [1,3]
```


#### aggregate

`aggregate(array, <initial accumulator value>, lambdaExpression to accumulate the value): array`

이진 연산자를 배열의 초기 상태와 모든 요소에 적용하고 단일 상태로 줄입니다. finish 함수를 적용하여 최종 상태가 최종 결과로 변환됩니다.

예:

```sql
> SELECT aggregate(array(1, 2, 3), 0, (acc, x) -> acc + x);
  6
> SELECT aggregate(array(1, 2, 3), 0, (acc, x) -> acc + x, acc -> acc * 10);
  60
```
