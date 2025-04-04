---
title: 머신 러닝에서 생성된 예측 모델을 사용하여 성향 점수 결정
description: 쿼리 서비스를 사용하여 예측 모델을 Experience Platform 데이터에 적용하는 방법에 대해 알아봅니다. 이 문서에서는 Experience Platform 데이터를 사용하여 각 방문에서 고객의 구매 성향을 예측하는 방법을 보여 줍니다.
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# 머신 러닝이 생성한 예측 모델을 사용하여 성향 점수 결정

쿼리 서비스를 사용하면 머신 러닝 플랫폼에 구축된 예측 모델(예: 성향 점수)을 활용하여 Experience Platform 데이터를 분석할 수 있습니다.

이 안내서에서는 컴퓨팅 전자 필기장에서 모델을 교육하기 위해 쿼리 서비스를 사용하여 데이터를 머신 러닝 플랫폼으로 보내는 방법을 설명합니다. 훈련된 모델은 SQL을 사용하여 데이터에 적용하여 각 방문에 대한 고객의 구매 성향을 예측할 수 있습니다.

## 시작하기

이 프로세스의 일부로 머신 러닝 모델을 교육해야 하므로 이 문서에서는 하나 이상의 머신 러닝 환경에 대한 작업 지식을 가정합니다.

