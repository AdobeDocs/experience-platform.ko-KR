---
keywords: Experience Platform;교육 및 평가;데이터 과학 작업 공간;인기 항목;모델 만들기;교육 실행 만들기
solution: Experience Platform
title: Data Science Workspace UI에서 모델 교육 및 평가
type: Tutorial
description: Adobe Experience Platform Data Science Workspace에서 모델 의도에 적합한 기존 레서피를 결합하여 기계 학습 모델을 생성합니다. 그런 다음 연관된 Hyperparameters를 세밀하게 조정하여 모델의 운영 효율성과 효과를 최적화하기 위해 Model을 교육 및 평가합니다. 레서피는 재사용할 수 있습니다. 즉, 여러 모델을 생성하고 하나의 레서피로 특정 목적에 맞게 조정할 수 있습니다.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 2%

---

# Data Science Workspace UI에서 모델 교육 및 평가

Adobe Experience Platform Data Science Workspace에서 모델 의도에 적합한 기존 레서피를 결합하여 기계 학습 모델을 생성합니다. 그런 다음 연관된 Hyperparameters를 세밀하게 조정하여 모델의 운영 효율성과 효과를 최적화하기 위해 Model을 교육 및 평가합니다. 레서피는 재사용할 수 있습니다. 즉, 여러 모델을 생성하고 하나의 레서피로 특정 목적에 맞게 조정할 수 있습니다.

이 자습서에서는 모델을 생성, 교육 및 평가하는 단계를 안내합니다.

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]. 의 조직에 액세스할 수 없는 경우 [!DNL Experience Platform]을(를) 계속하기 전에 시스템 관리자에게 문의하십시오.

이 자습서에는 기존 레서피가 필요합니다. 레서피가 없는 경우, [UI에서 패키지된 레서피 가져오기](./import-packaged-recipe-ui.md) 계속하기 전에 자습서를 참조하십시오.

## 모델 만들기

Experience Platform에서 **[!UICONTROL 모델]** 왼쪽 탐색에 있는 탭을 선택한 다음 찾아보기 탭을 선택하여 기존 모델을 봅니다. 선택 **[!UICONTROL 모델 만들기]** 모델 작성 프로세스를 시작할 페이지 오른쪽 상단 근처에 있습니다.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

기존 레서피 목록을 탐색하고, 모델을 생성하는 데 사용할 레서피 를 찾아 선택하고 선택합니다 **[!UICONTROL 다음]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

적절한 입력 데이터 세트를 선택하고 을(를) 선택합니다 **[!UICONTROL 다음]**. 이 경우 모델의 기본 입력 교육 데이터 세트가 설정됩니다.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

모델 이름을 입력하고 기본 모델 구성을 검토합니다. 배합식 생성 중에 기본 구성이 적용되었으며, 값을 두 번 눌러 구성 값을 검토 및 수정합니다.

새 구성 세트를 제공하려면 **[!UICONTROL 새 구성 업로드]** 모델 구성이 들어 있는 JSON 파일을 브라우저 창으로 드래그합니다. 선택 **[!UICONTROL 완료]** 모델 생성

