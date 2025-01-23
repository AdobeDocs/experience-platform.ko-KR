---
title: SQL 기반 로지스틱 회귀분석으로 고객 이탈 예측
description: SQL 기반 로지스틱 회귀 분석을 사용하여 고객 이탈을 예측하는 방법을 알아봅니다. 이 안내서에서는 모형 작성에서 평가 및 예측에 이르는 전 과정을 다룬다. 고객 구매 행동을 통해 실행 가능한 통찰력을 확보하여 사전 보존 전략을 구현하고 비즈니스 의사 결정을 최적화합니다.
source-git-commit: 95c7ad3f8eb86cacd42077008824eea9e25b4db0
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---

# SQL 기반 로지스틱 회귀분석으로 고객 이탈 예측

고객 이탈을 예측하면 실용적인 통찰력을 통해 만족도와 충성도를 향상시켜 기업이 고객을 유지하고 리소스를 최적화하고 수익성을 높일 수 있습니다.

SQL 기반 로지스틱 회귀 분석을 사용하여 고객 이탈을 예측하는 방법을 알아봅니다. 이 포괄적인 SQL 안내서를 사용하여 원시 전자 상거래 데이터를 주요 행동 지표(예: 구매 빈도, 평균 주문 가격 및 최근 구매)를 기반으로 의미 있는 고객 인사이트로 변환합니다. 이 문서에서는 데이터 준비 및 기능 엔지니어링에서 모델 생성, 평가 및 예측에 이르는 전체 프로세스를 다룹니다.

이 안내서를 사용하여 위험이 있는 고객을 식별하고 보존 전략을 구체화하며 비즈니스 의사 결정을 향상시키는 강력한 이탈 예측 모델을 구축하십시오. 여기에는 데이터 환경 내에서 머신 러닝 기술을 자신 있게 적용하는 데 도움이 되는 단계별 지침, SQL 쿼리 및 자세한 설명이 포함되어 있습니다.

## 시작하기

이탈 모델을 생성하기 전에 주요 고객 기능과 데이터 요구 사항을 살펴보는 것이 중요합니다. 다음 섹션에서는 정확한 모델 교육을 위한 필수 고객 속성 및 필수 데이터 필드에 대해 간략히 설명합니다.

### 고객 기능 정의 {#define-customer-features}

이탈을 정확히 분류하기 위해 모형은 구매 습관과 추세를 분석한다. 아래 표에는 모델에 사용된 주요 고객 행동 기능이 요약되어 있습니다.

| 기능 | 설명 |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | 고객이 구매한 총 횟수입니다. |
| `total_revenue` | 고객 구매에서 생성된 총 매출입니다. |
| `avg_order_value` | 고객 구매의 평균 값입니다. |
| `customer_lifetime` | 고객의 첫 구매와 마지막 구매 사이의 일 수입니다. |
| `days_since_last_purchase` | 고객이 마지막으로 구매한 이후 경과된 일 수입니다. |
| `purchase_frequency` | 고객이 구매한 개별 월의 수입니다. |

### 가정 및 필수 필드 {#assumptions-required-fields}

고객 이탈 예측을 생성하기 위해 모델은 고객 거래 세부 정보를 캡처하는 `webevents` 테이블 내의 키 필드에 따라 달라집니다. 데이터 세트에는 다음 필드가 포함되어야 합니다.

| 필드 | 설명 |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | 세션 간 고객을 추적하는 데 사용되는 고유 식별자. |
| `productListItems.priceTotal[0]` | 트랜잭션당 구매한 항목의 총 비용. |
| `productListItems.quantity[0]` | 구매의 총 항목 수입니다. |
| `timestamp` | 각 구매 이벤트의 정확한 날짜 및 시간. |
| `commerce.order.purchaseID` | 완료된 구매를 확인하는 필수 값. |

데이터 세트에는 구조화된 내역 고객 거래 레코드가 포함되어야 하며 각 행은 구매 이벤트를 나타냅니다. 각 이벤트에는 SQL `DATEDIFF` 함수와 호환되는 적절한 날짜-시간 형식의 타임스탬프가 포함되어야 합니다(예: YYYY-MM-DD HH:MI:SS). 또한 고객을 고유하게 식별하려면 각 레코드에 `identityMap` 필드에 올바른 Experience Cloud ID(`ECID`)가 있어야 합니다.

>[!TIP]
>
>수백만 개의 레코드로 대용량 데이터 세트를 처리하는 것은 성능에 상당한 영향을 미칠 수 있습니다. 쿼리 실행을 최적화하려면 타임스탬프로 경험 데이터 세트를 분할하고, 스냅샷을 사용하여 증분 처리를 수행하고, 필요에 따라 효율적인 집계 함수를 적용하십시오. 또한 집계 전에 데이터를 필터링하여 처리 오버헤드를 줄일 수 있습니다.

## 모델 만들기 {#create-a-model}

고객 이탈을 예측하려면 고객 구매 내역 및 행동 지표를 분석하는 SQL 기반 로지스틱 회귀 모델을 생성해야 합니다. 모델은 지난 90일 이내에 구매했는지 여부를 확인하여 고객을 `churned` 또는 `not churned`(으)로 분류합니다.

### SQL을 사용하여 이탈 예측 모델 만들기 {#sql-create-model}

SQL 기반 모델은 90일 비활성 규칙에 따라 주요 지표를 집계하고 이탈 레이블을 할당하여 `webevents` 데이터를 처리합니다. 이 접근 방식은 활성 고객과 위험 상태의 고객을 구별합니다. 또한 SQL 쿼리는 모델 정확도를 높이고 이탈 분류를 개선하기 위해 기능 엔지니어링을 수행합니다. 이러한 통찰력을 통해 기업은 타겟팅된 유지 전략을 구현하고 이탈을 줄이며 고객 생애 가치를 극대화할 수 있습니다.

