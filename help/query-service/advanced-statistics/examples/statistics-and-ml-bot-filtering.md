---
title: 통계 및 머신 러닝을 사용한 보트 필터링
description: 데이터 Distiller 통계 및 머신 러닝을 사용하여 보트 활동을 식별하고 필터링하여 정확한 분석과 향상된 데이터 무결성을 보장하는 방법을 알아봅니다.
source-git-commit: a8abbf61bdc646c0834c296a64b27c71c98ea1d3
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# 통계 및 머신 러닝을 사용한 보트 필터링

보트 필터링의 실제 적용은 다양한 산업에 걸쳐 있다. 전자상거래에서 전환율 지표의 안정성을 높이고, 뉴스 웹사이트는 허위 참여 지표를 완화해 이점을 얻을 수 있으며, 광고 네트워크는 공정한 결제를 보장할 수 있습니다. 정확한 분석을 유지하고 클릭스트림 또는 웹 트래픽 데이터의 데이터 무결성을 보장하려면 봇 활동을 해결해야 합니다. Data Distiller을 사용하여 효과적인 보트 필터링을 구현하고 원치 않는 트래픽을 제거하여 고품질 분석 데이터를 보장할 수 있습니다.

이 문서에서는 SQL 및 머신 러닝 기술을 사용하여 보트 활동을 식별하고 필터링하는 방법에 대한 포괄적인 안내서를 제공합니다. 기본 필터링을 시작으로 머신러닝 기반 탐지 및 평가로 나아가는 상호 보완적인 접근의 진행을 제시한다. 이 강력한 프레임워크를 채택하여 보트 감지를 강화하고 데이터 무결성을 유지합니다.

## 보트 활동 이해 {#understand-bot-activity}

봇 활동은 특정 시간 간격 내에 사용자 액션의 스파이크를 탐지함으로써 식별될 수 있다. 예를 들어 짧은 기간에 단일 사용자가 수행한 과도한 클릭은 보트 동작을 나타낼 수 있습니다. 보트 필터링에 사용되는 두 가지 주요 속성은 다음과 같습니다.

- **ECID(Experience Cloud 방문자 ID):** 방문자를 식별하는 범용 영구 ID입니다.
- **타임스탬프:** 웹 사이트에서 활동이 발생하는 시간과 날짜입니다.

아래 예에서는 SQL 및 머신 러닝 기술을 사용하여 보트 활동을 식별, 세분화 및 예측하는 방법을 보여 줍니다. 이러한 방법을 사용하여 데이터 무결성을 향상시키고 실행 가능한 분석을 보장합니다.

## SQL 기반 보트 필터링 {#sql-based-bot-filtering}

이 SQL 기반 보트 필터링 예제는 SQL 쿼리를 사용하여 임계값을 정의하고 사전 정의된 규칙을 기반으로 보트 활동을 감지하는 방법을 보여 줍니다. 이 기본 접근 방식은 비정상적인 활동을 제거하여 웹 트래픽의 예외 항목을 식별하는 데 도움이 됩니다. 정의된 임계값과 간격으로 감지 규칙을 사용자 정의하여 특정 트래픽 패턴에 맞게 보트 필터링을 효과적으로 조정할 수 있습니다.

### 보트 활동에 대한 임계값 정의 {#define-thresholds}

먼저 데이터 세트를 분석하여 사용자 행동을 식별하고 분류합니다. ECID, 타임스탬프 및 `webPageDetails.name`(방문한 웹 페이지의 이름)과 같은 특성에 초점을 맞추어 사용자 작업을 그룹화하고 봇 활동을 나타내는 패턴을 감지합니다.

아래의 SQL 쿼리는 1분 동안 60번 이상 클릭의 임계값을 적용하여 의심스러운 활동을 식별하는 방법을 보여 줍니다.

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### 여러 간격으로 확장 {#expand-to-multiple-intervals}

그런 다음 임계값에 대해 서로 다른 시간 간격을 정의합니다. 이러한 간격에는 다음이 포함될 수 있습니다.