>[!NOTE]
>
>구성은 의도한 배합식에 고유하며, 이는 소매 판매 배합식에 대한 구성이 제품 Recommendations 배합식에 대해 작동하지 않음을 의미합니다. 자세한 내용은 [참조](#reference) 소매 판매 배합식 구성 목록에 대한 섹션을 참조하십시오.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 교육 실행 만들기

Experience Platform에서 **[!UICONTROL 모델]** 왼쪽 탐색에 있는 탭을 선택한 다음 찾아보기 탭을 선택하여 기존 모델을 봅니다. 교육할 모델 이름에 첨부된 하이퍼링크를 찾아 선택합니다.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

현재 교육 상태가 있는 모든 기존 교육 실행이 나열됩니다. 를 사용하여 생성된 모델의 경우 [!DNL Data Science Workspace] 사용자 인터페이스에서는 기본 구성 및 입력 교육 데이터 세트를 사용하여 교육 실행이 자동으로 생성되고 실행됩니다.

을(를) 선택하여 새 교육 실행 만들기 **[!UICONTROL 트레인]** 모델 개요 페이지의 오른쪽 상단 근처에 있습니다.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

교육 실행에 대한 교육 입력 데이터 세트를 선택한 다음 **[!UICONTROL 다음]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

모델 생성 중에 제공된 기본 구성이 표시되고, 값을 두 번 눌러 해당 구성을 변경하고 수정합니다. 선택 **[!UICONTROL 완료]** 교육 실행을 생성하고 실행하기 위해

>[!NOTE]
>
>구성은 의도한 배합식에 고유하며, 이는 소매 판매 배합식에 대한 구성이 제품 Recommendations 배합식에 대해 작동하지 않음을 의미합니다. 자세한 내용은 [참조](#reference) 소매 판매 배합식 구성 목록에 대한 섹션을 참조하십시오.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## 모델 평가

Experience Platform에서 **[!UICONTROL 모델]** 왼쪽 탐색에 있는 탭을 선택한 다음 찾아보기 탭을 선택하여 기존 모델을 봅니다. 평가할 모델 이름에 첨부된 하이퍼링크를 찾아 선택합니다.

![모델 선택](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

현재 교육 상태가 있는 모든 기존 교육 실행이 나열됩니다. 여러 개의 완료된 교육 실행이 있으면 모델 평가 차트의 여러 교육 실행에서 평가 지표를 비교할 수 있습니다. 그래프 위의 드롭다운 목록을 사용하여 평가 지표를 선택합니다.

평균 절대 비율 오류(MAPE) 지표는 정확도를 오류 백분율로 나타냅니다. 이 변수는 성과가 가장 높은 실험을 식별하는 데 사용됩니다. MAPE가 낮을수록 좋습니다.

![교육 실행 개요](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

정밀도 지표는 총계 대비 관련 인스턴스 비율을 설명합니다 *검색됨* 인스턴스. 정밀도는 임의로 선택한 결과가 정확할 확률을 보여 줍니다.

![여러 실행 실행 실행 실행](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

특정 교육 실행을 선택하면 평가 페이지를 열어 실행한 세부 정보가 제공됩니다. 이 작업은 실행이 완료되기 전에도 수행할 수 있습니다. 평가 페이지에서는 교육 실행과 관련된 다른 평가 지표, 구성 매개 변수 및 시각화를 볼 수 있습니다.

![로그 미리 보기](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

활동 로그를 다운로드하여 실행 세부 사항을 볼 수도 있습니다. 로그는 특히 잘못된 내용을 보기 위해 실패한 실행에 유용합니다.

![활동 로그](../images/models-recipes/train-evaluate-ui/activity_logs.png)

하이퍼매개 변수는 교육할 수 없으며, 하이퍼매개 변수의 다양한 조합을 테스트하여 모델을 최적화해야 합니다. 최적화된 모델에 도달할 때까지 이 모델 교육 및 평가 프로세스를 반복합니다.

## 다음 단계

이 자습서에서는 의 모델 만들기, 교육 및 평가를 안내합니다 [!DNL Data Science Workspace]. 최적화된 모델에 도달하면 숙련된 모델을 사용하여 다음 정보를 수행하여 통찰력을 생성할 수 있습니다 [UI에서 모델 점수 책정](./score-model-ui.md) 자습서입니다.

## 참조 {#reference}

### 소매 판매 레서피 구성

하이퍼매개 변수는 모델의 교육 동작을 결정하며, 하이퍼매개 변수를 수정하면 모델의 정확도와 정밀도에 영향을 줍니다.

| Hyperparameter | 설명 | 권장 범위 |
| --- | --- | --- |
| learn_rate | 학습 비율은 learning_rate로 각 트리의 기여도를 낮춥니다. learning_rate 와 n_estimators 간에 교환이 있습니다. | 0.1 |
| n_견적 툴 | 수행할 증폭 단계 수입니다. 그라데이션 승진은 대개 오버피팅에 상당히 강력하므로 일반적으로 성능이 향상됩니다. | 100 |
| max_depth | 개별 회귀 추정자의 최대 깊이입니다. 최대 깊이는 트리의 노드 수를 제한합니다. 최상의 성능을 위해 이 매개 변수를 조정하십시오. 가장 좋은 값은 입력 변수의 상호 작용에 따라 달라집니다. | 3 |

추가 매개변수는 모델의 기술 속성을 결정합니다.

| 매개 변수 키 | 유형 | 설명 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 속성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 속성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부를 결정합니다 |
| `tenantId` | 문자열 | 이 ID를 사용하면 생성한 리소스가 적절하게 대체되고 조직 내에 포함되어 있습니다. [다음 단계를 수행합니다.](../../xdm/api/getting-started.md#know-your-tenant_id) 임차인 ID를 찾으려면 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화를 위한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델을 평가하는 데 사용할 평가 지표의 쉼표로 구분된 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델 점수에 사용되는 출력 스키마입니다. |
