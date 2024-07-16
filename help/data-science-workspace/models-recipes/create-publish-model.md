---
keywords: Experience Platform;머신 러닝 모델;Data Science Workspace;인기 주제;모델 만들기 및 게시
solution: Experience Platform
title: 머신 러닝 모델 만들기 및 Publish
type: Tutorial
description: 다음 안내서에서는 머신 러닝 모델을 만들고 게시하는 데 필요한 단계에 대해 설명합니다.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---


# 머신 러닝 모델 만들기 및 게시

다음 안내서에서는 머신 러닝 모델을 만들고 게시하는 데 필요한 단계에 대해 설명합니다. 각 섹션에는 수행할 작업에 대한 설명과 설명된 단계를 수행하기 위한 UI 및 API 설명서에 대한 링크가 포함되어 있습니다.

## 시작하기

이 자습서를 시작하기 전에 다음 사전 요구 사항이 있어야 합니다.

- [!DNL Adobe Experience Platform]에 액세스. [!DNL Experience Platform]의 조직에 대한 액세스 권한이 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

- 모든 데이터 과학 Workspace 자습서에서는 Luma 성향 모델을 사용합니다. 계속하려면 [Luma 성향 모델 스키마 및 데이터 세트](./create-luma-data.md)를 만들어야 합니다.

### 데이터 탐색 및 스키마 이해

