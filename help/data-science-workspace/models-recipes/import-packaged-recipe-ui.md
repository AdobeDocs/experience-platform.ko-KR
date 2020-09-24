---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics;recipes;ui;create engine
solution: Experience Platform
title: 패키지된 레서피 가져오기(UI)
topic: tutorial
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 예제를 사용하여 패키지된 레서피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 튜토리얼이 끝나면 Adobe Experience Platform 데이터 과학 작업 공간에서 모델을 생성, 교육 및 평가할 수 있습니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 0%

---


# 패키지된 레서피 가져오기(UI)

이 자습서에서는 제공된 소매 판매 예제를 사용하여 패키지된 레서피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 튜토리얼이 끝나면 Adobe Experience Platform에서 모델을 만들고, 교육하고, 평가할 준비가 됩니다 [!DNL Data Science Workspace].

## 전제 조건

이 자습서에서는 Docker 이미지 URL 형식의 패키지된 레시피가 필요합니다. 자세한 내용은 소스 파일을 레서피에 [패키지하는 방법에 대한 자습서를](./package-source-files-recipe.md) 참조하십시오.

## UI 워크플로우

패키지된 레서피를 가져오려면 단일 JSON(JavaScript Object Notation) 파일로 컴파일된 특정 레서피 구성이 [!DNL Data Science Workspace] 필요합니다. 이 레서피 구성 컴파일을 **구성 파일이라고 합니다**. 특정 구성 세트가 있는 패키지된 레시피는 **레서피 인스턴스라고 합니다**. 한 레시피는 여러 레서피 인스턴스를 만드는 데 사용될 수 있다 [!DNL Data Science Workspace].