- **1분 간격:** 최대 클릭 수 60회.
- **5분 간격:** 최대 클릭 수 300회.
- **30분 간격:** 최대 1,800번의 클릭으로 실행할 수 있습니다.

다음 SQL 쿼리는 `analytics_events_clicks_count_criteria`(이)라는 보기를 만들어 여러 간격에서 임계값을 처리합니다. 이 명령문은 1분, 5분 및 30분 간격에 대한 클릭 수를 구조화된 데이터 세트로 통합하고 사전 정의된 임계값을 기반으로 잠재적 봇 활동에 플래그를 지정합니다.

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

문이 `mcid` 값 및 웹 페이지를 사용하여 `table_count_1_min`, `table_count_5_mins` 및 `table_count_30_mins`의 데이터를 조인합니다. 그런 다음 여러 시간 간격 동안 각 사용자에 대한 클릭 수를 통합하여 사용자 활동을 완전히 볼 수 있습니다. 마지막으로 플래그 지정 논리는 1분 동안 50번의 클릭을 초과하는 사용자를 식별하고 봇(`isBot = 1`)으로 표시합니다.

### 출력 데이터 세트 구조

출력 데이터 세트는 플랫 필드와 중첩 필드로 구조화됩니다. 이 구조는 무형성 트래픽을 탐지할 때 유연성을 허용하며 SQL 및 머신 러닝을 사용하는 고급 필터링 전략을 지원합니다. 중첩된 필드에는 활동 임계값 및 웹 페이지에 대한 세부 정보를 캡슐화하는 `count` 및 `web`이(가) 포함됩니다. 이러한 지표를 캡처한다는 것은 교육 및 예측 작업을 위해 기능을 쉽게 추출할 수 있음을 의미합니다.

다음 스키마 다이어그램은 결과 데이터 세트의 구조를 간략하게 설명하고 효율적인 처리 및 봇 탐지를 위해 중첩된 필드와 플랫 필드를 사용할 수 있는 방법을 강조합니다.

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### 교육에 사용될 출력 데이터 세트

이 표현식의 결과는 아래에 제공된 표와 유사할 수 있습니다. 표에서 `isBot` 열은 봇 활동과 비봇 활동을 구분하는 레이블 역할을 합니다.

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## 보트 필터링을 위한 고급 통계 함수 {#statistical-functions-for-bot-filtering}

이 두 번째 예는 임계값을 구체화하고 필터링 정확도를 개선하기 위해 머신 러닝 기술을 통합하여 기본 SQL 필터링을 기반으로 합니다. 이 접근 방식은 회귀 분석 또는 클러스터링 알고리즘과 같은 고급 통계 함수를 사용하여 복잡한 데이터 세트를 더 정밀하게 처리하기 위해 모델을 개발하는 데 사용할 수 있는 예측 기능을 제공합니다.

### 교육 데이터 세트 구축 {#build-a-training-dataset}

먼저 (위에서 설명한 대로) 머신 러닝 모델이 사용할 수 있는 평면적이고 중첩된 구조의 데이터 세트를 준비합니다. 이 작업을 수행하는 방법에 대한 자세한 지침은 [중첩 데이터 구조 작업 설명서](../../key-concepts/nested-data-structures.md)에서 확인할 수 있습니다. 타임스탬프, 사용자 ID 및 웹 페이지 이름별로 데이터를 그룹화하여 봇 활동의 패턴을 식별합니다.

### 모델 생성을 위해 TRANSFORM 및 OPTIONS 절 사용 {#transform-and-preprocess}

데이터 세트를 변환하고 머신 러닝 모델을 효과적으로 구성하려면 아래 단계를 따르십시오. 이 절차에서는 null 값을 처리하고, 피쳐를 준비하고 최적의 성능을 위해 모델의 매개변수를 정의하는 방법에 대해 자세히 설명합니다.

>[!TIP]
>
>데이터 변환 및 사전 처리에 대한 자세한 내용은 [기능 변환 기법 설명서](../feature-transformation.md)를 참조하세요.

