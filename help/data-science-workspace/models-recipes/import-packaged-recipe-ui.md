---
keywords: Experience Platform;패키지된 레시피 가져오기;Data Science Workspace;인기 주제;레시피;ui;엔진 만들기
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 패키지된 레시피 가져오기
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 예제를 사용하여 패키지된 레시피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 자습서가 끝날 때까지 Adobe Experience Platform 데이터 과학 작업 영역에서 모델을 만들고, 교육하고, 평가할 준비가 될 것입니다.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 0%

---

# 데이터 과학 작업 공간 UI에서 패키지된 레시피 가져오기

이 자습서에서는 제공된 소매 판매 예제를 사용하여 패키지된 레시피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 자습서가 끝날 때까지 Adobe Experience Platform에서 모델을 만들고, 교육하고, 평가할 준비가 될 것입니다 [!DNL Data Science Workspace].

## 전제 조건

이 자습서에서는 도커 이미지 URL 형태로 패키지된 레시피가 필요합니다. 다음 방법에 대한 튜토리얼 보기 [소스 파일을 레시피에 패키징](./package-source-files-recipe.md) 추가 정보.

## UI 워크플로

패키지된 레시피를으로 가져오기 [!DNL Data Science Workspace] 단일 JavaScript 개체 표기법(JSON) 파일로 컴파일된 특정 레시피 구성이 필요합니다. 이 레시피 구성 컴파일을 구성 파일이라고 합니다. 특정 세트의 구성들을 갖는 패키징된 레시피는 레시피 인스턴스로서 지칭된다. 하나의 레시피를 사용하여 [!DNL Data Science Workspace].

