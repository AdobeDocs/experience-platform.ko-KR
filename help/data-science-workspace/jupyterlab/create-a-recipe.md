---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Jupiter 노트북을 사용하여 레서피 만들기
topic: Tutorial
translation-type: tm+mt
source-git-commit: 3190f2f01ae13d25cc3a3a540b83cc1fc0819f0a

---


# Jupiter 노트북을 사용하여 레서피 만들기

이 자습서는 두 개의 주요 섹션으로 구성됩니다. 먼저 JupiterLab Notebook 내에서 템플릿을 사용하여 기계 학습 모델을 만듭니다. 그런 다음 JupiterLab에서 레서피 워크플로우에 대한 노트북을 실행하여 데이터 과학 작업 공간 내에서 레서피를 만들 수 있습니다.
- [JupiterLab 노트북 환경 시작하기](#get-started-with-the-jupyterlab-notebook-environment)
- [레서피 파일을 편집합니다.](#make-edits-to-recipe-files)
- [Recipe Builder 노트북 시작하기](#get-started-with-the-recipe-builder-notebook)
   - [요구 사항 파일](#requirements-file)
   - [구성 파일](#configuration-files)
   - [교육 데이터 로더](#training-data-loader)
   - [점수 데이터 로더](#scoring-data-loader)
   - [파이프라인 파일](#pipeline-file)
   - [평가기 파일](#evaluator-file)
   - [데이터 보호기 파일](#data-saver-file)
- [트레이닝 및 점수](#training-and-scoring)
- [레서피 만들기](#create-recipe)

## 개념 도입:

- **레서피:** 레서피는 Adobe의 모델 사양 용어로, 특정 기계 학습, AI 알고리즘 또는 알고리즘의 조합, 처리 로직 및 구성을 나타내는 최상위 컨테이너로, 숙련된 모델을 만들고 실행하는 데 필요한 구성, 특정 비즈니스 문제를 해결하는 데 도움이 됩니다.
- **모델:** 모델은 비즈니스 사용 사례를 해결하기 위해 내역 데이터 및 구성을 사용하여 교육되는 기계 학습 레서피의 한 예입니다.
- **교육:** 트레이닝은 레이블이 지정된 데이터에서 패턴과 인사이트를 학습하는 프로세스입니다.
- **점수 지정:** 점수 책정기는 교육된 모델을 사용하여 데이터에서 인사이트를 생성하는 프로세스입니다.

## JupiterLab 노트북 환경 시작하기

처음부터 레서피 만들기는 데이터 과학 작업 공간에서 수행할 수 있습니다. 시작하려면 Adobe Experience [Platform](https://platform.adobe.com) 으로 이동하고 왼쪽의 **ML Models** 탭을 클릭하여 데이터 과학 작업 영역으로 이동합니다. 여기서 노트북 하위 **탭을 클릭하고** Jupiterlab launcher 화면에서 Recipe Builder 템플릿을 선택하여 새 전자 필기장을 만듭니다.

Recipe Builder 전자 필기장을 사용하면 노트북 내에서 트레이닝 및 점수 지정 실행을 실행할 수 있습니다. 이렇게 하면 교육 실행 `train()` 및 점수 지정 데이터 간의 해당 방법과 `score()` 방법을 변경할 수 있습니다. 트레이닝 및 점수의 결과에 만족하면 Recipe Builder 노트북에 내장된 레서피 기능을 사용하여 데이터 과학 작업 공간에서 사용할 레서피를 만들 수 있습니다.

>[!NOTE] Recipe Builder 전자 필기장은 모든 파일 포맷을 사용하여 작업할 수 있지만 현재 레서피 만들기 기능은 Python만 지원합니다.

![](../images/jupyterlab/create-recipe/notebook_launcher.png)

launcher에서 Recipe Builder 전자 필기장을 클릭하면 해당 전자 필기장이 탭에 열립니다. 전자 필기장에 사용되는 템플릿은 Python Retail Sales Forecast Recipe이며 [이 공용 저장소에서 찾을 수 있습니다](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

도구 모음에는 기차, 점수, 레서피 만들기 등 세 가지 추가 **작업이****** **있습니다**. 이러한 아이콘은 Recipe Builder 전자 필기장에만 나타납니다. 이러한 작업에 대한 자세한 내용은 전자 필기장에서 레서피를 [작성한 후 교육 및 점수 지정 섹션에서](#training-and-scoring) 설명합니다.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 레서피 파일을 편집합니다.

<!-- Databricks update to recipe needed -->
레서피 파일을 편집하려면 파일 경로에 해당하는 Jupiter의 셀로 이동합니다. 예를 들어, 를 변경하려면 `evaluator.py`를 `%%writefile demo-recipe/evaluator.py`찾습니다.

셀에 필요한 변경 작업을 시작하고 완료되면 셀을 실행하기만 하면 됩니다. 이 `%%writefile filename.py` 명령은 셀의 내용을 에 씁니다 `filename.py`. 변경 사항이 있는 각 파일에 대해 셀을 수동으로 실행해야 합니다.

>[!NOTE] 해당되는 경우 셀을 수동으로 실행해야 합니다.

## Recipe Builder 노트북 시작하기

이제 JupiterLab 노트북 환경의 기본 사항을 알고 있으므로 머신 러닝 모델 레서피를 구성하는 파일을 살펴볼 수 있습니다. 다음에 대해 설명하는 파일이 표시됩니다.

- [요구 사항 파일](#requirements-file)
- [구성 파일](#configuration-files)
- [교육 데이터 로더](#training-data-loader)
- [점수 데이터 로더](#scoring-data-loader)
- [파이프라인 파일](#pipeline-file)
- [평가기 파일](#evaluator-file)
- [데이터 보호기 파일](#data-saver-file)




### 요구 사항 파일

요구 사항 파일은 레서피에 사용할 추가 라이브러리를 선언하는 데 사용됩니다. 종속성이 있는 경우 버전 번호를 지정할 수 있습니다. 추가 라이브러리를 보려면 https://anaconda.org을 참조하십시오. 이미 사용 중인 기본 라이브러리 목록은 다음과 같습니다.

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE] 추가한 라이브러리 또는 특정 버전은 위의 라이브러리와 호환되지 않을 수 있습니다.



### 구성 파일

구성 파일 `training.conf` 및 `scoring.conf`는 하이퍼링크 매개 변수를 추가하는 것뿐만 아니라 교육 및 점수 지정에 사용할 데이터 세트를 지정하는 데 사용됩니다. 트레이닝 및 채점에는 별도의 구성이 있습니다.

교육 및 점수 지정을 실행하기 전에 다음 변수를 입력해야 합니다.
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

데이터 세트 및 스키마 ID를 찾으려면 왼쪽 탐색 막대의 전자 필기장 내 데이터 탭으로 이동합니다(폴더 아이콘 아래).

![](../images/jupyterlab/create-recipe/data_tab.png)

Adobe Experience Platform에서 스키마 [및 데이터](https://platform.adobe.com/) 집합 **[탭 아래에서](https://platform.adobe.com/schema)**동일한**[&#x200B;정보를](https://platform.adobe.com/dataset/overview)** 찾을 수있습니다.

기본적으로 다음 구성 매개 변수는 데이터에 액세스할 때 설정됩니다.

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`



## 교육 데이터 로더

교육 데이터 로더의 목적은 시스템 학습 모델을 만드는 데 사용되는 데이터를 인스턴스화하기 위한 것입니다. 일반적으로 교육 데이터 로더에서 수행하는 두 가지 작업이 있습니다.
- 플랫폼에서 데이터 로드
- 데이터 준비 및 기능 엔지니어링

다음 두 섹션은 데이터 로드 및 데이터 준비 단계를 진행합니다.

### 데이터 로드

이 단계에서는 [팬더 데이터 프레임을 사용합니다](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). 플랫폼 SDK(`platform_sdk`)를 사용하여 Adobe Experience Platform의 파일에서 또는 팬더의 `read_csv()` 기능이나 `read_json()` 기능을 사용하여 외부 소스에서 데이터를 로드할 수 있습니다.

- [플랫폼 SDK](#platform-sdk)
- [외부 소스](#external-sources)

>[!NOTE] Recipe Builder 전자 필기장에서 데이터는 `platform_sdk` 데이터 로더를 통해 로드됩니다.

### 플랫폼 SDK

데이터 로더 사용에 대한 자세한 자습서는 `platform_sdk` 플랫폼 SDK [가이드를](../authoring/platform-sdk.md)참조하십시오. 이 자습서에서는 인증 빌드, 기본 데이터 읽기 및 기본적인 데이터 쓰기에 대한 정보를 제공합니다.

### 외부 소스

이 섹션에서는 JSON 또는 CSV 파일을 팬더 개체에 가져오는 방법을 보여 줍니다. 팬더 라이브러리의 공식 설명서는 다음과 같습니다.
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

먼저, 다음은 CSV 파일을 가져오는 예입니다. 이 `data` 인수는 CSV 파일의 경로입니다. 이 변수는 `configProperties` 이전 섹션의 [](#configuration-files)에서 가져왔습니다.

```PYTHON
df = pd.read_csv(data)
```

JSON 파일에서도 가져올 수 있습니다. 이 `data` 인수는 CSV 파일의 경로입니다. 이 변수는 `configProperties` 이전 섹션의 [](#configuration-files)에서 가져왔습니다.

```PYTHON
df = pd.read_json(data)
```

이제 데이터가 데이터 프레임 개체에 있으며 [다음 섹션에서](#data-preparation-and-feature-engineering)분석 및 조작할 수 있습니다.



### 데이터 액세스 SDK에서(더 이상 사용되지 않음)

>[!CAUTION]  더 `data_access_sdk_python` 이상 권장되지 않습니다. 데이터 [로더 사용에 대한 지침은 데이터 액세스 코드를 플랫폼 SDK로](../authoring/platform-sdk.md) 변환을 참조하십시오 `platform_sdk` .

사용자는 데이터 액세스 SDK를 사용하여 데이터를 로드할 수 있습니다. 다음 줄을 포함하여 페이지 맨 위에 라이브러리를 가져올 수 있습니다.

`from data_access_sdk_python.reader import DataSetReader`

그런 다음 이 `load()` 방법을 사용하여 구성( `trainingDataSetId` ) 파일에 설정된`recipe.conf`대로 교육 데이터 세트를 가져옵니다.

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE] 구성 파일 [섹션에](#configuration-files)설명된 대로, 경험 플랫폼에서 데이터에 액세스할 때 다음 구성 매개 변수가 설정됩니다.
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


이제 데이터를 준비하면 데이터 준비 및 기능 엔지니어링부터 시작할 수 있습니다.

### 데이터 준비 및 기능 엔지니어링

데이터가 로드되면 데이터가 준비되고 `train` 및 `val` 데이터 세트로 분할됩니다. 샘플 코드는 다음과 같습니다.

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

이 예에서는 원본 데이터 세트에 대해 수행되는 다섯 가지 작업이 있습니다.
- 추가 `week` 및 `year` 열
- 표시기 `storeType` 변수로 변환
- 숫자 `isHoliday` 변수로 변환
- 차후 판매 `weeklySales` 가치 확보
- 데이터를 날짜별로, `train` 데이터 및 `val` 데이터 세트에 분할

첫 번째, `week` 및 `year` 열이 만들어지고 원래 `date` 열이 Python [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html)으로 변환됩니다. datetime 개체에서 주 및 연도 값이 추출됩니다.

그런 다음 `storeType` 세 개의 서로 다른 스토어 유형(`A`, `B`및 `C`)을 나타내는 세 개의 열로 변환됩니다. 각 요소에는 true인 부울 값이 `storeType` 포함됩니다. 열이 `storeType` 삭제됩니다.

마찬가지로 `weeklySales` `isHoliday` 부울을 숫자 표현 1이나 0으로 변경합니다.

이 데이터는 `train` 데이터 세트와 `val` 데이터 세트 간에 분할됩니다.

이 `load()` 함수는 `train` 및 `val` 데이터 세트를 출력물로 작성해야 합니다.

### 점수 데이터 로더

점수 지정을 위해 데이터를 로드하는 절차는 `split()` 함수의 로드 교육 데이터와 유사합니다. Adobe는 데이터 액세스 SDK를 사용하여 `scoringDataSetId` `recipe.conf` 파일에 있는 데이터로부터 데이터를 로드합니다.

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

데이터 로드 후 데이터 준비 및 기능 엔지니어링이 수행됩니다.

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

Adobe 모델의 목적은 향후 주별 매출을 예측하는 것이기 때문에 모델의 예측치가 얼마나 잘 수행되는지를 평가하는 데 사용되는 점수 데이터 세트를 만들어야 합니다.

이 Recipe Builder 전자 필기장은 주별Sales 7일의 전달을 상쇄하여 이렇게 합니다. 매주 45개의 스토어에 대한 측정값이 있으므로 45개의 데이터 세트를 새 열()로 전달할 수 `weeklySales` `weeklySalesAhead`있습니다.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

마찬가지로, 45를 다시 `weeklySalesLag` 이동함으로써 열을 만들 수 있습니다. 이 기능을 사용하면 주간 판매의 차이를 계산하여 열에 저장할 수도 `weeklySalesDiff`있습니다.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

데이터 `weeklySales` 아포스트인 45개와 데이터 세트 45개를 뒤로 오프셋하여 새 열을 만들기 때문에 첫 번째 및 마지막 45개의 데이터 포인트에는 NaN 값이 있습니다. NaN 값이 있는 모든 행을 제거하는 `df.dropna()` 함수를 사용하여 데이터 세트에서 이러한 점을 제거할 수 있습니다.

```PYTHON
df.dropna(0, inplace=True)
```

점수 데이터 로더의 `load()` 함수는 점수 데이터 세트를 출력로 완료해야 합니다.



### 파이프라인 파일

이 `pipeline.py` 파일에는 트레이닝 및 점수 책정기가 포함됩니다. 다음 두 개 부문으로 모두 검토해 보겠습니다.

### 트레이닝

트레이닝의 목적은 트레이닝 데이터 세트에 있는 기능과 레이블을 사용하여 모델을 만드는 것입니다.

>[!NOTE]  기능은 _기계 학습 모델에서_ 레이블을 __&#x200B;예측하기 위해 사용하는 입력 변수를 나타냅니다.

이 `train()` 기능에는 트레이닝 모델이 포함되고 훈련 모델을 돌려주어야 합니다. 다양한 모델의 몇 가지 예는 [과학 기술 학습 사용 설명서](https://scikit-learn.org/stable/user_guide.html)문서를 참조하십시오.

교육 모델을 선택한 후 x 및 y 트레이닝 데이터 세트를 모델에 맞게 구성하면 이 함수는 트레이닝된 모델을 반환합니다. 이를 보여주는 예는 다음과 같습니다.

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

애플리케이션에 따라 `GradientBoostingRegressor()` 함수에 인수가 있습니다. `xTrainingDataset` 에는 트레이닝에 사용되는 기능이 포함되어 있어야 하며 레이블은 `yTrainingDataset` 포함되어야 합니다.



### 점수 지정

이 `score()` 함수에는 점수 지정 알고리즘이 포함되어 있어야 하며 모델이 얼마나 성공적으로 수행되는지를 나타내는 측정을 반환합니다. 이 `score()` 기능은 점수 데이터 세트 레이블과 트레이닝된 모델을 사용하여 예측된 기능 세트를 생성합니다. 그런 다음 이러한 예측된 값을 점수 데이터 세트의 실제 기능과 비교합니다. 이 예에서는 이 `score()` 함수가 교육 모델을 사용하여 점수 지정 데이터 세트의 레이블을 사용하여 기능을 예측합니다. 예측된 기능이 반환됩니다.

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### 평가기 파일

이 `evaluator.py` 파일에는 트레이닝된 레서피를 평가하는 방법과 교육 데이터를 분할하는 방법에 대한 로직이 포함되어 있습니다. 소매 판매 예에서 교육 데이터를 로드하고 준비하는 논리가 포함됩니다. 아래 두 부분으로 넘어가겠습니다

### 데이터 세트 분할

교육 데이터 준비 단계에서는 교육 및 테스트에 사용할 데이터 세트를 분할해야 합니다. 이 `val` 데이터는 교육 후 모델을 평가하는 데 암시적으로 사용됩니다. 이 프로세스는 채점과는 별개입니다.

이 섹션에는 데이터를 노트북으로 먼저 로드한 다음 데이터 세트에 있는 관련 없는 열을 제거하여 데이터를 정리하는 `split()` 함수가 표시됩니다. 여기서 기존 Raw 기능에서 추가 관련 기능을 생성하는 과정인 기능 엔지니어링을 수행할 수 있습니다. 이 프로세스의 예는 아래에 설명과 함께 확인할 수 있습니다.

이 `split()` 함수는 아래에 나와 있습니다. 인수에 제공된 데이터 프레임은 반환되는 `train` 변수와 `val` 변수로 분할됩니다.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### 교육된 모델 평가

이 `evaluate()` 기능은 모델이 교육된 후에 수행되며 모델이 얼마나 성공적으로 작동하는지 나타내는 지표를 반환합니다. 이 `evaluate()` 함수는 테스트 데이터 세트 레이블과 교육된 모델을 사용하여 기능 세트를 예측합니다. 그런 다음 이러한 예측된 값을 테스트 데이터 세트의 실제 기능과 비교합니다. 일반적인 점수 알고리즘에는 다음이 포함됩니다.
- [평균 절대 백분율 오류(MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [평균 절대 오류(매)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [루트 평균 제곱 오류(RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


소매 판매 샘플의 `evaluate()` 기능은 다음과 같습니다.

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

이 함수는 평가 지표 배열을 포함하는 `metric` 객체를 반환합니다. 이러한 지표는 훈련된 모델이 얼마나 잘 작동하는지 평가하는 데 사용됩니다.

### 데이터 보호기 파일

이 `datasaver.py` 파일에는 점수 지정 시 예측을 저장하는 `save()` 함수가 들어 있습니다. 이 `save()` 함수는 예측을 가져와 Experience Platform Catalog API를 사용하여 데이터를 `scoringResultsDataSetId` `scoring.conf` 파일에 지정한 데이터에 기록합니다.

소매 판매 샘플 레서피에 사용된 예는 여기 있습니다. 라이브러리를 사용하여 플랫폼에 데이터를 `DataSetWriter` 쓸 수 있습니다.

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```


## 트레이닝 및 점수

전자 필기장을 변경하고 레서피를 교육하려면 막대 맨 위에 있는 관련 단추를 클릭하여 셀에서 교육 실행을 만들 수 있습니다. 이 단추를 클릭하면 교육 스크립트의 명령 및 출력 로그가 `evaluator.py` 셀 아래에 있는 전자 필기장에 나타납니다. Conda가 먼저 모든 종속성을 설치한 다음 교육이 시작됩니다.

점수를 매기려면 먼저 적어도 한 번은 교육을 실행해야 합니다. [점수 **실행** ] 단추를 클릭하면 교육 중에 생성된 교육 모델에서 점수가 매겨집니다. 점수 지정 스크립트가 아래에 표시됩니다 `datasaver.py`.

디버깅을 위해 숨겨진 출력을 보려면 출력 셀의 `debug` 끝에 추가한 후 다시 실행하십시오.

## 레서피 만들기

레서피 편집이 완료되고 교육/점수 출력에 만족하면 레서피 만들기를 눌러 수첩에서 레서피를 만들 **수 있습니다**. 단추를 누르면 레서피 이름을 입력하라는 메시지가 표시됩니다. 이 이름은 플랫폼에서 만든 실제 레시피를 나타냅니다.

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

확인을 **누르면** Adobe Experience Platform에서 새로운 레시피로 이동할 [수 있습니다](https://platform.adobe.com/). 레서피 보기 **버튼을 클릭하여** ML 모델 아래의 **레서피** 탭으로 **이동할 수있습니다.**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

과정이 완료되면 레서피는 다음과 같이 표시됩니다.

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
> - 파일 셀을 삭제하지 않음
> - 파일 셀 위쪽에 있는 `%%writefile` 줄을 편집하지 마십시오
> - 여러 전자 필기장에서 동시에 레서피 만들기 안 함


## 다음 단계

이 튜토리얼을 완료하여 Recipe Builder 노트북에서 머신 러닝 모델을 만드는 방법을 알아보았습니다. 또한 노트북 내에서 레서피 워크플로우에 노트북을 사용하여 데이터 과학 작업 공간 내에서 레서피를 만드는 방법을 학습했습니다.

데이터 과학 작업 공간에서 리소스를 사용하여 작업하는 방법을 계속 학습하려면 데이터 과학 작업 공간 레서피 및 모델 드롭다운을 방문하십시오.

## Journey Orchestration용

다음 비디오는 모델 구축 및 배포에 대한 사용자의 이해를 지원하기 위해 만들어졌습니다.

>[!VIDEO](https://images-tv.adobe.com/mpcv3/65884d30-94fe-47ef-8d4e-efafe5303260_1578451719.1920x1080at3000_h264.mp4)


