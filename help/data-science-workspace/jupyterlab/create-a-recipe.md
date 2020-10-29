---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics;create recipe
solution: Experience Platform
title: Jupiter 노트북을 사용하여 레시피 만들기
topic: tutorial
type: Tutorial
description: 이 튜토리얼은 두 개의 기본 섹션을 살펴봅니다. 먼저 JupiterLab 노트북 내에서 템플릿을 사용하여 기계 학습 모델을 만듭니다. 그런 다음 JupiterLab 내에서 레서피 워크플로우에 맞게 노트북을 실행함으로써 데이터 과학 작업 공간 내에 레서피 작업을 만들 수 있습니다.
translation-type: tm+mt
source-git-commit: adaa7fbaf78a37131076501c21bf18559c17ed94
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 0%

---


# Jupiter 노트북을 사용하여 레시피 만들기

이 튜토리얼은 두 개의 기본 섹션을 살펴봅니다. 먼저, 안에 템플릿을 사용하여 기계 학습 모델을 만듭니다 [!DNL JupyterLab Notebook]. 그런 다음 노트북 내에서 레서피 작업 과정 [!DNL JupyterLab] 을 수행하여 레서피 내의 레서피 [!DNL Data Science Workspace]를 만듭니다.

## 개념 도입:

- **레서피:** 레시피는 모델 사양에 대한 Adobe의 용어로, 특정 기계 학습, AI 알고리즘 또는 알고리즘, 처리 로직, 구성 등을 나타내는 최상위 컨테이너로, 숙련된 모델을 구축하고 실행하는 데 필요한 처리 로직 및 구성을 나타냅니다. 따라서 특정 비즈니스 문제를 해결하는 데 도움이 됩니다.
- **모델:** 모델은 비즈니스 사용 사례를 해결하기 위해 내역 데이터 및 구성을 사용하여 교육되는 기계 학습 레서피 인스턴스입니다.
- **교육:** 트레이닝은 레이블이 지정된 데이터에서 패턴과 인사이트를 배우는 프로세스입니다.
- **점수 지정:** 채점이란 교육된 모델을 사용하여 데이터로부터 통찰력을 생성하는 프로세스입니다.

## 노트북 환경 [!DNL JupyterLab] 시작하기