패키지 레시피를 가져오는 워크플로우는 다음 단계로 구성됩니다.
- [레시피 구성](#configure)
- [도커 기반 레시피 가져오기 - Python](#python)
- [도커 기반 레시피 가져오기 - R](#r)
- [도커 기반 레시피 가져오기 - PySpark](#pyspark)
- [도커 기반 레시피 가져오기 - Scala](#scala)

### 레시피 구성 {#configure}

의 모든 레시피 인스턴스 [!DNL Data Science Workspace] 는 특정 사용 사례에 맞게 레시피 인스턴스를 맞춤화하는 구성 세트와 함께 제공됩니다. 구성 파일은 이 레시피 인스턴스를 사용하여 만든 모델의 기본 교육 및 채점 동작을 정의합니다.

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
| `max_depth` | 숫자 | Random Forest 분류자의 최대 트리 깊이입니다. |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 속성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 속성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부를 결정합니다 |
| `tenantId` | 문자열 | 이 ID는 사용자가 만드는 리소스의 이름 간격이 제대로 지정되고 IMS 조직 내에 포함되어 있는지 확인합니다. [다음 단계를 수행합니다](../../xdm/api/getting-started.md#know-your-tenant_id) 테넌트 ID를 찾습니다. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. UI에서 가져올 때는 이 항목을 비워 두고 API를 사용하여 가져올 때는 교육 SchemaID로 대체합니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화를 위한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델을 평가하는 데 사용할 평가 지표를 쉼표로 구분한 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델의 점수를 매기는 데 사용되는 출력 스키마입니다. UI에서 가져올 때는 이 항목을 비워 두고 API를 사용하여 가져올 때는 채점 SchemaID로 대체합니다. |

이 자습서에서는 소매 판매 레시피의 기본 구성 파일을 [!DNL Data Science Workspace] 있는 그대로를 참고하세요.

### 도커 기반 레시피 가져오기 - [!DNL Python] {#python}

탐색 및 선택하여 시작 **[!UICONTROL 워크플로]** 의 왼쪽 상단에 있음 [!DNL Platform] UI. 그런 다음 을 선택합니다. **레시피 가져오기** 및 선택 **[!UICONTROL 시작]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

다음 **구성** 페이지 **레시피 가져오기** 워크플로가 나타납니다. 배합식의 이름과 설명을 입력한 다음 선택합니다. **[!UICONTROL 다음]** 오른쪽 상단 모서리입니다.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 다음에서 [소스 파일을 레시피에 패키징](./package-source-files-recipe.md) 자습서에서는 Python 소스 파일을 사용하여 소매 판매 레시피를 작성하는 마지막에 도커 URL이 제공되었습니다.

다음에 접속하면 **소스 선택** 페이지를, 을 사용하여 빌드된 패키지된 레시피에 해당하는 도커 URL을 붙여 넣습니다. [!DNL Python] 의 소스 파일 **[!UICONTROL 소스 URL]** 필드. 그런 다음 제공된 구성 파일을 드래그 앤 드롭하여 가져오거나 파일 시스템을 사용합니다 **브라우저**. 제공된 구성 파일은에서 찾을 수 있습니다. `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. 선택 **[!UICONTROL Python]** 다음에서 **런타임** 드롭다운 및 **[!UICONTROL 분류]** 다음에서 **유형** 드롭다운입니다. 모든 항목이 작성되면 다음을 선택합니다. **[!UICONTROL 다음]** 오른쪽 상단 모서리에서 **스키마 관리**.

>[!NOTE]
>
> 유형 지원 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**. 모델이 이러한 유형 중 하나에 해당하지 않는 경우 다음을 선택합니다. **[!UICONTROL 사용자 정의]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

그런 다음 섹션 아래에서 소매 판매 입력 및 출력 스키마를 선택합니다 **스키마 관리**&#x200B;에서 제공된 부트스트랩 스크립트를 사용하여 작성되었습니다. [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 튜토리얼.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

아래 **기능 관리** 섹션에서 스키마 뷰어의 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 피쳐를 강조표시하고 다음 중 하나를 선택하여 입력 및 출력 피쳐를 선택합니다 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 오른쪽에서 **[!UICONTROL 필드 속성]** 창. 이 자습서의 목적을 위해 다음을 설정하십시오. **[!UICONTROL weeklySales]** (으)로  **[!UICONTROL Target 기능]** 및 기타 모든 항목 **[!UICONTROL 입력 기능]**. 선택 **[!UICONTROL 다음]** 을 클릭하여 새로 구성된 레시피를 검토합니다.

레시피를 검토하고 필요에 따라 구성을 추가, 수정 또는 제거합니다. 선택 **[!UICONTROL 완료]** 레시피를 만들 수 있습니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

다음으로 진행 [다음 단계](#next-steps) 에서 모델을 만드는 방법을 알아보려면 [!DNL Data Science Workspace] 새로 생성된 소매 판매 레시피 사용.

### 도커 기반 레시피 가져오기 - R {#r}

탐색 및 선택하여 시작 **[!UICONTROL 워크플로]** 의 왼쪽 상단에 있음 [!DNL Platform] UI. 그런 다음 을 선택합니다. **레시피 가져오기** 및 선택 **[!UICONTROL 시작]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

다음 **구성** 페이지 **레시피 가져오기** 워크플로가 나타납니다. 배합식의 이름과 설명을 입력한 다음 선택합니다. **[!UICONTROL 다음]** 오른쪽 상단 모서리입니다.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 다음에서 [소스 파일을 레시피에 패키징](./package-source-files-recipe.md) 자습서에서는 R 소스 파일을 사용하여 소매 판매 레시피를 작성하는 마지막에 도커 URL이 제공되었습니다.

다음에 접속하면 **소스 선택** 페이지에서 R 소스 파일을 사용하여 빌드된 패키지된 레시피에 해당하는 도커 URL을 **[!UICONTROL 소스 URL]** 필드. 그런 다음 제공된 구성 파일을 드래그 앤 드롭하여 가져오거나 파일 시스템을 사용합니다 **브라우저**. 제공된 구성 파일은에서 찾을 수 있습니다. `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. 선택 **[!UICONTROL R]** 다음에서 **런타임** 드롭다운 및 **[!UICONTROL 분류]** 다음에서 **유형** 드롭다운입니다. 모든 항목이 작성되면 다음을 선택합니다. **[!UICONTROL 다음]** 오른쪽 상단 모서리에서 **스키마 관리**.

>[!NOTE]
>
> *유형* 지원 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**. 모델이 이러한 유형 중 하나에 해당하지 않는 경우 다음을 선택합니다. **[!UICONTROL 사용자 정의]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

그런 다음 섹션 아래에서 소매 판매 입력 및 출력 스키마를 선택합니다 **스키마 관리**&#x200B;에서 제공된 부트스트랩 스크립트를 사용하여 작성되었습니다. [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 튜토리얼.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

아래 *기능 관리* 섹션에서 스키마 뷰어의 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 피쳐를 강조표시하고 다음 중 하나를 선택하여 입력 및 출력 피쳐를 선택합니다 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 오른쪽에서 **[!UICONTROL 필드 속성]** 창. 이 자습서의 목적을 위해 다음을 설정하십시오. **[!UICONTROL weeklySales]** (으)로  **[!UICONTROL Target 기능]** 및 기타 모든 항목 **[!UICONTROL 입력 기능]**. 선택 **[!UICONTROL 다음]** 를 클릭하여 새로 구성된 레시피를 검토합니다.

레시피를 검토하고 필요에 따라 구성을 추가, 수정 또는 제거합니다. 선택 **완료** 레시피를 만들 수 있습니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

다음으로 진행 [다음 단계](#next-steps) 에서 모델을 만드는 방법을 알아보려면 [!DNL Data Science Workspace] 새로 생성된 소매 판매 레시피 사용.

### 도커 기반 레시피 가져오기 - PySpark {#pyspark}

탐색 및 선택하여 시작 **[!UICONTROL 워크플로]** 의 왼쪽 상단에 있음 [!DNL Platform] UI. 그런 다음 을 선택합니다. **레시피 가져오기** 및 선택 **[!UICONTROL 시작]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

다음 **구성** 페이지 **레시피 가져오기** 워크플로가 나타납니다. 배합식의 이름과 설명을 입력한 다음 선택합니다. **[!UICONTROL 다음]** 오른쪽 상단 모서리에서 을 참조하십시오.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 다음에서 [소스 파일을 레시피에 패키징](./package-source-files-recipe.md) 자습서에서는 PySpark 소스 파일을 사용하여 소매 판매 레시피를 작성하는 마지막에 도커 URL이 제공되었습니다.

다음에 접속하면 **소스 선택** 페이지에서 PySpark 소스 파일을 사용하여 빌드된 패키지된 레시피에 해당하는 도커 URL을 **[!UICONTROL 소스 URL]** 필드. 그런 다음 제공된 구성 파일을 드래그 앤 드롭하여 가져오거나 파일 시스템을 사용합니다 **브라우저**. 제공된 구성 파일은에서 찾을 수 있습니다. `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. 선택 **[!UICONTROL PySparc]** 다음에서 **런타임** 드롭다운입니다. PySpark 런타임을 선택하면 기본 아티팩트가 자동으로 채워집니다 **[!UICONTROL 도커]**. 그런 다음 을 선택합니다. **[!UICONTROL 분류]** 다음에서 **유형** 드롭다운입니다. 모든 항목이 작성되면 다음을 선택합니다. **[!UICONTROL 다음]** 오른쪽 상단 모서리에서 **스키마 관리**.

>[!NOTE]
>
> *유형* 지원 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**. 모델이 이러한 유형 중 하나에 해당하지 않는 경우 다음을 선택합니다. **[!UICONTROL 사용자 정의]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

그런 다음 다음을 사용하여 소매 판매 입력 및 출력 스키마를 선택합니다 **스키마 관리** 선택기에서 제공된 부트스트랩 스크립트를 사용하여 스키마를 만들었습니다. [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 튜토리얼.

![스키마 관리](../images/models-recipes/import-package-ui/manage-schemas.png)

아래 **기능 관리** 섹션에서 스키마 뷰어의 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 피쳐를 강조표시하고 다음 중 하나를 선택하여 입력 및 출력 피쳐를 선택합니다 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 오른쪽에서 **[!UICONTROL 필드 속성]** 창. 이 자습서의 목적을 위해 다음을 설정하십시오. **[!UICONTROL weeklySales]** (으)로  **[!UICONTROL Target 기능]** 및 기타 모든 항목 **[!UICONTROL 입력 기능]**. 선택 **[!UICONTROL 다음]** 을 클릭하여 새로 구성된 레시피를 검토합니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

레시피를 검토하고 필요에 따라 구성을 추가, 수정 또는 제거합니다. 선택 **[!UICONTROL 완료]** 레시피를 만들 수 있습니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

다음으로 진행 [다음 단계](#next-steps) 에서 모델을 만드는 방법을 알아보려면 [!DNL Data Science Workspace] 새로 생성된 소매 판매 레시피 사용.

### 도커 기반 레시피 가져오기 - Scala {#scala}

탐색 및 선택하여 시작 **[!UICONTROL 워크플로]** 의 왼쪽 상단에 있음 [!DNL Platform] UI. 그런 다음 을 선택합니다. **레시피 가져오기** 및 선택 **[!UICONTROL 시작]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

다음 **구성** 페이지 **레시피 가져오기** 워크플로가 나타납니다. 배합식의 이름과 설명을 입력한 다음 선택합니다. **[!UICONTROL 다음]** 오른쪽 상단 모서리에서 을 참조하십시오.

![워크플로우 구성](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 다음에서 [소스 파일을 레시피에 패키징](./package-source-files-recipe.md) 자습서에서는 Scala를 사용하여 소매 판매 레시피를 빌드한 끝에 도커 URL이 제공되었습니다([!DNL Spark]) 소스 파일.

다음에 접속하면 **소스 선택** 페이지에서 소스 URL 필드에 Scala 소스 파일을 사용하여 빌드된 패키지된 레시피에 해당하는 도커 URL을 붙여 넣습니다. 그런 다음 제공된 구성 파일을 드래그 앤 드롭하여 가져오거나 파일 시스템 브라우저를 사용합니다. 제공된 구성 파일은에서 찾을 수 있습니다. `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. 선택 **[!UICONTROL 스파크]** 다음에서 **런타임** 드롭다운입니다. 한 번 [!DNL Spark] 런타임이 선택됩니다. 기본 아티팩트는 **[!UICONTROL 도커]**. 그런 다음 을 선택합니다. **[!UICONTROL 회귀]** 다음에서 **유형** 드롭다운입니다. 모든 항목이 작성되면 다음을 선택합니다. **[!UICONTROL 다음]** 오른쪽 상단 모서리에서 **스키마 관리**.

>[!NOTE]
>
> 유형 지원 **[!UICONTROL 분류]** 및 **[!UICONTROL 회귀]**. 모델이 이러한 유형 중 하나에 해당하지 않는 경우 다음을 선택합니다. **[!UICONTROL 사용자 정의]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

그런 다음 다음을 사용하여 소매 판매 입력 및 출력 스키마를 선택합니다 **스키마 관리** 선택기에서 제공된 부트스트랩 스크립트를 사용하여 스키마를 만들었습니다. [소매 판매 스키마 및 데이터 세트 만들기](../models-recipes/create-retails-sales-dataset.md) 튜토리얼.

![스키마 관리](../images/models-recipes/import-package-ui/manage-schemas.png)

아래 **기능 관리** 섹션에서 스키마 뷰어의 테넌트 ID를 선택하여 소매 판매 입력 스키마를 확장합니다. 원하는 피쳐를 강조표시하고 다음 중 하나를 선택하여 입력 및 출력 피쳐를 선택합니다 **[!UICONTROL 입력 기능]** 또는 **[!UICONTROL Target 기능]** 오른쪽에서 **[!UICONTROL 필드 속성]** 창. 이 자습서의 목적을 위해 &quot;[!UICONTROL weeklySales]을(를) (으)로  **[!UICONTROL Target 기능]** 및 기타 모든 항목 **[!UICONTROL 입력 기능]**. 선택 **[!UICONTROL 다음]** 을 클릭하여 새로 구성된 레시피를 검토합니다.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

레시피를 검토하고 필요에 따라 구성을 추가, 수정 또는 제거합니다. 선택 **[!UICONTROL 완료]** 레시피를 만들 수 있습니다.

![](../images/models-recipes/import-package-ui/recipe_review.png)

다음으로 진행 [다음 단계](#next-steps) 에서 모델을 만드는 방법을 알아보려면 [!DNL Data Science Workspace] 새로 생성된 소매 판매 레시피 사용.

## 다음 단계 {#next-steps}

이 자습서에서는 레시피를 구성하고 로 가져오는 방법에 대한 통찰력을 제공했습니다 [!DNL Data Science Workspace]. 이제 새로 만든 레시피를 사용하여 모델을 만들고, 교육하고, 평가할 수 있습니다.

- [UI에서 모델 교육 및 평가](./train-evaluate-model-ui.md)
- [API를 사용하여 모델 교육 및 평가](./train-evaluate-model-api.md)