1. 숫자, 문자열 및 부울 열에서 null 값을 채우려면 각각 `numeric_imputer`, `string_imputer` 및 `boolean_imputer` 함수를 사용합니다. 이 단계에서는 머신 러닝 알고리즘이 오류 없이 데이터를 처리할 수 있도록 합니다.
2. 피쳐 변환을 적용하여 모델링할 데이터를 준비합니다. `binarized`, `quantile_discretizer` 또는 `string_indexer`을(를) 적용하여 열을 분류하거나 표준화합니다. 그런 다음, 가져오기(`numeric_imputer` 및 `string_imputer`)의 출력을 `string_indexer` 또는 `quantile_discretizer`과(와) 같은 후속 변환기에 전달하여 의미 있는 기능을 만듭니다.
3. `vector_assembler` 함수를 사용하여 변환된 열을 하나의 기능 열로 결합하십시오. 그런 다음 `min_max_scaler`을(를) 사용하여 기능의 크기를 조정하여 더 나은 모델 성능을 위해 값을 정규화합니다. 참고: SQL 예제에서 TRANSFORM 절 내에 언급된 마지막 변환은 머신 러닝 모델에 사용되는 기능 열이 됩니다.
4. 모델 유형 및 기타 하이퍼매개 변수를 OPTIONS 절에 지정합니다. 예를 들어 분류 문제이므로 여기에서 `decision_tree_classifier`을(를) 선택했습니다. 더 나은 성능을 위해 모델을 튜닝하기 위해 `max_depth`과(와) 같은 다른 매개 변수가 조정되었습니다(`MAX_DEPTH=4`).
5. 기능을 결합하고 출력 데이터에 레이블을 지정합니다. SELECT 절을 사용하여 교육을 위한 데이터 세트를 지정합니다. 이 절에는 작업이 봇인지 여부를 나타내는 기능 열(`count_per_id`, `web`, `id`)과 레이블 열(`isBot`)이 모두 포함되어야 합니다.

명령문은 아래 예제와 유사할 수 있습니다.

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**결과**

아래에 표시된 결과에서 `bot_filtering_model` 모델이 고유 ID, 이름 및 버전을 사용하여 만들어졌습니다. 이 출력은 모델 추적 및 관리를 위한 참조 역할을 합니다. 이러한 참조를 사용하여 예측 또는 평가에 필요한 정확한 구성 및 버전을 식별합니다.

```console
           Created Model ID           |       Created Model       | Version
--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### 훈련된 모델 평가 {#evaluate-trained-model}

모델을 만든 후 `MODEL_EVALUATE` 명령을 사용하여 성능을 평가합니다. 이 단계에서는 모델이 보트 활동을 감지하기 위한 정확도 및 성능 요구 사항을 충족하도록 합니다.

SQL 명령에서 다음 인수를 사용하여 모델을 평가합니다.

1. 평가할 모델을 나타내려면 모델 이름(`bot_filtering_model`)을 지정하십시오. 이 이름은 `CREATE MODEL` 명령을 사용하여 이전에 만든 이름과 일치해야 합니다.
2. 두 번째 인수에 모델 버전(`1`)을 입력하여 평가할 모델의 버전을 지정하십시오. 여러 버전이 있는 경우 올바른 버전이 사용되도록 합니다.
3. 평가를 위한 데이터 세트를 정의할 평가 데이터 세트를 포함합니다. 데이터 집합에 교육 중에 사용된 동일한 기능 열(`count_per_id`, `web`, `id`)과 레이블 열(`isBot`)이 포함되어 있는지 확인하십시오.

>[!NOTE]
>
>모델 훈련 시 적용된 변형은 평가 시 자동으로 적용된다.

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**결과**

응답은 정확도, 정밀도, 리콜 및 AUC-ROC와 같은 메트릭을 포함한다. 그 결과를 통해 모형이 잘 수행되었는지 여부를 확인할 수 있다.

>[!NOTE]
>
>0-1 범위의 값은 비율 또는 확률을 나타내며, 1.0은 완벽한 성능을 나타냅니다.

```console
auc_roc | accuracy | precision | recall
---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **지표** | **설명** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | 이 지표는 모델이 봇과 비봇을 얼마나 효과적으로 분류할 수 있는지 나타냅니다. 이는 분류 모델을 평가하는 데 널리 사용됩니다. |
| `accuracy` | 모델이 한 올바른 예측의 백분율입니다. |
| `precision` | 모든 예측 보트 중 실제 보트 예측의 비율입니다. |
| `recall` | 모든 실제 보트 중에서 검색된 실제 보트의 비율입니다. |

