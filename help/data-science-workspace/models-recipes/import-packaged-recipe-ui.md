---
keywords: Experience Platform;패키지화된 레서피 가져오기;데이터 과학 작업 공간;인기 있는 주제;레서피;ui;엔진 만들기
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 패키지된 레서피 가져오기
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 예제를 사용하여 패키지화된 레서피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 자습서가 끝나면 Adobe Experience Platform Data Science Workspace에서 모델을 생성, 교육 및 평가할 수 있습니다.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 0%

---

# 데이터 과학 작업 공간 UI에서 패키지된 레서피 가져오기

이 자습서에서는 제공된 소매 판매 예제를 사용하여 패키지화된 레서피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 자습서가 끝나면 Adobe Experience Platform [!DNL Data Science Workspace]에서 모델을 만들고, 교육하고, 평가할 준비가 됩니다.

## 전제 조건

이 자습서에서는 Docker 이미지 URL 형식의 패키지화된 레시피가 필요합니다. 자세한 내용은 [소스 파일을 레서피](./package-source-files-recipe.md)에 패키지하는 방법에 대한 자습서를 참조하십시오.

## UI 워크플로우

패키지화된 레서피를 [!DNL Data Science Workspace]으로 가져오려면 단일 JSON(JavaScript Object Notation) 파일로 컴파일된 특정 레서피 구성이 필요합니다. 이 레서피 구성 모음은 구성 파일이라고 합니다. 특정 구성 세트가 있는 패키지된 레서피를 레서피 인스턴스라고 합니다. 하나의 레서피를 사용하여 [!DNL Data Science Workspace]에서 많은 레서피 인스턴스를 만들 수 있습니다.

