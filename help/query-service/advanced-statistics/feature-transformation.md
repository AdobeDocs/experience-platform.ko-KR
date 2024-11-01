---
title: 기능 변환 기법
description: 통계 모델 교육을 위한 데이터를 준비하는 데이터 변환, 인코딩 및 기능 스케일링과 같은 필수 사전 처리 기술에 대해 알아봅니다. 모델 성능과 정확도를 향상시키기 위해 결측치 처리 및 범주형 데이터 변환의 중요성에 대해 다룹니다.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '3437'
ht-degree: 8%

---

# 기능 변환 기법

변환은 데이터를 모델 교육 및 분석에 적합한 형식으로 변환하거나 크기를 조정하여 최적의 성능과 정확성을 보장하는 중요한 사전 처리 단계입니다. 이 문서는 보조 구문 리소스 역할을 하며, 데이터 사전 처리를 위한 주요 기능 변환 기법에 대한 자세한 내용을 제공합니다.

기계 학습 모델은 문자열 값이나 null 값을 직접 처리할 수 없어 데이터 사전 처리가 필수적이다. 이 안내서에서는 다양한 변환을 사용하여 누락된 값을 지정하고, 범주형 데이터를 숫자 형식으로 변환하고, 원핫 인코딩 및 벡터화와 같은 기능 확장 기술을 적용하는 방법에 대해 설명합니다. 이러한 방법을 통해 모델은 데이터를 효과적으로 해석하고 학습할 수 있으므로 궁극적으로 성능이 향상됩니다.

## 자동 기능 변환 {#automatic-transformations}

`CREATE MODEL` 명령에서 `TRANSFORM` 절을 건너뛰도록 선택하면 기능 변환이 자동으로 수행됩니다. 자동 데이터 사전 처리에는 null 대체 및 표준 기능 변환(데이터 유형 기반)이 포함됩니다. 숫자 및 텍스트 열이 자동으로 가져온 다음, 데이터가 머신 러닝 모델 교육에 적합한 포맷인지 확인하기 위해 기능 변환이 수행됩니다. 이 프로세스에는 누락된 데이터 처리와 범주별, 숫자 및 부울 변환이 포함됩니다.

>[!IMPORTANT]
>
>트레이닝 시에 사용된 특징 변환은 예측 및 평가 시의 특징 변환에도 사용될 것이다.

다음 표에서는 `CREATE MODEL` 명령 중에 `TRANSFORM` 절을 생략한 경우 다른 데이터 형식이 처리되는 방식을 설명합니다.

### Null 대체 {#automatic-null-replacement}

| 데이터 유형 | Null 대체 |
|-----------------|-----------------------------------------------------|
| 숫자 | Null은 열의 평균 값으로 대체됩니다. |
| 단정적으로 | Null은 `ml_unknown` 키워드로 대체됩니다. |
| 부울 | Null은 `FALSE` 값으로 대체됩니다. |
| 타임스탬프 | 이는 지속적인 필드가 될 것으로 예상됩니다. |
| 중첩/구조체 | 대체 항목은 리프 노드의 데이터 유형에 따라 다릅니다. |

### 기능 변환 {#automatic-feature-transformation}

| 데이터 유형 | 기능 변환 |
|-----------------|-----------------------------------------------------|
| 숫자 | 필수 아님 - 이 데이터 유형은 머신 러닝 알고리즘으로 이해되므로. |
| 문자열 | 문자열 인덱싱이 발생합니다. |
| 부울 | 문자열 인덱싱이 발생합니다. |
| 타임스탬프 | 작업이 수행되지 않습니다. |
| 구조 | 값이 리프 노드로 확장됩니다. 변환은 리프 노드의 데이터 형식을 기반으로 발생합니다. |

**예**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## 수동 기능 변환 {#manual-transformations}

