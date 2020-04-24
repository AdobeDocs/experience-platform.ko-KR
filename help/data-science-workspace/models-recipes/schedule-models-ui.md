---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 모델 예약(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# 모델 예약(UI)

Adobe Experience Platform 데이터 과학 작업 영역을 사용하면 머신 러닝 서비스에서 예약된 점수 지정 및 트레이닝 실행을 설정할 수 있습니다. 트레이닝 및 점수 지정 프로세스를 자동화하면 데이터 내의 패턴을 유지하여 시간의 경과에 따라 서비스의 효율성을 유지 관리하고 개선하는 데 도움이 됩니다.

이 자습서는 서비스 갤러리를 통해 기존 서비스에 대한 교육 및 점수 지정 일정을 구성하는 단계를 *안내합니다*. 다음과 같은 주요 섹션으로 구분됩니다.

- [예약된 점수 구성](#configure-scheduled-scoring)
- [예약된 교육 구성](#configure-scheduled-training)

## 시작하기

이 튜토리얼을 완료하려면 Experience Platform에 액세스할 수 있어야 합니다. Experience Platform에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자에게 문의하십시오.

이 자습서에는 기존 서비스가 필요합니다. 액세스할 수 있는 서비스가 없는 경우 UI 튜토리얼의 서비스로 모델 [게시 서비스를 따라 서비스를 만들 수](./publish-model-service-ui.md) 있습니다.

## 예약된 점수 구성 {#configure-scheduled-scoring}

모델 점수 책정기는 예약 기반으로 자동화된 프로세스로 구성할 수 있습니다. 서비스가 만들어지면 아래 절차에 따라 점수 지정 일정을 구성하고 적용할 수 있습니다.

1. Adobe Experience Platform에서 **왼쪽** 탐색 열에 있는 서비스 탭을 클릭하여 서비스 갤러리에 *액세스합니다*. 점수 지정 실행을 예약하려는 서비스를 찾고 열기를 **클릭하여** 개요 *페이지를* 봅니다.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. 개요 페이지에는 서비스의 점수 정보가 표시됩니다. 점수 **지정** 일정을 구성하려면 예약 업데이트 링크를 클릭합니다.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. 점수 지정 일정에 대한 빈도, 시작 날짜, 종료 날짜, 입력 데이터 세트 및 출력 데이터 세트를 구성합니다. 구성에 만족하면 만들기를 클릭하여 **서비스의** 점수 지정 일정을 업데이트합니다.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. 업데이트된 점수 지정 일정은 서비스의 개요 *페이지에* 표시됩니다.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## 예약된 교육 구성 {#configure-scheduled-training}

서비스에서 예약된 교육 실행을 구성하면 시스템 학습 모델이 최신 데이터 패턴으로 업데이트됩니다. 예정된 트레이닝 실행이 완료될 때마다, 다음 예정된 트레이닝이 실행될 때까지 서비스에 전원을 공급하는 데 훈련 모델이 사용됩니다.

서비스가 만들어지면 아래 절차에 따라 교육 일정을 구성하고 적용할 수 있습니다.

1. Adobe Experience Platform에서 **왼쪽** 탐색 열에 있는 서비스 탭을 클릭하여 서비스 갤러리에 *액세스합니다*. 교육 실행을 예약할 서비스를 찾고 [열기] **를** 클릭하여 [개요] *페이지를* 봅니다.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. 개요 페이지에는 서비스의 교육 정보가 표시됩니다. [예약 **업데이트** ] 링크를 클릭하여 교육 일정을 구성합니다.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. 교육 일정에 사용되는 빈도, 시작 날짜, 종료 날짜 및 입력 데이터 세트를 구성합니다. 구성에 만족하면 만들기를 클릭하여 **서비스의** 교육 일정을 업데이트합니다.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. 업데이트된 교육 일정은 서비스의 개요 *페이지에 나와* 있습니다.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## 다음 단계

이 튜토리얼을 따라 서비스의 자동 트레이닝 및 점수 지정 실행을 성공적으로 예약하고 데이터 과학 작업 공간 자습서 UI 워크플로우를 완료했습니다. 아직 자습서를 [다시 시작한 적이 없는 경우 API 워크플로우에 따라 모델을 생성, 트레이닝, 점수 및 게시하십시오](./create-retails-sales-dataset.md) .