이 예제에서는 [!DNL Jupyter Notebook]을(를) 개발 환경으로 사용합니다. 사용할 수 있는 옵션은 많지만 계산 요구 사항이 낮은 오픈 소스 웹 응용 프로그램이므로 [!DNL Jupyter Notebook]을(를) 사용하는 것이 좋습니다. 공식 사이트에서 [다운로드](https://jupyter.org/)할 수 있습니다.

아직 수행하지 않았다면 이 안내서를 계속하기 전에 [Adobe Experience Platform 쿼리 서비스와 연결 [!DNL Jupyter Notebook] 하기](../clients/jupyter-notebook.md)하는 단계를 따르십시오.

이 예제에서 사용되는 라이브러리는 다음과 같습니다.

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## Experience Platform에서 [!DNL Jupyter Notebook]&#x200B;(으)로 분석 테이블 가져오기 {#import-analytics-tables}

성향 점수 모델을 생성하려면 Experience Platform에 저장된 분석 데이터의 프로젝션을 [!DNL Jupyter Notebook]&#x200B;(으)로 가져와야 합니다. 쿼리 서비스에 연결된 [!DNL Python] 3 [!DNL Jupyter Notebook]에서 다음 명령은 가상 의류 매장인 Luma에서 고객 동작 데이터 세트를 가져옵니다. Experience Platform 데이터가 XDM(Experience Data Model) 형식을 사용하여 저장되므로 스키마의 구조를 준수하는 샘플 JSON 개체를 생성해야 합니다. [샘플 JSON 개체를 생성](../../xdm/ui/sample.md)하는 방법에 대한 지침은 설명서를 참조하세요.

![여러 명령이 강조 표시된 [!DNL Jupyter Notebook] 대시보드입니다.](../images/use-cases/jupyter-commands.png)

출력에는 [!DNL Jupyter Notebook] 대시보드 내에 있는 Luma의 동작 데이터 세트의 모든 열이 표로 표시된 보기가 표시됩니다.

![Luma의 가져온 고객 동작 데이터 세트의 표로 구분된 출력 [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## 머신 러닝을 위한 데이터 준비 {#prepare-data-for-machine-learning}

머신 러닝 모델을 교육하려면 대상 열을 식별해야 합니다. 구매 성향이 이 사용 사례의 목표이므로 `analytic_action` 열이 Luma 결과에서 대상 열로 선택됩니다. 값 `productPurchase`은(는) 고객 구매를 나타냅니다. `purchase_value` 및 `purchase_num` 열도 제품 구매 작업과 직접적으로 관련되어 있으므로 제거됩니다.

이러한 작업을 수행하는 명령은 다음과 같습니다.

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

다음으로, Luma 데이터 세트의 데이터는 적절한 표현들로 변환되어야 한다. 다음 두 단계가 필요합니다.

1. 숫자를 나타내는 열을 숫자 열로 변환합니다. 이렇게 하려면 `dataframe`의 데이터 형식을 명시적으로 변환하십시오.
1. 범주 열을 숫자 열로 변형할 수도 있습니다.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

*one hot encoding*(이)라는 기법은 컴퓨터 및 딥러닝 알고리즘과 함께 사용할 범주형 데이터 변수를 변환하는 데 사용됩니다. 이는 결과적으로 모델의 분류 정확도뿐만 아니라 예측도 향상시킵니다. `Sklearn` 라이브러리를 사용하여 각 범주형 값을 별도의 열에 표현합니다.

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

`X`(으)로 정의된 데이터가 테이블화되어 다음과 같이 표시됩니다.

![[!DNL Jupyter Notebook] 내의 X의 표로 정리된 출력입니다.](../images/use-cases/x-output-table.png)


이제 머신 러닝에 필요한 데이터를 사용할 수 있으므로 [!DNL Python]의 `sklearn` 라이브러리에 미리 구성된 머신 러닝 모델에 맞게 조정할 수 있습니다. [!DNL Logistics Regression]은(는) 성향 모델을 교육하는 데 사용되며 테스트 데이터의 정확성을 확인할 수 있도록 해 줍니다. 이 경우 약 85%입니다.

머신 러닝 알고리즘의 성능을 추정하는 데 사용되는 [!DNL Logistic Regression] 알고리즘 및 트레인 테스트 분할 방법을 아래 코드 블록으로 가져옵니다.

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

테스트 데이터 정확도는 0.8518518518518519입니다.

물류 회귀 분석을 사용하여 구매 이유를 시각화하고 내림차순에서 등급 중요도별로 성향을 결정하는 기능을 정렬할 수 있습니다. 첫 번째 열은 구매 행동으로 이어지는 더 높은 인과관계를 나타낸다. 후자의 열들은 구매 행동으로 이어지지 않는 요인들을 나타낸다.

결과를 두 막대 차트로 시각화하는 코드는 다음과 같습니다.

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

결과의 세로 막대 차트 시각화는 아래에 표시됩니다.

![구매 성향을 정의하는 상위 10개 기능의 시각화.](../images/use-cases/visualized-results.png)

막대 차트에서 몇 가지 패턴을 식별할 수 있습니다. 채널 판매 지점(POS) 및 환급으로서의 콜 주제는 구매 행동을 결정하는 가장 중요한 요소입니다. Call topics as complaints 및 invoices 는 구매하지 않는 행동을 정의하는 중요한 역할입니다. 이러한 통찰력은 마케터가 마케팅 캠페인을 수행하는 데 활용하여 이러한 고객의 구매 성향을 해결할 수 있는 수량화되고 실행 가능한 통찰력입니다.

## 쿼리 서비스를 사용하여 학습된 모델 적용 {#use-query-service-to-apply-trained-model}

훈련된 모델이 만들어지면 Experience Platform에 있는 데이터에 적용해야 합니다. 이렇게 하려면 머신 러닝 파이프라인의 논리를 SQL로 변환해야 합니다. 이 전환의 두 가지 주요 구성 요소는 다음과 같습니다.

- 먼저 예측 레이블의 확률을 얻으려면 SQL에서 [!DNL Logistics Regression] 모듈을 대신해야 합니다. Logistics Regression에서 만든 모델은 가중치 `w` 및 절편 `c`이(가) 모델의 출력인 회귀 모델 `y = wX + c`을(를) 생성했습니다. SQL 특징은 확률을 얻기 위해 가중치를 곱하는 데 사용될 수 있다.

- 두 번째로, 하나의 핫 인코딩으로 [!DNL Python]에서 달성한 엔지니어링 프로세스도 SQL에 통합해야 합니다. 예를 들어 원본 데이터베이스에 카운티를 저장할 열이 `geo_county`개 있지만 열은 `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`(으)로 변환됩니다. 다음 SQL 문은 동일한 변환을 수행합니다. 여기서 `w1`, `w2` 및 `w3`은(는) [!DNL Python]의 모델에서 학습한 가중치로 대체할 수 있습니다.

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

숫자 피쳐의 경우 아래 SQL 문에서 볼 수 있듯이 열에 가중치를 직접 곱할 수 있습니다.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

숫자가 얻어지면 Logistics Regression 알고리즘이 최종 예측을 생성하는 시그모이드 함수로 포팅될 수 있습니다. 아래 문에서 `intercept`은(는) 회귀에서 절편의 수입니다.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### 전체적인 예

두 개의 열(`c1` 및 `c2`)이 있는 경우 `c1`에 두 개의 범주가 있으면 [!DNL Logistic Regression] 알고리즘이 다음 함수로 학습됩니다.
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
SQL에서 이와 동일한 기능은 다음과 같습니다.

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```
 
번역 프로세스를 자동화하는 [!DNL Python] 코드는 다음과 같습니다.

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

SQL을 사용하여 데이터베이스를 유추하는 경우 출력은 다음과 같습니다.

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

테이블화된 결과에 각 고객 세션에 대한 구매 성향이 표시됩니다. `0`은(는) 구매 성향이 없음을 의미하고 `1`은(는) 구매 성향이 확인되었음을 의미합니다.

![SQL을 사용하여 데이터베이스 추론을 표로 정리한 결과입니다.](../images/use-cases/inference-results.png)

## 샘플링된 데이터 작업: 부트스트래핑 {#working-on-sampled-data}

데이터 크기가 너무 커서 로컬 컴퓨터에서 모델 교육에 대한 데이터를 저장할 수 없는 경우 쿼리 서비스에서 전체 데이터 대신 샘플을 가져올 수 있습니다. 쿼리 서비스에서 샘플링하는 데 필요한 데이터의 양을 알려면 부트스트랩 이라는 기술을 적용할 수 있습니다. 이와 관련하여, 부트스트래핑은 모델이 다양한 샘플로 여러 번 트레이닝되고, 상이한 샘플 사이에서 모델의 정확도의 분산이 검사되는 것을 의미한다. 위에 제공된 성향 모델 예제를 조정하기 위해, 먼저 전체 기계 학습 워크플로우를 함수로 캡슐화합니다. 코드는 다음과 같습니다.

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

그런 다음 이 함수는 루프에서 여러 번, 예를 들어 10번 실행할 수 있습니다. 이전 코드와 다른 점은 이제 전체 표에서 샘플을 가져오는 것이 아니라 행의 샘플에서만 샘플을 가져온다는 것입니다. 예를 들어 아래 샘플 코드는 1000개의 행만 사용합니다. 각 반복에 대한 정확도를 저장할 수 있습니다.

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

그런 다음 부트스트랩 모델의 정확도가 정렬됩니다. 그 후, 모델의 정확도의 10번째 및 90번째 분위수는 주어진 샘플 크기로 모델의 정확도에 대한 95% 신뢰 구간이 된다.

![성향 점수의 신뢰 구간을 표시하는 인쇄 명령입니다.](../images/use-cases/confidence-interval.png)

위 그림은 모델을 교육하기 위해 1000개의 행만 사용하는 경우 정확도가 약 84%와 88% 사이에 떨어질 것으로 예상할 수 있음을 나타냅니다. 모델의 성능을 보장하기 위해 필요에 따라 쿼리 서비스 쿼리에서 `LIMIT` 절을 조정할 수 있습니다.
