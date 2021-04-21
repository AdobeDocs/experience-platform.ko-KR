---
keywords: Experience Platform;JupiterLab;레서피;노트북;데이터 과학 작업 공간;인기 있는 주제;레서피 만들기
solution: Experience Platform
title: Jupiter 공책을 사용하여 레서피 만들기
topic-legacy: tutorial
type: Tutorial
description: 이 자습서는 두 개의 기본 섹션을 살펴봅니다. 먼저 JupiterLab Notebook 내에 템플릿을 사용하여 기계 학습 모델을 만듭니다. 그런 다음 JupiterLab 내의 레서피 워크플로에 노트북을 실행하여 데이터 과학 작업 공간 내에서 레서피 작업을 만듭니다.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# Jupiter Notebook을 사용하여 레시피 만들기

이 자습서는 두 개의 기본 섹션을 살펴봅니다. 먼저 [!DNL JupyterLab Notebook] 내의 템플릿을 사용하여 기계 학습 모델을 만듭니다. 그런 다음 [!DNL JupyterLab] 내에서 레서피 작업 과정에 전자 필기장을 실행하여 [!DNL Data Science Workspace] 내에 레서피를 만듭니다.

## 도입됨:

- **레서피:** 레서피는 모델 사양에 대한 Adobe의 용어이며 특정 기계 학습, AI 알고리즘 또는 알고리즘, 처리 로직 및 구성을 나타내는 최상위 컨테이너로, 훈련 모델을 만들고 실행하는 데 필요한 특정 비즈니스 문제를 해결하는 데 도움이 됩니다.
- **모델:** 모델은 비즈니스 사용 사례를 해결하기 위해 내역 데이터 및 구성을 사용하여 교육되는 기계 학습 레서피 인스턴스입니다.
- **트레이닝:** 트레이닝은 레이블이 지정된 데이터에서 패턴 및 인사이트를 학습하는 프로세스입니다.
- **점수** 채점: 채점이란 훈련된 모델을 사용하여 데이터로부터 통찰력을 생성하는 프로세스입니다.

## [!DNL JupyterLab] 노트북 환경 시작하기

