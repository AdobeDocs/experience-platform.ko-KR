---
keywords: Experience Platform; 주피터랩; 처방; 노트북; 데이터 과학 작업 영역; 인기 있는 주제; 레서피 만들기
solution: Experience Platform
title: JupyterLab Notebooks를 사용하여 모델 만들기
type: Tutorial
description: 이 튜토리얼은 JupiterLab 노트북 레서피 빌더 템플릿을 사용하여 레서피를 만드는 데 필요한 단계를 안내합니다.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 0%

---

# JupyterLab Notebooks를 사용하여 모델 만들기

>[!NOTE]
>
>Data Science 작업 영역은(는) 더 이상 구매할 수 없습니다.
>
>이 설명서는 데이터 과학 작업 영역 이전에 사용 권한이 있는 기존 고객을 대상으로 합니다.

이 튜토리얼은 JupiterLab 노트북 레서피 빌더 템플릿을 사용하여 모델을 생성하는 데 필요한 단계를 안내합니다.

## 도입된 개념:

- **레시피:** 레서피는 모델 사양에 대한 Adobe Systems 용어이며 특정 기계 학습, AI 알고리즘 또는 알고리즘 앙상블, 처리 논리 및 학습된 모델을 빌드 및 실행하는 데 필요한 구성을 나타내는 최상위 컨테이너입니다.
- **모델:** 모델은 비즈니스 사용 사례를 해결하기 위해 내역 데이터 및 구성을 사용하여 학습된 기계 학습 레서피의 인스턴스입니다.
- **학습:** 학습은 레이블이 지정된 데이터에서 패턴과 인사이트를 학습하는 프로세스입니다.
- **채점:** 채점은 학습된 모델을 사용하여 데이터에서 인사이트를 생성하는 프로세스입니다.

## 필요한 에셋 다운로드 {#assets}

이 자습서를 진행하기 전에 필요한 스키마 및 데이터 세트를 만들어야 합니다. [Luma 성향 모델 스키마 및 데이터 세트 만들기](../models-recipes/create-luma-data.md)에 대한 자습서를 방문하여 필요한 자산을 다운로드하고 사전 요구 사항을 설정합니다.

## [!DNL JupyterLab] 전자 필기장 환경 시작

