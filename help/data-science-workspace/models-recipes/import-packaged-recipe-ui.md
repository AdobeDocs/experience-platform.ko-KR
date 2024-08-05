---
keywords: Experience Platform;패키지된 레시피 가져오기;Data Science Workspace;인기 주제;레시피;ui;엔진 만들기
solution: Experience Platform
title: 데이터 과학 Workspace UI에서 패키지된 레시피 가져오기
type: Tutorial
description: 이 튜토리얼에서는 제공된 소매 판매 예제를 사용하여 패키지 레서피 구성하고 가져오는 방법에 대한 인사이트 제공합니다. 이 자습서가 끝날 때까지 Adobe Experience Platform Data Science Workspace에서 모델을 만들고 교육하고 평가할 수 있습니다.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 0%

---

# 데이터 과학 작업 영역 UI에서 패키지된 레서피 가져오기

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

이 자습서에서는 제공된 소매 판매 예제를 사용하여 패키지된 레시피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 자습서가 끝날 때까지 Adobe Experience Platform [!DNL Data Science Workspace]에서 모델을 만들고, 교육하고, 평가할 준비가 될 것입니다.

## 전제 조건

이 자습서에서는 도커 이미지 URL 형태로 패키지된 레시피가 필요합니다. 자세한 내용은 [레시피에 소스 파일을 패키지하는 방법](./package-source-files-recipe.md)에 대한 자습서를 참조하십시오.

## UI 워크플로

패키지된 레시피를 [!DNL Data Science Workspace](으)로 가져오려면 단일 JavaScript 개체 표기법(JSON) 파일로 컴파일된 특정 레시피 구성이 필요합니다. 이 레시피 구성 컴파일을 구성 파일이라고 합니다. 특정 세트의 구성들을 갖는 패키징된 레시피는 레시피 인스턴스로서 지칭된다. 한 레시피를 사용하여 [!DNL Data Science Workspace]에서 여러 레시피 인스턴스를 만들 수 있습니다.

