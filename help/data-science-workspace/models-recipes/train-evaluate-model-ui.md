---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: 모델 트레이닝 및 평가(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 2%

---


# 모델 트레이닝 및 평가(UI)

Adobe Experience Platform 데이터 과학 작업 공간에서 기계 학습 모델은 모델의 의도에 적합한 기존 레서피를 결합함으로써 만들어집니다. 그런 다음 연관된 하이퍼매개 변수를 세밀하게 조정하여 모델의 운영 효율성과 효과를 최적화하기 위해 교육을 받고 평가합니다. 레서피는 재사용할 수 있습니다. 즉, 하나의 레서피를 사용하여 여러 모델을 생성하고 특정 목적에 맞게 변경할 수 있습니다.

이 자습서에서는 모델을 생성, 교육 및 평가하는 단계를 안내합니다.

## 시작하기

이 자습서를 완료하려면 액세스 권한이 있어야 합니다 [!DNL Experience Platform]. 에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자 [!DNL Experience Platform]에게 연락하여 진행하십시오.

이 자습서에는 기존 레서피가 필요합니다. 레서피가 없는 경우 계속하기 전에 UI [에서 패키지된 레서피 가져오기 자습서를](./import-packaged-recipe-ui.md) 따르십시오.

## 모델 만들기

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 모델]** 링크를 클릭하여 모든 기존 모델을 나열합니다. 페이지 **[!UICONTROL 오른쪽 상단의 모델]** 만들기를 클릭하여 모델 생성 프로세스를 시작합니다.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 기존 레서피 목록을 탐색하고, 모델을 생성하는 데 사용할 레서피(Recipe)를 찾아 선택하고 **[!UICONTROL 다음]**을 클릭합니다.
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. 적절한 입력 데이터 세트를 선택하고 **[!UICONTROL 다음을 클릭합니다]**. 그러면 모델의 기본 입력 교육 데이터 세트가 설정됩니다.
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. 모델 이름을 입력하고 기본 모델 구성을 검토하십시오. 기본 구성은 레서피 생성 중에 적용되었으며 값을 두 번 클릭하여 구성 값을 검토하고 수정했습니다. 새 구성 세트를 제공하려면 새 구성 **[!UICONTROL 업로드]** 를 클릭하고 모델 구성이 포함된 JSON 파일을 브라우저 창으로 드래그합니다. 마침 **[!UICONTROL 을]** 클릭하여 모델을 생성합니다.
   >[!NOTE]구성은 의도한 배합식에 고유하며, 이것은 소매 영업 레서피에 대한 구성이 제품 추천 레시피에 대해 작동하지 않음을 의미합니다. 소매 영업 [레서피 구성 목록은 참조](#reference) 섹션을 참조하십시오.

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 교육 실행 만들기

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 모델]** 링크를 클릭하여 모든 기존 모델을 나열합니다. 교육할 모델의 이름을 찾아 클릭합니다.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 현재 교육 상태와 함께 모든 기존 교육이 나열됩니다. 사용자 인터페이스를 사용하여 생성된 모델의 경우 기본 구성 및 입력 교육 데이터 세트를 사용하여 교육 실행이 자동으로 생성되고 실행됩니다. [!DNL Data Science Workspace]
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. 모델 개요 페이지의 오른쪽 **[!UICONTROL 위]** 근처에 있는 기차를 클릭하여 새 교육 실행을 만듭니다.
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. 교육 실행에 대한 교육 입력 데이터 세트를 선택하고 [다음]을 **[!UICONTROL 클릭합니다]**.
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. 모델을 생성하는 동안 제공된 기본 구성이 표시되고 값을 두 번 클릭하여 변경하고 이에 따라 수정합니다. [ **[!UICONTROL 마침]** ]을 클릭하여 교육 실행을 만들고 실행합니다.
   >[!NOTE]구성은 의도한 배합식에 고유하며, 이것은 소매 영업 레서피에 대한 구성이 제품 추천 레시피에 대해 작동하지 않음을 의미합니다. 소매 영업 [레서피 구성 목록은 참조](#reference) 섹션을 참조하십시오.

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## 모델 평가

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 모델]** 링크를 클릭하여 모든 기존 모델을 나열합니다. 평가할 모델의 이름을 찾아 클릭합니다.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 현재 교육 상태와 함께 모든 기존 교육이 나열됩니다. 완료된 여러 개의 교육 실행이 있는 경우, 평가 지표를 모델 평가 차트의 여러 교육 실행 간에 비교할 수 있습니다. 그래프 위의 드롭다운 목록을 사용하여 평가 지표를 선택합니다.

   MAPE(평균 절대 퍼센트 오류) 지표는 정확성을 오류 백분율로 나타냅니다. 이 방법은 성과가 가장 높은 실험을 식별하는 데 사용됩니다. MAPE가 낮을수록 좋습니다.

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   &quot;정밀도&quot; 지표는 검색된 총 인스턴스 수와 관련된 인스턴스의 비율을 *설명합니다* . 정밀도는 임의로 선택한 결과가 정확할 확률을 보여 줍니다.
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   특정 교육 실행을 클릭하여 해당 실행에 대한 세부 사항을 확인합니다. 이 작업은 실행이 완료되기 전에도 수행할 수 있습니다. 실행 세부 정보 페이지에서는 교육 실행과 관련된 다른 평가 지표, 구성 매개 변수 및 시각화를 볼 수 있습니다. 실행 세부 사항을 보기 위해 활동 로그를 다운로드할 수도 있습니다. 로그는 실패한 실행에 대해 잘못된 내용을 확인하는 데 특히 유용합니다.
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. 하이퍼매개 변수는 교육할 수 없으며, 여러 하이퍼매개 변수의 조합을 테스트하여 모델을 최적화해야 합니다. 최적화된 모델에 도착할 때까지 이 모델 교육 및 평가 과정을 반복합니다.

