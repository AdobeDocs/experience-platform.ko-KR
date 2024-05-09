---
keywords: Experience Platform;모델 게시;Data Science Workspace;인기 있는 주제;서비스 점수 매기기
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 모델을 서비스로 게시
type: Tutorial
description: Adobe Experience Platform Data Science Workspace 를 사용하면 교육되고 평가된 모델을 Service로 게시할 수 있으므로 조직 내의 사용자가 자체 모델을 만들 필요 없이 데이터에 점수를 매길 수 있습니다.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: d6a4b149b911cd6e7dbbd6c1289fce64be76b506
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# 데이터 과학 작업 공간 UI에서 모델을 서비스로 게시 {#publish-a-model-as-a-service}

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="Model as a Service 게시"
>abstract=""

Adobe Experience Platform Data Science Workspace 를 사용하면 교육되고 평가된 모델을 Service로 게시할 수 있으므로 조직 내의 사용자가 자체 모델을 만들 필요 없이 데이터에 점수를 매길 수 있습니다.

## 시작하기

이 자습서를 완료하려면 다음에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]. 에서 조직에 대한 액세스 권한이 없는 경우 [!DNL Experience Platform]을(를) 계속하려면 시스템 관리자에게 문의하십시오.

이 자습서에는 교육 실행이 정상적으로 수행된 기존 모델이 필요합니다. 게시 가능한 모델이 없는 경우 [UI에서 모델 교육 및 평가](./train-evaluate-model-ui.md) 튜토리얼을 참조하십시오.

Sensei 머신 러닝 API를 사용하여 모델을 게시하려면 다음을 참조하십시오. [API 튜토리얼](./publish-model-service-api.md).

## 모델 게시 {#publish-a-model}

Adobe Experience Platform에서 **[!UICONTROL 모델]** 왼쪽 탐색 열에 있는 을(를) 선택한 다음 **[!UICONTROL 찾아보기]** 탭을 사용하여 기존 모델을 모두 나열합니다. 서비스로 게시하려는 모델의 이름을 선택합니다.

![](../images/models-recipes/publish-model/browse_model.png)

선택 **[!UICONTROL 게시]** 모델 개요 페이지의 오른쪽 상단 근처에서 서비스 만들기 프로세스를 시작합니다.

![](../images/models-recipes/publish-model/view_training.png)

원하는 서비스 이름을 입력하고 필요에 따라 서비스 설명을 입력한 후 다음을 선택합니다. **[!UICONTROL 다음]** 완료 시.

![](../images/models-recipes/publish-model/configure_training.png)

모델에 대한 모든 성공적인 교육 실행이 나열됩니다. 새 서비스는 선택한 교육 실행에서 교육 및 채점 구성을 상속합니다.

![](../images/models-recipes/publish-model/select_training_run.png)

선택 **[!UICONTROL 완료]** 서비스를 만들고 로 리디렉션하려면 **[!UICONTROL 서비스 갤러리]** 새로 생성된 서비스를 포함하여 사용 가능한 모든 서비스를 표시합니다.

![](../images/models-recipes/publish-model/service_gallery.png)

## 서비스를 사용한 점수 {#access-a-service}

Adobe Experience Platform에서 **[!UICONTROL 서비스]** 왼쪽 탐색 열에 있는 탭에 액세스하여 **[!UICONTROL 서비스 갤러리]**. 사용할 서비스를 찾은 다음 선택합니다 **[!UICONTROL 열기]**.

![](../images/models-recipes/publish-model/open_service.png)

서비스 개요 페이지에서 다음을 선택합니다. **[!UICONTROL 점수]**.

![](../images/models-recipes/publish-model/score_service.png)

채점 실행에 적합한 입력 데이터 세트를 선택한 다음 를 선택합니다 **[!UICONTROL 다음]**. 채점 데이터 세트에 대해 동일한 단계를 수행해야 합니다. 입력 및 출력 데이터 세트를 선택하면 구성을 업데이트할 수 있습니다.

![](../images/models-recipes/publish-model/select_datasets.png)

서비스가 만들어지면 기본 채점 구성을 상속합니다. 이러한 구성을 검토하고 값을 두 번 클릭하여 필요에 따라 조정할 수 있습니다. 구성이 만족스러우면 다음을 선택합니다. **[!UICONTROL 완료]** 채점 실행을 시작합니다.

![](../images/models-recipes/publish-model/scoring_configs.png)

서비스의 **개요** 새 채점 작업 및 진행 상황에 대한 세부 정보가 표시됩니다. 작업이 완료되면 **[!UICONTROL 가장 최근]** 헤더 내 **[!UICONTROL 채점]** 컨테이너가 업데이트되었습니다.

![](../images/models-recipes/publish-model/pending_scoring.png)

## 다음 단계 {#next-steps}

이 자습서를 따라 모델을 액세스 가능한 서비스로 게시하고 를 통해 새 서비스를 사용하여 데이터에 점수를 매겼습니다 [!UICONTROL 서비스 갤러리]. 다음 튜토리얼을 계속 진행하여 다음과 같은 작업을 수행하는 방법에 대해 알아보십시오 [서비스에서 자동화된 교육 및 채점 실행 예약](./schedule-models-ui.md).
