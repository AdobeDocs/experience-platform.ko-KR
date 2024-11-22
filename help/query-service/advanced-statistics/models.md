---
title: 모델
description: Data Distiller SQL 확장 기능으로 라이프사이클 관리 모델링 모델 버전 관리, 평가 및 예측과 같은 주요 프로세스를 포함하여 SQL을 사용하여 고급 통계 모델을 생성, 교육 및 관리하여 데이터에서 실행 가능한 통찰력을 도출하는 방법에 대해 알아봅니다.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 6a61900b19543f110c47e30f4d321d0016b65262
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 1%

---

# 모델

>[!AVAILABILITY]
>
>이 기능은 Data Distiller 추가 기능을 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

이제 쿼리 서비스가 모델을 구축하고 배포하는 핵심 프로세스를 지원합니다. SQL을 사용하여 데이터를 사용하여 모델을 교육하고 정확도를 평가한 다음 교육 모델을 적용하여 새 데이터에 대한 예측을 수행할 수 있습니다. 그런 다음 모델을 사용하여 과거 데이터에서 일반화하여 실제 시나리오에 대한 정보에 입각한 결정을 내릴 수 있습니다.

실행 가능한 통찰력을 생성하기 위한 모델 라이프사이클의 세 단계는 다음과 같습니다.

1. **교육**: 모델이 제공된 데이터 집합에서 패턴을 학습합니다. (모델 만들기 또는 바꾸기)
2. **테스트/평가**: 모델의 성능은 별도의 데이터 세트를 사용하여 평가됩니다. (`model_evaluate`)
3. **예측**: 훈련된 모델은 새로운 확인되지 않은 데이터에 대한 예측을 수행하는 데 사용됩니다.

기존 SQL 문법에 추가된 모델 SQL 확장을 사용하여 비즈니스 요구에 따라 모델 라이프사이클을 관리합니다. 이 문서에서는 모델 만들기 또는 바꾸기, 교육, 평가, 필요한 경우 재교육 및 통찰력 예측에 필요한 SQL을 다룹니다.

## 모델 생성 및 교육 {#create-and-train}

SQL 명령을 사용하여 머신 러닝 모델을 정의, 구성 및 교육하는 방법에 대해 알아봅니다. 아래 SQL에서는 모델을 만들고, 기능 엔지니어링 변환을 적용하고, 교육 프로세스를 시작하여 나중에 사용할 수 있도록 모델이 올바르게 구성되도록 하는 방법을 보여 줍니다. 다음 SQL 명령은 모델 생성 및 관리를 위한 다양한 옵션을 자세히 설명합니다.

- **모델 만들기**: 지정한 데이터 집합에 새 모델을 만들고 교육합니다. 같은 이름의 모델이 이미 있으면 이 명령은 오류를 반환합니다.
- **없는 경우 모델 만들기**: 지정한 데이터 집합에 이름이 같은 모델이 없는 경우에만 새 모델을 만들고 교육합니다.
- **CREATE OR REPLACE MODEL**: 모델을 만들고 교육합니다. 지정된 데이터 세트에 있는 동일한 이름으로 기존 모델의 최신 버전을 바꿉니다.

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**예**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

모델 생성 및 교육 프로세스의 주요 구성 요소와 구성을 이해하는 데 도움이 되도록 위의 SQL 예에서 각 요소의 목적과 기능을 설명하는 참고 사항이 있습니다.

- `<model_alias>`: 모델 별칭은 모델에 할당된 재사용 가능한 이름이며 나중에 참조할 수 있습니다. 모델의 이름을 지정해야 합니다.
- `transform`: 모델 교육 전에 기능 엔지니어링 변환(예: 핫형 인코딩 및 문자열 인덱싱)을 데이터 집합에 적용하는 데 transform 절을 사용합니다. `TRANSFORM` 문의 마지막 절은 모델 교육에 대한 기능을 구성하는 열 목록이 있는 `vector_assembler` 또는 `vector_assembler`의 파생 형식(`max_abs_scaler(feature)`, `standard_scaler(feature)` 등)이어야 합니다. 마지막 절에 언급된 열만 교육에 사용됩니다. `SELECT` 쿼리에 포함되더라도 다른 모든 열은 제외됩니다.
- `label = <label-COLUMN>`: 모델이 예측하려는 대상 또는 결과를 지정하는 교육 데이터 집합의 레이블 열입니다.
- `training-dataset`: 이 구문은 모델 교육에 사용되는 데이터를 선택합니다.
- `type = 'LogisticRegression'`: 이 구문은 사용할 기계 학습 알고리즘의 유형을 지정합니다. 옵션에는 `LinearRegression`, `LogisticRegression` 및 `KMeans`이(가) 있습니다.
- `options`: 이 키워드는 모델을 구성하는 유연한 키-값 쌍 집합을 제공합니다.
   - `Key model_type`: `model_type = '<supported algorithm>'`: 사용할 기계 학습 알고리즘의 유형을 지정합니다. 지원되는 옵션은 `LinearRegression`, `LogisticRegression` 및 `KMeans`입니다.
   - `Key label`: `label = <label_COLUMN>`: 모델이 예측하려는 대상 또는 결과를 나타내는 레이블 열을 교육 데이터 집합에 정의합니다.

SQL을 사용하여 교육에 사용되는 데이터 세트를 참조합니다.

## 모델 업데이트 {#update}

새로운 기능 엔지니어링 변환을 적용하고 알고리즘 유형 및 레이블 열과 같은 옵션을 구성하여 기존 머신 러닝 모델을 업데이트하는 방법에 대해 알아봅니다. 각 업데이트에서는 마지막 버전에서 증분된 새로운 버전의 모델을 만듭니다. 이렇게 하면 변경 사항이 추적되고 모델이 향후 평가 또는 예측 단계에서 재사용될 수 있습니다.