패키지 레시피를 가져오는 워크플로우는 다음 단계로 구성됩니다.
- [레시피 구성](#configure)
- [Docker 기반 레서피 가져오기 - Python](#python)
- [Docker 기반 레서피 가져오기 - R](#r)
- [Docker 기반 레서피 가져오기 - PySpark](#pyspark)
- [Docker 기반 레서피 가져오기 - Scala](#scala)

### 레서피 구성 {#configure}

모든 레서피 인스턴스 [!DNL Data Science Workspace] 에는 특정 사용 사례에 맞게 레서피 인스턴스 조정하는 구성 세트가 함께 제공됩니다. 구성 파일은 이 레시피 인스턴스를 사용하여 만든 모델의 기본 교육 및 채점 동작을 정의합니다.

>[!NOTE]
>
>구성 파일은 레시피와 사례에 따라 다릅니다.

다음은 소매 판매 레시피에 대한 기본 교육 및 채점 동작을 보여 주는 샘플 구성 파일입니다.

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
| `learning_rate` | 숫자 | 그라데이션 곱의 경우 스칼라. |
| `n_estimators` | 숫자 | 임의 포리스트 분류자에 대한 포리스트의 트리 수입니다. |
| `max_depth` | 숫자 | Random Forest 분류자에 있는 트리의 최대 깊이입니다. |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 속성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 속성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부를 결정합니다 |
| `tenantId` | 문자열 | 이 ID는 사용자가 만드는 리소스의 이름 간격이 제대로 지정되고 조직 내에 포함되어 있는지 확인합니다. [여기](../../xdm/api/getting-started.md#know-your-tenant_id)의 단계에 따라 테넌트 ID를 찾으십시오. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. UI에서 가져올 때는 이 항목을 비워 두고 API를 사용하여 가져올 때는 교육 SchemaID로 대체합니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화에 대한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델 평가에 사용할 평가 지표의 쉼표로 구분된 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델의 점수를 매기는 데 사용되는 출력 스키마입니다. UI 에서 가져올 때는 비워 두고, API를 사용하여 가져올 때는 점수 지정 SchemaID로 바꿉니다. |

이 튜토리얼 목적에 따라 소매 판매 레서피 기본 구성 파일을 그대로 참조에 [!DNL Data Science Workspace] 그대로 둘 수 있습니다.

### Docker 기반 레서피 가져오기 - [!DNL Python] {#python}

UI의 왼쪽 [!DNL Platform] 상단에 있는 워크플로우&#x200B;]**를 탐색하고 선택하여**[!UICONTROL &#x200B;시작. 다음 가져오기 레서피&#x200B;**선택하고** Launch ]**선택합니다**[!UICONTROL .

![](../images/models-recipes/import-package-ui/launch-import.png)

**레시피 가져오기** 워크플로에 대한 **구성** 페이지가 나타납니다. 레시피의 이름과 설명을 입력한 다음 오른쪽 상단에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![워크플로 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> [레시피에 소스 파일 패키징](./package-source-files-recipe.md) 자습서에서 Python 소스 파일을 사용하여 소매 판매 레시피를 빌드한 끝에 도커 URL이 제공되었습니다.

**소스 선택** 페이지에 있는 경우 **[!UICONTROL Source URL]** 필드에 [!DNL Python] 소스 파일을 사용하여 만든 패키지된 레시피에 해당하는 도커 URL을 붙여 넣으십시오. 그런 다음 제공된 구성 파일을 드래그 앤 드롭하여 가져오거나 파일 시스템 **브라우저**&#x200B;를 사용하십시오. 제공된 구성 파일을 `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`에서 찾을 수 있습니다. 런타임&#x200B;**드롭다운에서** Python ]**을 선택하고**[!UICONTROL &#x200B;유형&#x200B;**드롭다운에서**&#x200B;분류&#x200B;]**를 선택합니다**[!UICONTROL . 모든 항목이 다 채워지면 오른쪽 상단에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 **스키마 관리**(으)로 진행합니다.

>[!NOTE]
>
> 형식이 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**&#x200B;을(를) 지원합니다. 모델이 이러한 유형 중 하나에 해당되지 않는 경우 **[!UICONTROL 사용자 지정]**&#x200B;을 선택하세요.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

그런 다음 **스키마 관리** 섹션에서 소매 판매 입력 및 출력 스키마를 선택합니다. 이 스키마는 [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 자습서에서 제공된 부트스트랩 스크립트를 사용하여 만들어졌습니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

**기능 관리** 섹션에서 스키마 뷰어 테넌트 ID를 선택하여 Retail Sales 입력 스키마를 확장합니다. 원하는 피처를 강조 표시하고 오른쪽 **[!UICONTROL 필드 속성]** 창에서 입력 피처&#x200B;]**또는**[!UICONTROL  Target 피처&#x200B;]**를 선택하여**[!UICONTROL &#x200B;입력 및 출력 피처를 선택합니다. 이 튜토리얼 목적에 따라 weeklySales ]**를 Target 기능]**&#x200B;으로 **[!UICONTROL 설정하고 다른 모든 항목을 입력 기능]**&#x200B;으로 **[!UICONTROL 설정합니다**[!UICONTROL . [다음&#x200B;]**]을 선택하여**[!UICONTROL &#x200B;새로 구성된 레서피를 검토합니다.

레시피를 검토하고 필요에 따라 구성을 추가, 수정 또는 제거합니다. **[!UICONTROL 완료]**&#x200B;를 선택하여 레시피를 만드십시오.

![](../images/models-recipes/import-package-ui/recipe_review.png)

[다음 단계](#next-steps)로 진행하여 새로 만든 소매 판매 레시피를 사용하여 [!DNL Data Science Workspace]에서 모델을 만드는 방법을 알아봅니다.

### 도커 기반 레시피 가져오기 - R {#r}

[!DNL Platform] UI의 왼쪽 상단에 있는 **[!UICONTROL 워크플로]**&#x200B;를 탐색하고 선택하여 시작합니다. 다음으로 **레시피 가져오기**&#x200B;를 선택하고 **[!UICONTROL 시작]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/launch-import.png)

**레시피 가져오기** 워크플로에 대한 **구성** 페이지가 나타납니다. 레시피의 이름과 설명을 입력한 다음 오른쪽 상단에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![워크플로 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> [레시피에 소스 파일 패키징](./package-source-files-recipe.md) 자습서에서 R 소스 파일을 사용하여 소매 판매 레시피를 빌드한 끝에 도커 URL이 제공되었습니다.

**소스 선택** 페이지에 있는 경우 R 소스 파일을 사용하여 만든 패키지된 레시피에 해당하는 도커 URL을 **[!UICONTROL Source URL]** 필드에 붙여 넣으십시오. 그런 다음 제공된 구성 파일을 드래그 앤 드롭하여 가져오거나 파일 시스템 **브라우저**&#x200B;를 사용하십시오. 제공된 구성 파일을 `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`에서 찾을 수 있습니다. **런타임** 드롭다운에서 **[!UICONTROL R]**&#x200B;을(를) 선택하고 **유형** 드롭다운에서 **[!UICONTROL 분류]**&#x200B;을(를) 선택합니다. 모든 항목이 채워지면 오른쪽 위 모서리에서 다음&#x200B;]**을 선택하여**[!UICONTROL &#x200B;스키마 관리를 진행&#x200B;**합니다**.

>[!NOTE]
>
> *유형은* 분류&#x200B;]**및**[!UICONTROL &#x200B;회귀를&#x200B;]**지원합니다**[!UICONTROL . 모델이 이러한 유형 중 하나에 속하지 않으면 사용자 지정&#x200B;]**을 선택합니다**[!UICONTROL .

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

다음, 스키마 관리 섹션에서 **소매 판매 입력 및 출력 스키마를 선택하며, 소매 판매 스키마 및 데이터 세트](../models-recipes/create-retails-sales-dataset.md) 만들기 튜토리얼 에서 제공된 부트스트랩 스크립트를 [사용하여 생성**&#x200B;되었습니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

*기능 관리* 섹션에서 스키마 뷰어 테넌트 ID를 선택하여 Retail Sales 입력 스키마를 확장합니다. 원하는 피처를 강조 표시하고 오른쪽 **[!UICONTROL 필드 속성]** 창에서 입력 피처&#x200B;]**또는**[!UICONTROL  Target 피처&#x200B;]**를 선택하여**[!UICONTROL &#x200B;입력 및 출력 피처를 선택합니다. 이 튜토리얼 목적에 따라 weeklySales ]**를 Target 기능]**&#x200B;으로 **[!UICONTROL 설정하고 다른 모든 항목을 입력 기능]**&#x200B;으로 **[!UICONTROL 설정합니다**[!UICONTROL . [다음&#x200B;]**]을 선택하여**[!UICONTROL &#x200B;새로 구성된 레서피 검토

레시피를 검토하고 필요에 따라 구성을 추가, 수정 또는 제거합니다. **완료**&#x200B;를 선택하여 레시피를 만드십시오.

![](../images/models-recipes/import-package-ui/recipe_review.png)

[다음 단계](#next-steps)로 진행하여 새로 만든 소매 판매 레시피를 사용하여 [!DNL Data Science Workspace]에서 모델을 만드는 방법을 알아봅니다.

### 도커 기반 레시피 가져오기 - PySpark {#pyspark}

[!DNL Platform] UI의 왼쪽 상단에 있는 **[!UICONTROL 워크플로]**&#x200B;를 탐색하고 선택하여 시작합니다. 다음으로 **레시피 가져오기**&#x200B;를 선택하고 **[!UICONTROL 시작]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/launch-import.png)

**레시피 가져오기** 워크플로에 대한 **구성** 페이지가 나타납니다. 레시피의 이름과 설명을 입력한 다음 오른쪽 상단에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속 진행하십시오.

![워크플로 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> [레시피에 소스 파일 패키징](./package-source-files-recipe.md) 자습서에서 PySpark 소스 파일을 사용하여 소매 판매 레시피를 빌드한 끝에 도커 URL이 제공되었습니다.

**소스 선택** 페이지에 있는 경우 **[!UICONTROL Source URL]** 필드에 PySpark 소스 파일을 사용하여 만든 패키지된 레시피에 해당하는 도커 URL을 붙여 넣으십시오. 그런 다음 제공된 구성 파일을 드래그 앤 드롭하여 가져오거나 파일 시스템 **브라우저**&#x200B;를 사용하십시오. 제공된 구성 파일을 `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`에서 찾을 수 있습니다. **런타임** 드롭다운에서 **[!UICONTROL PySpark]**&#x200B;을(를) 선택합니다. PySpark 런타임을 선택하면 기본 아티팩트가 Docker ]**에**[!UICONTROL &#x200B;자동으로 채워집니다. 다음, 유형&#x200B;**드롭다운에서**&#x200B;분류&#x200B;]**를 선택합니다**[!UICONTROL . 모든 항목이 채워지면 오른쪽 위 모서리에서 다음&#x200B;]**을 선택하여**[!UICONTROL &#x200B;스키마 관리를 진행&#x200B;**합니다**.

>[!NOTE]
>
> *유형은* 분류&#x200B;]**및**[!UICONTROL &#x200B;회귀를&#x200B;]**지원합니다**[!UICONTROL . 모델이 이러한 유형 중 하나에 속하지 않으면 사용자 지정&#x200B;]**을 선택합니다**[!UICONTROL .

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

그런 다음 **스키마 관리** 선택기를 사용하여 소매 판매 입력 및 출력 스키마를 선택합니다. [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 자습서에서 제공된 부트스트랩 스크립트를 사용하여 스키마를 만들었습니다.

![스키마 관리](../images/models-recipes/import-package-ui/manage-schemas.png)

**기능 관리** 섹션 아래에서 스키마 뷰어의 테넌트 ID에서 을(를) 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 **[!UICONTROL 필드 속성]** 창에서 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL 대상 기능]**&#x200B;을(를) 선택하여 입력 및 출력 기능을 선택합니다. 이 자습서에서는 **[!UICONTROL weeklySales]**&#x200B;을(를) **[!UICONTROL 대상 기능]**(으)로 설정하고 그 외의 모든 기능을 **[!UICONTROL 입력 기능]**(으)로 설정합니다. 새로 구성된 레시피를 검토하려면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

레시피를 검토하고 필요에 따라 구성을 추가, 수정 또는 제거합니다. **[!UICONTROL 완료]**&#x200B;를 선택하여 레시피를 만드십시오.

![](../images/models-recipes/import-package-ui/recipe_review.png)

[다음 단계](#next-steps)로 진행하여 새로 만든 소매 판매 레시피를 사용하여 [!DNL Data Science Workspace]에서 모델을 만드는 방법을 알아봅니다.

### 도커 기반 레시피 가져오기 - Scala {#scala}

[!DNL Platform] UI의 왼쪽 상단에 있는 **[!UICONTROL 워크플로]**&#x200B;를 탐색하고 선택하여 시작합니다. 다음으로 **레시피 가져오기**&#x200B;를 선택하고 **[!UICONTROL 시작]**&#x200B;을 선택합니다.

![](../images/models-recipes/import-package-ui/launch-import.png)

**레시피 가져오기** 워크플로에 대한 **구성** 페이지가 나타납니다. 레시피의 이름과 설명을 입력한 다음 오른쪽 상단에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속 진행하십시오.

![워크플로 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> [레시피에 소스 파일 패키징](./package-source-files-recipe.md) 자습서에서 Scala([!DNL Spark]) 소스 파일을 사용하여 소매 판매 레시피를 빌드한 끝에 도커 URL이 제공되었습니다.

소스&#x200B;**선택 페이지에**&#x200B;있으면 소스 URL 필드에 Scala 소스 파일을 사용하여 빌드된 패키지된 레서피에 해당하는 Docker URL 붙여넣습니다. 다음, 드래그 앤 드롭으로 제공된 구성 파일을 가져오거나 파일 시스템 브라우저를 사용하십시오. 제공된 구성 파일은 에서 `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`찾을 수 있습니다. 런타임&#x200B;**드롭다운에서 Spark]**&#x200B;를 **선택합니다**[!UICONTROL . 런타임을 [!DNL Spark] 선택하면 기본 아티팩트가 Docker ]**에**[!UICONTROL &#x200B;자동으로 채워집니다. 다음, 유형&#x200B;**드롭다운에서**&#x200B;회귀를&#x200B;]**선택합니다**[!UICONTROL . 모든 항목이 채워지면 오른쪽 위 모서리에서 다음&#x200B;]**을 선택하여**[!UICONTROL &#x200B;스키마 관리를 진행&#x200B;**합니다**.

>[!NOTE]
>
> 유형은 분류&#x200B;]**및**[!UICONTROL &#x200B;회귀를&#x200B;]**지원합니다**[!UICONTROL . 모델이 이러한 유형 중 하나에 속하지 않으면 사용자 지정&#x200B;]**을 선택합니다**[!UICONTROL .

![](../images/models-recipes/import-package-ui/scala-databricks.png)

그런 다음 **스키마 관리** 선택기를 사용하여 소매 판매 입력 및 출력 스키마를 선택합니다. [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 자습서에서 제공된 부트스트랩 스크립트를 사용하여 스키마를 만들었습니다.

![스키마 관리](../images/models-recipes/import-package-ui/manage-schemas.png)

**기능 관리** 섹션 아래에서 스키마 뷰어의 테넌트 ID에서 을(를) 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 기능을 강조 표시하고 오른쪽 **[!UICONTROL 필드 속성]** 창에서 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL 대상 기능]**&#x200B;을(를) 선택하여 입력 및 출력 기능을 선택합니다. 이 자습서에서는 &quot;[!UICONTROL weeklySales]&quot;을(를) **[!UICONTROL Target 기능]**(으)로 설정하고 그 외의 모든 기능을 **[!UICONTROL 입력 기능]**(으)로 설정하십시오. 새로 구성된 레시피를 검토하려면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

레서피 검토, 필요에 따라 구성을 추가, 수정 또는 제거합니다. 마침&#x200B;]**을 선택하여**[!UICONTROL &#x200B;레서피 만들기.

![](../images/models-recipes/import-package-ui/recipe_review.png)

[다음 단계](#next-steps)로 진행하여 새로 만든 소매 판매 레시피를 사용하여 [!DNL Data Science Workspace]에서 모델을 만드는 방법을 알아봅니다.

## 다음 단계 {#next-steps}

이 자습서에서는 레시피를 구성하고 [!DNL Data Science Workspace](으)로 가져오는 방법에 대한 통찰력을 제공했습니다. 이제 새로 만든 레서피 기능을 사용하여 모델을 생성, 훈련 및 평가할 수 있습니다.

- [UI 내에서 모델 훈련 및 평가](./train-evaluate-model-ui.md)
- [API를 사용한 모델 훈련 및 평가](./train-evaluate-model-api.md)
