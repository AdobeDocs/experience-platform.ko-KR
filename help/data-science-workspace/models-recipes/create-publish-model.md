---
keywords: Experience Platform;machine learning model;Data Science Workspace;popular topics;create and publish a model
solution: Experience Platform
title: 기계 학습 모델 연습 만들기 및 게시
topic: tutorial
type: Tutorial
description: Adobe Experience Platform 데이터 과학 작업 공간은 미리 만들어진 제품 Recommendations 레서피를 사용하여 목표를 달성할 수 있는 방법을 제공합니다. 이 튜토리얼을 따라 소매 데이터에 액세스하고, 이해하고, 기계 학습 모델을 만들고, 최적화하고, 데이터 과학 작업 공간에서 통찰력을 생성하는 방법을 확인하십시오.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---


# 기계 학습 모델 연습 만들기 및 게시

![](../images/models-recipes/model-walkthrough/objective.png)

온라인 소매 웹 사이트를 소유하고 있다고 가정해 보십시오. 고객이 소매 웹 사이트에서 쇼핑할 때 개인화된 제품 권장 사항을 제시하여 비즈니스에 제공하는 다양한 기타 제품을 표시하고 싶을 것입니다. 웹 사이트 존재의 기간 동안 고객 데이터를 지속적으로 수집하여 이 데이터를 통해 맞춤형 제품 추천을 생성하고자 합니다.

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 사전 제작된 [제품 Recommendations 레시피를 사용하여 목표를 달성할 수 있는 방법을 제공합니다](../pre-built-recipes/product-recommendations.md). 이 튜토리얼에 따라 소매 데이터에 액세스하고 이를 이해하며 기계 학습 모델을 생성 및 최적화하고 인사이트를 생성하는 방법을 확인하십시오 [!DNL Data Science Workspace].

이 자습서는 기계 학습 모델 [!DNL Data Science Workspace]을 만들기 위한 다음 단계에 대해 설명합니다.

