---
keywords: Experience Platform;모델 게시;데이터 과학 작업 공간;인기 있는 주제;서비스 점수
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 서비스로 모델 게시
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace를 사용하면 교육 및 평가 모델을 서비스로 게시하여 IMS 조직 내의 사용자가 모델을 직접 작성하지 않고도 데이터를 기록할 수 있습니다.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# 데이터 과학 작업 공간 UI에서 서비스로 모델 게시

Adobe Experience Platform Data Science Workspace를 사용하면 교육 및 평가 모델을 서비스로 게시하여 IMS 조직 내의 사용자가 모델을 직접 작성하지 않고도 데이터를 기록할 수 있습니다.

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]에서 IMS 조직에 액세스할 수 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

이 자습서에서는 성공적인 트레이닝 실행을 가진 기존 모델이 필요합니다. 게시 가능한 모델이 없는 경우 계속하기 전에 [UI](./train-evaluate-model-ui.md) 튜토리얼에서 모델 트레이닝을 수행하고 평가하십시오.

Sensei 기계 학습 API를 사용하여 모델을 게시하려면 [API 자습서](./publish-model-service-api.md)를 참조하십시오.

## 모델 {#publish-a-model} 게시

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 모델]** 링크를 클릭하여 모든 기존 모델을 나열합니다. 서비스로 게시할 모델의 이름을 찾아 클릭합니다.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. 모델 개요 페이지의 오른쪽 상단 근처에 있는 **[!UICONTROL 게시]**를 클릭하여 서비스 만들기 프로세스를 시작합니다.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. 원하는 서비스 이름을 입력하고 선택적으로 서비스 설명을 입력하고 완료되면 **[!UICONTROL 다음]**을 클릭합니다.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. 모델에 대한 모든 성공적인 교육 실행이 나열됩니다. 새 서비스는 선택한 교육 실행의 교육 및 채점 구성을 상속합니다.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. **[!UICONTROL 완료]**&#x200B;를 클릭하여 서비스를 만들고 **[!UICONTROL 서비스 갤러리]**로 리디렉션하여 새로 만든 서비스를 포함하여 사용 가능한 모든 서비스를 표시합니다.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## 서비스 {#access-a-service}를 사용한 점수

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 서비스]** 탭을 클릭하여 **[!UICONTROL 서비스 갤러리]**&#x200B;에 액세스합니다. 사용할 서비스를 찾고 **[!UICONTROL 점수]**를 클릭합니다.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. 점수 실행을 위해 적절한 입력 데이터 세트를 선택한 다음 **[!UICONTROL 다음]**을 클릭합니다.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. 점수 결과에 해당하는 출력 데이터 세트를 선택한 다음 **[!UICONTROL 다음]**을 클릭합니다.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. 서비스가 생성되면 기본 점수 지정 구성이 상속됩니다. 값을 두 번 클릭하여 이러한 구성을 검토하고 필요에 따라 조정할 수 있습니다. 구성이 만족스러우면 **[!UICONTROL 완료]**를 클릭하여 채점 실행을 시작합니다.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. 서비스의 **개요** 페이지에서 새 채점 작업과 진행 상태에 대한 세부 정보가 표시됩니다. 작업이 완료되면 **[!UICONTROL 채점]** 컨테이너 내 **[!UICONTROL 가장 최근]** 헤더가 업데이트됩니다.
   ![](../images/models-recipes/publish-model/score_pending.png)

## 다음 단계 {#next-steps}

이 자습서를 따라 액세스 가능한 서비스로 모델을 게시했으며 [!UICONTROL 서비스 갤러리]를 통해 새 서비스를 사용하여 데이터를 점수가 매겼습니다. 서비스](./schedule-models-ui.md)에서 자동 트레이닝 및 점수 지정 실행을 [예약할 수 있는 방법에 대해 알아보려면 다음 자습서를 계속 참조하십시오.