처음부터 레서피 만들기는 [!DNL Data Science Workspace] 내에서 수행할 수 있습니다. 시작하려면 [Adobe Experience Platform](https://platform.adobe.com)으로 이동하고 왼쪽의 **[!UICONTROL Notebooks]** 탭을 클릭합니다. [!DNL JupyterLab Launcher]에서 레서피 빌더 템플릿을 선택하여 새 전자 필기장을 만듭니다.

[!UICONTROL Recipe Builder] 전자 필기장을 사용하면 노트북 내에서 트레이닝과 점수 지정 실행을 실행할 수 있습니다. 따라서 교육 및 점수 데이터에 대한 실험을 실행하는 동안 `train()` 및 `score()` 메서드를 변경할 수 있습니다. 트레이닝 및 점수 출력 결과가 만족스러우면 Recipe Builder 노트북에 내장된 레서피 기능을 사용하여 [!DNL Data Science Workspace]에서 사용할 레서피를 만들 수 있습니다.

>[!NOTE]
>
>Recipe Builder 전자 필기장은 모든 파일 형식 작업을 지원하지만 현재 레서피 만들기 기능은 [!DNL Python]만 지원합니다.

![](../images/jupyterlab/create-recipe/recipe_builder.png)

launcher에서 Recipe Builder 전자 필기장을 클릭하면 전자 필기장이 탭에서 열립니다. 노트북에 사용되는 템플릿은 [이 공용 저장소](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)에서도 찾을 수 있는 Python Retail 판매 예측 레서피입니다.

도구 모음에는 **[!UICONTROL Train]**, **[!UICONTROL Score]** 및 **[!UICONTROL Create Recipe]** 등 3개의 추가 작업이 있습니다. 이러한 아이콘은 [!UICONTROL Recipe Builder] 전자 필기장에만 나타납니다. 이러한 작업에 대한 자세한 내용은 전자 필기장에서 레서피를 작성한 후 교육 및 점수 지정 섹션](#training-and-scoring)에서 [에 대해 설명합니다.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 레서피 파일을 편집합니다.

레서피 파일을 편집하려면 파일 경로에 해당하는 Jupiter의 셀로 이동합니다. 예를 들어 `evaluator.py`을 변경하려면 `%%writefile demo-recipe/evaluator.py`을 찾습니다.

셀에 필요한 변경 작업을 시작하고 완료되면 셀을 실행하기만 하면 됩니다. `%%writefile filename.py` 명령은 `filename.py`에 셀의 내용을 기록합니다. 변경 사항이 있는 각 파일에 대해 셀을 수동으로 실행해야 합니다.

>[!NOTE]
>
>해당되는 경우 셀을 수동으로 실행해야 합니다.

## Recipe Builder 노트북 시작하기

이제 [!DNL JupyterLab] 노트북 환경의 기본 사항을 알고 있으므로 기계 학습 모델 레서피를 구성하는 파일을 볼 수 있습니다. 다음에 대해 설명하는 파일이 표시됩니다.

- [요구 사항 파일](#requirements-file)
- [구성 파일](#configuration-files)
- [교육 데이터 로더](#training-data-loader)
- [점수 데이터 로더](#scoring-data-loader)
- [파이프라인 파일](#pipeline-file)
- [평가기 파일](#evaluator-file)
- [데이터 보호기 파일](#data-saver-file)

### 요구 사항 파일 {#requirements-file}

요구 사항 파일은 레서피에 사용할 추가 라이브러리를 선언하는 데 사용됩니다. 종속성이 있는 경우 버전 번호를 지정할 수 있습니다. 추가 라이브러리를 찾으려면 [아나콘다.org](https://anaconda.org)를 방문하십시오. 요구 사항 파일의 형식을 지정하는 방법에 대해 알아보려면 [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually)를 방문하십시오. 이미 사용 중인 기본 라이브러리 목록은 다음과 같습니다.

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>추가한 라이브러리 또는 특정 버전은 위의 라이브러리와 호환되지 않을 수 있습니다. 또한 환경 파일을 수동으로 만들도록 선택하는 경우 `name` 필드는 재정의할 수 없습니다.

### 구성 파일 {#configuration-files}

구성 파일인 `training.conf` 및 `scoring.conf`은 하이퍼매개 변수를 추가하는 것뿐만 아니라 교육 및 채점하는 데 사용할 데이터 세트를 지정하는 데 사용됩니다. 교육과 채점에는 별도의 구성이 있습니다.

교육 및 점수를 실행하기 전에 다음 변수를 입력해야 합니다.
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

데이터 세트 및 스키마 ID를 찾으려면 왼쪽 탐색 막대의 전자 필기장 내 ![데이터 탭](../images/jupyterlab/create-recipe/dataset-tab.png)으로 이동합니다(폴더 아이콘 아래).

![](../images/jupyterlab/create-recipe/dataset_tab.png)

[Adobe Experience Platform](https://platform.adobe.com/)스키마](https://platform.adobe.com/schema)**및**[&#x200B;데이터 집합](https://platform.adobe.com/dataset/overview)**탭에서 동일한 정보를 찾을 수 있습니다.**[

기본적으로 다음 구성 매개 변수는 데이터에 액세스할 때 설정됩니다.

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 교육 데이터 로더 {#training-data-loader}

교육 데이터 로더의 목적은 기계 학습 모델을 만드는 데 사용되는 데이터를 인스턴스화하는 것입니다. 일반적으로 교육 데이터 로더에서 수행하는 2가지 작업은 다음과 같습니다.
- [!DNL Platform]에서 데이터 로드
- 데이터 준비 및 기능 엔지니어링

다음 두 섹션은 데이터 로드 및 데이터 준비 단계를 안내합니다.

### 데이터 {#loading-data} 로드 중

이 단계에서는 [판다 데이터 프레임](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)을 사용합니다. [!DNL Platform] SDK(`platform_sdk`)를 사용하여 [!DNL Adobe Experience Platform]의 파일에서 또는 팬더의 `read_csv()` 또는 `read_json()` 함수를 사용하는 외부 소스에서 데이터를 로드할 수 있습니다.

- [[!DNL Platform SDK]](#platform-sdk)
- [외부 소스](#external-sources)

>[!NOTE]
>
>레서피 빌더 노트북에서 데이터는 `platform_sdk` 데이터 로더를 통해 로드됩니다.

### [!DNL Platform] SDK {#platform-sdk}

`platform_sdk` 데이터 로더 사용에 대한 자세한 자습서는 [플랫폼 SDK 안내서](../authoring/platform-sdk.md)를 참조하십시오. 이 자습서에서는 빌드 인증, 기본적인 데이터 읽기 및 기본적인 데이터 쓰기에 대한 정보를 제공합니다.

### 외부 소스 {#external-sources}

이 섹션에서는 JSON 또는 CSV 파일을 판다 객체로 가져오는 방법을 보여 줍니다. 판다 라이브러리의 공식 설명서는 아래와 같다.
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

먼저, 다음은 CSV 파일을 가져오는 예입니다. `data` 인수는 CSV 파일의 경로입니다. 이 변수는 [이전 섹션](#configuration-files)의 `configProperties`에서 가져왔습니다.

```PYTHON
df = pd.read_csv(data)
```

JSON 파일에서도 가져올 수 있습니다. `data` 인수는 CSV 파일의 경로입니다. 이 변수는 [이전 섹션](#configuration-files)의 `configProperties`에서 가져왔습니다.

```PYTHON
df = pd.read_json(data)
```

이제 데이터가 데이터 프레임 개체에 있으며 [다음 섹션](#data-preparation-and-feature-engineering)에서 분석 및 조작할 수 있습니다.

### 플랫폼 SDK에서

플랫폼 SDK를 사용하여 데이터를 로드할 수 있습니다. 다음 줄을 포함하여 페이지 맨 위에 라이브러리를 가져올 수 있습니다.

`from platform_sdk.dataset_reader import DatasetReader`

그런 다음 `load()` 메서드를 사용하여 `trainingDataSetId`의 교육 데이터 집합을 구성(`recipe.conf`) 파일에 설정된 대로 가져옵니다.

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
>[구성 파일 섹션](#configuration-files)에서 설명한 바와 같이 `client_context`를 사용하여 Experience Platform의 데이터에 액세스할 때 다음 구성 매개 변수가 설정됩니다.
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


이제 데이터를 준비하면서 데이터 준비 및 기능 엔지니어링부터 시작할 수 있습니다.

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

이 예제에서는 원래 데이터 세트에 대해 다음 5가지를 수행합니다.
- `week` 및 `year` 열 추가
- `storeType`을(를) 표시기 변수로 변환
- `isHoliday`을(를) 숫자 변수로 변환
- 미래 및 이전 판매 값을 얻기 위해 `weeklySales` 오프셋
- 데이터를 날짜별로 `train` 및 `val` 데이터 세트에 분할

먼저 `week` 및 `year` 열이 만들어지고 원래 `date` 열이 [!DNL Python] [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html)으로 변환됩니다. datetime 객체에서 주 및 연도 값이 추출됩니다.

다음으로 `storeType`은(는) 세 가지 다른 스토어 유형(`A`, `B` 및 `C`)을 나타내는 3개의 열로 변환됩니다. 각 항목에는 `storeType`이(가) true인 부울 값이 포함됩니다. `storeType` 열이 삭제됩니다.

마찬가지로 `weeklySales`은 `isHoliday` 부울을 숫자 표현인 1이나 0으로 변경합니다.

이 데이터는 `train`과 `val` 데이터 세트 간에 분할됩니다.

`load()` 함수는 `train` 및 `val` 데이터 집합을 출력으로 완료해야 합니다.

### 점수 데이터 로더 {#scoring-data-loader}

점수 지정을 위해 데이터를 로드하는 절차는 `split()` 함수의 로드 교육 데이터와 유사합니다. 데이터 액세스 SDK를 사용하여 `recipe.conf` 파일에 있는 `scoringDataSetId`의 데이터를 로드합니다.

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

데이터를 로드하면 데이터 준비 및 기능 엔지니어링이 수행됩니다.

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

Adobe 모델의 목적은 향후 주별 매출을 예측하기 위한 것이므로 모델의 예측치가 얼마나 잘 수행되는지를 평가하는 데 사용되는 점수 데이터 세트를 만들어야 합니다.

이 Recipe Builder 노트북은 주간 판매 7일을 전달합니다. 매주 45개의 스토어에 대한 측정값이 있으므로 `weeklySales` 값 45개를 `weeklySalesAhead`이라는 새 열로 전송할 수 있습니다.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

마찬가지로 이동된 45로 `weeklySalesLag` 열을 만들 수도 있습니다. 이를 사용하여 주별 매출에서의 차이를 계산하고 `weeklySalesDiff` 열에 저장할 수도 있습니다.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

`weeklySales` 데이터를 45개의 데이터 세트와 45개의 데이터 세트를 뒤로 오프셋하여 새 열을 만들기 때문에 첫 번째 및 마지막 45개의 데이터 포인트에는 NaN 값이 있습니다. NaN 값이 있는 모든 행을 제거하는 `df.dropna()` 함수를 사용하여 데이터 세트에서 이러한 점을 제거할 수 있습니다.

```PYTHON
df.dropna(0, inplace=True)
```

점수 데이터 로더의 `load()` 함수는 점수 데이터 세트를 출력로 완료해야 합니다.

### 파이프라인 파일 {#pipeline-file}

`pipeline.py` 파일에는 트레이닝 및 점수에 대한 로직이 포함되어 있습니다.

### 교육 {#training}

교육 목적은 교육 데이터 세트에 있는 기능과 레이블을 사용하여 모델을 만드는 것입니다.

>[!NOTE]
> 
>기능은 기계 학습 모델에서 레이블을 예측하기 위해 사용하는 입력 변수를 참조합니다.

`train()` 함수는 교육 모델을 포함하고 훈련된 모델을 반환해야 합니다. 다른 모델의 몇 가지 예는 [scikit-learn 사용 안내서 설명서](https://scikit-learn.org/stable/user_guide.html)에서 찾을 수 있습니다.

트레이닝 모델을 선택한 후 x 및 y 트레이닝 데이터 세트를 모델에 맞게 구성하면 이 함수는 트레이닝된 모델을 반환합니다. 이를 보여주는 예는 다음과 같습니다.

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

응용 프로그램에 따라 `GradientBoostingRegressor()` 함수에 인수가 있습니다. `xTrainingDataset` 에는 트레이닝에 사용되는 기능이 포함되어야 하며 이때 레이블은  `yTrainingDataset` 포함되어야 합니다.

### 점수 지정 {#scoring}

`score()` 함수는 점수 지정 알고리즘을 포함하고 측정을 반환하여 모델이 얼마나 성공적으로 수행되는지를 나타냅니다. `score()` 함수는 점수 데이터 집합 레이블과 훈련된 모델을 사용하여 예측된 기능 집합을 생성합니다. 그런 다음 이러한 예측된 값을 점수 데이터 세트의 실제 기능과 비교합니다. 이 예에서 `score()` 함수는 훈련 모델을 사용하여 점수 지정 데이터 세트의 레이블을 사용하여 기능을 예측합니다. 예측된 기능이 반환됩니다.

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

`evaluator.py` 파일에는 트레이닝 데이터를 분할하는 방법뿐만 아니라 트레이닝된 레서피를 평가할 방법에 대한 로직이 포함되어 있습니다. 소매 판매 예에서 교육 데이터를 로드하고 준비하는 논리가 포함됩니다. 아래 두 부분으로 넘어가겠습니다

### 데이터 세트 {#split-the-dataset} 분할

교육 데이터 준비 단계를 수행하려면 교육 및 테스트에 사용할 데이터 세트를 분할해야 합니다. 이 `val` 데이터는 교육을 받은 후 모델을 평가하는 데 암시적으로 사용됩니다. 이 프로세스는 채점과는 별개입니다.

이 섹션에는 데이터를 노트북에 먼저 로드한 다음 데이터 세트에 있는 관련 없는 열을 제거하여 데이터를 정리하는 `split()` 함수가 표시됩니다. 여기서, 데이터의 기존 원시 기능에서 관련 추가 기능을 만드는 과정인 기능 엔지니어링을 수행할 수 있습니다. 이 프로세스의 예는 아래에 설명과 함께 확인할 수 있습니다.

`split()` 함수가 아래에 표시됩니다. 인수에 제공된 데이터 프레임은 반환될 `train` 및 `val` 변수로 분할됩니다.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### 교육된 모델 {#evaluate-the-trained-model} 평가

`evaluate()` 함수는 모델이 훈련된 후에 수행되며 모델이 성공적으로 수행되는 방식을 나타내는 지표를 반환합니다. `evaluate()` 함수는 테스트 데이터 세트 레이블과 Trained 모델을 사용하여 일련의 기능을 예측합니다. 그런 다음 이러한 예측된 값을 테스트 데이터 세트의 실제 기능과 비교합니다. 일반적인 채점 알고리즘에는 다음이 포함됩니다.
- [절대 백분율 평균 오류(MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [평균 절대 오류(MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [루트 평균 제곱형 오류(RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


소매 판매 샘플의 `evaluate()` 함수는 아래와 같습니다.

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

### 데이터 보호기 파일 {#data-saver-file}

`datasaver.py` 파일에는 점수를 테스트하는 동안 예측을 저장할 `save()` 함수가 포함되어 있습니다. `save()` 함수는 예측을 수행하고 [!DNL Experience Platform Catalog] API를 사용하여 `scoring.conf` 파일에 지정한 `scoringResultsDataSetId`에 데이터를 씁니다.

소매 판매 샘플 레서피에 사용된 예는 여기에 있습니다. `DataSetWriter` 라이브러리를 사용하여 플랫폼에 데이터를 쓸 수 있습니다.

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

## 트레이닝 및 점수 {#training-and-scoring}

전자 필기장에 대한 변경 작업을 완료하고 레서피 교육을 받으려면 막대 맨 위에 있는 관련 단추를 클릭하여 셀에서 교육 실행을 만들 수 있습니다. 단추를 클릭하면 교육 스크립트의 명령 및 출력 로그가 전자 필기장(`evaluator.py` 셀 아래)에 나타납니다. Conda는 먼저 모든 종속성을 설치한 다음, 교육이 시작됩니다.

점수를 매기기 전에 최소 한 번 트레이닝을 실행해야 합니다. **[!UICONTROL Run Scoring]** 단추를 클릭하면 교육 중에 생성된 훈련 모델에 점수가 지정됩니다. 채점 스크립트가 `datasaver.py` 아래에 나타납니다.

디버깅을 위해 숨겨진 출력을 보려면 출력 셀의 끝에 `debug`을 추가하고 다시 실행하십시오.

## 레서피 {#create-recipe} 만들기

레서피를 편집하고 트레이닝/점수 출력 결과에 만족하면 오른쪽 위 탐색에서 **[!UICONTROL Create Recipe]**&#x200B;을 눌러 노트북에서 레서피를 만들 수 있습니다.

![](../images/jupyterlab/create-recipe/create-recipe.png)

단추를 누르면 레서피 이름을 입력하라는 메시지가 표시됩니다. 이 이름은 [!DNL Platform]에서 만든 실제 레서피를 나타냅니다.

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

**[!UICONTROL Ok]**&#x200B;을 누르면 [Adobe Experience Platform](https://platform.adobe.com/)에서 새 레서피를 탐색할 수 있습니다. **[!UICONTROL View Recipes]** 단추를 클릭하여 **[!UICONTROL ML Models]** 아래의 **[!UICONTROL Recipes]** 탭으로 이동할 수 있습니다.

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

과정이 완료되면 레시피는 다음과 같이 표시됩니다.

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - 파일 셀을 삭제하지 않음
> - 파일 셀의 맨 위에 있는 `%%writefile` 행을 편집하지 마십시오.
> - 여러 전자 필기장에서 동시에 레서피를 만들지 마십시오.


## 다음 단계 {#next-steps}

이 자습서를 완료하면 Recipe Builder 노트북에서 기계 학습 모델을 만드는 방법을 알아보았습니다. 또한 전자 필기장 내의 레서피 작업 과정을 사용하여 [!DNL Data Science Workspace] 내에 레서피를 만드는 방법을 학습했습니다.

[!DNL Data Science Workspace] 내에서 리소스를 사용하여 작업하는 방법을 계속 학습하려면 [!DNL Data Science Workspace] 레서피 및 모델 드롭다운을 방문하십시오.

## 추가 리소스 {#additional-resources}

다음 비디오는 모델 구축 및 배포에 대한 이해를 지원하기 위해 만들어졌습니다.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)
