---
title: 탐색적 데이터 분석
description: Data Distiller을 사용하여 Python 노트북에서 데이터를 탐색하고 분석하는 방법에 대해 알아봅니다.
exl-id: 1dd4cf6e-f7cc-4f4b-afbd-bfc1d342a2c3
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 16%

---

# 탐색적 데이터 분석

이 문서에서는 Data Distiller을 사용하여 의 데이터를 탐색하고 분석하기 위한 몇 가지 기본 예와 모범 사례를 제공합니다. [!DNL Python] 전자 필기장.

## 시작하기

이 안내서를 계속 진행하기 전에 의 Data Distiller에 대한 연결을 만들었는지 확인하십시오. [!DNL Python] 전자 필기장. 방법에 대한 지침은 설명서 를 참조하십시오 [연결 [!DNL Python] notebook에서 Data Distiller으로](./establish-connection.md).

## 기본 통계 얻기 {#basic-statistics}

아래 코드를 사용하여 데이터 세트에 있는 행 수와 개별 프로필을 검색합니다.

```python
table_name = 'ecommerce_events'

basic_statistics_query = f"""
SELECT
    COUNT(_id) as "totalRows",
    COUNT(DISTINCT _id) as "distinctUsers"
FROM {table_name}"""

df = qs_cursor.query(basic_statistics_query, output="dataframe")
df
```

**샘플 출력**

|     | 합계 행 수 | 고유 사용자 수 |
| --- | ----------- | -------------- |
| 0 | 1276563 | 1276563 |

## 대용량 데이터 세트의 샘플 버전 만들기 {#create-dataset-sample}

쿼리하려는 데이터 세트가 매우 크거나 탐색적 쿼리의 정확한 결과가 필요하지 않은 경우 [샘플링 기능](../../essential-concepts/dataset-samples.md) 데이터 Distiller 쿼리에 사용할 수 있습니다. 2단계 프로세스입니다.

- 첫 번째, **분석** 지정된 샘플링 비율로 샘플링된 버전을 만드는 데이터 집합입니다.
- 그런 다음, 샘플링된 데이터 세트 버전을 쿼리합니다. 샘플링된 데이터 세트에 적용하는 함수에 따라 출력을 전체 데이터 세트에 대한 숫자로 조정할 수 있습니다

### 5% 샘플 만들기 {#create-sample}

아래 예제는 데이터 세트를 분석하고 5% 샘플을 만듭니다.

```python
# A sampling rate of 10 is 100% in Query Service, so for 5% use a sampling rate 0.5
sampling_rate = 0.5

analyze_table_query=f"""
SET aqp=true;
ANALYZE TABLE {table_name} TABLESAMPLE SAMPLERATE {sampling_rate}"""

qs_cursor.query(analyze_table_query, output="raw")
```

### 샘플 보기 {#view-sample}

다음을 사용할 수 있습니다. `sample_meta` 함수 를 사용하십시오. 아래의 코드 조각은 `sample_meta` 함수.

```python
sampled_version_of_table_query = f'''SELECT sample_meta('{table_name}')'''

df_samples = qs_cursor.query(sampled_version_of_table_query, output="dataframe")
df_samples
```

**샘플 출력**:

|   | sample_table_name | sample_dataset_id | parent_dataset_id | sample_type | sampling_rate | filter_condition_on_source_dataset | sample_num_rows | 생성됨 |
|---|---|---|---|---|---|---|---|---|
| 0 | cmle_synthetic_data_experience_event_dataset_c... | 650f7a09ed6c3e28d34d7fc2 | 64fb4d7a7d748828d304a2f4 | 균일 | 0.5 | 6427 | 23/09/2023 | 11:51:37 |

{style="table-layout:auto"}

### 샘플 쿼리 {#query-sample-data}

반환된 메타데이터에서 샘플 테이블 이름을 참조하여 샘플을 직접 쿼리할 수 있습니다. 그런 다음 결과에 샘플링 비율을 곱하여 추정치를 구할 수 있습니다.

```python
sample_table_name = df_samples[df_samples["sampling_rate"] == sampling_rate]["sample_table_name"].iloc[0]

count_query=f'''SELECT count(*) as cnt from {sample_table_name}'''

df = qs_cursor.query(count_query, output="dataframe")
# Divide by the sampling rate to extrapolate to the full dataset
approx_count = df["cnt"].iloc[0] / (sampling_rate / 100)

print(f"Approximate count: {approx_count} using {sampling_rate *10}% sample")
```

**샘플 출력**

```console
Approximate count: 1284600.0 using 5.0% sample
```

## 이메일 단계 분석 {#email-funnel-analysis}

단계 분석은 목표 결과에 도달하는 데 필요한 단계와 이러한 각 단계를 통과하는 사용자 수를 이해하는 방법입니다. 아래 예제는 뉴스레터를 구독하는 사용자에게 연결되는 단계를 간단하게 분석하는 방법을 보여 줍니다. 구독 결과는 의 이벤트 유형으로 표시됩니다. `web.formFilledOut`.

