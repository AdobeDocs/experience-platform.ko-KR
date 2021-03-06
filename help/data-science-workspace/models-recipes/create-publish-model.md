---
keywords: Experience Platform;기계 학습 모델;데이터 과학 작업 공간;인기 있는 주제;모델 작성 및 게시
solution: Experience Platform
title: 기계 학습 모델 만들기 및 게시
topic-legacy: tutorial
type: Tutorial
description: 다음 안내서에서는 기계 학습 모델을 만들고 게시하는 데 필요한 단계를 설명합니다.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: ff8a3612f34d6547577564ba40261052cd78ef01
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---


# 기계 학습 모델 만들기 및 게시

다음 안내서에서는 기계 학습 모델을 만들고 게시하는 데 필요한 단계를 설명합니다. 각 섹션에는 수행할 작업에 대한 설명 및 UI 및 API 설명서에 대한 링크를 포함하여 설명된 단계를 설명합니다.

## 시작하기

이 자습서를 시작하기 전에 다음 전제 조건이 있어야 합니다.

- 액세스 권한 [!DNL Adobe Experience Platform]. 에서 IMS 조직에 액세스할 수 없는 경우 [!DNL Experience Platform]을(를) 계속하기 전에 시스템 관리자에게 문의하십시오.

- 모든 데이터 과학 작업 공간 자습서에서는 Luma 성향 모델을 사용합니다. 따라서 다음을 수행해야 합니다. [Luma 속성 모델 스키마 및 데이터 세트](./create-luma-data.md).

### 데이터 탐색 및 스키마 이해