## 다음 단계

이 자습서에서는 모델을 만들고, 교육하고, 평가하는 과정을 안내합니다 [!DNL Data Science Workspace]. 최적화된 모델에 도달하고 나면 UI [튜토리얼에서 모델](./score-model-ui.md) 점수 지정 튜토리얼을 따라 훈련된 모델을 사용하여 통찰력을 생성할 수 있습니다.

## 참조 {#reference}

### 소매 영업 레서피 구성

하이퍼매개 변수는 모델의 교육 동작을 결정하며, 하이퍼매개 변수를 수정하면 모델의 정확성과 정확성에 영향을 줍니다.

| 하이퍼매개 변수 | 설명 | 권장 범위 |
--- | --- | ---
| learning_rate | 학습 비율은 learning_rate로 각 트리의 기여도를 축소합니다. learning_rate와 n_estimator 사이에 상쇄 효과가 있습니다. | 0.1 | [2 - 10] / 견적 담당자 수 |
| n_견적 | 수행할 부흥 단계 수입니다. 그라데이션 강화는 지나치게 맞춤화하기에 상당히 강력하기 때문에 보통 많은 수가 더 나은 성능을 얻을 수 있습니다. | 100 | 100 - 1000 |
| max_depth | 개별 회귀 견적 도구의 최대 깊이입니다. 최대 깊이는 트리의 노드 수를 제한합니다. 최상의 성능을 위해 이 매개 변수를 조정하십시오. 가장 좋은 값은 입력 변수의 상호 작용에 따라 달라집니다. | 3 | 4 - 10 |

추가 매개 변수는 모델의 기술 속성을 결정합니다.

| 매개 변수 키 | 유형 | 설명 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 속성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 특성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부 결정 |
| `tenantId` | 문자열 | 이 ID를 사용하면 만든 리소스가 적절하게 대체되고 IMS 조직 내에 포함됩니다. [테넌트 ID를 찾으려면 여기](../../xdm/api/getting-started.md#know-your-tenant_id) 단계를 따르십시오. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화에 대한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델을 평가하는 데 사용할 평가 지표의 쉼표로 구분된 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델 채점하는 데 사용되는 출력 스키마입니다. |