먼저 쿼리를 실행하여 각 단계의 사용자 수를 가져옵니다.

```python
simple_funnel_analysis_query = f'''SELECT eventType, COUNT(DISTINCT _id) as "distinctUsers",COUNT(_id) as "distinctEvents" FROM {table_name} GROUP BY eventType ORDER BY distinctUsers DESC'''

funnel_df = qs_cursor.query(simple_funnel_analysis_query, output="dataframe")
funnel_df
```

**샘플 출력**

|   | eventType | 고유 사용자 수 | distinctEvents |
|---|---|---|---|
| 0 | directMarketing.emailSent | 598840 | 598840 |
| 1 | directMarketing.emailOpened | 239028 | 239028 |
| 2 | web.webpagedetails.pageViews | 120118 | 120118 |
| 3 | advertising.impressions | 119669 | 119669 |
| 4 | directMarketing.emailClicked | 51581 | 51581 |
| 5 | commerce.productViews | 37915 | 37915 |
| 6 | decisioning.propositionDisplay | 37650 | 37650 |
| 7 | web.webinteraction.linkClicks | 37581 | 37581 |
| 8 | web.formFilledOut | 17860 | 17860 |
| 9 | advertising.clicks | 7610 | 7610 |
| 10 | decisioning.propositionInteract | 2964 | 2964 |
| 11 | decisioning.propositionDismiss | 2889 | 2889 |
| 12 | commerce.purchases | 2858 | 2858 |

{style="table-layout:auto"}

### 그래프 쿼리 결과 {#plot-results}

그런 다음 다음을 사용하여 쿼리 결과를 플롯합니다. [!DNL Python] `plotly` 라이브러리:

```python
import plotly.express as px

email_funnel_events = ["directMarketing.emailSent", "directMarketing.emailOpened", "directMarketing.emailClicked", "web.formFilledOut"]
email_funnel_df = funnel_df[funnel_df["eventType"].isin(email_funnel_events)]

fig = px.funnel(email_funnel_df, y='eventType', x='distinctUsers')
fig.show()
```

**샘플 출력**

![eventType 이메일 단계의 인포그래픽입니다.](../../images/data-distiller/email-funnel.png)

## 이벤트 상관 관계 {#event-correlations}

또 다른 일반적인 분석은 이벤트 유형과 대상 전환 이벤트 유형 간의 상관 관계를 계산하는 것입니다. 이 예제에서 구독 이벤트는 `web.formFilledOut`. 이 예에서는 [!DNL Spark] 함수 는 다음 단계를 수행하기 위해 데이터 Distiller 쿼리에서 사용할 수 있습니다.

1. 프로필별로 각 이벤트 유형에 대한 이벤트 수를 카운트합니다.
2. 프로필에서 각 이벤트 유형의 개수를 집계하고, 각 이벤트 유형의 상관 관계를 `web,formFilledOut`.
3. 카운트 및 상관 관계의 데이터 프레임을 대상 이벤트가 있는 각 피쳐(이벤트 유형 카운트)의 피어슨 상관 계수 표로 변환합니다.
4. 플롯에서 결과를 시각화합니다.

다음 [!DNL Spark] 함수는 데이터를 집계하여 작은 결과 테이블을 반환하므로 전체 데이터 세트에서 이 유형의 쿼리를 실행할 수 있습니다.

```python
large_correlation_query=f'''
SELECT SUM(webFormsFilled) as webFormsFilled_totalUsers,
       SUM(advertisingClicks) as advertisingClicks_totalUsers,
       SUM(productViews) as productViews_totalUsers,
       SUM(productPurchases) as productPurchases_totalUsers,
       SUM(propositionDismisses) as propositionDismisses_totaUsers,
       SUM(propositionDisplays) as propositionDisplays_totaUsers,
       SUM(propositionInteracts) as propositionInteracts_totalUsers,
       SUM(emailClicks) as emailClicks_totalUsers,
       SUM(emailOpens) as emailOpens_totalUsers,
       SUM(webLinkClicks) as webLinksClicks_totalUsers,
       SUM(webPageViews) as webPageViews_totalusers,
       corr(webFormsFilled, emailOpens) as webForms_EmailOpens,
       corr(webFormsFilled, advertisingClicks) as webForms_advertisingClicks,
       corr(webFormsFilled, productViews) as webForms_productViews,
       corr(webFormsFilled, productPurchases) as webForms_productPurchases,
       corr(webFormsFilled, propositionDismisses) as webForms_propositionDismisses,
       corr(webFormsFilled, propositionInteracts) as webForms_propositionInteracts,
       corr(webFormsFilled, emailClicks) as webForms_emailClicks,
       corr(webFormsFilled, emailOpens) as webForms_emailOpens,
       corr(webFormsFilled, emailSends) as webForms_emailSends,
       corr(webFormsFilled, webLinkClicks) as webForms_webLinkClicks,
       corr(webFormsFilled, webPageViews) as webForms_webPageViews
FROM(
    SELECT _{tenant_id}.cmle_id as userID,
            SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) as webFormsFilled,
            SUM(CASE WHEN eventType='advertising.clicks' THEN 1 ELSE 0 END) as advertisingClicks,
            SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) as productViews,
            SUM(CASE WHEN eventType='commerce.productPurchases' THEN 1 ELSE 0 END) as productPurchases,
            SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) as propositionDismisses,
            SUM(CASE WHEN eventType='decisioning.propositionDisplay' THEN 1 ELSE 0 END) as propositionDisplays,
            SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) as propositionInteracts,
            SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) as emailClicks,
            SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) as emailOpens,
            SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) as emailSends,
            SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) as webLinkClicks,
            SUM(CASE WHEN eventType='web.webinteraction.pageViews' THEN 1 ELSE 0 END) as webPageViews
    FROM {table_name}
    GROUP BY userId
)
'''
large_correlation_df = qs_cursor.query(large_correlation_query, output="dataframe")
large_correlation_df
```