에 로그인합니다. [Adobe Experience Platform](https://platform.adobe.com/) 을(를) 선택합니다. **[!UICONTROL 데이터 세트]** 기존 데이터 세트를 모두 나열하고 탐색할 데이터 세트를 선택합니다. 이 경우 **Luma 웹 데이터** 데이터 세트.

![luma 웹 데이터 세트 선택](../images/models-recipes/model-walkthrough/luma-dataset.png)

데이터 집합 활동 페이지가 열리고 데이터 집합에 대한 정보가 나열됩니다. 선택할 수 있습니다 **[!UICONTROL 데이터 집합 미리 보기]** 샘플 레코드를 검사할 오른쪽 상단 근처에 있습니다. 선택한 데이터 세트에 대한 스키마를 볼 수도 있습니다.

![Luma 웹 데이터 미리 보기](../images/models-recipes/model-walkthrough/preview-dataset.png)

오른쪽 레일에서 스키마 링크를 선택합니다. 아래에 있는 링크를 선택하는 팝업 창이 나타납니다 **[!UICONTROL 스키마 이름]** 새 탭에서 스키마를 엽니다.

![luma 웹 데이터 스키마 미리 보기](../images/models-recipes/model-walkthrough/preview-schema.png)

제공된 EDA(Quetical Data Analysis) 전자 필기장을 사용하여 데이터를 추가로 탐색할 수 있습니다. 이 노트북은 Luma 데이터의 패턴을 이해하고, 데이터 안전성을 확인하고, 예측 성향 모델에 대한 관련 데이터를 요약하는 데 사용할 수 있습니다. 예비 데이터 분석에 대해 자세히 알아보려면 [EDA 설명서](../jupyterlab/eda-notebook.md).

## Luma 성향 레서피 만들기 {#author-your-model}

의 기본 구성 요소 [!DNL Data Science Workspace] 라이프사이클에는 레서피 및 모델 작성이 포함됩니다. Luma 성향 모델은 고객이 Luma에서 제품을 구매할 가능성이 높은지 여부에 대한 예측을 생성하도록 설계되었습니다.

Luma 성향 모델을 만들기 위해 레서피 빌더 템플릿이 사용됩니다. 레서피는 특정 문제를 해결하기 위해 고안된 기계 학습 알고리즘과 논리를 포함하므로 모델의 기반입니다. 더 중요한 것은 레서피 를 사용하면 조직 전체에서 기계 학습을 대중화할 수 있으므로 다른 사용자가 코드를 작성하지 않고도 다양한 사용 사례에 대한 모델에 액세스할 수 있습니다.

다음을 수행합니다 [JupiterLab 노트북을 사용하여 모델 생성](../jupyterlab/create-a-model.md) 후속 자습서에서 사용되는 Luma 성향 모델 레서피를 만드는 자습서입니다.

## 외부 출처의 배합식을 임포트하고 패키징합니다(*옵션*)

Data Science Workspace에서 사용할 레서피를 가져와서 패키지하려면 소스 파일을 아카이브 파일로 패키지해야 합니다. 다음을 수행합니다 [조리법에 소스 파일 패키지](./package-source-files-recipe.md) 자습서입니다. 이 자습서에서는 소스 파일을 레서피로 패키지하는 방법을 보여 줍니다. 이 단계는 레서피를 Data Science Workspace로 가져오기 위한 사전 요구 단계입니다. 자습서가 완료되면 Azure 컨테이너 레지스트리에 해당 이미지 URL과 보관 파일을 함께 제공합니다.

이 아카이브 파일은 [UI 워크플로우](./import-packaged-recipe-ui.md) 또는 [API 워크플로우](./import-packaged-recipe-api.md).

## 모델 교육 및 평가 {#train-and-evaluate-your-model}

이제 데이터가 준비되고 레서피가 준비되었으므로 기계 학습 모델을 더 만들고, 교육하고, 평가할 수 있습니다. 레서피 빌더를 사용하는 동안 레서피에 패키지하기 전에 이미 교육을 하고, 점수를 매기고, 평가해야 합니다.

Data Science Workspace UI 및 API를 사용하여 레서피를 모델로 게시할 수 있습니다. 또한 하이퍼매개 변수 추가, 제거 및 변경과 같은 모델의 특정 측면을 세밀하게 조정할 수 있습니다.

### 모델 만들기

UI를 사용하여 모델을 만드는 방법에 대해 자세히 알아보려면 기차를 방문하여 데이터 과학 작업 영역에서 모델을 평가하십시오 [UI 자습서](./train-evaluate-model-ui.md) 또는 [API 자습서](./train-evaluate-model-api.md). 이 자습서에서는 하이퍼매개 변수를 만들고, 교육하고, 업데이트하여 모델을 세밀하게 조정하는 방법에 대한 예를 제공합니다.

>[!NOTE]
>
> 하이퍼매개 변수는 알 수 없으므로, 훈련 실행 전에 할당해야 합니다. 하이퍼매개 변수를 조정하면 숙련된 모델의 정확도가 변경될 수 있습니다. 모델 최적화는 반복적인 프로세스이므로 만족할만한 평가를 수행하기 전에 여러 개의 교육 실행이 필요할 수 있습니다.

## 모델 점수 책정 {#score-a-model}

모델을 만들고 게시하는 다음 단계는 데이터 레이크 및 실시간 고객 프로필에서 통찰력을 얻고 소비하기 위해 모델을 운영 화하는 것입니다.

데이터 과학 작업 공간에서 채점하는 방법은 입력 데이터를 기존의 숙련된 모델에 공급하면 됩니다. 그러면 점수 결과가 저장되고 지정된 출력 데이터 세트에 새 배치로 표시됩니다.

모델의 점수를 매기는 방법을 배우려면 모델 점수를 참조하십시오 [UI 자습서](./score-model-ui.md) 또는 [API 자습서](./score-model-api.md).

## 점수를 매긴 모델을 서비스로 게시

Data Science Workspace를 사용하면 훈련된 모델을 서비스로 게시할 수 있습니다. 이를 통해 IMS 조직 내의 사용자는 자체 모델을 만들지 않고도 데이터에 점수를 매길 수 있습니다.

모델을 서비스로 게시하는 방법에 대해 알아보려면 [UI 자습서](./publish-model-service-ui.md) 또는 [API 자습서](./publish-model-service-api.md).

### 서비스에 대한 자동 교육 예약

모델을 서비스로 게시하면 기계 학습 서비스에 대해 예약된 점수 및 교육 실행을 설정할 수 있습니다. 교육 및 점수 책정 프로세스를 자동화하면 데이터 내의 패턴을 유지하여 시간 경과에 따른 서비스 효율성을 유지 관리하고 향상시키는 데 도움이 됩니다. 다음 방문 [데이터 과학 작업 공간 UI에서 모델 예약](./schedule-models-ui.md) 자습서입니다.

>[!NOTE]
>
> UI에서 자동화된 교육 및 점수 책정 모델만 예약할 수 있습니다.

## 다음 단계 {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] 데이터 예측 및 인사이트를 생성하는 기계 학습 모델을 생성, 평가 및 활용할 수 있는 도구와 리소스를 제공합니다. 머신 러닝 인사이트를 [!DNL Profile]-활성화된 데이터 세트로서 동일한 데이터가 수집됩니다. [!DNL Profile] 다음으로 세그먼트화할 수 있는 레코드 [!DNL Adobe Experience Platform Segmentation Service].

프로필 및 시계열 데이터가 수집되면 실시간 고객 프로필은 기존 데이터와 병합하고 통합 보기를 업데이트하기 전에 스트리밍 세그먼테이션이라는 진행 중인 프로세스를 통해 해당 데이터를 세그먼트에서 포함 또는 제외하도록 자동으로 결정합니다. 결과적으로 고객이 브랜드와 상호 작용할 때 즉시 계산을 수행하고 개인화된 향상된 경험을 고객에게 제공할 수 있습니다.

다음 기간 동안 자습서를 확인하십시오 [머신 러닝 인사이트로 실시간 고객 프로필 보강](./enrich-profile.md) 기계 학습 인사이트를 활용하는 방법에 대한 자세한 내용을 살펴보십시오.
