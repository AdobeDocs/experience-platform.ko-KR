---
keywords: Experience Platform;교육 및 평가;데이터 과학 Workspace;인기 주제;모델 만들기;교육 실행 만들기
solution: Experience Platform
title: 데이터 과학 Workspace UI에서 모델 교육 및 평가
type: Tutorial
description: Adobe Experience Platform Data Science Workspace에서 모델의 의도에 적합한 기존 레시피를 통합하여 머신 러닝 모델이 생성됩니다. 그런 다음 모델은 관련된 하이퍼파라미터를 미세 조정하여 작동 효율 및 효능을 최적화하도록 훈련 및 평가된다. 레시피는 재사용할 수 있습니다. 즉, 단일 레시피로 여러 모델을 만들고 특정 목적에 맞게 맞춤화할 수 있습니다.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# 데이터 과학 Workspace UI에서 모델 교육 및 평가

>[!NOTE]
>
>Data Science 작업 영역은(는) 더 이상 구매할 수 없습니다.
>
>이 설명서는 데이터 과학 작업 영역 이전에 사용 권한이 있는 기존 고객을 대상으로 합니다.

Adobe Experience Platform Data Science 작업 영역에서 기계 학습 모델은 모델의 의도에 적합한 기존 레서피를 통합하여 만들어집니다. 그런 다음 모델을 훈련하고 평가하여 연결된 하이퍼 매개 변수를 미세 조정하여 운영 효율성과 효율성을 최적화합니다. 레시피는 재사용이 가능하므로 하나의 레시피로 여러 모델을 만들고 특정 목적에 맞게 조정할 수 있습니다.

이 튜토리얼 단계에서는 모델을 생성, 훈련 및 평가하는 단계를 안내합니다.

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]에 대한 액세스 권한이 있어야 합니다. 에 있는 [!DNL Experience Platform]조직에 대한 액세스 권한이 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

이 자습서에는 기존 레시피가 필요합니다. 레시피가 없는 경우 계속하기 전에 [UI에서 패키지된 레시피 가져오기](./import-packaged-recipe-ui.md) 자습서를 따르십시오.

## 모델 만들기

Experience Platform에서 왼쪽 탐색에 있는 **[!UICONTROL 모델]** 탭을 선택한 다음 찾아보기 탭을 선택하여 기존 모델을 봅니다. 페이지 오른쪽 상단 근처에 있는 모델&#x200B;]**만들기를 선택하여**[!UICONTROL &#x200B;모델 생성 프로세스를 시작합니다.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

