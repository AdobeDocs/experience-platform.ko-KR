---
keywords: Experience Platform;교육 및 평가;데이터 과학 작업 공간;인기 있는 주제;모델 만들기;교육 실행 만들기
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 모델 트레이닝 및 평가
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform 데이터 과학 작업 공간에서 기계 학습 모델은 모델의 의도에 적합한 기존 레서피를 결합하여 만들어집니다. 그런 다음 연관된 하이퍼매개 변수를 미세 조정하여 모델의 운영 효율성과 효과를 최적화하기 위해 교육 및 평가를 수행합니다. 레서피는 재사용 가능하므로, 하나의 레서피를 사용하여 여러 모델을 생성하고 특정 목적에 맞게 변경할 수 있습니다.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# 데이터 과학 작업 공간 UI에서 모델 트레이닝 및 평가

Adobe Experience Platform 데이터 과학 작업 공간에서 기계 학습 모델은 모델의 의도에 적합한 기존 레서피를 결합하여 만들어집니다. 그런 다음 연관된 하이퍼매개 변수를 미세 조정하여 모델의 운영 효율성과 효과를 최적화하기 위해 교육 및 평가를 수행합니다. 레서피는 재사용 가능하므로, 하나의 레서피를 사용하여 여러 모델을 생성하고 특정 목적에 맞게 변경할 수 있습니다.

이 자습서에서는 모델을 생성, 교육 및 평가하는 단계를 안내합니다.

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]에서 IMS 조직에 액세스할 수 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