**샘플 출력**:

|   | webFormsFilled_totalUsers | advertisingClicks_totalUsers | productViews_totalUsers | productPurchases_totalUsers | propositionDismisses_totaUsers | propositionDisplays_totaUsers | propositionInteracts_totalUsers | emailClicks_totalUsers | emailOpens_totalUsers | webLinksClicks_totalUsers | ... | webForms_advertisingClicks | webForms_productViews | webForms_제품 구매 | webForms_propositionDismisses | webForms_propositionInteracts | webForms_emailClicks | webForms_emailOpen | webForms_emailSends | webForms_webLinkClicks | webForms_webPageViews |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 17860 | 7610 | 37915 | 0 | 2889 | 37650 | 2964 | 51581 | 239028 | 37581 | … | 0.026805 | 0.2779 | None | 0.06014 | 0.143656 | 0.305657 | 0.218874 | 0.192836 | 0.259353 | None |

{style="table-layout:auto"}

### 행을 이벤트 유형 상관 관계로 변환 {#event-type-correlation}

그런 다음 위의 쿼리 출력에 있는 단일 데이터 행을 각 이벤트 유형과 대상 구독 이벤트의 상관 관계를 보여 주는 표로 변환합니다.

```python
cols = large_correlation_df.columns
corrdf = large_correlation_df[[col for col in cols if ("webForms_"  in col)]].melt()
corrdf["feature"] = corrdf["variable"].apply(lambda x: x.replace("webForms_", ""))
corrdf["pearsonCorrelation"] = corrdf["value"]

corrdf.fillna(0)
```

**샘플 출력**:

|    | 변수를 채우는 방법을 설명합니다 | 값 | 기능 | pearsonCorrelation |
| --- | ---  |  ---  |  ---  | --- |
| 0 | `webForms_EmailOpens` | 0.218874 | 이메일 열람수 | 0.218874 |
| 1 | `webForms_advertisingClicks` | 0.026805 | advertisingClicks | 0.026805 |
| 2 | `webForms_productViews` | 0.277900 | 제품 보기 | 0.277900 |
| 3 | `webForms_productPurchases` | 0.000000 | 제품 구매 | 0.000000 |
| 4 | `webForms_propositionDismisses` | 0.060140 | 제안 취소 | 0.060140 |
| 5 | `webForms_propositionInteracts` | 0.143656 | propositionInteract | 0.143656 |
| 6 | `webForms_emailClicks` | 0.305657 | emailClicks | 0.305657 |
| 7 | `webForms_emailOpens` | 0.218874 | emailOpens | 0.218874 |
| 8 | `webForms_emailSends` | 0.192836 | 이메일 전송 횟수 | 0.192836 |
| 9 | `webForms_webLinkClicks` | 0.259353 | webLinkClicks | 0.259353 |
| 10 | `webForms_webPageViews` | 0.000000 | webPageViews | 0.000000 |


마지막으로 과의 상관 관계를 시각화할 수 있습니다. `matplotlib` 파이썬 라이브러리:

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(5,10))
sns.barplot(data=corrdf.fillna(0), y="feature", x="pearsonCorrelation")
ax.set_title("Pearson Correlation of Events with the outcome event")
```

![이벤트 결과 이벤트의 Pearson 상관 관계에 대한 막대 그래프](../../images/data-distiller/pearson-correlations.png)

## 다음 단계

이 문서를 읽고 Data Distiller을 사용하여 의 데이터를 탐색하고 분석하는 방법을 배웠습니다. [!DNL Python] 전자 필기장. 머신 러닝 환경에서 Experience Platform에서 피드 사용자 지정 모델로의 기능 파이프라인을 만드는 다음 단계는 다음과 같습니다 [머신 러닝을 위한 엔지니어 기능](./feature-engineering.md).