처음부터 조리법을 만드는 것은 안에서 할 수 [!DNL Data Science Workspace]있다. 시작하려면 [Adobe Experience Platform](https://platform.adobe.com) 로 이동하고 **[!UICONTROL 왼쪽에 있는 노트북]** 탭을 클릭합니다. 폴더에서 레서피 빌더 템플릿을 선택하여 새 노트를 만듭니다 [!DNL JupyterLab Launcher].

Recipe [!UICONTROL Builder] 전자 필기장을 사용하면 노트북 내에서 트레이닝과 점수 지정을 실행할 수 있습니다. 이렇게 하면 교육 실행 및 점수 지정 데이터 간 `train()` 의 해당 방법과 `score()` 방법을 변경할 수 있습니다. 트레이닝 및 점수 출력 결과에 만족하면 Recipe Builder 노트북에 내장된 레서피 기능을 사용하여 전자 필기장을 [!DNL Data Science Workspace] 사용하는 레시피를 만들 수 있습니다.

>[!NOTE]
>
>Recipe Builder 전자 필기장은 모든 파일 포맷을 사용하여 작업할 수 있지만 현재 레서피 만들기 기능은 지원만 합니다 [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder.png)

론쳐에서 레서피 빌더 노트북을 클릭하면 해당 노트가 탭에서 열립니다. 노트북에 사용되는 템플릿은 Python Retail Sales Forecast Recipe이며 [이 공용 저장소에서 찾을 수 있습니다](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

도구 모음에는 기차 **[!UICONTROL , 점수]**&#x200B;및 레서피 **[!UICONTROL 만들기]**&#x200B;등 세 가지 추가 작업 **[!UICONTROL 이 있음을 알 수]**&#x200B;있습니다. 이러한 아이콘은 [!UICONTROL 레서피 빌더] 노트북에만 나타납니다. 이러한 작업에 대한 자세한 내용은 노트북 [에서 레서피](#training-and-scoring) 작성 후 교육 및 점수 지정 섹션에서 다룹니다.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 레서피 파일을 편집합니다

레서피 파일을 편집하려면 파일 경로에 해당하는 Jupiter의 셀로 이동합니다. 예를 들어 를 변경하려면 `evaluator.py`찾습니다 `%%writefile demo-recipe/evaluator.py`.

셀에 필요한 변경 작업을 시작하고 완료되면 셀을 실행하기만 하면 됩니다. 이 `%%writefile filename.py` 명령은 셀의 내용을 에 씁니다 `filename.py`. 변경 사항이 있는 각 파일에 대해 셀을 수동으로 실행해야 합니다.

>[!NOTE]
>
>해당되는 경우 셀을 수동으로 실행해야 합니다.

## Recipe Builder 노트북 시작하기

이제 노트북 환경의 기본 사항을 알고 있으므로 기계 학습 모델 레시피를 구성하는 파일을 볼 수 있습니다. [!DNL JupyterLab] Adobe가 설명하는 파일은 다음과 같습니다.

- [요구 사항 파일](#requirements-file)
- [구성 파일](#configuration-files)
- [교육 데이터 로더](#training-data-loader)
- [점수 데이터 로더](#scoring-data-loader)
- [파이프라인 파일](#pipeline-file)
- [평가기 파일](#evaluator-file)
- [데이터 보호기 파일](#data-saver-file)

### 요구 사항 파일 {#requirements-file}

요구 사항 파일은 레시피에서 사용할 추가 라이브러리를 선언하는 데 사용됩니다. 종속성이 있는 경우 버전 번호를 지정할 수 있습니다. 추가 라이브러리를 찾으려면 [anconda.org를 방문하십시오](https://anaconda.org). 요구 사항 파일의 형식을 지정하는 방법을 알아보려면 Content를 [참조하십시오](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). 이미 사용 중인 기본 라이브러리 목록은 다음과 같습니다.

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>추가한 라이브러리 또는 특정 버전은 위의 라이브러리와 호환되지 않을 수 있습니다. 또한 환경 파일을 수동으로 만들도록 선택하는 경우 이 `name` 필드는 재정의할 수 없습니다.

### 구성 파일 {#configuration-files}

구성 파일 `training.conf` 과 `scoring.conf`는 하이퍼링크 매개 변수를 추가하는 것은 물론 교육 및 점수 지정에 사용할 데이터 세트를 지정하는 데 사용됩니다. 교육 및 채점에는 별도의 구성이 있습니다.

교육 및 점수 지정을 실행하기 전에 다음 변수를 입력해야 합니다.
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

데이터 세트 및 스키마 ID를 찾으려면 왼쪽 탐색 막대의 전자 필기장 내 데이터 탭으로 이동합니다(폴더 아이콘).

![](../images/jupyterlab/create-recipe/datasets.png)

스키마 및 데이터 세트 탭 아래의 [Adobe Experience Platform](https://platform.adobe.com/) 에서 **[동일한 정보를](https://platform.adobe.com/schema)** 찾을 **[수](https://platform.adobe.com/dataset/overview)** 있습니다.

기본적으로 다음 구성 매개 변수는 데이터에 액세스할 때 설정됩니다.

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 교육 데이터 로더 {#training-data-loader}

교육 데이터 로더의 목적은 기계 학습 모델을 만드는 데 사용되는 데이터를 인스턴스화하는 것입니다. 일반적으로 교육 데이터 로더가 수행하는 두 가지 작업이 있습니다.
- 데이터 로드 위치 [!DNL Platform]
- 데이터 준비 및 기능 엔지니어링

다음 두 섹션에서는 데이터 및 데이터 준비를 자세히 설명합니다.

### 데이터 로드 중 {#loading-data}

이 단계에서는 [판다 데이터 프레임을 사용합니다](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). SDK( [!DNL Adobe Experience Platform] SDK)를 [!DNL Platform] 사용하여 파일`platform_sdk`에서 또는 판다의 `read_csv()` 기능이나 기능을 사용하는 외부 소스에서 데이터를 로드할 수 `read_json()` 있습니다.

- [[!DNL Platform SDK]](#platform-sdk)
- [외부 소스](#external-sources)

>[!NOTE]
>
>레서피 빌더 노트북에서 데이터는 `platform_sdk` 데이터 로더를 통해 로드됩니다.

### [!DNL Platform] SDK {#platform-sdk}

데이터 로더 사용에 대한 자세한 자습서는 `platform_sdk` 플랫폼 SDK 가이드를 참조하십시오 [](../authoring/platform-sdk.md). 이 자습서에서는 인증 빌드, 데이터 기본 읽기 및 데이터 기본 쓰기에 대한 정보를 제공합니다.

### 외부 소스 {#external-sources}

이 섹션에서는 JSON 또는 CSV 파일을 판다 오브젝트로 가져오는 방법을 보여 줍니다. 판다 라이브러리의 공식 설명서도 확인할 수 있다.
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

먼저, 다음은 CSV 파일을 가져오는 예입니다. 이 `data` 인수는 CSV 파일의 경로입니다. 이 변수는 `configProperties` 이전 섹션 [](#configuration-files)의

```PYTHON
df = pd.read_csv(data)
```

JSON 파일에서도 가져올 수 있습니다. 이 `data` 인수는 CSV 파일의 경로입니다. 이 변수는 `configProperties` 이전 섹션 [](#configuration-files)의

```PYTHON
df = pd.read_json(data)
```

이제 데이터가 데이터 프레임 개체에 있으며 [다음 섹션에서 분석 및 조작할 수 있습니다](#data-preparation-and-feature-engineering).

### 플랫폼 SDK에서

플랫폼 SDK를 사용하여 데이터를 로드할 수 있습니다. 다음 줄을 포함하여 페이지 맨 위에 라이브러리를 가져올 수 있습니다.

`from platform_sdk.dataset_reader import DatasetReader`

그런 다음 이 `load()` 방법을 사용하여 구성( `trainingDataSetId` ) 파일에 설정된`recipe.conf`대로 교육 데이터 세트를 가져옵니다.

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    
    dataset_reader = DatasetReader(client_context, config_properties['trainingDataSetId'])
    
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

>[!NOTE]
>
>구성 [파일 섹션에](#configuration-files)설명된 대로 다음을 사용하여 Experience Platform의 데이터에 액세스할 때 다음과 같은 구성 매개 변수가 설정됩니다 `client_context`.
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


이제 데이터 준비 및 기능 엔지니어링부터 시작할 수 있습니다.

### 데이터 준비 및 기능 엔지니어링 {#data-preparation-and-feature-engineering}

데이터가 로드되면 데이터가 준비를 거쳐 `train` 및 `val` 데이터 세트로 분할됩니다. 샘플 코드는 다음과 같습니다.

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

이 예에서는 원래 데이터 세트에 대해 수행되는 다섯 가지 작업이 있습니다.
- 추가 `week` 및 `year` 열
- 표시기 변수 `storeType` 로 변환
- 숫자 변수 `isHoliday` 로 변환
- 차후 `weeklySales` 의 판매 가치 및 이전
- 데이터를 날짜별로, 데이터 `train` 및 `val` 데이터 세트에 분할

첫 번째, `week` 및 `year` 열이 만들어지고 원래 `date` 열이 datetime으로 [!DNL Python][변환됩니다](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). datetime 개체에서 주 및 연도 값이 추출됩니다.

다음으로 `storeType` 세 가지 다른 스토어 유형(`A`, `B`및 `C`)을 나타내는 세 개의 열로 변환됩니다. 각에는 true인 부울 값 `storeType` 이 포함됩니다. 열이 `storeType` 삭제됩니다.

마찬가지로 `weeklySales` 부울을 숫자 표현 1이나 0으로 `isHoliday` 변경합니다.

이 데이터는 데이터 세트 `train` 와 데이터 세트 간에 `val` 분할됩니다.

이 `load()` 함수는 출력물로 `train` 및 `val` 데이터 세트를 포함해야 합니다.

### 점수 데이터 로더 {#scoring-data-loader}

점수 지정을 위해 데이터를 로드하는 절차는 함수 로딩 교육 데이터와 `split()` 유사합니다. Adobe는 데이터 액세스 SDK를 사용하여 Adobe `scoringDataSetId` 파일 `recipe.conf` 에서 찾은 데이터를 로드합니다.

```PYTHON
def load(config_properties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    client_context = get_client_context(config_properties)

    dataset_reader = DatasetReader(client_context, config_properties['scoringDataSetId'])
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

데이터를 로드한 후 데이터 준비 및 기능 엔지니어링이 수행됩니다.

```PYTHON
    #########################################
    # Data Preparation/Feature Engineering
    #########################################
    if '_id' in dataframe.columns:
        #Rename columns to strip tenantId
        dataframe = dataframe.rename(columns = lambda x : str(x)[str(x).find('.')+1:])
        #Drop id, eventType and timestamp
        dataframe.drop(['_id', 'eventType', 'timestamp'], axis=1, inplace=True)

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

    print("Scoring Data Load Finish")

    return dataframe
```

이 모델의 목적은 향후 주간 판매를 예측하는 것이기 때문에 모델의 예측치가 얼마나 잘 수행되는지 평가하기 위해 점수 데이터 세트를 만들어야 합니다.

이 Recipe Builder 전자 필기장은 주간 판매 7일을 전달하여 이 작업을 수행합니다. 매주 45개의 스토어에 대한 측정들이 있으므로 45개의 데이터 세트 값을 `weeklySales` 새로운 열(New Column)으로 전송할 수 있습니다 `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

마찬가지로, 45개의 뒤로 이동하여 열 `weeklySalesLag` 을 만들 수 있습니다. 이를 사용하여 주별 매출에서 차이를 계산하여 열에 저장할 수도 있습니다 `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

45개의 데이터 세트와 45개의 데이터 세트를 뒤로 `weeklySales` 오프셋하여 새 열을 만들기 때문에 첫 번째 및 마지막 45개의 데이터 포인트에는 NaN 값이 있습니다. NaN 값이 있는 모든 행을 제거하는 `df.dropna()` 함수를 사용하여 데이터 세트에서 이러한 점을 제거할 수 있습니다.

```PYTHON
df.dropna(0, inplace=True)
```

점수 데이터 로더의 `load()` 함수는 점수 데이터 세트를 출력로 완료해야 합니다.

### 파이프라인 파일 {#pipeline-file}

이 `pipeline.py` 파일에는 트레이닝 및 점수에 대한 논리가 포함되어 있습니다.

### 교육 {#training}

교육 목적은 교육 데이터 세트에 있는 기능과 레이블을 사용하여 모델을 만드는 것입니다.

>[!NOTE]
> 
>기능은 기계 학습 모델에서 레이블을 예측하기 위해 사용하는 입력 변수를 나타냅니다.

이 `train()` 기능은 훈련 모델을 포함하고 훈련된 모델을 반납해야 한다. 다양한 모델의 몇 가지 예는 [scickit-learn 사용 안내서 설명서에서 확인할 수 있습니다](https://scikit-learn.org/stable/user_guide.html).

트레이닝 모델을 선택한 후 x 및 y 트레이닝 데이터 세트에 맞게 모델이 조정되고 이 기능은 훈련 모델을 반환합니다. 예를 들면 다음과 같습니다.

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

애플리케이션에 따라 `GradientBoostingRegressor()` 함수에 인수가 있습니다. `xTrainingDataset` 에는 트레이닝에 사용되는 기능이 포함되지만 레이블은 `yTrainingDataset` 포함되어야 합니다.

### 점수 지정 {#scoring}

이 `score()` 함수에는 점수 지정 알고리즘이 포함되어 있어야 하며 모델이 얼마나 성공했는지 나타내는 측정을 반환합니다. 이 `score()` 함수는 점수 데이터 세트 레이블과 트레이닝된 모델을 사용하여 예측된 일련의 기능을 생성합니다. 그런 다음 이러한 예측된 값을 점수 데이터 세트에 있는 실제 기능과 비교합니다. 이 예에서 이 `score()` 함수는 훈련 모델을 사용하여 점수 지정 데이터 세트의 레이블을 사용하여 기능을 예측합니다. 예측된 기능이 반환됩니다.

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

### 평가기 파일 {#evaluator-file}

이 `evaluator.py` 파일에는 트레이닝 레시피를 평가할 방법과 교육 데이터를 분할할 방법에 대한 논리가 포함되어 있습니다. 소매 판매 예에서 교육 데이터를 로드하고 준비하는 논리가 포함됩니다. 아래 두 부분으로 넘어가겠습니다

### 데이터 세트 분할 {#split-the-dataset}

교육 데이터 준비 단계를 수행하려면 교육 및 테스트에 사용할 데이터 세트를 분할해야 합니다. 이 `val` 데이터는 훈련 후에 모델을 평가하는 데 암시적으로 사용됩니다. 이 프로세스는 채점과는 별개입니다.

이 섹션에는 데이터를 먼저 노트북에 로드한 다음 데이터 세트에 있는 관련 없는 열을 제거하여 데이터를 정리하는 기능이 표시됩니다. `split()` 여기서 기존 Raw 기능에서 추가 관련 기능을 만드는 과정인 기능 엔지니어링을 수행할 수 있습니다. 이 프로세스의 예는 아래에 설명과 함께 확인할 수 있습니다.

이 `split()` 함수는 아래에 나와 있습니다. 인수에 제공된 데이터 프레임은 반환되는 변수 `train` 및 변수로 `val` 분할됩니다.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### 교육된 모델 평가 {#evaluate-the-trained-model}

이 `evaluate()` 기능은 모델이 교육된 후에 수행되며 모델이 얼마나 성공하는지를 나타내는 지표를 반환합니다. 이 `evaluate()` 함수는 테스트 데이터 세트 레이블과 교육된 모델을 사용하여 일련의 기능을 예측합니다. 그런 다음 이러한 예측된 값을 테스트 데이터 세트의 실제 기능과 비교합니다. 일반적인 점수 알고리즘에는 다음이 포함됩니다.
- [평균 절대 백분율 오류(MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [평균 절대 오류(MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
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

이 함수는 평가 지표의 배열을 포함하는 `metric` 개체를 반환한다는 것을 확인합니다. 이러한 지표는 훈련된 모델이 얼마나 잘 작동하는지 평가하는 데 사용됩니다.

### 데이터 보호기 파일 {#data-saver-file}

이 `datasaver.py` 파일에는 점수 지정 시 예측을 저장하는 `save()` 함수가 들어 있습니다. 이 `save()` 함수를 사용하면 예측 및 [!DNL Experience Platform Catalog] API를 사용할 수 있으며, 데이터를 `scoringResultsDataSetId` 파일에 지정한 데이터 `scoring.conf` 에 작성할 수 있습니다.

소매 판매 샘플 레서피에 사용된 예는 여기에 나와 있습니다. 라이브러리를 사용하여 플랫폼에 데이터를 `DataSetWriter` 작성할 수 있습니다.

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

## 트레이닝 및 채점 {#training-and-scoring}

전자 필기장을 변경하고 레서피 교육을 수행하려는 경우 막대 맨 위에 있는 관련 단추를 클릭하여 셀에서 교육 실행을 만들 수 있습니다. 이 단추를 클릭하면 교육 스크립트의 명령 및 출력 로그가 `evaluator.py` 셀 아래에 있는 전자 필기장에 나타납니다. Conda는 먼저 모든 종속성을 설치한 다음, 교육을 시작합니다.

점수를 매기려면 최소 한 번은 교육을 실행해야 합니다. [점수 **[!UICONTROL 실행]** ] 단추를 클릭하면 교육 중에 생성된 교육된 모델에 대해 점수가 매겨집니다. 점수 지정 스크립트가 아래에 나타납니다 `datasaver.py`.

디버깅을 위해 숨겨진 출력을 보려면 출력 셀 끝 `debug` 에 추가하고 다시 실행하십시오.

## 레서피 만들기 {#create-recipe}

레서피 편집 작업이 완료되고 교육/점수 출력 결과에 만족하면 오른쪽 위 탐색 영역에서 레서피 **[!UICONTROL 만들기]** 를 눌러 노트북에서 레서피 레시피를 만들 수 있습니다.

![](../images/jupyterlab/create-recipe/create-recipe.png)

단추를 누른 후 레서피 이름을 입력하라는 메시지가 표시됩니다. 이 이름은 에서 만든 실제 레시피를 나타냅니다 [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

확인 **[!UICONTROL 을]** 누르면 [Adobe Experience Platform](https://platform.adobe.com/)의 새로운 조리법을 찾을 수 있다. 레서피 **[!UICONTROL 보기]** 버튼을 클릭하여 **[!UICONTROL ML 모델 아래의]** 레서피 **[!UICONTROL 탭으로이동할 수있습니다]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

과정이 완료되면 레시피는 다음과 같이 표시됩니다.

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - 파일 셀을 삭제하지 않음
> - 파일 셀 위쪽에 있는 `%%writefile` 줄을 편집하지 마십시오
> - 여러 전자 필기장에서 동시에 레시피를 만들지 마십시오


## 다음 단계 {#next-steps}

이 튜토리얼을 완료하여 Recipe Builder 노트북에서 기계 학습 모델을 만드는 방법을 학습했습니다. 또한 노트북 내에서 레서피 워크플로우에 노트를 적용하는 방법을 학습하여 레서피 내에 레서피를 만드는 방법을 학습했습니다 [!DNL Data Science Workspace].

내에서 리소스를 사용하여 작업하는 방법을 계속 학습하려면 [!DNL Data Science Workspace]레서피 및 모델 드롭다운을 [!DNL Data Science Workspace] 방문하십시오.

## 추가 리소스 {#additional-resources}

다음 비디오는 모델 구축 및 배포에 대한 사용자의 이해를 지원하기 위해 만들어졌습니다.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


