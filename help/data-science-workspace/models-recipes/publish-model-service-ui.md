---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics;score a service
solution: Experience Platform
title: 모델을 서비스로 게시(UI)
topic: tutorial
type: Tutorial
description: Adobe Experience Platform 데이터 과학 작업 공간을 사용하면 교육되고 평가된 모델을 서비스로 게시하여 IMS 조직 내의 사용자가 자신의 모델을 만들지 않고도 데이터를 평가할 수 있습니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# 모델을 서비스로 게시(UI)

Adobe Experience Platform 데이터 과학 작업 공간을 사용하면 교육되고 평가된 모델을 서비스로 게시하여 IMS 조직 내의 사용자가 자신의 모델을 만들지 않고도 데이터를 평가할 수 있습니다.

## 시작하기

이 자습서를 완료하려면 액세스 권한이 있어야 합니다 [!DNL Experience Platform]. 에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자 [!DNL Experience Platform]에게 연락하여 진행하십시오.

이 자습서에서는 성공적인 트레이닝 실행을 가진 기존 모델이 필요합니다. 게시 가능한 모델이 없는 경우 계속하기 전에 UI [튜토리얼에서](./train-evaluate-model-ui.md) 트레이닝을 수행하고 모델을 평가하십시오.

Sensei Machine Learning API를 사용하여 모델을 게시하려면 [API 자습서를 참조하십시오](./publish-model-service-api.md).

## 모델 게시 {#publish-a-model}

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 모델]** 링크를 클릭하여 모든 기존 모델을 나열합니다. 서비스로 게시될 모델의 이름을 찾아 클릭합니다.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. 모델 **[!UICONTROL 개요]** 페이지 오른쪽 상단의 게시(Publish)를 클릭하여 서비스 생성 프로세스를 시작합니다.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. 원하는 서비스 이름을 입력하고, 필요에 따라 서비스 설명을 입력하고, 완료되면 **[!UICONTROL 다음]** 을 클릭합니다.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. 모델에 대해 실행된 모든 교육이 나열됩니다. 새 서비스는 선택한 교육 실행에서 트레이닝 및 점수 지정 구성을 상속받게 됩니다.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. 마침 **[!UICONTROL 을]** 클릭하여 서비스를 만들고 **[!UICONTROL 서비스 갤러리로]** 이동하여 새로 만든 서비스를 포함하여 사용 가능한 모든 서비스를 표시합니다.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## 서비스를 사용한 점수 {#access-a-service}

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 서비스]** 탭을 클릭하여 **[!UICONTROL 서비스 갤러리에 액세스합니다]**. 사용할 서비스를 찾아 **[!UICONTROL 점수를 클릭합니다]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. 점수 실행 시 적절한 입력 데이터 세트를 선택한 다음 **[!UICONTROL 다음을 클릭합니다]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. 점수 결과에 적합한 출력 데이터 세트를 선택한 다음 **[!UICONTROL 다음을 클릭합니다]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. 서비스가 생성되면 기본 점수 지정 구성이 상속됩니다. 이러한 구성을 검토하고 필요에 따라 값을 두 번 클릭하여 조정할 수 있습니다. 구성에 만족하면 **[!UICONTROL 마침을]** 클릭하여 점수 실행을 시작합니다.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. 서비스의 **개요** 페이지에 새로운 점수 지정 작업과 진행 상황에 대한 세부 정보가 표시됩니다. 작업이 완료되면 점수 지정 컨테이너 **[!UICONTROL 내]** 가장 최근 **** 헤더가업데이트됩니다.
   ![](../images/models-recipes/publish-model/score_pending.png)

## 다음 단계 {#next-steps}

이 튜토리얼을 따라 액세스 가능한 서비스로 모델을 성공적으로 게시하고 서비스 갤러리를 통해 새로운 서비스를 사용하여 데이터를 [!UICONTROL 획득한 것입니다]. 서비스에서 자동 트레이닝 및 점수 지정을 [예약하는 방법에 대해 알려면 다음 튜토리얼을 계속 사용하십시오](./schedule-models-ui.md).