[Adobe Experience Platform](https://platform.adobe.com/)에 로그인하고 **[!UICONTROL 데이터 세트]**&#x200B;를 선택하여 모든 기존 데이터 세트를 나열하고 탐색할 데이터 세트를 선택합니다. 이 경우 **Luma 웹 데이터** 데이터 세트를 선택해야 합니다.

![Luma 웹 데이터 세트 선택](../images/models-recipes/model-walkthrough/luma-dataset.png)

데이터 세트 활동 페이지가 열리고 데이터 세트와 관련된 정보가 나열됩니다. 오른쪽 상단 근처에서 **[!UICONTROL 데이터 집합 미리 보기]**&#x200B;를 선택하여 샘플 레코드를 검사할 수 있습니다. 선택한 데이터 세트에 대한 스키마를 볼 수도 있습니다.

![Luma 웹 데이터 보기](../images/models-recipes/model-walkthrough/preview-dataset.png)

오른쪽 레일에서 스키마 링크를 선택합니다. **[!UICONTROL 스키마 이름]** 아래에서 링크를 선택하면 새 탭에서 스키마가 열립니다.

![luma 웹 데이터 스키마 미리 보기](../images/models-recipes/model-walkthrough/preview-schema.png)

제공된 EDA(Explorative Data Analysis) 전자 필기장을 사용하여 데이터를 추가로 탐색할 수 있습니다. 이 전자 필기장을 사용하여 Luma 데이터의 패턴을 이해하고, 데이터의 온전성을 확인하며, 예측 성향 모델에 대한 관련 데이터를 요약할 수 있습니다. 탐색적 데이터 분석에 대한 자세한 내용은 [EDA 설명서](../jupyterlab/eda-notebook.md)를 참조하세요.

## Luma 성향 레시피 만들기 {#author-your-model}

[!DNL Data Science Workspace] 주기의 주 구성 요소에는 레시피 및 모델 작성이 포함됩니다. Luma 성향 모델은 고객이 Luma에서 제품을 구매하려는 성향이 높은지 여부에 대한 예측을 생성하도록 설계되었습니다.

Luma 성향 모델을 만들기 위해 레시피 빌더 템플릿을 사용합니다. 레시피는 특정 문제를 해결하기 위해 고안된 기계 학습 알고리즘과 논리를 포함하고 있어 모형의 기초가 된다. 더 중요한 것은 레서피를 통해 조직 전체에서 머신 러닝을 대중화할 수 있으므로 다른 사용자가 코드를 작성하지 않고도 다양한 사용 사례에 대한 모델에 액세스할 수 있다는 것입니다.

[JupyterLab Notebooks를 사용하여 모델 만들기](../jupyterlab/create-a-model.md) 자습서에 따라 후속 자습서에서 사용되는 Luma 성향 모델 레시피를 만듭니다.

## 외부 소스에서 레시피 가져오기 및 패키지(*선택 사항*)

Data Science Workspace에서 사용할 레시피를 가져와서 패키징하려면 소스 파일을 아카이브 파일로 패키징해야 합니다. [레시피에 소스 파일 패키지](./package-source-files-recipe.md) 자습서를 따르십시오. 이 자습서에서는 소스 파일을 레시피로 패키지화하는 방법을 보여 줍니다. 레시피는 Data Science Workspace으로 레시피를 가져오기 위한 사전 요구 사항 단계입니다. 자습서가 완료되면 Azure Container Registry에 도커 이미지가 해당 이미지 URL, 즉 아카이브 파일과 함께 제공됩니다.

이 보관 파일은 [UI 워크플로](./import-packaged-recipe-ui.md) 또는 [API 워크플로](./import-packaged-recipe-api.md)를 사용하여 레시피 가져오기 워크플로를 따라 Data Science Workspace에서 레시피를 만드는 데 사용할 수 있습니다.

## 모델 교육 및 평가 {#train-and-evaluate-your-model}

이제 데이터가 준비되고 레시피가 준비되었으므로 머신 러닝 모델을 추가로 만들고, 교육하고, 평가할 수 있습니다. 레시피 빌더를 사용하는 동안 모델을 레시피로 패키징하기 전에 이미 교육하고, 채점하고, 평가했어야 합니다.

데이터 과학 Workspace UI 및 API를 사용하면 레시피를 모델로 게시할 수 있습니다. 또한 하이퍼파라미터를 추가, 제거 및 변경하는 것과 같은 모델의 특정 측면을 더욱 세밀하게 조정할 수 있습니다.

### 모델 만들기

UI를 사용하여 모델을 만드는 방법에 대해 자세히 알아보려면 기차를 방문하여 데이터 과학 Workspace [UI 튜토리얼](./train-evaluate-model-ui.md) 또는 [API 튜토리얼](./train-evaluate-model-api.md)에서 모델을 평가하십시오. 이 자습서에서는 모델을 미세 조정하기 위해 하이퍼파라미터를 만들고, 교육하고, 업데이트하는 방법에 대한 예를 제공합니다.

>[!NOTE]
>
> 하이퍼매개 변수는 학습할 수 없으므로 교육 실행이 발생하기 전에 할당해야 합니다. 하이퍼파라미터를 조정하면 훈련된 모델의 정확도가 변경될 수 있습니다. 모델을 최적화하는 것은 반복적인 프로세스이기 때문에, 만족스러운 평가가 이루어지기 전에 다수의 교육 실행이 필요할 수 있다.

## 모델에 점수 매기기 {#score-a-model}

모델을 만들고 게시하는 다음 단계는 데이터 레이크 및 실시간 고객 프로필에서 점수를 매기고 통찰력을 소비하기 위해 모델을 운영하는 것입니다.

데이터 과학 Workspace의 점수는 입력 데이터를 기존의 훈련된 모델에 공급하여 달성할 수 있습니다. 그런 다음 채점 결과가 저장되고 지정된 출력 데이터 세트에 새 배치로 볼 수 있습니다.

모델에 점수를 매기는 방법을 알아보려면 모델 점수 [UI 튜토리얼](./score-model-ui.md) 또는 [API 튜토리얼](./score-model-api.md)을(를) 참조하세요.

## Publish a 점수 모델 as a service

데이터 과학 Workspace을 사용하면 훈련된 모델을 서비스로 게시할 수 있습니다. 이를 통해 조직 내의 사용자는 고유한 모델을 만들 필요 없이 데이터에 점수를 매길 수 있습니다.

모델을 서비스로 게시하는 방법에 대해 알아보려면 [UI 튜토리얼](./publish-model-service-ui.md) 또는 [API 튜토리얼](./publish-model-service-api.md)을(를) 방문하세요.

### 서비스에 대한 자동화된 교육 예약

모델을 서비스로 게시하면 머신 러닝 서비스에 대해 예약된 채점 및 교육 실행을 설정할 수 있습니다. 교육 및 채점 프로세스를 자동화하면 데이터 내 패턴을 준수하여 시간을 통해 서비스의 효율성을 유지 및 향상시키는 데 도움이 될 수 있습니다. 데이터 과학 Workspace UI에서 [모델 예약](./schedule-models-ui.md) 자습서를 방문하세요.

>[!NOTE]
>
> UI에서 자동화된 교육 및 점수에 대한 모델만 예약할 수 있습니다.

## 다음 단계 {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace]은(는) 데이터 예측 및 통찰력을 생성하기 위해 머신 러닝 모델을 만들고, 평가하고, 활용할 수 있는 도구와 리소스를 제공합니다. 머신 러닝 인사이트가 [!DNL Profile]을(를) 사용할 수 있는 데이터 세트로 수집되면 동일한 데이터도 [!DNL Profile] 레코드로 수집되어 [!DNL Adobe Experience Platform Segmentation Service]을(를) 사용하여 세그먼트화할 수 있습니다.

프로필 및 시계열 데이터가 수집되면 실시간 고객 프로필은 기존 데이터와 병합하고 유니온 보기를 업데이트하기 전에 스트리밍 세그먼테이션이라는 진행 중인 프로세스를 통해 해당 데이터를 세그먼트에서 포함하거나 제외하도록 자동으로 결정합니다. 따라서 고객이 브랜드와 상호 작용할 때 즉시 계산을 수행하고 고객에게 향상된 개인화된 경험을 제공하기 위한 결정을 내릴 수 있습니다.

[머신 러닝 인사이트를 통해 실시간 고객 프로필을 보강](./enrich-profile.md)하는 튜토리얼을 방문하여 머신 러닝 인사이트를 활용하는 방법에 대해 자세히 알아보십시오.