레시피를 처음부터 만드는 작업은 [!DNL Data Science Workspace] 내에 수행할 수 있습니다. 시작하려면 [Adobe Experience Platform](https://platform.adobe.com)(으)로 이동하여 왼쪽의 **[!UICONTROL 전자 필기장]** 탭을 선택하십시오. 새 전자 필기장을 만들려면 [!DNL JupyterLab Launcher]에서 Recipe Builder 템플릿을 선택하십시오.

Recipe Builder] 노트북을 [!UICONTROL 사용하면 노트북 내에서 교육 및 채점 실행을 실행할 수 있습니다. 이렇게 하면 교육 및 점수 매기기 데이터에 대한 실험 실행 사이에 메서드를 `score()` 변경할 `train()` 수 있는 유연성이 제공됩니다. 교육 및 채점의 결과가 만족스러우면 레서피를 만들고 레서피를 사용하여 기능성을 모델링하는 모델로 게시할 수 있습니다.

>[!NOTE]
>
>Recipe Builder 노트북은 [!UICONTROL 모든 파일 형식 작업을 지원하지만 현재 레서피 만들기 기능은 [!DNL Python].]

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

런처에서 Recipe Builder] 노트북을 [!UICONTROL 선택하면 노트북이 새 탭 열립니다.

맨 위에 있는 새 Notebook 탭에는 세 가지 추가 작업( **[!UICONTROL 학습]**, **[!UICONTROL 점수]** 매기기 및 **[!UICONTROL 레시피]** 만들기)이 포함된 도구 모음이 로드됩니다. 이러한 아이콘은 Recipe Builder] 노트북에만 [!UICONTROL 나타납니다. 이러한 작업에 대한 자세한 내용은 노트북에서 레시피를 작성한 후 교육 및 점수 섹션에서](#training-and-scoring) 확인할 [수 있습니다.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Recipe Builder] 노트북 시작하기 [!UICONTROL 

제공된 에셋 폴더에는 Luma 성향 모델 `propensity_model.ipynb`이(가) 있습니다. JupyterLab의 노트북 업로드 옵션을 사용하여 제공된 모델을 업로드하고 노트북을 엽니다.

![전자 필기장 업로드](../images/jupyterlab/create-recipe/upload_notebook.png)

이 자습서의 나머지 부분에서는 성향 모델 전자 필기장에 미리 정의된 다음 파일을 다룹니다.

- [요구 사항 파일](#requirements-file)
- [구성 파일](#configuration-files)
- [교육 데이터 로더](#training-data-loader)
- [점수 매기기 데이터 로더](#scoring-data-loader)
- [파이프라인 파일](#pipeline-file)
- [평가기 파일](#evaluator-file)
- [데이터 세이버 파일](#data-saver-file)

다음 비디오 튜토리얼 에서는 Luma 성향 모델 노트북에 대해 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### 요구 사항 파일 {#requirements-file}

요구 사항 파일은 모델에서 사용할 추가 라이브러리를 선언하는 데 사용됩니다. 종속성이 있는 경우 버전 번호를 지정할 수 있습니다. 추가 라이브러리를 찾으려면 anaconda.org](https://anaconda.org) 방문[. 요구 사항 파일을 포맷 방법을 알아보려면 Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually)를 방문[. 이미 사용 중인 기본 라이브러리 목록은 다음과 같습니다.

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>추가하는 라이브러리 또는 특정 버전은 위의 라이브러리와 호환되지 않을 수 있습니다. 또한 환경 파일을 수동으로 만들도록 선택하면 `name` 필드를 재정의할 수 없습니다.

Luma 성향 모델 노트북의 경우 요구 사항을 업데이트할 필요가 없습니다.

### 구성 파일 {#configuration-files}

구성 파일 `training.conf` 및 `scoring.conf`은(는) 하이퍼매개 변수를 추가하고 교육 및 채점에 사용할 데이터 세트를 지정하는 데 사용됩니다. 교육 및 채점에 대한 별도의 구성이 있습니다.

모델이 교육 교육을 실행하려면 , `ACP_DSW_TRAINING_XDM_SCHEMA`, 및 `tenantId`를 제공해야 `trainingDataSetId`합니다. 또한 점수를 매기려면 , `tenantId`, 및 `scoringResultsDataSetId `를 제공해야 `scoringDataSetId`합니다.

데이터 세트 및 스키마 ID를 찾으려면 왼쪽 탐색 표시줄(폴더 아이콘 아래)에 있는 Notebook 내의 데이터 탭 ![데이터 탭](../images/jupyterlab/create-recipe/dataset-tab.png) 로 이동합니다. 세 가지 다른 데이터 세트 ID를 제공해야 합니다. `scoringResultsDataSetId` 모델 점수 매기기 결과를 스토어 데 사용되며 빈 데이터 세트이어야 합니다. 이러한 데이터 세트는 이전에 [필수 자산](#assets) 단계에서 만들어졌습니다.

![](../images/jupyterlab/create-recipe/dataset_tab.png)

스키마 및 **[데이터 세트](https://platform.adobe.com/dataset/overview)** 탭 아래의&#x200B;**](https://platform.adobe.com/schema)**[ Adobe Experience Platform](https://platform.adobe.com/)에서 동일한 정보를 찾을 [수 있습니다.

경쟁하면 교육 및 점수 구성이 다음 스크린샷과 유사해야 합니다.

![구성](../images/jupyterlab/create-recipe/config.png)

기본적으로 다음 구성 매개 변수는 데이터를 학습하고 점수를 매길 때 설정됩니다.

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 교육 데이터 로더 이해 {#training-data-loader}

교육 데이터 로더의 목적은 기계 학습 모델을 만드는 데 사용되는 데이터를 인스턴스화하는 것입니다. 일반적으로 교육 데이터 로더가 수행하는 작업은 다음 두 가지가 있습니다.

- 데이터 로드 위치 [!DNL Platform]
- 데이터 준비 및 기능 엔지니어링

다음 두 섹션에서는 데이터 로드 및 데이터 준비에 대해 설명합니다.

### 데이터 로드 {#loading-data}

이 단계에서는 pandas 데이터 프레임](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)을 [사용합니다. 데이터는 SDK ()를 [!DNL Platform] 사용하여 파일 [!DNL Adobe Experience Platform] 에서로드하거나 pandas의 `read_csv()` 또는 `read_json()` 함수를 사용하여 외부 소스에서로드 할 수 있습니다.`platform_sdk`

- [[!DNL Platform SDK]](#platform-sdk)
- [외부 소스](#external-sources)

>[!NOTE]
>
>Recipe Builder 노트북에서 데이터는 데이터 로더를 통해 로드됩니다 `platform_sdk` .

### [!DNL Platform] SDK {#platform-sdk}

데이터 로더 사용에 `platform_sdk` 대한 자세한 튜토리얼 보려면 Platform SDK 안내서](../authoring/platform-sdk.md) 방문[하십시오. 이 튜토리얼에서는 빌드 인증, 기본 데이터 읽기 및 기본 데이터 쓰기에 대한 정보를 제공합니다.

### 외부 소스 {#external-sources}

이 섹션에서는 JSON 또는 CSV 파일을 pandas 객체로 가져오는 방법을 보여줍니다. pandas 라이브러리의 공식 문서는 다음에서 찾을 수 있습니다.
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

먼저 CSV 파일을 가져오는 예를 살펴보겠습니다. `data` 인수는 CSV 파일의 경로입니다. 이 변수 는 이전 섹션에서 가져왔 `configProperties` [습니다](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

JSON 파일에서 가져올 수도 있습니다. `data` 인수는 CSV 파일의 경로입니다. 이 변수 는 이전 섹션에서 가져왔 `configProperties` [습니다](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

이제 데이터가 데이터 프레임 개체에 있으며 [다음 섹션](#data-preparation-and-feature-engineering)에서 분석 및 조작할 수 있습니다.

## 교육 데이터 로더 파일

이 예에서 데이터는 Platform SDK를 사용하여 로드됩니다. 다음 줄을 포함하여 페이지 맨 위에 라이브러리를 가져올 수 있습니다.

`from platform_sdk.dataset_reader import DatasetReader`

그런 다음 `load()` 메서드를 사용하여 구성(`recipe.conf`) 파일에 설정된 대로 `trainingDataSetId`에서 교육 데이터 세트를 가져올 수 있습니다.

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>구성 파일 섹션에](#configuration-files) 언급된 [대로 다음을 사용하여 `client_context = get_client_context(config_properties)`Experience Platform 에서 데이터에 액세스할 때 다음 구성 매개 변수가 설정됩니다.
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`

이제 데이터가 있으므로 데이터 준비 및 기능 엔지니어링을 시작할 수 있습니다.

### 데이터 준비 및 기능 엔지니어링 {#data-preparation-and-feature-engineering}

데이터가 로드된 후에는 데이터를 정리하고 데이터 준비를 거쳐야 합니다. 이 예제에서 모델의 목표는 고객이 제품을 주문할지 여부를 예측하는 것입니다. 모델이 특정 제품을 검토하지 않기 때문에 사용자가 필요하지 `productListItems` 않으므로 열이 삭제됩니다. 다음, 단일 열에 단일 값 또는 두 개의 값만 포함하는 추가 열이 삭제됩니다. 모델을 교육 할 때 목표를 예측하는 데 도움이되는 유용한 데이터 만 유지하는 것이 중요합니다.

![데이터 준비의 예](../images/jupyterlab/create-recipe/data_prep.png)

불필요한 데이터를 삭제한 후에는 기능 엔지니어링을 시작할 수 있습니다. 이 예제에 사용된 데모 데이터에는 세션 정보가 포함되어 있지 않습니다. 일반적으로 특정 고객의 현재 및 과거 세션에 대한 데이터를 보유해야 합니다. 세션 정보의 부족으로 인해 이 예는 대신 여정 경계를 통해 현재 및 과거 세션을 모방합니다.

![여정 경계](../images/jupyterlab/create-recipe/journey_demarcation.png)

경계가 완료되면 데이터에 레이블이 지정되고 여정이 만들어집니다.

![데이터에 레이블 지정](../images/jupyterlab/create-recipe/label_data.png)

다음으로 피쳐가 생성되고 과거와 현재로 나뉩니다. 그런 다음 불필요한 열이 삭제되어 Luma 고객의 과거 및 현재 여정이 모두 표시됩니다. 이러한 여정은 고객이 항목을 구매했는지 여부, 구매까지 소요한 여정 등과 같은 정보를 포함합니다.

![최종 현재 교육](../images/jupyterlab/create-recipe/final_journey.png)

## 채점 데이터 로더 {#scoring-data-loader}

점수 매기기를 위해 데이터를 로드하는 절차는 교육 데이터 로드와 비슷합니다. 코드를 자세히 살펴보면 를 제외한 `scoringDataSetId` 모든 것이 동일하다는 것을 알 수 있습니다 `dataset_reader`. 이는 동일한 Luma 데이터 소스가 교육 및 점수 매기기에 모두 사용되기 때문입니다.

교육 및 점수 매기기에 서로 다른 데이터 파일을 사용하려는 경우 교육 및 점수 매기기 데이터 로더는 별개입니다. 이렇게 하면 필요한 경우 교육 데이터 매핑과 같은 추가 전처리를 수행할 수 있습니다.

## 파이프라인 파일 {#pipeline-file}

파일에는 교육 및 채점을 위한 논리가 `pipeline.py` 포함되어 있습니다.

교육의 목적은 교육 데이터 세트 기능과 레이블을 사용하여 모델을 만드는 것입니다. 교육 모델을 선택한 후 x 및 y 교육 데이터 세트를 모델에 적합해야 하며 함수는 교육된 모델을 반환합니다.

>[!NOTE]
> 
>특징은 라벨을 예측하기 위해 기계학습 모형에서 사용하는 입력 변수를 의미한다.

![def train](../images/jupyterlab/create-recipe/def_train.png)

`score()` 함수는 채점 알고리즘을 포함하고 모델이 얼마나 성공적으로 수행되는지 나타내는 측정을 반환해야 합니다. `score()` 함수는 채점 데이터 세트 레이블과 학습된 모델을 사용하여 예측된 기능 집합을 생성합니다. 그런 다음 이러한 예측된 값을 채점 데이터 세트의 실제 기능과 비교합니다. 이 예제 `score()` 에서 함수는 학습된 모델을 사용하여 점수 매기기 데이터 세트 레이블을 사용하여 기능을 예측합니다. 예측된 기능이 반환됩니다.

![DEF 점수](../images/jupyterlab/create-recipe/def_score.png)

## 평가기 파일 {#evaluator-file}

이 파일에는 `evaluator.py` 학습된 레서피 평가 방법과 교육 데이터 분할 방법에 대한 논리가 포함되어 있습니다.

### 데이터 세트 분할 {#split-the-dataset}

교육을 위한 데이터 준비 단계에서는 교육 및 테스트에 사용할 데이터 세트를 분할해야 합니다. 이 `val` 데이터는 학습된 후 모델을 평가하는 데 암시적으로 사용됩니다. 이 프로세스는 점수 매기기와 별개입니다.

이 섹션에서는 데이터를 Notebook에 로드한 다음 데이터 세트 내에서 관련 없는 열을 제거하여 데이터를 정리하는 함수를 보여 줍니다 `split()` . 여기에서 데이터의 기존 원시 기능에서 추가 관련 기능을 만드는 프로세스인 기능 엔지니어링을 수행할 수 있습니다.

![분할 기능](../images/jupyterlab/create-recipe/split.png)

### 학습된 모델 평가 {#evaluate-the-trained-model}

`evaluate()` 함수는 모델을 학습한 후 모델이 얼마나 성공적으로 수행되는지 나타내는 지표를 반환합니다. `evaluate()` 함수는 테스트 데이터 세트 레이블과 학습된 모델을 사용하여 기능 집합을 예측합니다. 그런 다음 이러한 예측 값을 테스트 데이터 세트 내의 실제 기능과 비교합니다. 이 예에서 사용된 지표는 `precision`, `recall`, `f1`, 및 `accuracy`입니다. 이 함수는 평가 지표 배열을 포함하는 개체를 반환합니다 `metric` . 이러한 메트릭은 학습된 모델이 얼마나 잘 수행되는지 평가하는 데 사용됩니다.

![평가하다](../images/jupyterlab/create-recipe/evaluate.png)

추가하면 `print(metric)` 지표 결과를 볼 수 있습니다.

![지표 결과](../images/jupyterlab/create-recipe/evaluate_metric.png)

## 데이터 세이버 파일 {#data-saver-file}

이 `datasaver.py` 파일에는 함수가 `save()` 포함되어 있으며 점수를 테스트하는 동안 예측을 저장하는 데 사용됩니다. 이 `save()` 함수는 예측을 사용하고 API를 사용하여 [!DNL Experience Platform Catalog] 파일에 지정된 데이터에 데이터를 `scoringResultsDataSetId` 씁니다 `scoring.conf` . 당신은 할 수 있습니다

![데이터 세이버](../images/jupyterlab/create-recipe/data_saver.png)

## 교육 및 점수 매기기 {#training-and-scoring}

Notebook 변경을 완료하고 레서피 학습을 수행하려는 경우 막대 맨 위에 있는 관련 단추를 선택하여 셀에서 교육 실행을 만들 수 있습니다. 버튼 선택하면 교육 스크립트의 명령 및 출력 로그가 전자 필기장(셀 아래)에 `evaluator.py` 나타납니다. Conda는 먼저 모든 종속성을 설치 한 다음 교육 단계를 시작합니다.

점수 매기기를 실행하기 전에 교육 교육을 한 번 이상 실행해야 합니다. 점수 매기기&#x200B;]**실행 버튼 단추를 선택하면**[!UICONTROL &#x200B;교육 중에 생성된 학습된 모델에 점수가 매겨집니다. 점수 지정 스크립트가 .`datasaver.py`

디버깅을 위해 숨김 출력을 보려면 출력 셀의 끝에 추가하고 `debug` 다시 실행합니다.

![교육 및 점수](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 레시피 만들기 {#create-recipe}

레시피 편집이 완료되고 교육/채점 결과에 만족하면 오른쪽 상단에서 **[!UICONTROL 레시피 만들기]**&#x200B;를 선택하여 전자 필기장에서 레시피를 만들 수 있습니다.

![](../images/jupyterlab/create-recipe/create-recipe.png)

**[!UICONTROL 레시피 만들기]**&#x200B;를 선택하면 레시피 이름을 입력하라는 메시지가 표시됩니다. 이 이름은 [!DNL Platform]에서 만든 실제 레시피를 나타냅니다.

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

확인을&#x200B;]**선택하면**[!UICONTROL &#x200B;레서피 생성 프로세스가 시작됩니다. 이 작업에는 시간이 걸릴 수 있으며 레시피 만들기 단추 대신 진행률 표시줄이 표시됩니다. 완료되면 보기 Recipes ]**(**[!UICONTROL &#x200B;레서피) 버튼 선택하여 ML Models(ML 모델) **[!UICONTROL 아래의**[!UICONTROL  Recipes(]**레서피) 탭으로 이동할 수 있습니다]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - 파일 셀을 삭제하지 마십시오.
> - 파일 셀의 `%%writefile` 맨 위에 있는 줄은 편집하지 마십시오
> - 서로 다른 노트북에서 동시에 레서피를 만들지 마십시오

## 다음 단계 {#next-steps}

이 튜토리얼 완료를 통해 Recipe Builder] 노트북에서 [!UICONTROL 기계 학습 모델을 생성하는 방법을 배웠습니다. 레서피 작업 과정 위해 노트북을 연습하는 방법도 배웠습니다.

내에서 [!DNL Data Science Workspace]리소스를 사용하는 방법을 계속 배우려면 레서피 및 모델 드롭다운을 [!DNL Data Science Workspace] 방문 하십시오.