>[!NOTE]
>
>이탈 예측 모델은 90일의 기본 임계값을 사용하여 고객을 이탈된 것으로 분류합니다. 비즈니스 목표 및 보존 전략에 맞게 이 임계값을 조정하려면 SQL 쿼리에서 `DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90` 조건을 수정하십시오.

다음 SQL 문을 사용하여 지정된 기능 및 레이블을 사용하는 `retention_model_logistic_reg` 모델을 만드십시오.

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### 모델 출력 {#model-output}

출력 데이터 세트에는 고객 관련 지표와 이탈 상태가 포함되어 있습니다. 각 행은 고객, 해당 기능 값 및 이탈 상태를 나타냅니다. 이 출력을 사용하여 고객 행동을 분석하고, 예측 모델을 교육하고, 위험 상태에 있는 고객을 유지하기 위한 타깃팅된 유지 전략을 개발할 수 있습니다. 출력 테이블의 예는 다음과 같습니다.

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| 열 | 설명 |
|-----------|------------------------------------------------------------------------------------|
| `churned` | 값은 고객이 지난 90일 이내에 구매했는지 여부를 나타냅니다(0 = 이탈되지 않음, 1 = 이탈됨). |

## SQL을 사용하여 모델 평가 {#model-evaluation}

다음으로 이탈 예측 모델을 평가하여 위험 상태의 고객을 식별하는 데 효과성을 결정합니다. 정확도와 안정성을 측정하는 주요 지표로 모델 성능을 평가합니다.

고객 이탈을 예측할 때 `retention_model_logistic_reg` 모델의 정확도를 측정하려면 `model_evaluate` 함수를 사용하십시오. 다음 SQL 예제에서는 교육 데이터와 같이 구조화된 데이터 세트를 사용하여 모델을 평가합니다.

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### 모델 평가 출력

평가 결과에는 AUC-ROC, 정확도, 정밀도 및 회수와 같은 주요 성능 지표가 포함됩니다. 이러한 지표는 유지 전략을 구체화하고 데이터 기반 결정을 내리는 데 사용할 수 있는 모델 효과에 대한 통찰력을 제공합니다.

>[!NOTE]
>
>성능 값의 범위는 0부터 1까지이며, 여기서 1.0은 완벽한 성능을 나타냅니다.

```console
 auc_roc | accuracy | precision | recall 
---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| 지표 | 설명 |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | 이 지표는 이탈한 고객과 이탈하지 않은 고객을 구분하는 모델의 기능을 나타냅니다. 값이 1에 가까울수록 성능이 향상됩니다. |
| `accuracy` | 정확도 지표는 올바른 예측의 비율을 나타내므로 모델 성능의 전반적인 측정을 제공합니다. |
| `precision` | 정밀도는 올바르게 식별된 이탈 고객의 비율을 보여 주며 이탈 예측의 신뢰성을 나타냅니다. 값이 높으면 긍정 오류(false positive)가 적음을 의미합니다. |
| `recall` | 리콜은 실제 이탈한 모든 고객을 식별하는 모델의 기능을 측정합니다. 회수 값이 높으면 누락된 이탈 고객이 적다는 것을 나타냅니다. |

>[!NOTE]
>
>이 예제에서 거의 만점에 가까운 점수는 데모용입니다. 실제로, 실제 데이터는 소음 및 변동성으로 인해 더 낮은 값을 산출할 수 있다.

## 모델 예측 {#model-prediction}

모델이 평가되면 `model_predict`을(를) 사용하여 새 데이터 집합에 적용하고 고객 이탈을 예측합니다. 이러한 예측을 사용하여 위험이 있는 고객을 식별하고 타겟팅된 보존 전략을 구현할 수 있습니다.

### SQL을 사용하여 이탈 예측 생성 {#sql-model-predict}

아래 SQL 쿼리는 `retention_model_logistic_reg` 모델을 사용하여 교육 데이터와 같은 구조의 데이터 집합으로 고객 이탈을 예측합니다.

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### 모델 예측 출력 {#prediction-output}

출력 데이터 세트에는 주요 고객 기능과 고객이 이탈할 가능성이 있는지 여부를 나타내는 예측된 이탈 상태가 포함됩니다. 이러한 통찰력을 사용하여 사전 보존 전략을 구현하고 고객 이탈을 줄이십시오.

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| 열 | 설명 |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | 모델을 기반으로 고객의 예측된 이탈 상태(0 = 이탈되지 않음, 1 = 이탈됨)입니다. |

## 다음 단계

이제 SQL 기반 모델을 생성, 평가 및 사용하여 고객 이탈을 예측하는 방법에 대해 알아보았습니다. 이러한 토대를 통해 고객 행동을 분석하고, 위험이 있는 고객을 식별하고, 사전 예방적 보존 전략을 구현하여 고객 유지력을 향상시킬 수 있습니다. 이탈 예측 모델을 더욱 강화하고 적용하려면 다음 단계를 고려하십시오.

- 프로세스 자동화: 모델을 데이터 파이프라인에 통합하여 지속적인 모니터링 및 실시간 인사이트를 제공합니다. [SQL을 사용하여 데이터 집합을 확인하고 처리하는 방법을 살펴봅니다](../../../dashboards/query.md).
- 모델 성능 모니터링: 정확성과 관련성을 유지하기 위해 새로운 데이터로 모델을 지속적으로 평가합니다.  Adobe Experience Platform UI에서 [AI Assistant](../../../ai-assistant/landing.md)를 사용하여 주요 성능 변경 사항을 모니터링하고 [대상 트렌드 예측](../../../ai-assistant/new-features/audience-forecasting.md)을 수행합니다.