패키지 레서피를 가져오는 워크플로우는 다음 단계로 구성됩니다.
- [레서피 구성](#configure)
- [Import Docker based recipe - Python](#python)
- [Docker 기반 레서피 가져오기 - R](#r)
- [Docker 기반의 레서피 가져오기 - PySpark](#pyspark)
- [Docker 기반 레서피 가져오기 - Scala](#scala)

### 레서피 {#configure} 구성

[!DNL Data Science Workspace]의 모든 레서피 인스턴스에는 특정 사용 사례에 맞게 레서피 인스턴스를 맞춤화하는 구성 세트가 포함되어 있습니다. 구성 파일은 이 레서피 인스턴스를 사용하여 만든 모델의 기본 트레이닝 및 점수 지정 동작을 정의합니다.

>[!NOTE]
>
>구성 파일은 레서피 및 대/소문자를 구분합니다.

다음은 소매 판매 레서피에 대한 기본 트레이닝 및 점수 지정 행동을 보여주는 샘플 구성 파일입니다.

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
| `learning_rate` | 숫자 | 그레이디언트 곱셈을 위한 스칼라. |
| `n_estimators` | 숫자 | 임의 포리스트 분류에 대한 포리스트의 트리 수입니다. |
| `max_depth` | 숫자 | 임의 포리스트 분류기에서 트리의 최대 깊이입니다. |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 특성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 특성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부 결정 |
| `tenantId` | 문자열 | 이 ID를 사용하면 만든 리소스가 적절하게 지정되고 IMS 조직 내에 포함됩니다. [다음 단계에 따라 테넌트 ](../../xdm/api/getting-started.md#know-your-tenant_id) ID를 찾습니다. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. UI로 가져올 때 이 값을 비워 두고 API를 사용하여 가져올 때 교육 스키마 ID로 바꿉니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화에 대한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델을 평가하는 데 사용할 평가 지표의 쉼표로 구분된 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델 점수를 매기는 데 사용되는 출력 스키마입니다. UI로 가져올 때 이 값을 비워 두고 API를 사용하여 가져올 때 채점 스키마 ID로 바꿉니다. |

이 자습서를 위해 [!DNL Data Science Workspace] 참조 설명서의 소매 판매 레서피에 대한 기본 구성 파일을 원래 상태 그대로 둘 수 있습니다.

### Docker 기반 레서피 가져오기 - [!DNL Python] {#python}

[!DNL Platform] UI의 왼쪽 상단에 있는 **[!UICONTROL Workflows]**&#x200B;을 탐색하고 선택하여 시작합니다. 그런 다음 **레서피 가져오기**&#x200B;를 선택하고 **[!UICONTROL Launch]**&#x200B;를 선택합니다.

![](../images/models-recipes/import-package-ui/launch-import.png)

**레서피 가져오기** 작업 과정에 대한 **구성** 페이지가 나타납니다. 레서피에 대한 이름과 설명을 입력한 다음 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![워크플로 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> [Package 소스 파일을 Recipe](./package-source-files-recipe.md) 튜토리얼에서 Python 소스 파일을 사용하여 소매 판매 레서피를 빌드할 때 Docker URL이 제공되었습니다.

**소스 선택** 페이지에 있으면 **[!UICONTROL Source URL]** 필드에 [!DNL Python] 소스 파일을 사용하여 패키지된 레서피에 해당하는 Docker URL을 붙여 넣습니다. 그런 다음 드래그 앤 드롭하여 제공된 구성 파일을 가져오거나 파일 시스템 **Browser**&#x200B;을 사용합니다. 제공된 구성 파일은 `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`에서 찾을 수 있습니다. **Runtime** 드롭다운에서 **[!UICONTROL Python]**&#x200B;을 선택하고 **유형** 드롭다운에서 **[!UICONTROL Classification]**&#x200B;을 선택합니다. 모든 것이 채워지면 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 선택하여 **스키마 관리**&#x200B;로 진행합니다.

>[!NOTE]
>
> 유형은 **[!UICONTROL Classification]** 및 **[!UICONTROL Regression]**&#x200B;을 지원합니다. 모델이 이러한 유형 중 하나에 해당하지 않으면 **[!UICONTROL Custom]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

그런 다음 [소매 판매 스키마 만들기 및 데이터 세트](../models-recipes/create-retails-sales-dataset.md) 자습서에서 **스키마 관리** 섹션에 있는 소매 판매 입력 및 출력 스키마를 선택합니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

**기능 관리** 섹션에서 스키마 뷰어에서 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 **[!UICONTROL Field Properties]** 창에서 **[!UICONTROL Input Feature]** 또는 **[!UICONTROL Target Feature]**&#x200B;을 선택하여 입력 및 출력 기능을 선택합니다. 이 자습서를 위해 **[!UICONTROL weeklySales]**&#x200B;을(를) **[!UICONTROL Target Feature]**(으)로 설정하고 다른 모든 것을 **[!UICONTROL Input Feature]**(으)로 설정합니다. 새로 구성된 레서피를 검토하려면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

필요에 따라 레시피를 검토하고 구성을 추가, 수정 또는 제거합니다. **[!UICONTROL Finish]**&#x200B;을 선택하여 레서피를 만듭니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

새로 만든 소매 판매 레서피를 사용하여 [!DNL Data Science Workspace]에서 모델을 만드는 방법을 알아보려면 [다음 단계](#next-steps)로 이동하십시오.

### Docker 기반 레서피 가져오기 - R {#r}

[!DNL Platform] UI의 왼쪽 상단에 있는 **[!UICONTROL Workflows]**&#x200B;을 탐색하고 선택하여 시작합니다. 그런 다음 **레서피 가져오기**&#x200B;를 선택하고 **[!UICONTROL Launch]**&#x200B;를 선택합니다.

![](../images/models-recipes/import-package-ui/launch-import.png)

**레서피 가져오기** 작업 과정에 대한 **구성** 페이지가 나타납니다. 레서피에 대한 이름과 설명을 입력한 다음 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![워크플로 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> [소스 파일을 Recipe](./package-source-files-recipe.md) 튜토리얼에 패키징하면 R 소스 파일을 사용하여 소매 판매 레서피를 빌드할 때 Docker URL이 제공되었습니다.

**소스 선택** 페이지에 있으면 **[!UICONTROL Source URL]** 필드에 R 소스 파일을 사용하여 패키지된 레서피에 해당하는 Docker URL을 붙여 넣습니다. 그런 다음 드래그 앤 드롭하여 제공된 구성 파일을 가져오거나 파일 시스템 **Browser**&#x200B;을 사용합니다. 제공된 구성 파일은 `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`에서 찾을 수 있습니다. **Runtime** 드롭다운에서 **[!UICONTROL R]**&#x200B;을 선택하고 **유형** 드롭다운에서 **[!UICONTROL Classification]**&#x200B;을 선택합니다. 모든 것이 채워지면 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 선택하여 **스키마 관리**&#x200B;로 진행합니다.

>[!NOTE]
>
> *유형* 및  **[!UICONTROL Classification]** 를  **[!UICONTROL Regression]**&#x200B;지원합니다. 모델이 이러한 유형 중 하나에 해당하지 않으면 **[!UICONTROL Custom]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

그런 다음 [소매 판매 스키마 만들기 및 데이터 세트](../models-recipes/create-retails-sales-dataset.md) 자습서에서 **스키마 관리** 섹션에 있는 소매 판매 입력 및 출력 스키마를 선택합니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

*기능 관리* 섹션에서 스키마 뷰어에서 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 **[!UICONTROL Field Properties]** 창에서 **[!UICONTROL Input Feature]** 또는 **[!UICONTROL Target Feature]**&#x200B;을 선택하여 입력 및 출력 기능을 선택합니다. 이 자습서를 위해 **[!UICONTROL weeklySales]**&#x200B;을(를) **[!UICONTROL Target Feature]**(으)로 설정하고 다른 모든 것을 **[!UICONTROL Input Feature]**(으)로 설정합니다. **[!UICONTROL Next]**&#x200B;을 선택하여 새 구성된 레서피를 검토합니다.

필요에 따라 레시피를 검토하고 구성을 추가, 수정 또는 제거합니다. **완료**&#x200B;를 선택하여 레서피를 만듭니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

새로 만든 소매 판매 레서피를 사용하여 [!DNL Data Science Workspace]에서 모델을 만드는 방법을 알아보려면 [다음 단계](#next-steps)로 이동하십시오.

### Docker 기반 레서피 가져오기 - PySpark {#pyspark}

[!DNL Platform] UI의 왼쪽 상단에 있는 **[!UICONTROL Workflows]**&#x200B;을 탐색하고 선택하여 시작합니다. 그런 다음 **레서피 가져오기**&#x200B;를 선택하고 **[!UICONTROL Launch]**&#x200B;를 선택합니다.

![](../images/models-recipes/import-package-ui/launch-import.png)

**레서피 가져오기** 작업 과정에 대한 **구성** 페이지가 나타납니다. 레서피에 대한 이름과 설명을 입력한 다음 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 선택하여 계속 진행합니다.

![워크플로 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> [소스 파일을 Recipe](./package-source-files-recipe.md) 튜토리얼에 패키징하면 PySpark 소스 파일을 사용하여 소매 판매 레서피를 빌드할 때 Docker URL이 제공되었습니다.

**소스 선택** 페이지에 있는 경우 PySpark 소스 파일을 사용하여 만든 패키지화된 레서피에 해당하는 Docker URL을 **[!UICONTROL Source URL]** 필드에 붙여 넣습니다. 그런 다음 드래그 앤 드롭하여 제공된 구성 파일을 가져오거나 파일 시스템 **Browser**&#x200B;을 사용합니다. 제공된 구성 파일은 `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`에서 찾을 수 있습니다. **Runtime** 드롭다운에서 **[!UICONTROL PySpark]**&#x200B;을 선택합니다. PySpark 런타임을 선택하면 기본 가공물이 **[!UICONTROL Docker]**&#x200B;에 자동으로 채워집니다. 그런 다음 **유형** 드롭다운에서 **[!UICONTROL Classification]**&#x200B;을 선택합니다. 모든 것이 채워지면 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 선택하여 **스키마 관리**&#x200B;로 진행합니다.

>[!NOTE]
>
> *유형* 및  **[!UICONTROL Classification]** 를  **[!UICONTROL Regression]**&#x200B;지원합니다. 모델이 이러한 유형 중 하나에 해당하지 않으면 **[!UICONTROL Custom]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

그런 다음 **스키마 관리** 선택기를 사용하여 소매 판매 스키마 및 출력 스키마를 선택합니다. [소매 판매 스키마 및 데이터 세트](../models-recipes/create-retails-sales-dataset.md) 자습서 만들기에서 제공된 부트스트랩 스크립트를 사용하여 스키마가 생성되었습니다.

![스키마 관리](../images/models-recipes/import-package-ui/manage-schemas.png)

**기능 관리** 섹션에서 스키마 뷰어에서 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 **[!UICONTROL Field Properties]** 창에서 **[!UICONTROL Input Feature]** 또는 **[!UICONTROL Target Feature]**&#x200B;을 선택하여 입력 및 출력 기능을 선택합니다. 이 자습서를 위해 **[!UICONTROL weeklySales]**&#x200B;을(를) **[!UICONTROL Target Feature]**(으)로 설정하고 다른 모든 것을 **[!UICONTROL Input Feature]**(으)로 설정합니다. 새로 구성된 레서피를 검토하려면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

필요에 따라 레시피를 검토하고 구성을 추가, 수정 또는 제거합니다. **[!UICONTROL Finish]**&#x200B;을 선택하여 레서피를 만듭니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

새로 만든 소매 판매 레서피를 사용하여 [!DNL Data Science Workspace]에서 모델을 만드는 방법을 알아보려면 [다음 단계](#next-steps)로 이동하십시오.

### Docker 기반 레서피 가져오기 - Scala {#scala}

[!DNL Platform] UI의 왼쪽 상단에 있는 **[!UICONTROL Workflows]**&#x200B;을 탐색하고 선택하여 시작합니다. 그런 다음 **레서피 가져오기**&#x200B;를 선택하고 **[!UICONTROL Launch]**&#x200B;를 선택합니다.

![](../images/models-recipes/import-package-ui/launch-import.png)

**레서피 가져오기** 작업 과정에 대한 **구성** 페이지가 나타납니다. 레서피에 대한 이름과 설명을 입력한 다음 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 선택하여 계속 진행합니다.

![워크플로 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> [소스 파일을 Recipe](./package-source-files-recipe.md) 튜토리얼에 패키징하면 Scala([!DNL Spark]) 소스 파일을 사용하여 소매 판매 레서피를 빌드하는 마지막 시점에 Docker URL이 제공되었습니다.

**소스 선택** 페이지에 있는 경우 소스 URL 필드에 Scala 소스 파일을 사용하여 패키지화된 레서피에 해당하는 Docker URL을 붙여 넣습니다. 그런 다음 드래그 앤 드롭하여 제공된 구성 파일을 가져오거나 파일 시스템 브라우저를 사용합니다. 제공된 구성 파일은 `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`에서 찾을 수 있습니다. **Runtime** 드롭다운에서 **[!UICONTROL Spark]**&#x200B;을 선택합니다. [!DNL Spark] 런타임을 선택하면 기본 가공물은 **[!UICONTROL Docker]**&#x200B;에 자동으로 채워집니다. 그런 다음 **유형** 드롭다운에서 **[!UICONTROL Regression]**&#x200B;을 선택합니다. 모든 것이 채워지면 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 선택하여 **스키마 관리**&#x200B;로 진행합니다.

>[!NOTE]
>
> 유형은 **[!UICONTROL Classification]** 및 **[!UICONTROL Regression]**&#x200B;을 지원합니다. 모델이 이러한 유형 중 하나에 해당하지 않으면 **[!UICONTROL Custom]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

그런 다음 **스키마 관리** 선택기를 사용하여 소매 판매 스키마 및 출력 스키마를 선택합니다. [소매 판매 스키마 및 데이터 세트](../models-recipes/create-retails-sales-dataset.md) 자습서 만들기에서 제공된 부트스트랩 스크립트를 사용하여 스키마가 생성되었습니다.

![스키마 관리](../images/models-recipes/import-package-ui/manage-schemas.png)

**기능 관리** 섹션에서 스키마 뷰어에서 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 **[!UICONTROL Field Properties]** 창에서 **[!UICONTROL Input Feature]** 또는 **[!UICONTROL Target Feature]**&#x200B;을 선택하여 입력 및 출력 기능을 선택합니다. 이 자습서를 위해 &quot;[!UICONTROL weeklySales]&quot;을(를) **[!UICONTROL Target Feature]**(으)로 설정하고 다른 모든 것을 **[!UICONTROL Input Feature]**(으)로 설정합니다. 새로 구성된 레서피를 검토하려면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

필요에 따라 레시피를 검토하고 구성을 추가, 수정 또는 제거합니다. **[!UICONTROL Finish]**&#x200B;을 선택하여 레서피를 만듭니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

새로 만든 소매 판매 레서피를 사용하여 [!DNL Data Science Workspace]에서 모델을 만드는 방법을 알아보려면 [다음 단계](#next-steps)로 이동하십시오.

## 다음 단계 {#next-steps}

이 자습서에서는 레서피를 구성 및 [!DNL Data Science Workspace]으로 가져오는 방법에 대한 통찰력을 제공합니다. 이제 새로 만든 레시피를 사용하여 모델을 생성, 교육 및 평가할 수 있습니다.

- [UI에서 모델 트레이닝 및 평가](./train-evaluate-model-ui.md)
- [API를 사용하여 모델 트레이닝 및 평가](./train-evaluate-model-api.md)
