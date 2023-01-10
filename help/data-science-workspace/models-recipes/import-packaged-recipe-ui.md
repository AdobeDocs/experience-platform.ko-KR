---
keywords: Experience Platform;패키지된 레서피 가져오기;데이터 과학 작업 공간;인기 항목;레서피;ui;엔진 만들기
solution: Experience Platform
title: Data Science Workspace UI에서 패키지된 레서피 가져오기
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 예를 사용하여 패키지된 레서피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 자습서를 마치면 Adobe Experience Platform Data Science Workspace에서 모델을 생성, 훈련 및 평가할 수 있습니다.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 0%

---

# Data Science Workspace UI에서 패키지된 레서피 가져오기

이 자습서에서는 제공된 소매 판매 예를 사용하여 패키지된 레서피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 자습서를 마치면 Adobe Experience Platform에서 모델을 만들고, 훈련하고, 평가할 준비가 됩니다 [!DNL Data Science Workspace].

## 전제 조건

이 자습서에서는 Docker 이미지 URL 형식의 패키지된 레시피가 필요합니다. 방법에 대한 자습서를 참조하십시오 [배합식에 소스 파일 패키지](./package-source-files-recipe.md) 추가 정보.

## UI 워크플로우

패키지된 레시피를 로 가져오기 [!DNL Data Science Workspace] 에서는 단일 JSON(JavaScript Object 표기법) 파일로 컴파일된 특정 레서피 구성이 필요합니다. 이 레서피 구성 컴파일을 구성 파일이라고 합니다. 특정 구성 세트가 있는 패키지된 레서피를 레서피 인스턴스라고 합니다. 하나의 조리법을 사용하여 [!DNL Data Science Workspace].

