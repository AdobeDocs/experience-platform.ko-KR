---
keywords: Experience Platform;모델 예약;데이터 과학 작업 공간;인기 있는 주제;점수 지정;일정 교육
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 모델 예약
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace를 사용하면 머신 러닝 서비스에서 예약된 점수 지정 및 트레이닝 실행을 설정할 수 있습니다. 트레이닝 및 채점 과정을 자동화하면 데이터 내의 패턴을 유지하여 시간 경과에 따라 서비스의 효율성을 유지 관리하고 개선하는 데 도움이 됩니다.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# 데이터 과학 작업 공간 UI에서 모델 예약

Adobe Experience Platform [!DNL Data Science Workspace]에서는 기계 학습 서비스에서 예약된 점수 지정 및 교육 실행을 설정할 수 있습니다. 트레이닝 및 채점 과정을 자동화하면 데이터 내의 패턴을 유지하여 시간 경과에 따라 서비스의 효율성을 유지 관리하고 개선하는 데 도움이 됩니다.

이 자습서는 [!UICONTROL 서비스 갤러리]를 통해 기존 서비스에 대한 교육 및 채점 일정을 구성하는 단계를 안내합니다. 다음과 같은 주요 섹션으로 구분됩니다.

- [예약된 점수 구성](#configure-scheduled-scoring)
- [예약된 교육 구성](#configure-scheduled-training)

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]에서 IMS 조직에 액세스할 수 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

이 자습서를 사용하려면 기존 서비스가 필요합니다. 액세스할 수 있는 서비스가 없는 경우 UI](./publish-model-service-ui.md) 튜토리얼의 [모델을 서비스로 게시합니다.

## 예약된 점수 {#configure-scheduled-scoring} 구성

모델 채점 방식을 예약 기반으로 자동화된 프로세스로 구성할 수 있습니다. 서비스가 생성되면 아래 절차에 따라 점수 지정 일정을 구성하고 적용할 수 있습니다.

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 서비스]** 탭을 클릭하여 **[!DNL Service Gallery]**&#x200B;에 액세스합니다. 점수 지정 실행을 예약하려는 서비스를 찾고 **[!UICONTROL 열기]**&#x200B;를 클릭하여 **개요** 페이지를 봅니다.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. 개요 페이지에는 서비스의 점수 정보가 표시됩니다. 점수 지정 일정을 구성하려면 **[!UICONTROL 예약 업데이트]** 링크를 클릭합니다.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. 점수 지정 일정에 대한 빈도, 시작 날짜, 종료 날짜, 입력 데이터 세트 및 출력 데이터 세트를 구성합니다. 구성에 만족하면 **[!UICONTROL 만들기]**를 클릭하여 서비스의 점수 지정 일정을 업데이트합니다.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. 업데이트된 점수 지정 일정은 서비스의 **개요** 페이지에 표시됩니다.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## 예약된 교육 {#configure-scheduled-training} 구성

서비스에서 예약된 교육을 구성하여 머신 러닝 모델이 최신 데이터 패턴으로 업데이트됩니다. 예약된 트레이닝 실행이 완료되면 예정된 다음 트레이닝이 실행될 때까지 서비스에 전원을 공급하는 데 지정된 모델을 사용합니다.

서비스가 만들어지면 아래 절차에 따라 교육 일정을 구성하고 적용할 수 있습니다.

1. Adobe Experience Platform에서 왼쪽 탐색 열에 있는 **[!UICONTROL 서비스]** 탭을 클릭하여 **[!UICONTROL 서비스 갤러리]**&#x200B;에 액세스합니다. 교육 실행을 예약할 서비스를 찾고 **[!UICONTROL 열기]**&#x200B;를 클릭하여 **개요** 페이지를 봅니다.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. 개요 페이지에는 서비스의 교육 정보가 표시됩니다. 교육 일정을 구성하려면 **[!UICONTROL 예약 업데이트]** 링크를 클릭합니다.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. 교육 일정에 사용되는 빈도, 시작 날짜, 종료 날짜 및 입력 데이터 세트를 구성합니다. 구성에 만족하면 **[!UICONTROL 만들기]**를 클릭하여 서비스의 교육 일정을 업데이트합니다.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. 업데이트된 교육 일정은 서비스의 **개요** 페이지에 표시됩니다.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## 다음 단계

이 튜토리얼을 따라 서비스에서 자동 트레이닝 및 점수 지정을 성공적으로 예약하고 [!DNL Data Science Workspace] 자습서 UI 작업 과정을 완료했습니다. 아직 시작하지 않은 경우 [튜토리얼](./create-retails-sales-dataset.md)을 다시 시작하고 API 작업 과정에 따라 모델을 만들고, 교육하고, 점수를 매기고, 게시할 수 있습니다.
