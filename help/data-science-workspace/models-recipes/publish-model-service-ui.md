---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 모델을 서비스로 게시(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: af491361c5c3518e9bcc0af41a5aa79022229a2d

---


# 모델을 서비스로 게시(UI)

Adobe Experience Platform Data Science Workspace를 사용하면 교육되고 평가된 모델을 서비스로 게시하여 IMS 조직 내에서 사용자가 모델을 직접 만들지 않고도 데이터를 평가할 수 있습니다.

이 자습서에서는 모델을 서비스로 게시하고 서비스 갤러리를 통해 서비스를 사용하여 데이터를 평가하는 단계를 *안내합니다*. 다음과 같은 주요 섹션으로 구분됩니다.

- [모델 게시](#publish-a-model)
- [서비스를 사용한 점수](#access-a-service)

## 시작하기

이 튜토리얼을 완료하려면 Experience Platform에 액세스할 수 있어야 합니다. Experience Platform에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자에게 문의하십시오.

이 자습서에서는 성공적인 트레이닝 실행이 있는 기존 모델이 필요합니다. 게시 가능한 모델이 없는 경우 계속하기 전에 UI [자습서에서 모델 트레이닝을](./train-evaluate-model-ui.md) 따라 평가하십시오.

Sensei Machine Learning API를 사용하여 모델을 게시하려면 API [자습서를](./publish-model-service-api.md)참조하십시오.

## 모델 게시

1. Adobe Experience Platform에서 왼쪽 **탐색** 열에 있는 모델 링크를 클릭하여 모든 기존 모델을 나열합니다. 서비스로 게시할 모델의 이름을 찾아 클릭합니다.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
1. 모델 **개요** 페이지의 오른쪽 상단 근처에 있는 게시를 클릭하여 서비스 생성 프로세스를 시작합니다.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
1. 서비스에 원하는 이름을 입력하고 선택적으로 서비스 설명을 입력하고 완료되면 **다음을** 클릭합니다.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
1. 모델에 대한 모든 성공적인 교육 실행이 나열됩니다. 새 서비스는 선택한 교육 실행에서 트레이닝 및 점수 지정 구성을 상속받게 됩니다.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
1. 마침을 **클릭하여** 서비스를 만들고 서비스 갤러리로 리디렉션하여 **새로 만든 서비스를 포함하여 사용 가능한** 모든 서비스를 표시합니다.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## 서비스를 사용한 점수

1. Adobe Experience Platform에서 **왼쪽** 탐색 열에 있는 서비스 탭을 클릭하여 서비스 갤러리에 *액세스합니다*. 사용할 서비스를 찾고 점수를 **클릭합니다**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
1. 점수 실행을 위한 적절한 입력 데이터 세트를 선택한 다음 다음을 **클릭합니다**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
1. 점수 지정 결과에 적합한 출력 데이터 세트를 선택한 다음 다음을 **클릭합니다**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
1. 서비스가 생성되면, 이것은 기본 점수 지정 구성을 상속합니다. 이러한 구성을 검토하고 필요에 따라 값을 두 번 클릭하여 조정할 수 있습니다. 구성에 만족하면 마침을 클릭하여 **점수** 실행을 시작합니다.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
1. 서비스의 개요 *페이지에서* 새로운 점수 지정 작업과 진행 상태에 대한 세부 정보가 표시됩니다. 작업이 완료되면 최근 **점수** 채점 작업이 업데이트됩니다.
   ![](../images/models-recipes/publish-model/score_pending.png)

## 다음 단계

이 튜토리얼을 따라 액세스 가능한 서비스로 모델을 게시하고 서비스 갤러리를 통해 새로운 서비스를 사용하여 데이터를 *집계했습니다*. 다음 튜토리얼을 통해 서비스의 자동 트레이닝 및 점수 매기기를 [예약하는 방법을 살펴볼 수 있습니다](./schedule-models-ui.md).