1. [데이터 준비](#prepare-your-data)
2. [모델 작성](#author-your-model)
3. [모델 트레이닝 및 평가](#train-and-evaluate-your-model)
4. [모델 운영](#operationalize-your-model)

## 시작하기

이 튜토리얼을 시작하기 전에 다음 전제 조건이 필요합니다.

* 액세스 권한 [!DNL Adobe Experience Platform]. 에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자 [!DNL Experience Platform]에게 연락하여 진행하십시오.

* 활성 에셋. 다음 항목을 제공하려면 계정 담당자에게 문의하십시오.
   * Recommendations 레서피
   * Recommendations 입력 데이터 세트
   * Recommendations 입력 스키마
   * Recommendations 출력 데이터 세트
   * Recommendations 출력 스키마
   * 골든 데이터 세트 postValues
   * 골든 데이터 집합 스키마

* Adobe [!DNL Jupyter Notebook] 공용 저장소에서 [필요한 세 개의 파일 [!DNL Git] 을 다운로드하면](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs)이 파일을 사용하여 작업 과정을 [!DNL JupyterLab] 보여줍니다 [!DNL Data Science Workspace].

* 이 튜토리얼에서 사용되는 다음 주요 개념에 대한 작업 이해:
   * [[!DNL 경험 데이터 모델]](../../xdm/home.md):Adobe이 고객 경험 관리를 위한 표준 스키마(예: [!DNL Profile] 및 ExperienceEvent)를 정의하는 데 주도적인 표준화 활동입니다.
   * 데이터 집합:실제 데이터를 위한 저장 및 관리 구성 XDM 스키마의 실제 인스턴스화된 [인스턴스입니다](../../xdm/schema/field-dictionary.md).
   * 배치:데이터 세트는 배치로 구성됩니다. 일괄 처리란 일정 기간 동안 수집된 데이터 집합이며 하나의 단위로 함께 처리됩니다.
   * [!DNL JupyterLab]: [[!DNL JupiterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) 은 프로젝트를 위한 오픈 소스 웹 기반 인터페이스 [!DNL Jupyter] 로 긴밀하게 통합되어 [!DNL Experience Platform]있습니다.

## 데이터 준비 {#prepare-your-data}

고객에게 개인화된 제품을 추천할 수 있는 기계 학습 모델을 만들려면 웹 사이트에서 이전에 구입한 고객을 분석해야 합니다. 이 섹션에서는 이 데이터가 어떻게 수집되는지 [!DNL Platform] 와 이 데이터가 기계 학습 모델에 의해 사용되는 기능 데이터 세트로 어떻게 변환되는지 [!DNL Adobe Analytics]살펴봅니다.

### 데이터 탐색 및 스키마 이해

1. Adobe Experience Platform에 [로그인한 다음](https://platform.adobe.com/) 데이터 **** 세트를 클릭하여 기존 데이터 세트를 모두 나열하고 탐색할 데이터 세트를 선택합니다. 이 경우 데이터 세트 [!DNL Analytics]**골든 데이터 세트 postValues가 표시됩니다**.
   ![](../images/models-recipes/model-walkthrough/datasets_110.png)
2. 오른쪽 위 **[!UICONTROL 의 데이터 세트]** 미리 보기를 선택하여 샘플 레코드를 검사한 다음 닫기를 **[!UICONTROL 클릭합니다]**.
   ![](../images/models-recipes/model-walkthrough/golden_data_set_110.png)
3. 오른쪽 레일의 스키마 아래 링크를 선택하여 데이터 세트에 대한 스키마를 본 다음 데이터 세트 세부 정보 페이지로 돌아갑니다.&quot;
   ![](../images/models-recipes/model-walkthrough/golden_schema_110.png)

다른 데이터 세트는 미리 보기 목적으로 배치로 미리 채워집니다. 위 단계를 반복하여 이러한 데이터 세트를 볼 수 있습니다.

| 데이터 세트 이름 | 스키마 | 설명 |
| ----- | ----- | ----- |
| 골든 데이터 세트 postValues | 골든 데이터 집합 스키마 | [!DNL Analytics] 웹 사이트의 소스 데이터 |
| Recommendations 입력 데이터 세트 | Recommendations 입력 스키마 | 이 [!DNL Analytics] 데이터는 기능 파이프라인을 사용하여 교육 데이터 세트로 변환됩니다. 이 데이터는 제품 Recommendations 기계 학습 모델을 교육하는 데 사용됩니다. `itemid` 해당 고객이 구매한 제품에 `userid` 해당합니다. |
| Recommendations 출력 데이터 세트 | Recommendations 출력 스키마 | 점수 지정 결과가 저장되는 데이터 세트에 각 고객에 대해 권장되는 제품 목록이 포함됩니다. |

## 모델 작성 {#author-your-model}

라이프사이클의 두 번째 구성 요소에는 [!DNL Data Science Workspace] 레서피 및 모델 작성에 포함됩니다. 제품 Recommendations 레시피는 과거 구매 데이터와 머신 러닝을 활용하여 제품 추천을 규모에 맞게 생성하도록 설계되었습니다.

레서피는 특정 문제를 해결하기 위해 고안된 기계 학습 알고리즘과 로직을 포함하고 있어 모델의 기본입니다. 더욱 중요한 것은 레서피 솔루션을 통해 조직 전체에서 머신 러닝을 민주화할 수 있으므로 다른 사용자가 코드를 작성하지 않고도 서로 다른 사용 사례에 맞는 모델을 이용할 수 있습니다.

### 제품 Recommendations 레시피 살펴보기

1. 에서 왼쪽 탐색 [!DNL Adobe Experience Platform]열 **[!UICONTROL 에서]** 모델 **[!UICONTROL 으로 이동한 다음]** 맨 위에 있는 레서피를 클릭하여 조직에서 사용할 수 있는 레서피 목록을 확인합니다.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. 제공된 **[!UICONTROL Recommendations 레시피]** 이름을 클릭하여 해당 레서피를 찾아 엽니다.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. 오른쪽 레일에서 **[!UICONTROL Recommendations 입력 스키마를]** 클릭하여 레서피를 강력하게 하는 스키마를 봅니다. 스키마 필드 **[!UICONTROL itemId]** 및 **[!UICONTROL userId]** 는 특정 시간(타임스탬프)에 해당 고객이 구매한 제품(**[!UICONTROL interactionType]**)에&#x200B;****&#x200B;해당합니다. 동일한 단계에 따라 **[!UICONTROL Recommendations 출력 스키마의 필드를 검토하십시오]**.
   ![](../images/models-recipes/model-walkthrough/preview_schemas.png)

이제 제품 Recommendations 레서피에 필요한 입력 및 출력 스키마를 검토했습니다. 이제 다음 섹션으로 이동하여 제품 Recommendations 모델을 생성, 교육 및 평가하는 방법을 확인할 수 있습니다.

## 모델 트레이닝 및 평가 {#train-and-evaluate-your-model}

데이터가 준비되고 레서피 사용 준비가 되었으니 기계 학습 모델을 만들고, 교육하고, 평가할 수 있습니다.

### 모델 만들기

모델은 레서피 인스턴스로, 데이터를 규모에 따라 트레이닝하고 점수를 매길 수 있습니다.

1. 에서 왼쪽 탐색 [!DNL Adobe Experience Platform]열 **[!UICONTROL 에서]** 모델 **[!UICONTROL 으로 이동한 다음 페이지]** 맨 위에 있는 레서피를 클릭하여 조직에 대해 사용 가능한 모든 레서피 목록을 표시합니다.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. 해당 이름을 클릭하고 레서피 **[!UICONTROL 개요 페이지를 입력하여 제공된]** Recommendations 레서피를 찾아 엽니다. 중심(기존 모델이 없는 경우) **[!UICONTROL 이나 레서피]** 개요 페이지의 오른쪽 상단에서 모델 만들기를 클릭합니다.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. 교육에 사용할 수 있는 입력 데이터 집합 목록이 표시되면 **[!UICONTROL Recommendations 입력 데이터]** 집합을 선택하고 **[!UICONTROL 다음을 클릭합니다]**.
   ![](../images/models-recipes/model-walkthrough/select_dataset.png)
4. &quot;제품 Recommendations 모델&quot;과 같이 모델의 이름을 입력합니다. 모델의 기본 교육 및 점수 지정 동작에 대한 설정이 포함된 모델에 대한 사용 가능한 구성이 나열됩니다. 이러한 구성은 조직에 따라 다르므로 변경할 필요가 없습니다. 구성을 검토하고 마침을 **[!UICONTROL 클릭합니다]**.
   ![](../images/models-recipes/model-walkthrough/configure_model.png)
5. 이제 모델이 생성되고 모델의 *개요* 페이지가 새로 생성된 교육 실행 내에 나타납니다. 모델이 생성될 때 기본적으로 교육 실행이 생성됩니다.
   ![](../images/models-recipes/model-walkthrough/model_post_creation.png)

교육 실행이 끝날 때까지 기다리거나 다음 섹션에서 새 교육 실행을 계속 만들 수 있습니다.

### 사용자 지정 하이퍼매개 변수를 사용하여 모델 트레이닝

1. [ *모델 개요* ] 페이지에서 오른쪽 위 **[!UICONTROL 의]** [교육]을 클릭하여 새 교육 실행을 만듭니다. 모델을 만들 때 사용한 것과 동일한 입력 데이터 세트를 선택하고 **[!UICONTROL 다음을 클릭합니다]**.
   ![](../images/models-recipes/model-walkthrough/training_select_dataset.png)
2. 구성 *페이지가* 나타납니다. 여기서는 Hyperparameter라고도 하는 교육 실행의 **[!UICONTROL num_recommendations]** 값을 구성할 수 있습니다. 훈련되고 최적화된 모델은 트레이닝 실행 결과를 기반으로 가장 성과가 좋은 하이퍼링크 매개 변수를 활용합니다.

   하이퍼매개 변수는 알 수 없으므로, 교육이 실행되기 전에 할당해야 합니다. 하이퍼매개 변수를 조정하면 훈련된 모델의 정확도가 변경될 수 있습니다. 모델 최적화는 반복적인 프로세스이므로 만족스러운 평가가 이루어지기 전에 여러 개의 교육 실행이 필요할 수 있습니다.

   >[!TIP]
   >
   >num_recommendations **[!UICONTROL 를]** 10으로 설정합니다.

   ![](../images/models-recipes/model-walkthrough/configure_hyperparameter.png)
3. 새 교육 실행이 완료되면 모델 평가 차트에 추가 데이터 포인트가 나타납니다. 이 작업은 최대 몇 분 정도 걸릴 수 있습니다.
   ![](../images/models-recipes/model-walkthrough/post_training_run.png)

### 모델 평가

교육 실행이 완료될 때마다 결과 평가 지표를 보고 모델이 얼마나 잘 수행되었는지 확인할 수 있습니다.

1. 교육 실행을 클릭하여 완료된 각 교육 실행에 대한 평가 지표(정밀도 및 회수)를 검토합니다.
2. 각 평가 지표에 대해 제공된 정보를 살펴보십시오. 이러한 지표가 높을수록 모델이 더 잘 수행됩니다.
   ![](../images/models-recipes/model-walkthrough/evaluation_metrics.png)
3. 오른쪽 레일에서 각 교육 실행에 사용되는 데이터 세트, 스키마 및 구성 매개 변수를 볼 수 있습니다.
4. [모델] 페이지로 돌아가서 평가 지표를 관찰하여 실행 중인 성과가 가장 높은 교육 실행을 확인합니다.

## 모델 운영 {#operationalize-your-model}

데이터 과학 워크플로우의 마지막 단계는 데이터 저장소에서 통찰력을 수집하고 사용하기 위해 모델을 조작하는 것입니다.

### 성과 및 인사이트 생성

1. 제품 권장 사항 모델 *개요* 페이지에서 가장 높은 회수 및 정밀도 값으로 성과가 좋은 교육 실행 이름을 클릭합니다.
2. 교육 실행 세부 사항 페이지의 오른쪽 맨 위에서 **[!UICONTROL 점수를 클릭합니다]**.
3. 모델을 만들고 해당 교육 실행을 실행할 때 사용한 데이터 세트와 동일한 점수 입력 데이터 **[!UICONTROL 세트로]** Recommendations 입력 데이터 세트를 선택합니다. 그런 다음 **[!UICONTROL 다음을 클릭합니다]**.
   ![](../images/models-recipes/model-walkthrough/scoring_input.png)
4. 점수 **[!UICONTROL 출력 데이터]** 세트로 Recommendations 출력 데이터 세트를 선택합니다. 점수 지정 결과는 이 데이터 세트에 일괄 저장됩니다.
   ![](../images/models-recipes/model-walkthrough/scoring_output.png)
5. 점수 구성 검토 이러한 매개 변수에는 해당 스키마와 함께 이전에 선택한 입력 및 출력 데이터 집합이 포함됩니다. 마침 **[!UICONTROL 을]** 클릭하여 점수 실행을 시작합니다. 실행을 완료하는 데 몇 분 정도 걸릴 수 있습니다.
   ![](../images/models-recipes/model-walkthrough/scoring_configure.png)


### 점수에 따른 통찰력 보기

점수부여 실행이 성공적으로 완료되면 결과를 미리 보고 생성된 인사이트를 볼 수 있습니다.

1. 점수 지정 실행 페이지에서 완료된 점수 실행을 클릭한 다음 오른쪽 레일에 있는 **[!UICONTROL 미리 보기 점수]** 결과 데이터 세트를 클릭합니다.
   ![](../images/models-recipes/model-walkthrough/score_complete.png)
2. 미리 보기 테이블에서 각 행은 특정 고객에 대한 제품 권장 사항을 포함하며 각각 **[!UICONTROL recommendations]** 및 **[!UICONTROL userId로 레이블이]** 지정됩니다. 샘플 스크린샷에서 **[!UICONTROL num_recommendations]** Hyperparameter가 10으로 설정되었으므로 권장 사항의 각 행은 숫자 기호(#)로 구분된 최대 10개의 제품 ID를 포함할 수 있습니다.
   ![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## 다음 단계 {#next-steps}

제품 추천을 성공적으로 생성했습니다.

이 자습서에서는 기계 학습을 통해 처리되지 않은 원시 데이터를 유용한 정보로 변환하는 방법을 [!DNL Data Science Workspace]시연하는 작업 과정을 소개합니다. 사용 방법에 대한 자세한 내용 [!DNL Data Science Workspace]은 소매 판매 스키마 및 데이터 세트 [를 만드는 방법에 대한 다음 가이드를 계속 참조하십시오](./create-retails-sales-dataset.md).