>[!TIP]
>
>프로덕션 샌드박스에서 사용하려면 테스트 데이터 세트에서 모델을 평가하여 효율적으로 일반화하는지 확인하십시오.

### 보트 활동 예측 {#predict-bot-activity}

훈련된 모델과 함께 `MODEL_PREDICT` 명령을 사용하여 봇인 사용자(`id`)를 식별하십시오. 봇 활동을 식별하기 위한 예측을 생성하려면 아래 단계를 수행하십시오.

1. 예측에 사용할 모델을 지정하려면 첫 번째 인수에 모델 이름(`bot_filtering_model`)을 사용하십시오.
2. 두 번째 인수에서 모델 버전(`1`)을 지정하여 모델의 올바른 버전을 사용하도록 하십시오.
3. 예측에 올바른 데이터를 제공하려면 SELECT 문을 사용하여 기능 열(`count_per_id`, `web`, `id`)을 지정하십시오. 모델이 이 필드에 대한 예측을 생성하므로 레이블 열(`isBot`)을 포함하지 마십시오.

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**결과**

응답에는 각 사용자(`id`)에 대한 예측과 함께 해당 활동 및 모델의 분류 결과에 대한 세부 정보가 포함됩니다. 이 출력을 통해 사용자 행동과 모델의 보트 활동 분류를 세부적으로 검토할 수 있습니다.

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

아래 표에서는 각 지표에 대해 설명합니다.

| 열 이름 | 설명 |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | 각 사용자의 고유 식별자입니다. |
| `count.one_minute` | 1분 간격으로 집계된 클릭수입니다. |
| `count.five_minute` | 5분 간격으로 집계된 클릭수입니다. |
| `count.thirty_minute` | 30분 간격으로 집계된 클릭수입니다. |
| `web.webpagedetails.name` | 방문한 웹 페이지의 이름입니다. 이렇게 하면 사용자 활동에 대한 컨텍스트가 제공됩니다. |
| `prediction` | 모델의 예측입니다. `1.0` 결과는 사용자가 활동 패턴을 기반으로 봇으로 플래그가 지정되었음을 나타냅니다. |

## 모델 관리 {#manage-models}

머신 러닝 모델을 관리하려면 아래 섹션에 나열된 SQL 키워드를 사용하십시오.

### 사용 가능한 모델 나열 {#list-available-models}

`SHOW MODELS;` 명령을 사용하여 모델을 효율적으로 관리하고 검토합니다. 이 명령은 현재 작업 영역에서 만들어진 모든 기계 학습 모델을 나열합니다. 출력에서는 사용 가능한 모델의 개요를 제공하며 해당 이름, 버전 및 기타 메타데이터를 포함합니다.

```sql
SHOW MODELS;
```

### 모델 삭제 {#delete-models}

리소스를 확보하고 관련 모델만 유지하려면 `DROP MODEL` 명령을 사용하여 오래되거나 불필요한 모델을 제거하십시오. 이 명령은 키워드 뒤에 지정된 머신 러닝 모델을 삭제합니다. 아래 예제에서 `bot_filtering_model`은(는) 시스템에서 제거됩니다.

```sql
DROP MODEL bot_filtering_model;
```

## 다음 단계

이 문서를 읽고 SQL을 사용하여 보트 활동을 식별하고 필터링하는 방법과 Data Distiller 메서드를 사용하는 머신 러닝 기술을 배웠습니다. 그런 다음 이러한 개념을 데이터 세트에 적용하고 지속적인 개선을 위해 모델 재교육을 자동화합니다.