이 자습서에는 기존 레서피가 필요합니다. 레서피가 없는 경우 계속하기 전에 UI](./import-packaged-recipe-ui.md) 튜토리얼에서 [패키지된 레서피 가져오기를 따르십시오.

## 모델 만들기

Experience Platform에서 왼쪽 탐색 창에 있는 **[!UICONTROL Models]** 탭을 선택한 다음 찾아보기 탭을 선택하여 기존 모델을 확인합니다. 모델 생성 프로세스를 시작하려면 페이지 오른쪽 상단의 **[!UICONTROL Create Model]**&#x200B;을 선택합니다.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

기존 레서피 목록을 탐색하고, 모델을 생성하는 데 사용할 레서피를 찾아 선택하고 **[!UICONTROL Next]**을 선택합니다.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

적절한 입력 데이터 세트를 선택하고 **[!UICONTROL Next]**을 선택합니다. 그러면 모델에 대한 기본 입력 교육 데이터 세트가 설정됩니다.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

모델 이름을 입력하고 기본 모델 구성을 검토합니다. 기본 구성은 레서피 생성 중에 적용되었으며 값을 두 번 클릭하여 구성 값을 검토하고 수정합니다.

새 구성 세트를 제공하려면 **[!UICONTROL Upload New Config]**&#x200B;을 선택하고 모델 구성이 포함된 JSON 파일을 브라우저 창으로 드래그합니다. **[!UICONTROL Finish]**&#x200B;을 선택하여 모델을 생성합니다.

>[!NOTE]
>
>구성은 고유하며 의도한 레서피에 따라 달라지며, 이것은 소매 판매 레서피에 대한 구성이 제품 Recommendations 레서피에 대해 작동하지 않음을 의미합니다. 소매 판매 레서피 구성 목록은 [참조](#reference) 섹션을 참조하십시오.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 교육 실행 만들기

Experience Platform에서 왼쪽 탐색 창에 있는 **[!UICONTROL Models]** 탭을 선택한 다음 찾아보기 탭을 선택하여 기존 모델을 확인합니다. 트레이닝할 모델 이름에 첨부된 하이퍼링크를 찾아 선택합니다.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

현재 교육 상태의 모든 기존 교육 실행이 나열됩니다. [!DNL Data Science Workspace] 사용자 인터페이스를 사용하여 만든 모델의 경우 기본 구성 및 입력 교육 데이터 세트를 사용하여 교육 실행이 자동으로 생성되고 실행됩니다.

모델 개요 페이지의 오른쪽 상단 근처에 있는 **[!UICONTROL Train]**&#x200B;을 선택하여 새 교육 실행을 만듭니다.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

교육 실행에 대한 교육 입력 데이터 세트를 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

모델을 생성하는 동안 제공된 기본 구성이 표시되고 값을 두 번 클릭하여 변경하고 이에 따라 수정합니다. **[!UICONTROL Finish]**&#x200B;을 선택하여 교육 실행을 만들고 실행합니다.

>[!NOTE]
>
>구성은 고유하며 의도한 레서피에 따라 달라지며, 이것은 소매 판매 레서피에 대한 구성이 제품 Recommendations 레서피에 대해 작동하지 않음을 의미합니다. 소매 판매 레서피 구성 목록은 [참조](#reference) 섹션을 참조하십시오.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## 모델 평가

Experience Platform에서 왼쪽 탐색 창에 있는 **[!UICONTROL Models]** 탭을 선택한 다음 찾아보기 탭을 선택하여 기존 모델을 확인합니다. 평가할 모델의 이름에 첨부된 하이퍼링크를 찾아 선택합니다.

![모델 선택](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

현재 교육 상태의 모든 기존 교육 실행이 나열됩니다. 여러 개의 완료된 교육 실행을 사용할 경우 모델 평가 차트에서 여러 교육 실행 간에 평가 지표를 비교할 수 있습니다. 그래프 위의 드롭다운 목록을 사용하여 평가 지표를 선택합니다.

MAPE(평균 절대 퍼센트 오류) 지표는 정확도를 오류 백분율로 나타냅니다. 이 방법은 성과가 가장 높은 실험을 식별하는 데 사용됩니다. MAPE가 낮을수록 좋습니다.

![교육 실행 개요](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

&quot;정밀도&quot; 지표는 총 *retried* 인스턴스와 비교하여 관련 인스턴스의 백분율을 설명합니다. 정밀도는 무작위로 선택된 결과가 정확할 확률을 볼 수 있습니다.

![여러 실행 실행 실행](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

특정 교육 실행을 선택하면 평가 페이지를 열어 실행되는 세부 정보가 제공됩니다. 이 작업은 실행이 완료되기 전에도 수행할 수 있습니다. 평가 페이지에서 교육 실행에만 적용되는 다른 평가 지표, 구성 매개 변수 및 시각화를 볼 수 있습니다.

![미리 보기 로그](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

실행 세부 사항을 보려면 활동 로그를 다운로드할 수도 있습니다. 로그는 실패한 실행이 잘못된 내용을 확인하는 데 특히 유용합니다.

![활동 로그](../images/models-recipes/train-evaluate-ui/activity_logs.png)

하이퍼매개 변수를 교육할 수 없으며, 서로 다른 하이퍼매개 변수 조합을 테스트하여 모델을 최적화해야 합니다. 최적화된 모델에 도착할 때까지 이 모델 교육 및 평가 과정을 반복합니다.

## 다음 단계

이 자습서에서는 [!DNL Data Science Workspace]에서 모델을 만들고, 교육하고, 평가하는 과정을 안내합니다. 최적화된 모델에 도달하면 UI](./score-model-ui.md) 튜토리얼에서 [모델 점수 지정  튜토리얼을 따라 훈련된 모델을 사용하여 통찰력을 생성할 수 있습니다.

## 참조 {#reference}

### 소매 영업 레서피 구성

하이퍼매개 변수는 모델의 교육 동작을 결정하며, 하이퍼매개 변수를 수정하면 모델의 정확성과 정확성에 영향을 미칩니다.

| 하이퍼매개 변수 | 설명 | 권장 범위 |
--- | --- | ---
| learning_rate | 학습 비율은 learning_rate로 각 트리의 기여도를 축소합니다. learning_rate와 n_estimators 사이에는 상쇄 조건이 있습니다. | 0.1 | [2 - 10] /견적 담당자 수 |
| n_견적 도구 | 수행할 부흥 단계 수입니다. 그레이디언트 증대는 지나치게 맞추기 때문에 일반적으로 많은 수가 더 나은 성능을 얻을 수 있습니다. | 100 | 100 - 1000 |
| max_depth | 개별 회귀 견적 도구의 최대 깊이입니다. 최대 깊이는 트리의 노드 수를 제한합니다. 최상의 성능을 위해 이 매개 변수를 조정하십시오.가장 좋은 값은 입력 변수의 상호 작용에 따라 달라집니다. | 3 | 4 - 10 |

추가 매개 변수는 모델의 기술 속성을 결정합니다.

| 매개 변수 키 | 유형 | 설명 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 문자열 | 쉼표로 구분된 입력 스키마 특성 목록입니다. |
| `ACP_DSW_TARGET_FEATURES` | 문자열 | 쉼표로 구분된 출력 스키마 특성 목록입니다. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 부울 | 입력 및 출력 기능을 수정할 수 있는지 여부 결정 |
| `tenantId` | 문자열 | 이 ID를 사용하면 만든 리소스가 적절하게 지정되고 IMS 조직 내에 포함됩니다. [다음 단계에 따라 테넌트 ](../../xdm/api/getting-started.md#know-your-tenant_id) ID를 찾습니다. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 문자열 | 모델 교육에 사용되는 입력 스키마입니다. |
| `evaluation.labelColumn` | 문자열 | 평가 시각화에 대한 열 레이블입니다. |
| `evaluation.metrics` | 문자열 | 모델을 평가하는 데 사용할 평가 지표의 쉼표로 구분된 목록입니다. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 문자열 | 모델 점수를 매기는 데 사용되는 출력 스키마입니다. |