다음 예제에서는 새 변형 및 옵션을 사용하여 모델을 업데이트하는 방법을 보여 줍니다.

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**예**

버전 관리 프로세스를 이해하는 데 도움이 되도록 다음 명령을 고려하십시오.

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

이 명령이 실행되면 아래 표와 같이 모델에 새 버전이 생깁니다.

| 업데이트된 모델 ID | 업데이트된 모델 | 새 버전 |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

다음 주석은 모델 업데이트 워크플로우의 주요 구성 요소 및 옵션에 대해 설명합니다.

- `UPDATE model <model_alias>`: update 명령은 버전 관리를 처리하고 마지막 버전에서 증가한 새 모델 버전을 만듭니다.
- `version`: 새 버전을 만들도록 명시적으로 지정하는 업데이트 중에만 사용되는 선택적 키워드입니다. 생략하면 버전이 자동으로 증가합니다.


## 모델 평가 {#evaluate-model}

신뢰할 수 있는 결과를 얻으려면 `model_evaluate` 키워드를 사용하여 예측을 위해 모델을 배포하기 전에 모델의 정확성과 유효성을 평가하십시오. 아래의 SQL 문은 테스트 데이터 세트, 특정 열 및 모델의 성능을 평가하여 모델을 테스트할 모델의 버전을 지정합니다.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

`model_evaluate` 함수는 `model-alias`을(를) 첫 번째 인수로 사용하고 유연한 `SELECT` 문을 두 번째 인수로 사용합니다. 쿼리 서비스가 먼저 `SELECT` 문을 실행하고 결과를 `model_evaluate` Adobe 정의 함수(ADF)에 매핑합니다. 시스템은 `SELECT` 문 결과의 열 이름 및 데이터 형식이 교육 단계에서 사용된 열 이름과 일치해야 합니다. 이러한 열 이름 및 데이터 유형은 평가를 위해 테스트 데이터 및 레이블 데이터로 처리됩니다.

>[!IMPORTANT]
>
>평가(`model_evaluate`)와 예측(`model_predict`)할 때 교육 시 수행된 변환이 사용됩니다.

## 예측 {#predict}

그런 다음 `model_predict` 키워드를 사용하여 지정된 모델과 버전을 데이터 집합에 적용하고 선택한 열에 대한 예측을 생성합니다. 아래 SQL에서는 모델의 별칭 및 버전을 사용하여 결과를 예측하는 방법을 보여 주는 이 프로세스를 보여 줍니다.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict`은(는) 모델 별칭을 첫 번째 인수로 허용하고 유연한 `SELECT` 문을 두 번째 인수로 허용합니다. 쿼리 서비스가 먼저 `SELECT` 문을 실행하고 결과를 `model_predict` ADF에 매핑합니다. `SELECT` 문 결과의 열 이름 및 데이터 형식이 교육 단계의 열 이름과 일치해야 합니다. 그런 다음 이 데이터는 점수를 매기고 예측을 생성하는 데 사용됩니다.

>[!IMPORTANT]
>
>평가(`model_evaluate`)와 예측(`model_predict`)할 때 교육 시 수행된 변환이 사용됩니다.

## 모델 평가 및 관리

`SHOW MODELS` 명령을 사용하여 만든 사용 가능한 모든 모델을 나열합니다. 이 필드를 사용하여 교육되었으며 평가 또는 예측에 사용할 수 있는 모델을 봅니다. 질의하면 모델 생성 중에 업데이트되는 모델 저장소에서 정보를 가져옵니다. 반환된 세부 사항은 모델 ID, 모델 이름, 버전, 소스 데이터 세트, 알고리즘 세부 사항, 옵션/매개 변수, 생성/업데이트 시간 및 모델을 만든 사용자입니다.

```sql
SHOW MODELS;
```

결과는 아래에 표시된 것과 유사한 표에 나타납니다.

| model-id | model-name | 버전 | 소스-데이터 세트 | 유형 | 옵션 | 변형 | 필드 | 생성됨 | 업데이트됨 | 만든 사람 |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1.0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[&quot;name&quot;, &quot;gender&quot;\] | 2024-08-14 오전 10:30 | 2024-08-14 오전 11:00 | `JohnSnow@adobe.com` |

## 모델 정리 및 유지 관리

`DROP MODELS` 명령을 사용하여 모델 레지스트리에서 만든 모델을 삭제합니다. 오래된 모델, 사용하지 않은 모델 또는 원하지 않는 모델을 제거하는 데 사용할 수 있습니다. 따라서 리소스를 확보하고 관련 모델만 유지 관리할 수 있습니다. 특수성을 개선하기 위해 선택적 모델 이름을 포함할 수도 있습니다. 제공된 모델 버전이 있는 모델만 삭제됩니다.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## 다음 단계

이제 이 문서를 읽고 Data Distiller을 사용하여 신뢰할 수 있는 모델을 만들고, 교육하고, 관리하는 데 필요한 기본 SQL 구문을 이해합니다. 다음으로 [고급 통계 모델 구현 문서](./implement-models/implement-models.md)를 살펴보고 사용 가능한 다양한 신뢰할 수 있는 모델과 SQL 워크플로 내에서 효과적으로 구현하는 방법에 대해 알아봅니다. 아직 수행하지 않았다면 [기능 엔지니어링](./feature-engineering.md) 문서를 검토하여 데이터가 모델 교육에 맞게 최적으로 준비되었는지 확인하십시오.