패키지 레서피 가져오기 워크플로우는 다음 단계로 구성됩니다.
- [레서피 구성](#configure)
- [Docker 기반 레시피 가져오기 - Python](#python)
- [Docker 기반 레서피 가져오기 - R](#r)
- [Docker 기반의 레서피 가져오기 - PySpark](#pyspark)
- [Docker 기반 레서피 가져오기 - Scala](#scala)

### 레서피 구성 {#configure}

모든 레서피 인스턴스 [!DNL Data Science Workspace] 는 특정 사용 사례에 맞게 레서피 인스턴스를 맞춤화하는 구성 세트와 함께 제공됩니다. 구성 파일은 이 레서피 인스턴스를 사용하여 생성된 모델의 기본 교육 및 점수 동작을 정의합니다.

>[!NOTE]
>
>구성 파일은 레시피 및 대/소문자를 구분합니다.

다음은 소매 영업 레서피에 대한 기본 트레이닝 및 점수 지정 행동을 보여주는 샘플 구성 파일입니다.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| 매개 변수 키 | 유형 | 설명 |
| ----- | ----- | ----- |
| `learning_rate` | 숫자 | 그래디언트 곱셈을 위한 스칼라 |
| `n_estimators` | 숫자 | 임의 포리스트 분류자의 포리스트 내 트리 수입니다. |
| `max_depth` | 숫자 | 임의 포리스트 분류기의 트리 최대 깊이입니다. |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 속성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 특성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부 결정 |
| `tenantId` | 문자열 | 이 ID를 사용하면 만든 리소스가 적절하게 대체되고 IMS 조직 내에 포함됩니다. [테넌트 ID를 찾으려면 여기](../../xdm/api/getting-started.md#know-your-tenant_id) 단계를 따르십시오. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. UI에서 가져올 때는 이 값을 비워 두고, API를 사용하여 가져올 때 교육 스키마 ID로 바꿉니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화에 대한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델을 평가하는 데 사용할 평가 지표의 쉼표로 구분된 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델 채점하는 데 사용되는 출력 스키마입니다. UI에서 가져올 때는 이 값을 비워 두고, API를 사용하여 가져올 때 점수 지정 스키마 ID로 바꿉니다. |

이 자습서의 목적을 위해, 소매 판매 레서피에 대한 기본 구성 파일을 참조(Reference)에 있는 [!DNL Data Science Workspace] 방식으로 둘 수 있습니다.

### Docker 기반 레서피 가져오기 - [!DNL Python] {#python}

먼저 **[!UICONTROL UI의 왼쪽 상단에 있는 워크플로우]** 를 찾아 선택합니다 [!DNL Platform] . 그런 다음 레서피 *가져오기를* 선택하고 **[!UICONTROL 론치를 클릭합니다]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

레서피 *가져오기* 워크플로우에 대한 *구성* 페이지가나타납니다. 레서피에 대한 이름과 설명을 입력한 다음 **[!UICONTROL 오른쪽 위 모서리에서]** 다음을 선택합니다.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Recipe [자습서로](./package-source-files-recipe.md) 패키지 소스 파일의 경우 Python 소스 파일을 사용하여 소매 판매 레서피 작성 종료 시 Docker URL이 제공되었습니다.

소스 *선택* 페이지에 있으면 소스 URL [!DNL Python] 필드에 소스 파일을 사용하여 작성한 패키지된 레서피에 해당하는 Docker URL을 **[!UICONTROL 붙여넣습니다]** . 그런 다음 드래그 앤 드롭하여 제공된 구성 파일을 가져오거나 파일 시스템 **브라우저를 사용합니다**. 제공된 구성 파일은 에서 찾을 수 있습니다 `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Runtime **[!UICONTROL 드롭다운에서 Python]**** 을 **[!UICONTROL 선택하고]** TypeBlackdown *에서 Classification을* 선택합니다. 모든 것이 채워지면 오른쪽 위 **[!UICONTROL 의]** [다음]을 클릭하여 스키마 *관리로 이동합니다*.

>[!NOTE]
>
> *유형은* 분류 **[!UICONTROL 및 회귀]** 를 **[!UICONTROL 지원합니다]**. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 사용자 지정 **[!UICONTROL 을 선택합니다]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

다음으로, [스키마 *관리] 섹션*&#x200B;아래의 소매 판매 입출력 스키마를 선택하여 소매 판매 스키마 및 데이터 세트 자습서 [를 만드는 데 제공된 부트스트랩 스크립트를 사용하여](../models-recipes/create-retails-sales-dataset.md) 만들었습니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

기능 *관리* 섹션 아래에서 스키마 뷰어에서 테넌트 ID를 클릭하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 필드 속성 창에서 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 을 선택하여 **[!UICONTROL 입력 및 출력 기능을]** 선택합니다. 이 자습서의 목적을 위해 weeklySales를 **[!UICONTROL Target]** 기능으로 **[!UICONTROL 설정하고 그 외의 모든 것을]** 입력 기능으로 **[!UICONTROL 설정하십시오]**. 다음 **[!UICONTROL 을]** 클릭하여 새로 구성된 레시피를 검토합니다.

필요에 따라 레시피를 검토하고 구성을 추가, 수정 또는 제거합니다. 마침 **[!UICONTROL 을]** 클릭하여 레시피를 생성합니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

새로 만든 소매 판매 레서피를 사용하여 모델을 생성하는 방법 [을 살펴보려면 다음 단계를](#next-steps) [!DNL Data Science Workspace] 수행합니다.

### Docker 기반 레서피 가져오기 - R {#r}

먼저 **[!UICONTROL UI의 왼쪽 상단에 있는 워크플로우]** 를 찾아 선택합니다 [!DNL Platform] . 그런 다음 레서피 *가져오기를* 선택하고 **[!UICONTROL 론치를 클릭합니다]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

레서피 *가져오기* 워크플로우에 대한 *구성* 페이지가나타납니다. 레서피에 대한 이름과 설명을 입력한 다음 **[!UICONTROL 오른쪽 위 모서리에서]** 다음을 선택합니다.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Recipe [자습서에 소스 파일을](./package-source-files-recipe.md) 패키지하면 R 소스 파일을 사용하여 소매 판매 레서피 작성 끝에 Docker URL이 제공됩니다.

소스 *선택* 페이지에 있으면 소스 URL **[!UICONTROL 필드에 R 소스 파일을 사용하여 작성한 패키지된 레시피에 해당하는 Docker URL을 붙여]** 넣습니다. 그런 다음 드래그 앤 드롭하여 제공된 구성 파일을 가져오거나 파일 시스템 **브라우저를 사용합니다**. 제공된 구성 파일은 에서 찾을 수 있습니다 `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. 런타임 **[!UICONTROL 드롭다운에서]** *R* 을 **[!UICONTROL 선택하고]** Type드롭다운 *에서 분류* 를선택합니다. 모든 것이 채워지면 오른쪽 위 **[!UICONTROL 의]** [다음]을 클릭하여 스키마 *관리로 이동합니다*.

>[!NOTE]
>
> *유형은* 분류 **[!UICONTROL 및 회귀]** 를 **[!UICONTROL 지원합니다]**. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 사용자 지정 **[!UICONTROL 을 선택합니다]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

다음으로, [스키마 *관리] 섹션*&#x200B;아래의 소매 판매 입출력 스키마를 선택하여 소매 판매 스키마 및 데이터 세트 자습서 [를 만드는 데 제공된 부트스트랩 스크립트를 사용하여](../models-recipes/create-retails-sales-dataset.md) 만들었습니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

기능 *관리* 섹션 아래에서 스키마 뷰어에서 테넌트 ID를 클릭하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 필드 속성 창에서 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 을 선택하여 **[!UICONTROL 입력 및 출력 기능을]** 선택합니다. 이 자습서의 목적을 위해 weeklySales를 **[!UICONTROL Target]** 기능으로 **[!UICONTROL 설정하고 그 외의 모든 것을]** 입력 기능으로 **[!UICONTROL 설정하십시오]**. 새로 구성된 **[!UICONTROL 레서피를]** 검토하려면 다음을 클릭합니다.

필요에 따라 레시피를 검토하고 구성을 추가, 수정 또는 제거합니다. 마침 **을** 클릭하여 레시피를 생성합니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

새로 만든 소매 판매 레서피를 사용하여 모델을 생성하는 방법 [을 살펴보려면 다음 단계를](#next-steps) [!DNL Data Science Workspace] 수행합니다.

### Docker 기반의 레서피 가져오기 - PySpark {#pyspark}

먼저 **[!UICONTROL UI의 왼쪽 상단에 있는 워크플로우]** 를 찾아 선택합니다 [!DNL Platform] . 그런 다음 레서피 *가져오기를* 선택하고 **[!UICONTROL 론치를 클릭합니다]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

레서피 *가져오기* 워크플로우에 대한 *구성* 페이지가나타납니다. 레서피에 대한 이름과 설명을 입력한 다음 **[!UICONTROL 오른쪽 상단]** 모서리에서 다음을 선택하여 진행합니다.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Package 소스 파일을 Recipe [](./package-source-files-recipe.md) 튜토리얼로 가져올 때 PySpark 소스 파일을 사용하여 소매 판매 레서피 작성 종료 시 Docker URL이 제공되었습니다.

소스 *선택* 페이지에 있으면 **[!UICONTROL 소스 URL]** 필드에 PySpark 소스 파일을 사용하여 작성한 패키지된 레시피에 해당하는 Docker URL을 붙여 넣습니다. 그런 다음 드래그 앤 드롭하여 제공된 구성 파일을 가져오거나 파일 시스템 **브라우저를 사용합니다**. 제공된 구성 파일은 에서 찾을 수 있습니다 `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Runtime **[!UICONTROL 드롭다운에서 PySpark]** 를 ** 선택합니다. PySpark 런타임을 선택하면 기본 아티팩트는 Docker에 자동으로 **[!UICONTROL 채워집니다]**. 그런 다음 **[!UICONTROL 유형]** 드롭다운에서 *분류를* 선택합니다. 모든 것이 채워지면 오른쪽 위 **[!UICONTROL 의]** [다음]을 클릭하여 스키마 *관리로 이동합니다*.

>[!NOTE]
>
> *유형은* 분류 **[!UICONTROL 및 회귀]** 를 **[!UICONTROL 지원합니다]**. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 사용자 지정 **[!UICONTROL 을 선택합니다]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

다음으로, [스키마 *관리] 섹션*&#x200B;아래의 소매 판매 입출력 스키마를 선택하여 소매 판매 스키마 및 데이터 세트 자습서 [를 만드는 데 제공된 부트스트랩 스크립트를 사용하여](../models-recipes/create-retails-sales-dataset.md) 만들었습니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

기능 *관리* 섹션 아래에서 스키마 뷰어에서 테넌트 ID를 클릭하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 필드 속성 창에서 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 을 선택하여 **[!UICONTROL 입력 및 출력 기능을]** 선택합니다. 이 자습서의 목적을 위해 weeklySales를 **[!UICONTROL Target]** 기능으로 **[!UICONTROL 설정하고 그 외의 모든 것을]** 입력 기능으로 **[!UICONTROL 설정하십시오]**. 다음 **[!UICONTROL 을]** 클릭하여 새로 구성된 레시피를 검토합니다.

필요에 따라 레시피를 검토하고 구성을 추가, 수정 또는 제거합니다. 마침 **[!UICONTROL 을]** 클릭하여 레시피를 생성합니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

새로 만든 소매 판매 레서피를 사용하여 모델을 생성하는 방법 [을 살펴보려면 다음 단계를](#next-steps) [!DNL Data Science Workspace] 수행합니다.

### Docker 기반 레서피 가져오기 - Scala {#scala}

먼저 **[!UICONTROL UI의 왼쪽 상단에 있는 워크플로우]** 를 찾아 선택합니다 [!DNL Platform] . 그런 다음 레서피 *가져오기를* 선택하고 **[!UICONTROL 론치를 클릭합니다]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

레서피 *가져오기* 워크플로우에 대한 *구성* 페이지가나타납니다. 레서피에 대한 이름과 설명을 입력한 다음 **[!UICONTROL 오른쪽 상단]** 모서리에서 다음을 선택하여 진행합니다.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 소스 파일을 [레서피](./package-source-files-recipe.md) 자습서로 패키징하는 경우 Scala(소스 파일)를 사용하여 소매 영업 레서피를 빌드하는 끝 시점에 Docker URL이[!DNL Spark]제공되었습니다.

소스 *선택* 페이지에 있으면 소스 URL *필드에 Scala 소스 파일을 사용하여 작성한 패키지된 레시피에 해당하는 Docker URL을 붙여* 넣습니다. 그런 다음 드래그 앤 드롭하여 제공된 구성 파일을 가져오거나 파일 시스템 **브라우저를 사용합니다**. 제공된 구성 파일은 에서 찾을 수 있습니다 `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. 런타임 **[!UICONTROL 드롭다운에서]** Spark *를* 선택합니다. 런타임을 [!DNL Spark] 선택하면 기본 아티팩트는 Docker에 자동으로 **[!UICONTROL 채워집니다]**. 그런 다음 유형 **[!UICONTROL 드롭다운에서]** 회귀 *를* 선택합니다. 모든 것이 채워지면 오른쪽 위 **[!UICONTROL 의]** [다음]을 클릭하여 스키마 *관리로 이동합니다*.

>[!NOTE]
>
> *유형은* 분류 **[!UICONTROL 및 회귀]** 를 **[!UICONTROL 지원합니다]**. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 사용자 지정 **[!UICONTROL 을 선택합니다]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

다음으로, [스키마 *관리] 섹션*&#x200B;아래의 소매 판매 입출력 스키마를 선택하여 소매 판매 스키마 및 데이터 세트 자습서 [를 만드는 데 제공된 부트스트랩 스크립트를 사용하여](../models-recipes/create-retails-sales-dataset.md) 만들었습니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

기능 *관리* 섹션 아래에서 스키마 뷰어에서 테넌트 ID를 클릭하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 필드 속성 창에서 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 을 선택하여 **[!UICONTROL 입력 및 출력 기능을]** 선택합니다. 이 자습서의 목적을 위해 weeklySales를 **[!UICONTROL Target]** 기능으로 **[!UICONTROL 설정하고 그 외의 모든 것을]** 입력 기능으로 **[!UICONTROL 설정하십시오]**. 다음 **[!UICONTROL 을]** 클릭하여 새로 구성된 레시피를 검토합니다.

필요에 따라 레시피를 검토하고 구성을 추가, 수정 또는 제거합니다. 마침 **[!UICONTROL 을]** 클릭하여 레시피를 생성합니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

새로 만든 소매 판매 레서피를 사용하여 모델을 생성하는 방법 [을 살펴보려면 다음 단계를](#next-steps) [!DNL Data Science Workspace] 수행합니다.

## 다음 단계 {#next-steps}

이 자습서에서는 레서피 구성 및 가져오기에 대한 통찰력을 제공합니다 [!DNL Data Science Workspace]. 이제 새로 만든 레시피를 사용하여 모델을 생성, 교육 및 평가할 수 있습니다.

- [UI에서 모델 트레이닝 및 평가](./train-evaluate-model-ui.md)
- [API를 사용하여 모델 트레이닝 및 평가](./train-evaluate-model-api.md)