`CREATE MODEL` 문에서 사용자 지정 데이터 사전 처리를 정의하려면 `TRANSFORM` 절을 사용 가능한 변환 함수와 함께 사용합니다. 이러한 수동 사전 처리 기능은 `TRANSFORM` 절 외부에서 사용할 수도 있습니다. 아래 [변환기 섹션](#available-transformations)에서 설명한 모든 변환을 사용하여 데이터를 수동으로 사전 처리할 수 있습니다.

### 주요 특성

다음은 전처리 함수를 정의할 때 고려할 기능 변환의 주요 특성입니다.

- **구문**: `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - 별칭 이름은 구문에서 필수입니다. 별칭 이름을 제공해야 합니다. 그렇지 않으면 쿼리가 실패합니다.

- **매개 변수**: 매개 변수는 위치 인수입니다. 즉, 각 매개 변수는 특정 값만 사용할 수 있습니다. 어떤 함수가 어떤 인수를 사용하는지에 대한 자세한 내용은 관련 설명서를 참조하십시오.

- **변환기 연결**: 한 변환기의 출력이 다른 변환기에 대한 입력이 될 수 있습니다.

- **기능 사용**: 마지막 기능 변환이 머신 러닝 모델의 기능으로 사용됩니다.

**예**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## 사용 가능한 변형 {#available-transformations}

사용 가능한 변형은 19개입니다. 이러한 변환은 [일반 변환](#general-transformations), [숫자 변환](#numeric-transformations), [범주형 변환](#categorical-transformations) 및 [텍스트 변환](#textual-transformations)으로 분할됩니다.

### 일반 변형 {#general-transformations}

다양한 데이터 유형에 사용되는 변환기에 대한 자세한 내용은 이 섹션을 참조하십시오. 범주형 또는 텍스트 데이터에 특정되지 않은 변환을 적용해야 하는 경우 이 정보가 필수적입니다.

>[!NOTE]
>
>입력 데이터 유형은 위임이 적용되는 열을 나타냅니다. 출력 데이터 형식은 변환이 적용된 후 출력으로 생성되는 열을 나타냅니다.

#### 숫자 컴퓨터 {#numeric-imputer}

**숫자 컴퓨터** 변환기가 데이터 집합에 누락된 값을 완료합니다. 누락된 값이 있는 열의 평균, 중간값 또는 모드를 사용합니다. 입력 열은 `DoubleType` 또는 `FloatType`이어야 합니다. 자세한 내용과 예제는 [Spark 알고리즘 설명서](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer)에서 확인할 수 있습니다.

>[!NOTE]
>
>입력 열의 모든 null 값은 누락된 것으로 처리되므로 귀속됩니다.

**데이터 유형**

- 입력 데이터 유형: 숫자
- 출력 데이터 형식: 숫자

**정의**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | 귀책 전략. 사용 가능한 값은 [`mean`, `median`, `mode`]입니다. | 문자열 | 평균 | 선택 사항 |

{style="table-layout:auto"}

**전제 예시**

| ID | 시간 |
|---|---|
| 0 | 18.0 |
| 1 | null |
| 2 | 8.0 |

**귀속 후 예제(평균 전략 사용)**

| ID | 시간 |
|---|---|
| 0 | 18.0 |
| 1 | 13.0 |
| 2 | 8.0 |

#### 문자열 컴퓨터 {#string-imputer}

**문자열 컴퓨터** 변환기는 사용자가 함수 인수로 제공한 문자열을 사용하여 데이터 집합에 누락된 값을 완료합니다. 입력 및 출력 열은 `string` 데이터 형식이어야 합니다.

>[!NOTE]
>
>입력 열의 모든 null 값은 누락된 것으로 처리되고 지정된 문자열로 대체됩니다.

**데이터 유형**

- 입력 데이터 형식: 문자열
- 출력 데이터 형식: 문자열

**정의**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Null을 바꾸는 값입니다. | 문자열 | ml_unknown | 선택 사항 |

{style="table-layout:auto"}

**전제 예시**

| ID | 이름 |
|---|---|
| 0 | John |
| 1 | null |
| 2 | 앨리스 |

**전제 후의 예(대체 항목으로 &#39;ml_unknown&#39; 사용)**

| ID | 이름 |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | 앨리스 |

#### 부울 컴퓨터 {#imputer}

**부울 컴퓨터** 변환기가 부울 열에 대한 데이터 집합에서 누락된 값을 완료합니다. 입력 및 출력 열은 `Boolean` 형식이어야 합니다.

>[!NOTE]
>
>입력 열의 모든 null 값은 누락된 것으로 처리되고 지정된 부울 값으로 대체됩니다.

**데이터 유형**

- 입력 데이터 유형: 부울
- 출력 데이터 형식: 부울

**정의**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | 부울 컴퓨터입니다. 허용되는 값: [`true`, `false`]. | 부울 | false | 선택 사항 |

**전제 예시**

| ID | 플래그 |
|---|---|
| 0 | true |
| 1 | null |
| 2 | false |

**귀속 후의 예(대체 값으로 &#39;true&#39; 사용)**

| ID | 플래그 |
|---|---|
| 0 | true |
| 1 | true |
| 2 | false |

#### 벡터 어셈블러 {#vector-assembler}

`VectorAssembler` 변환기는 지정된 입력 열 목록을 단일 벡터 열에 결합하므로 머신 러닝 모델의 여러 기능을 보다 쉽게 관리할 수 있습니다. 이 기능은 원시 피쳐와 다른 피쳐 변환기에서 생성된 피쳐를 하나의 통합 피쳐 벡터로 병합하는 데 특히 유용합니다. `VectorAssembler`은(는) 숫자, 부울 및 벡터 형식의 입력 열을 허용합니다. 각 행에서 입력 열의 값은 지정된 순서로 벡터에 연결됩니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**데이터 유형**

- 입력 데이터 형식: `array[string]`(numeric/array[numeric] 값이 있는 열 이름)
- 출력 데이터 형식: `Vector[double]`

**정의**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
| -------- | ------------ | ----- | -------- | -------- |
| 해당 없음 | 이 변환기에는 추가 매개 변수가 필요하지 않습니다. | 해당 없음 | 해당 없음 | 해당 없음 |

{style="table-layout:auto"}

**변환 전 예제**

| ID | 시간 | mobile | 사용자 기능 | 클릭함 |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1.0 | [0.0, 10.0, 0.5] | 1.0 |

{style="table-layout:auto"}

**변환 후 예제**

| ID | 시간 | mobile | 사용자 기능 | 클릭함 | 기능 |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1.0 | [0.0, 10.0, 0.5] | 1.0 | [18.0, 1.0, 0.0, 10.0, 0.5] |

{style="table-layout:auto"}

### 숫자 변형 {#numeric-transformations}

수치 데이터를 처리하고 크기를 조정할 수 있는 사용 가능한 변환기에 대해 알아보려면 이 섹션을 참조하십시오. 이러한 변환기는 데이터 세트에서 숫자 기능을 처리하고 최적화하는 데 필요합니다.

#### 이나이저 {#binarizer}

`Binarizer` 변환기는 이진화라는 프로세스를 통해 숫자 기능을 이진(0/1) 기능으로 변환합니다. 지정된 임계값보다 큰 피쳐 값은 1.0으로 변환되지만 임계값보다 작거나 같은 값은 0.0으로 변환됩니다. `Binarizer`은(는) 입력 열에 대해 `Vector` 및 `Double` 형식을 모두 지원합니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**데이터 유형**

- 입력 데이터 유형: 숫자 열
- 출력 데이터 형식: 숫자

**정의**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | 연속 피쳐를 이진화하는 데 사용되는 임계값의 매개변수입니다. 임계값보다 큰 피쳐는 1.0으로 이진화되고 임계값보다 작거나 같은 피쳐는 0.0으로 이진화됩니다. | int/double | 0.0 | 선택 사항 |

{style="table-layout:auto"}

**이진화 전 입력 예**

| ID | 등급 |
|---|---------|
| 0 | -18.0 |
| 1 | 13.0 |
| 2 | 8.0 |

**이진화 후 출력 예(기본 임계값 0.0)**

| ID | 등급 |
|---|---------|
| 0 | 0.0 |
| 1 | 1.0 |
| 2 | 1.0 |

**사용자 지정 임계값이 있는 정의**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**이진화 후 출력 예(임계값 14.0)**

| ID | 나이 |
|---|-------|
| 0 | 0.0 |
| 1 | 0.0 |
| 2 | 1.0 |

#### 버킷타이저 {#bucketizer}

`Bucketizer` 변환기는 사용자 지정 임계값을 기반으로 연속 기능의 열을 기능 버킷의 열로 변환합니다. 이 프로세스는 연속 데이터를 개별 빈 또는 버킷으로 세그먼트화하는 데 유용합니다. `Bucketizer`에는 버킷의 경계를 정의하는 `splits` 매개 변수가 필요합니다.

**데이터 유형**

- 입력 데이터 유형: 숫자 열
- 출력 데이터 유형: 숫자(바인딩된 값)

**정의**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | 연속 피쳐를 버킷에 매핑하기 위한 매개변수입니다. `n+1` 분할을 사용하면 `n` 버킷이 있습니다. 분할은 엄격하게 증가하는 순서여야 하며, 범위(x,y)는 y가 포함된 마지막 버켓을 제외한 각 버켓에 사용됩니다. | array(double) | N/A | 선택 사항 |

{style="table-layout:auto"}

**분할의 예**

- 배열(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- 배열(0.0, 1.0, 2.0)

분할은 Double 값의 전체 범위를 포함해야 합니다. 그렇지 않으면 지정된 분할 외부의 값이 오류로 처리됩니다.

**변환 예**

이 예제에서는 연속 기능(`course_duration`) 열을 가져와서 제공된 `splits`에 따라 비운 다음 결과 버킷을 다른 기능과 어셈블합니다.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

`MinMaxScaler` 변환기는 벡터 행 데이터 집합에 있는 각 기능을 지정된 범위(일반적으로 [0, 1])로 다시 계산합니다. 이렇게 하면 모든 기능이 모델에 동일하게 기여할 수 있습니다. 이는 특히 구배 하강 기반 알고리즘과 같은 피쳐 스케일링에 민감한 모델에 유용하다. `MinMaxScaler`은(는) 다음 매개 변수에서 작동합니다.

- **분**: 모든 기능이 공유하는 변환의 하한입니다. 기본값은 `0.0`입니다.
- **max**: 모든 기능이 공유하는 변환의 상한입니다. 기본값은 `1.0`입니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**데이터 유형**

- 입력 데이터 형식: `Array[Double]`
- 출력 데이터 형식: `Array[Double]`

**정의**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | 변환 후 하한, 모든 기능에 의해 공유됨. | 중복 | 0.0 | 선택 사항 |
| `max` | 변환 후 상한값, 모든 기능에 의해 공유됩니다. | 중복 | 1.0 | 선택 사항 |

**변환 예**

이 예제에서는 여러 가지 다른 변형을 적용한 후 MinMaxScaler를 사용하여 지정된 범위로 크기 조절하면서 기능 집합을 변환합니다.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

`MaxAbsScaler` 변환기는 각 기능의 최대 절대값으로 나누어 벡터 행 데이터 집합에서 각 기능을 [-1, 1] 범위로 다시 계산합니다. 이 변환은 데이터를 이동하거나 중심에 두지 않으므로 양수 값과 음수 값을 모두 사용하는 데이터 세트의 희소성을 유지하는 데 이상적입니다. 따라서 `MaxAbsScaler`은(는) 거리 계산과 관련된 모델과 같이 입력 기능의 크기에 민감한 모델에 특히 적합합니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**데이터 유형**

- 입력 데이터 형식: `Array[Double]`
- 출력 데이터 형식: `Array[Double]`

**정의**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| 해당 없음 | MaxAbsScaler는 작업에 추가 매개 변수가 필요하지 않습니다. | 해당 없음 | 해당 없음 | 해당 없음 |

**변환 예**

이 예제에서는 `MaxAbsScaler`을(를) 포함한 몇 가지 변환을 적용하여 기능을 [-1, 1] 범위로 크기 조정합니다.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### 정규화기 {#normalizer}

`Normalizer`은(는) 벡터 행의 데이터 집합에서 각 벡터를 정규화하여 단위 norm을 갖는 변환기입니다. 이 프로세스는 벡터의 방향을 변경하지 않고 일관된 스케일을 보장한다. 이 변환은 특히 벡터의 크기가 크게 다를 때 거리 측정값이나 다른 벡터 기반 계산에 의존하는 머신 러닝 모델에 특히 유용합니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**데이터 유형**

- 입력 데이터 형식: `array[double]` / `vector[double]`
- 출력 데이터 형식: `vector[double]`

**정의**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | 정규화에 사용되는 `p-norm`을(를) 지정합니다(예: `1-norm`, `2-norm` 등). | 정수 | 2 | 선택 사항 |

**변환 예**

이 예제에서는 지정된 `p-norm`을(를) 사용하여 기능 집합을 정규화하기 위해 `Normalizer`을(를) 비롯한 여러 변환을 적용하는 방법을 보여 줍니다.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### 분위분할자 {#quantilediscretizer}

`QuantileDiscretizer`은(는) 연속 기능이 있는 열을 빈 범주 기능으로 변환하는 변환기이며, 빈 수는 `numBuckets` 매개 변수에 의해 결정됩니다. 경우에 따라 충분한 수량을 만들 수 있는 고유 값이 너무 적은 경우 실제 버킷 수는 지정된 수보다 작을 수 있습니다.

이러한 변환은 연속 데이터의 표현을 단순화하거나 범주형 입력으로 더 잘 작동하는 알고리즘을 준비하는데 특히 유용하다.

**데이터 유형**

- 입력 데이터 유형: 숫자 열
- 출력 데이터 유형: 숫자 열(범주)

**정의**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | 데이터 포인트가 그룹화되는 버킷(수량 또는 카테고리) 수입니다. 이 숫자는 2보다 크거나 같아야 합니다. | 정수 | 2 | 선택 사항 |

**변환 예**

이 예에서는 `QuantileDiscretizer`이(가) 연속 기능(`hour`) 열을 세 개의 범주 버킷으로 비우는 방법을 보여 줍니다.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**분할하기 전과 후의 예**

| ID | 시간 | 결과 |
|---|------|--------|
| 0 | 18.0 | 2.0 |
| 1 | 19.0 | 2.0 |
| 2 | 8.0 | 1.0 |
| 3 | 5.0 | 1.0 |
| 4 | 2.2 | 0.0 |

#### StandardScaler {#standardscaler}

`StandardScaler`은(는) 벡터 행의 데이터 집합에서 각 특성을 표준화하여 단위 표준 편차 및/또는 평균 0을 갖는 변환기입니다. 이 과정은 특징이 일관된 척도로 0의 중심에 있다고 가정하는 알고리즘에 데이터를 더 적합하도록 한다. 이러한 변환은 SVM, 로지스틱 회귀 및 신경망과 같은 머신 러닝 모델에 특히 중요하며, 표준화되지 않은 데이터가 융합 문제를 일으키거나 정확도를 감소시킬 수 있습니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**데이터 유형**

- 입력 데이터 형식: 벡터
- 출력 데이터 형식: 벡터

**정의**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | 단위 표준 편차를 갖도록 데이터 크기를 조정합니다. | 부울 | True | 선택 사항 |
| `withMean` | 데이터를 크기 조정 전의 평균으로 가운데로 맞춥니다. 이 옵션은 고밀도 출력을 생성하므로 스파스 입력에 주의하십시오. | 부울 | False | 선택 사항 |

**변환 예**

이 예에서는 StandardScaler를 피쳐 집합에 적용하여 단위 표준 편차와 평균 0으로 정규화하는 방법을 보여 줍니다.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### 범주별 변형 {#categorical-transformations}

머신 러닝 모델용 범주형 데이터를 변환하고 사전 처리하도록 설계된 사용 가능한 변환기에 대한 개요는 이 섹션 을 참조하십시오. 이러한 변환은 숫자 값이 아닌 고유한 카테고리 또는 레이블을 나타내는 데이터 포인트를 위해 설계되었습니다.

#### StringIndex {#stringindexer}

`StringIndexer`은(는) 레이블의 문자열 열을 숫자 인덱스 열로 인코딩하는 변환기입니다. 인덱스의 범위는 0 ~ `numLabels`이며 레이블 빈도별로 정렬됩니다(가장 자주 사용하는 레이블은 인덱스 0을 받습니다). 입력 열이 숫자인 경우 색인화되기 전에 문자열로 캐스팅됩니다. 사용자가 지정한 경우 보이지 않는 레이블을 `numLabels` 인덱스에 할당할 수 있습니다.

이러한 변환은 범주형 문자열 데이터를 숫자 형태로 변환하여 수치 입력이 필요한 기계 학습 모델에 적합하도록 하는 데 특히 유용하다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**데이터 유형**

- 입력 데이터 형식: 문자열
- 출력 데이터 형식: 숫자

**정의**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------|-------------|------|---------|----------|
| 해당 없음 | `StringIndexer` 작업에는 추가 매개 변수가 필요하지 않습니다. | 해당 없음 | 해당 없음 | 해당 없음 |

**변환 예**

이 예제에서는 `StringIndexer`을(를) 숫자 인덱스로 변환하여 카테고리별 기능에 적용하는 방법을 보여 줍니다.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

`OneHotEncoder`은(는) 레이블 인덱스의 열을 스파스 이진 벡터의 열로 변환하는 변환기이며, 각 벡터에는 최대 하나의 값이 있습니다. 이 인코딩은 로지스틱 회귀와 같이 숫자 입력이 필요한 알고리즘이 범주 데이터를 효과적으로 통합할 수 있도록 하는 데 특히 유용합니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**데이터 유형**

- 입력 데이터 유형: 숫자
- 출력 데이터 형식: Vector[Int]

**정의**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------|-------------|------|---------|----------|
| 해당 없음 | OneHotEncoder 작업에는 추가 매개 변수가 필요하지 않습니다. | 해당 없음 | 해당 없음 | 해당 없음 |

**변환 예**

이 예제에서는 먼저 `StringIndexer`을(를) 범주별 기능에 적용한 다음 `OneHotEncoder`을(를) 사용하여 인덱싱된 값을 이진 벡터로 변환하는 방법을 보여 줍니다.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### 텍스트 변형 {#textual-transformations}

이 섹션에서는 텍스트 데이터를 처리하고 머신 러닝 모델에서 사용할 수 있는 형식으로 변환하는 데 사용할 수 있는 변환기에 대해 자세히 설명합니다. 이 섹션은 자연어 데이터 및 텍스트 분석으로 작업하는 개발자에게 중요합니다.

#### CountVectorizer {#countvectorizer}

`CountVectorizer`은(는) 텍스트 문서 컬렉션을 토큰 수의 벡터로 변환하여 말뭉치에서 추출된 어휘를 기반으로 스파스 표현을 생성하는 변환기입니다. 이 변환은 텍스트 데이터를 각 문서 내의 토큰 빈도를 표시하여 LDA(Latent Dirichlet Allocation)와 같은 머신 러닝 알고리즘에서 사용할 수 있는 숫자 형식으로 변환하는 데 필수적입니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**데이터 유형**

- 입력 데이터 형식: 배열[문자열]
- 출력 데이터 형식: 덴스 벡터

**정의**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | 어휘의 최대 크기입니다. CountVectorizer는 말뭉치의 용어 빈도별로 정렬된 상위 `vocabSize`개 용어만 고려하는 어휘를 만듭니다. | 정수 | 218 | 선택 사항 |
| `MIN_DOC_FREQ` | 용어가 어휘에 포함되기 위해 표시되어야 하는 서로 다른 문서의 최소 수를 지정합니다. 는 문서의 절대 수나 일부일 수 있습니다(2배일 경우). | 더블 | 1.0 | 선택 사항 |
| `MAX_DOC_FREQ` | 용어가 어휘에 포함될 수 있는 다양한 문서의 최대 수를 지정합니다. 는 문서의 절대 수나 일부일 수 있습니다(2배일 경우). | 더블 | (263)-1 | 선택 사항 |
| `MIN_TERM_FREQ` | 문서에서 희귀 단어를 필터링합니다. 빈도/카운트가 지정된 임계값보다 작은 용어는 무시됩니다. 는 문서 토큰 수의 절대 수나 일부일 수 있습니다. | 더블 | 1.0 | 선택 사항 |

{style="table-layout:auto"}

**변환 예**

이 예제에서는 CountVectorizer가 텍스트 배열 컬렉션을 토큰 수의 벡터로 변환하여 스파스 표현을 생성하는 방법을 보여 줍니다.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**벡터화 전후의 예제**

| ID | 텍스트 | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;) | (3,[0,1,2],[1.0,1.0,1.0]) |
| 1 | Array(&quot;a&quot;, &quot;b&quot;, &quot;b&quot;, &quot;c&quot;, &quot;a&quot;) | (3,[0,1,2],[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

`NGram`은(는) n그램 시퀀스를 생성하는 변환기이며, 여기서 n그램은 일부 정수(`𝑛`)에 대한 (&#39;??&#39;) 토큰 시퀀스(일반적으로 단어)입니다. 출력은 &#39;??&#39; 연속 단어의 공백으로 구분된 문자열로 구성되며 기계 학습 모델, 특히 자연어 처리에 중점을 둔 기능에서 기능으로 사용할 수 있습니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**데이터 유형**

- 입력 데이터 형식: 배열[문자열]
- 출력 데이터 형식: 배열[문자열]

**정의**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | 최소 n그램 길이는 1보다 크거나 같아야 합니다. | 정수 | 2(bigram 기능) | 선택 사항 |

{style="table-layout:auto"}

**변환 예**

이 예는 NGram 변환기가 텍스트 데이터에서 파생된 토큰 목록에서 3-그램의 시퀀스를 생성하는 방법을 보여줍니다.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**n그램 변환 전후의 예**

| ID | 텍스트 | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;this&quot;, &quot;was&quot;, &quot;an&quot;, &quot;entering&quot;, &quot;movie&quot;] | [&quot;이(가) &quot;an&quot;, &quot;was a entertaining&quot;, &quot;a entertaining movie&quot;] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

`StopWordsRemover`은(는) 일련의 문자열에서 정지어를 제거하여 중요한 의미를 갖지 않는 일반적인 단어를 필터링하는 변환기입니다. 문자열 시퀀스(예: 토큰화 장치의 출력)를 입력으로 사용하여 `stopWords` 매개 변수로 지정된 모든 정지어를 제거합니다.

이 변환은 텍스트 데이터를 전처리하는 데 유용하며, 전체 의미에 크게 기여하지 않는 단어를 제거하여 다운스트림 머신 러닝 모델의 효과를 향상시킵니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**데이터 유형**

- 입력 데이터 형식: 배열[문자열]
- 출력 데이터 형식: 배열[문자열]

**정의**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | 필터링할 단어입니다. | 배열 [문자열] | 기본값: 영어 정지어 | 선택 사항 |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**변환 예**

이 예제에서는 `StopWordsRemover`이(가) 토큰 목록에서 일반적인 영어 정지어를 필터링하는 방법을 보여 줍니다.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**정지어 제거 전후의 예**

| ID | raw | 필터링됨 |
|----|------------------------------|--------------------------|
| 0 | [보기, 빨강, 풍선] | [톱, 빨강, 풍선] |
| 1 | [마리, 가졌음, 조금, 어린 양] | [마리, 새끼, 양] |

**사용자 지정 정지어 예제**

이 예에서는 사용자 정의 정지어 목록을 사용하여 입력 시퀀스에서 특정 단어를 필터링하는 방법을 보여 줍니다.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**사용자 지정 정지어 제거 전후의 예**

| ID | raw | 필터링됨 |
|----|------------------------------|--------------------------|
| 0 | [보기, 빨강, 풍선] | [보기, 풍선] |
| 1 | [마리, 가졌음, 조금, 어린 양] | [마리, 조금, 어린 양] |

#### TF-IDF {#tf-idf}

`TF-IDF`(용어 빈도-역 문서 빈도)은 문서 내의 단어의 중요도를 말뭉치와 관련하여 측정하는 데 사용되는 변환기입니다. TF(용어 빈도)는 \(t\) 용어가 문서 \(d\)에 표시되는 횟수를 나타내는 반면 DF(문서 빈도)는 \(t\) 용어가 포함된 문서 \(D\)의 문서 수를 측정합니다. 이 방법은 &quot;a&quot;, &quot;the&quot;, &quot;of&quot;와 같이 고유한 정보를 거의 전달하지 않는 일반적으로 발생하는 단어의 영향을 줄이기 위해 텍스트 마이닝에서 널리 사용됩니다.

이 변환은 문서 내에서 그리고 전체 말뭉치에서 각 단어의 중요도에 숫자 값을 지정하므로 텍스트 마이닝 및 자연어 처리 작업에서 특히 중요합니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**데이터 유형**

- 입력 데이터 형식: 배열[문자열]
- 출력 데이터 형식: Vector[Int]

**정의**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | 생성할 기능의 수입니다. 0보다 커야 합니다. | 정수 | 262144 | 선택 사항 |
| `MIN_DOC_FREQ` | 모델에 반드시 포함되어야 하는 용어가 포함된 최소 문서 수입니다. | 정수 | 0 | 선택 사항 |

{style="table-layout:auto"}

**변환 예**

이 예제에서는 TF-IDF를 사용하여 토큰화된 문장을 전체 말뭉치의 컨텍스트에서 각 용어의 중요성을 나타내는 특징 벡터로 변환하는 방법을 보여 줍니다.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### 토큰화기 {#tokenizer}

`Tokenizer`은(는) 문장과 같은 텍스트를 개별 용어(일반적으로 단어)로 분류하는 변환기입니다. 문장을 토큰의 배열로 전환하여 추가적인 텍스트 분석이나 모델링 프로세스를 위해 데이터를 준비하는 텍스트 사전 처리의 기본 단계를 제공합니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**데이터 유형**

- 입력 데이터 형식: 텍스트 문장
- 출력 데이터 형식: 배열[문자열]

**정의**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|-----------|-------------|------|---------|----------|
| 해당 없음 | `Tokenizer` 작업에는 추가 매개 변수가 필요하지 않습니다. | 해당 없음 | 해당 없음 | 해당 없음 |

**변환 예**

이 예제에서는 `Tokenizer`이(가) 텍스트 처리 파이프라인의 일부로 문장을 개별 단어(토큰)로 분류하는 방법을 보여 줍니다.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

`Word2Vec`은(는) 문서를 나타내는 단어 시퀀스를 처리하고 `Word2VecModel`을(를) 교육하는 견적 도구입니다. 이 모델은 각 단어를 고유한 고정 크기 벡터로 매핑하고 문서 내 모든 단어의 벡터를 평균하여 각 문서를 벡터로 변환합니다. 자연어 처리 작업에 널리 사용되는 `Word2Vec`은(는) 의미론적 의미를 캡처하는 단어 임베딩을 만들어 텍스트 데이터를 단어 간의 관계를 나타내는 숫자 벡터로 변환하고 보다 효과적인 텍스트 분석 및 머신 러닝 모델을 가능하게 합니다.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**데이터 유형**

- 입력 데이터 형식: 배열[문자열]
- 출력 데이터 형식: Vector[Double]

**정의**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**매개 변수**

| 매개변수 | 설명 | 유형 | 기본 | 선택 사항입니다 |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | 각 단어가 변형되는 벡터의 치수입니다. | 정수 | 10 | 선택 사항 |
| `MIN_COUNT` | 토큰이 `Word2Vec` 모델의 어휘에 포함되어야 하는 최소 횟수입니다. | 정수 | 5 | 선택 사항 |

{style="table-layout:auto"}

**변환 예**

이 예제에서는 `Word2Vec`이(가) 토큰화된 검토를 문서에 있는 단어 벡터의 평균을 나타내는 고정 크기 벡터로 변환하는 방법을 보여 줍니다.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Word2Vec 변환 전후의 예**

| 리뷰 | 토큰화됨 | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| 이것은 재미있는 영화였다 | [이, 정말, 재밌는 영화였어] | [-0.025713888928294182,0.00818799751577899,0.0092235435731709,-0.01515385233797133,0.012175946310162545,3.1129065901041035E-4,0.0025145105042611252,0.005757019785232843,-0.021328244300093502,0.009335877187550069] |

{style="table-layout:auto"}