패키지 레서피를 가져오는 워크플로우는 다음 단계로 구성됩니다.
- [레서피 구성](#configure)
- [Docker 기반 레서피 가져오기 - Python](#python)
- [Docker 기반 레서피 가져오기 - R](#r)
- [Docker 기반 레서피 - PySpark 가져오기](#pyspark)
- [임포트 Docker 기반 레서피 - 스칼라](#scala)

### 레서피 구성 {#configure}

의 모든 레서피 인스턴스 [!DNL Data Science Workspace] 는 특정 사용 사례에 맞게 레서피 인스턴스를 조정하는 구성 세트와 함께 제공됩니다. 구성 파일은 이 레서피 인스턴스를 사용하여 생성된 모델의 기본 교육 및 점수 동작을 정의합니다.

>[!NOTE]
>
>구성 파일은 레서피 및 대/소문자를 구분합니다.

다음은 소매 판매 레서피에 대한 기본 교육 및 점수 행동을 보여주는 샘플 구성 파일입니다.

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
| `learning_rate` | 숫자 | 그라어를 사용하여 그라데이션 곱하기 |
| `n_estimators` | 숫자 | Random Forest 분류기의 포리스트에 있는 트리 수입니다. |
| `max_depth` | 숫자 | Random Forest 분류기의 최대 트리 깊이입니다. |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 속성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 속성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부를 결정합니다 |
| `tenantId` | 문자열 | 이 ID를 사용하면 사용자가 만드는 리소스가 적절하게 대체되고 IMS 조직 내에 포함되어 있습니다. [다음 단계를 수행합니다.](../../xdm/api/getting-started.md#know-your-tenant_id) 임차인 ID를 찾으려면 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. UI에서 가져올 때 이 필드를 비워 두고 API를 사용하여 가져올 때 교육 스키마 ID로 대체합니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화를 위한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델을 평가하는 데 사용할 평가 지표의 쉼표로 구분된 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델 점수에 사용되는 출력 스키마입니다. UI에서 가져올 때 이 필드를 비워 두고 API를 사용하여 가져올 때 점수 SchemaID로 바꿉니다. |

이 자습서를 위해 Retail Sales 레서피용 기본 구성 파일을 [!DNL Data Science Workspace] 있는 그대로 참고하세요.

### Docker 기반 레서피 가져오기 - [!DNL Python] {#python}

탐색 및 선택 **[!UICONTROL 워크플로우]** 의 왼쪽 상단에 있습니다. [!DNL Platform] UI. 다음 을 선택합니다. **레서피 가져오기** 을(를) 선택합니다. **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

다음 **구성** 페이지의 **레서피 가져오기** 워크플로우가 나타납니다. 배합식의 이름과 설명을 입력한 다음 **[!UICONTROL 다음]** 오른쪽 상단 모서리에서

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 에서 [배합식에 소스 파일 패키지](./package-source-files-recipe.md) 자습서에서는 Python 소스 파일을 사용하여 소매 판매 레서피 를 빌드할 때 Docker URL을 제공했습니다.

을(를) 시작하면 **소스 선택** 페이지에서 다음을 사용하여 작성한 패키지된 레서피에 해당하는 Docker URL을 붙여넣습니다 [!DNL Python] 의 소스 파일 **[!UICONTROL 소스 URL]** 필드. 그런 다음 제공된 구성 파일을 끌어서 놓거나 파일 시스템을 사용합니다 **브라우저**. 제공된 구성 파일은 `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. 선택 **[!UICONTROL 파이톤]** 에서 **런타임** 드롭다운 및 **[!UICONTROL 분류]** 에서 **유형** 드롭다운 모든 것을 채운 후 **[!UICONTROL 다음]** 오른쪽 위 모서리에서 을(를) 클릭하여 **스키마 관리**.

>[!NOTE]
>
> 유형 지원 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 을 선택합니다 **[!UICONTROL 사용자 지정]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

그런 다음 섹션에서 소매 판매 입출력 스키마를 선택합니다 **스키마 관리**&#x200B;를 채울 때 [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 자습서입니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

아래에 **기능 관리** 섹션에서 스키마 뷰어에서 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 피쳐를 강조 표시하고 다음 중 하나를 선택하여 입력 및 출력 피쳐를 선택합니다 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 오른쪽 **[!UICONTROL 필드 속성]** 창을 엽니다. 이 자습서를 위해 다음을 설정합니다. **[!UICONTROL weeklySales]** 로서의  **[!UICONTROL Target 기능]** 다른 모든 것 **[!UICONTROL 입력 기능]**. 선택 **[!UICONTROL 다음]** 새로 구성된 레시피를 검토하려면

필요에 따라 배합식을 검토, 구성을 추가, 수정 또는 제거합니다. 선택 **[!UICONTROL 완료]** 조리법을 만들려면

![](../images/models-recipes/import-package-ui/recipe_review.png)

다음 단계로 진행합니다. [다음 단계](#next-steps) 에서 모델을 만드는 방법을 알아봅니다. [!DNL Data Science Workspace] 새로 생성된 소매 판매 레서피 사용.

### Docker 기반 레서피 가져오기 - R {#r}

탐색 및 선택 **[!UICONTROL 워크플로우]** 의 왼쪽 상단에 있습니다. [!DNL Platform] UI. 다음 을 선택합니다. **레서피 가져오기** 을(를) 선택합니다. **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

다음 **구성** 페이지의 **레서피 가져오기** 워크플로우가 나타납니다. 배합식의 이름과 설명을 입력한 다음 **[!UICONTROL 다음]** 오른쪽 상단 모서리에서

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 에서 [배합식에 소스 파일 패키지](./package-source-files-recipe.md) 자습서에서는 R 소스 파일을 사용하여 Retail Sales Recipation을 빌드할 때 Docker URL을 제공했습니다.

을(를) 시작하면 **소스 선택** 페이지에서 R 소스 파일을 사용하여 만든 패키지된 레서피에 해당하는 Docker URL을 **[!UICONTROL 소스 URL]** 필드. 그런 다음 제공된 구성 파일을 끌어서 놓거나 파일 시스템을 사용합니다 **브라우저**. 제공된 구성 파일은 `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. 선택 **[!UICONTROL R]** 에서 **런타임** 드롭다운 및 **[!UICONTROL 분류]** 에서 **유형** 드롭다운 모든 것을 채운 후 **[!UICONTROL 다음]** 오른쪽 위 모서리에서 을(를) 클릭하여 **스키마 관리**.

>[!NOTE]
>
> *유형* 지원 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 을 선택합니다 **[!UICONTROL 사용자 지정]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

그런 다음 섹션에서 소매 판매 입출력 스키마를 선택합니다 **스키마 관리**&#x200B;를 채울 때 [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 자습서입니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

아래에 *기능 관리* 섹션에서 스키마 뷰어에서 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 피쳐를 강조 표시하고 다음 중 하나를 선택하여 입력 및 출력 피쳐를 선택합니다 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 오른쪽 **[!UICONTROL 필드 속성]** 창을 엽니다. 이 자습서를 위해 다음을 설정합니다. **[!UICONTROL weeklySales]** 로서의  **[!UICONTROL Target 기능]** 다른 모든 것 **[!UICONTROL 입력 기능]**. 선택 **[!UICONTROL 다음]** 새 구성된 배합식을 검토하려면

필요에 따라 배합식을 검토, 구성을 추가, 수정 또는 제거합니다. 선택 **완료** 조리법을 만들려면

![](../images/models-recipes/import-package-ui/recipe_review.png)

다음 단계로 진행합니다. [다음 단계](#next-steps) 에서 모델을 만드는 방법을 알아봅니다. [!DNL Data Science Workspace] 새로 생성된 소매 판매 레서피 사용.

### Docker 기반 레서피 - PySpark 가져오기 {#pyspark}

탐색 및 선택 **[!UICONTROL 워크플로우]** 의 왼쪽 상단에 있습니다. [!DNL Platform] UI. 다음 을 선택합니다. **레서피 가져오기** 을(를) 선택합니다. **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

다음 **구성** 페이지의 **레서피 가져오기** 워크플로우가 나타납니다. 배합식의 이름과 설명을 입력한 다음 **[!UICONTROL 다음]** 오른쪽 위 모서리에서 진행하십시오.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 에서 [배합식에 소스 파일 패키지](./package-source-files-recipe.md) 자습서에서는 PySpark 소스 파일을 사용하여 소매 판매 레서피 를 작성할 때 Docker URL을 제공했습니다.

을(를) 시작하면 **소스 선택** 페이지에서 PySpark 소스 파일을 사용하여 만든 패키지된 레서피에 해당하는 Docker URL을 **[!UICONTROL 소스 URL]** 필드. 그런 다음 제공된 구성 파일을 끌어서 놓거나 파일 시스템을 사용합니다 **브라우저**. 제공된 구성 파일은 `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. 선택 **[!UICONTROL PySpark]** 에서 **런타임** 드롭다운 PySpark 런타임이 선택되면 기본 아티팩트가 자동으로 **[!UICONTROL Docker]**. 다음 을 선택합니다. **[!UICONTROL 분류]** 에서 **유형** 드롭다운 모든 것을 채운 후 **[!UICONTROL 다음]** 오른쪽 위 모서리에서 을(를) 클릭하여 **스키마 관리**.

>[!NOTE]
>
> *유형* 지원 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 을 선택합니다 **[!UICONTROL 사용자 지정]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

그런 다음 를 사용하여 Retail Sales 입출력 스키마를 선택합니다 **스키마 관리** 선택기: 스키마는 [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 자습서입니다.

![스키마 관리](../images/models-recipes/import-package-ui/manage-schemas.png)

아래에 **기능 관리** 섹션에서 스키마 뷰어에서 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 피쳐를 강조 표시하고 다음 중 하나를 선택하여 입력 및 출력 피쳐를 선택합니다 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 오른쪽 **[!UICONTROL 필드 속성]** 창을 엽니다. 이 자습서를 위해 다음을 설정합니다. **[!UICONTROL weeklySales]** 로서의  **[!UICONTROL Target 기능]** 다른 모든 것 **[!UICONTROL 입력 기능]**. 선택 **[!UICONTROL 다음]** 새로 구성된 레시피를 검토하려면

![](../images/models-recipes/import-package-ui/recipe_schema.png)

필요에 따라 배합식을 검토, 구성을 추가, 수정 또는 제거합니다. 선택 **[!UICONTROL 완료]** 조리법을 만들려면

![](../images/models-recipes/import-package-ui/recipe_review.png)

다음 단계로 진행합니다. [다음 단계](#next-steps) 에서 모델을 만드는 방법을 알아봅니다. [!DNL Data Science Workspace] 새로 생성된 소매 판매 레서피 사용.

### 임포트 Docker 기반 레서피 - 스칼라 {#scala}

탐색 및 선택 **[!UICONTROL 워크플로우]** 의 왼쪽 상단에 있습니다. [!DNL Platform] UI. 다음 을 선택합니다. **레서피 가져오기** 을(를) 선택합니다. **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

다음 **구성** 페이지의 **레서피 가져오기** 워크플로우가 나타납니다. 배합식의 이름과 설명을 입력한 다음 **[!UICONTROL 다음]** 오른쪽 위 모서리에서 진행하십시오.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 에서 [배합식에 소스 파일 패키지](./package-source-files-recipe.md) 자습서에서는 Scala를 사용하여 Retail Sales Recipe를 작성하는 마지막 시점에 Docker URL을 제공했습니다([!DNL Spark]) 소스 파일.

을(를) 시작하면 **소스 선택** 페이지에서 소스 URL 필드에 Scala 소스 파일을 사용하여 작성된 패키지된 레서피에 해당하는 Docker URL을 붙여넣습니다. 그런 다음 제공된 구성 파일을 끌어다 놓거나 파일 시스템 브라우저를 사용하여 가져옵니다. 제공된 구성 파일은 `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. 선택 **[!UICONTROL 스파크]** 에서 **런타임** 드롭다운 한 번 [!DNL Spark] 런타임이 선택된 기본 아티팩트가 자동으로 채워집니다. **[!UICONTROL Docker]**. 다음 을 선택합니다. **[!UICONTROL 회귀]** 에서 **유형** 드롭다운 모든 것을 채운 후 **[!UICONTROL 다음]** 오른쪽 위 모서리에서 을(를) 클릭하여 **스키마 관리**.

>[!NOTE]
>
> 유형 지원 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 을 선택합니다 **[!UICONTROL 사용자 지정]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

그런 다음 를 사용하여 Retail Sales 입출력 스키마를 선택합니다 **스키마 관리** 선택기: 스키마는 [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 자습서입니다.

![스키마 관리](../images/models-recipes/import-package-ui/manage-schemas.png)

아래에 **기능 관리** 섹션에서 스키마 뷰어에서 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 피쳐를 강조 표시하고 다음 중 하나를 선택하여 입력 및 출력 피쳐를 선택합니다 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 오른쪽 **[!UICONTROL 필드 속성]** 창을 엽니다. 이 자습서를 사용하려면 &quot;을(를) 설정합니다.[!UICONTROL weeklySales]&quot;  **[!UICONTROL Target 기능]** 다른 모든 것 **[!UICONTROL 입력 기능]**. 선택 **[!UICONTROL 다음]** 새로 구성된 레시피를 검토하려면

![](../images/models-recipes/import-package-ui/recipe_schema.png)

필요에 따라 배합식을 검토, 구성을 추가, 수정 또는 제거합니다. 선택 **[!UICONTROL 완료]** 조리법을 만들려면

![](../images/models-recipes/import-package-ui/recipe_review.png)

다음 단계로 진행합니다. [다음 단계](#next-steps) 에서 모델을 만드는 방법을 알아봅니다. [!DNL Data Science Workspace] 새로 생성된 소매 판매 레서피 사용.

## 다음 단계 {#next-steps}

이 자습서에서는 레서피 구성 및 가져오기에 대한 통찰력을 제공합니다 [!DNL Data Science Workspace]. 이제 새로 생성된 배합식을 사용하여 모델을 생성, 교육 및 평가할 수 있습니다.

- [UI에서 모델 교육 및 평가](./train-evaluate-model-ui.md)
- [API를 사용하여 모델 교육 및 평가](./train-evaluate-model-api.md)
