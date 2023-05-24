---
keywords: Experience Platform;모델 예약;Data Science Workspace;인기 주제;채점 예약;교육 예약
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 모델 예약
type: Tutorial
description: Adobe Experience Platform 데이터 과학 작업 영역을 사용하면 머신 러닝 서비스에서 예약된 채점 및 교육 실행을 설정할 수 있습니다. 교육 및 채점 프로세스를 자동화하면 데이터 내의 패턴을 따라가며 시간이 지남에 따라 서비스의 효율성을 유지 및 향상시키는 데 도움이 될 수 있습니다.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 데이터 과학 작업 공간 UI에서 모델 예약

Adobe Experience Platform [!DNL Data Science Workspace] 머신 러닝 서비스에서 예약된 채점 및 교육 실행을 설정할 수 있습니다. 교육 및 채점 프로세스를 자동화하면 데이터 내 패턴을 준수하여 시간을 통해 서비스의 효율성을 유지 및 향상시키는 데 도움이 될 수 있습니다.

이 자습서에서는 다음을 통해 기존 서비스에 대한 교육 및 채점 일정을 구성하는 단계를 안내합니다. [!UICONTROL 서비스 갤러리]. 이 섹션은 다음과 같은 기본 섹션으로 분류됩니다.

- [예약된 채점 구성](#configure-scheduled-scoring)
- [예약된 교육 구성](#configure-scheduled-training)

## 시작하기

이 자습서를 완료하려면 다음에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]. 에서 조직에 대한 액세스 권한이 없는 경우 [!DNL Experience Platform]을(를) 계속하려면 시스템 관리자에게 문의하십시오.

이 자습서에는 기존 서비스가 필요합니다. 작업할 수 있는 액세스 가능한 서비스가 없는 경우 다음 자습서에 따라 서비스를 만들 수 있습니다. [모델을 서비스로 게시](./publish-model-service-ui.md).

## 예약된 채점 구성 {#configure-scheduled-scoring}

모델 채점은 일정에 따라 자동화된 프로세스로 구성할 수 있습니다. 서비스가 생성되면 아래 단계에 따라 채점 일정을 구성하고 적용할 수 있습니다.

Adobe Experience Platform에서 **[!UICONTROL 서비스]** 왼쪽 탐색 열에 있는 탭에 액세스하여 **[!DNL Service Gallery]**. 채점 실행을 예약할 서비스를 찾아 선택합니다. **[!UICONTROL 열기]** 보기 **[!UICONTROL 개요]** 페이지를 가리키도록 업데이트하는 중입니다.

![](../images/models-recipes/schedule/select_service.png)

개요 페이지에는 서비스의 점수 정보가 표시됩니다. 다음 항목 선택 **[!UICONTROL 일정 업데이트]** 채점 일정을 구성하는 링크.

![](../images/models-recipes/schedule/update_scoring.png)

채점 일정에 대한 빈도, 시작 날짜, 종료 날짜, 입력 데이터 세트 및 출력 데이터 세트를 구성합니다. 구성이 만족스러우면 다음을 선택합니다. **[!UICONTROL 만들기]** 서비스의 채점 일정을 업데이트합니다.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

업데이트된 채점 일정이 서비스에 표시됩니다. **[!UICONTROL 개요]** 페이지를 가리키도록 업데이트하는 중입니다.

![](../images/models-recipes/schedule/scoring_set.png)

## 예약된 교육 구성 {#configure-scheduled-training}

서비스에서 예약된 교육 실행을 구성하면 머신 러닝 모델이 최신 데이터 패턴으로 업데이트됩니다. 예약된 교육 실행이 완료될 때마다, 그 결과로 얻은 교육 모델은 다음 예약된 교육 실행이 완료될 때까지 서비스를 구동하는 데 사용됩니다.

서비스가 생성되면 아래 단계에 따라 교육 일정을 구성하고 적용할 수 있습니다.

Adobe Experience Platform에서 **[!UICONTROL 서비스]** 왼쪽 탐색 열에 있는 탭에 액세스하여 **[!UICONTROL 서비스 갤러리]**. 교육 실행을 예약할 서비스를 찾아 선택합니다. **[!UICONTROL 열기]** 보기 **[!UICONTROL 개요]** 페이지를 가리키도록 업데이트하는 중입니다.

![](../images/models-recipes/schedule/select_service.png)

개요 페이지에는 서비스의 교육 정보가 표시됩니다. 다음 항목 선택 **[!UICONTROL 일정 업데이트]** 교육 일정을 구성하는 링크입니다.

![](../images/models-recipes/schedule/update_training.png)

교육 일정에 사용되는 빈도, 시작 날짜, 종료 날짜 및 입력 데이터 세트를 구성합니다. 구성이 만족스러우면 다음을 선택합니다. **[!UICONTROL 만들기]** 서비스의 교육 일정을 업데이트합니다.

![](../images/models-recipes/schedule/set_training_schedule.png)

업데이트된 교육 일정은 서비스에 표시됩니다. **[!UICONTROL 개요]** 페이지를 가리키도록 업데이트하는 중입니다.

![](../images/models-recipes/schedule/training_set.png)

## 다음 단계

이 자습서를 따라 서비스에서 자동화된 교육 및 채점 실행을 예약하고 다음을 완료했습니다. [!DNL Data Science Workspace] 튜토리얼 UI 워크플로. 아직 수행하지 않았다면 다음을 고려하십시오. [튜토리얼 다시 시작](./create-retails-sales-dataset.md) API 워크플로에 따라 모델을 만들고, 교육하고, 평가하고, 게시합니다.