기존 레서피 목록을 검색하고, 모델을 만드는 데 사용할 레서피를 찾아 선택한 다음, 다음(Next ]**)을 선택합니다**[!UICONTROL .![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

적절한 입력 데이터 세트 를 선택하고 다음&#x200B;]**을 선택합니다**[!UICONTROL . 이렇게 하면 모델에 대한 기본 입력 교육 데이터 세트 설정됩니다.![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

모델의 이름을 입력하고 기본 모델 구성을 검토합니다. 레서피 생성 중에 기본 구성이 적용되었으며, 값을 두 번 클릭하여 구성 값을 검토하고 수정합니다.

새 구성 집합을 제공하려면 새로 만들기 구성&#x200B;]**업로드를 선택하고**[!UICONTROL &#x200B;모델 구성이 포함된 JSON 파일을 브라우저 창 창으로 드래그합니다. 마침&#x200B;]**을 선택하여**[!UICONTROL &#x200B;모델을 만듭니다.

>[!NOTE]
>
>구성은 고유하며 의도한 레시피에만 적용됩니다. 즉, 소매 판매 레시피에 대한 구성이 제품 Recommendations 레시피에는 작동하지 않습니다. 소매 판매 레시피 구성 목록은 [참조](#reference) 섹션을 참조하십시오.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 교육 실행 만들기

Experience Platform에서 왼쪽 탐색에 있는 **[!UICONTROL 모델]** 탭을 선택한 다음 찾아보기 탭을 선택하여 기존 모델을 봅니다. 교육하려는 모델의 이름에 첨부된 하이퍼링크를 찾아 선택합니다.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

현재 교육 상태의 기존 교육 실행이 모두 나열됩니다. 사용자 인터페이스를 사용하여 [!DNL Data Science Workspace] 생성된 모델의 경우 교육 실행이 자동으로 생성되고 기본 구성 및 입력 교육 데이터 세트 사용하여 실행됩니다.

모델 개요 페이지의 오른쪽 위에 있는 학습&#x200B;]**을 선택하여**[!UICONTROL &#x200B;새 교육 실행을 만들기.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

교육 실행에 대한 교육 입력 데이터 세트 선택한 다음, 다음&#x200B;]**선택합니다**[!UICONTROL .

![](../images/models-recipes/train-evaluate-ui/training_input.png)

모델을 만드는 동안 제공된 기본 구성이 표시되며, 값을 두 번 클릭하여 적절하게 변경하고 수정합니다. 마침&#x200B;]**을 선택하여**[!UICONTROL &#x200B;교육 실행을 만들고 실행합니다.

>[!NOTE]
>
>구성은 고유하고 의도한 레서피에 따라 다르며, 이는 소매 판매 레서피에 대한 구성이 제품 추천 레서피에 대해 작동하지 않음을 의미합니다. [Retail Sales Recipe 구성 목록에 대해서는 참조](#reference) 섹션을 참조하십시오.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## 모델 평가

Experience Platform에서 왼쪽 탐색에 있는 모델&#x200B;]**탭 선택한**[!UICONTROL &#x200B;다음 찾아보기 탭 선택하여 기존 모델을 봅니다. 평가하려는 모델 이름에 첨부된 하이퍼링크를 찾아 선택합니다.

![모델 선택](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

현재 교육 상태의 기존 교육 실행이 모두 나열됩니다. 완료된 교육 실행이 여러 개 있는 경우 모델 평가 차트에서 여러 교육 실행 간에 평가 지표를 비교할 수 있습니다. 그래프 위의 드롭다운 목록을 사용하여 평가 지표를 선택합니다.

MAPE(Mean Absolute Percent Error) 지표는 정확도를 오류의 백분율로 표시합니다. 가장 성과가 좋은 실험 항목을 식별하는 데 사용됩니다. MAPE는 낮을수록 좋습니다.

![교육 실행 개요](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

&quot;Precision&quot; 지표 는 검색된 총 *인스턴스와 비교한 관련 인스턴스의 백분율을* 나타냅니다. 정밀도는 임의로 선택한 결과가 정확할 확률로 볼 수 있습니다.

![여러 실행 실행](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

특정 교육 실행을 선택하면 평가 페이지를 열어 해당 실행에 대한 세부 정보가 제공됩니다. 실행이 완료되기 전이라도 이 작업을 수행할 수 있습니다. 평가 페이지에서 교육 실행과 관련된 다른 평가 지표, 구성 매개 변수 및 시각화를 확인할 수 있습니다.

![로그 미리 보기](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

활동 로그를 다운로드하여 실행의 세부 사항을 볼 수도 있습니다. 로그는 실패한 실행에서 무엇이 잘못되었는지 확인하는 데 특히 유용합니다.

![활동 로그](../images/models-recipes/train-evaluate-ui/activity_logs.png)

하이퍼 매개 변수는 학습할 수 없으며 하이퍼 매개 변수의 다양한 조합을 테스트하여 모델을 최적화해야 합니다. 최적화된 모델에 도달할 때까지 이 모델 교육 및 평가 프로세스를 반복합니다.

## 다음 단계

이 자습서에서는 [!DNL Data Science Workspace]에서 모델을 만들고, 교육하고, 평가하는 과정을 안내했습니다. 최적화된 모델에 도달하면 훈련된 모델을 사용하여 [UI에서 모델 점수 지정](./score-model-ui.md) 자습서에 따라 인사이트를 생성할 수 있습니다.

## 참조 {#reference}

### 리테일 판매 레시피 구성

하이퍼파라미터는 모델의 교육 동작을 결정하며, 하이퍼파라미터를 수정하면 모델의 정확도와 정밀도에 영향을 미칩니다.

| 하이퍼파라미터 | 설명 | 권장 범위 |
| --- | --- | --- |
| learning_rate | 학습률은 각 트리의 기여도를 learning_rate씩 줄입니다. learning_rate와 n_estimators 사이에는 상충관계가 있습니다. | 0.1 |
| n_estimators | 수행할 승압 스테이지의 수입니다. 그레이디언트 부스팅은 과적합에 매우 강력하므로 많은 수의 그래디언트 부스팅은 일반적으로 더 나은 성능을 제공합니다. | 100 |
| max_depth | 개별 회귀 추정기의 최대 깊이입니다. 최대 깊이는 트리의 노드 수를 제한합니다. 최상의 성능을 위해 이 매개 변수를 조정합니다. 가장 적합한 값은 입력 변수의 상호 작용에 따라 달라집니다. | 3 |

추가 매개변수는 모델의 기술적 특성을 결정합니다.

| 매개 변수 키 | 유형 | 설명 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 속성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 속성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부를 결정합니다 |
| `tenantId` | 문자열 | 이 ID를 사용하면 만든 리소스의 네임스페이스가 제대로 지정되고 조직 내에 포함됩니다. [여기의](../../xdm/api/getting-started.md#know-your-tenant_id) 단계에 따라 테넌트 ID를 찾습니다. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화를 위한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델 평가에 사용할 평가 지표의 쉼표로 구분된 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델의 점수를 매기는 데 사용되는 출력 스키마입니다. |
