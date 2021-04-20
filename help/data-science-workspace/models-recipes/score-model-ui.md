---
keywords: Experience Platform;점수 모델;데이터 과학 작업 공간;인기 항목;ui;점수 실행;점수 지정 결과
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 모델 점수 지정
topic: tutorial
type: Tutorial
description: 'Adobe Experience Platform Data Science Workspace에서 입력 데이터를 기존 트레이닝된 모델에 제공함으로써 점수를 향상시킬 수 있습니다. 그러면 점수 지정 결과가 저장되고 지정된 출력 데이터 세트에 새로운 일괄 처리로 표시됩니다. '
translation-type: tm+mt
source-git-commit: 7feda18351061600b05dc7be8afbbfb9a0fa7ec1
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---


# 데이터 과학 작업 공간 UI에서 모델 점수 지정

Adobe Experience Platform [!DNL Data Science Workspace]에서 채점하는 방법은 입력 데이터를 기존 트레이닝된 모델에 제공함으로써 달성됩니다. 그러면 점수 지정 결과가 저장되고 지정된 출력 데이터 세트에 새로운 일괄 처리로 표시됩니다.

이 자습서에서는 [!DNL Data Science Workspace] 사용자 인터페이스에서 모델을 점화하는 데 필요한 단계를 보여 줍니다.

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]에서 IMS 조직에 액세스할 수 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

이 자습서에서는 교육을 받은 모델이 필요합니다. 교육된 모델이 없는 경우 계속하기 전에 [트레이닝을 따라 UI](./train-evaluate-model-ui.md) 튜토리얼에서 모델을 평가하고 평가하십시오.

## 새 점수 실행 만들기

이전에 완료되고 평가된 교육 실행의 최적화된 구성을 사용하여 점수 지정 실행이 생성됩니다. 모델에 대한 최적의 구성 집합은 일반적으로 교육 실행 평가 지표를 검토하여 결정됩니다.

점수를 매기려면 해당 구성을 사용할 수 있는 최적의 트레이닝 런을 찾아보십시오. 그런 다음 이름에 첨부된 하이퍼링크를 선택하여 원하는 교육 실행을 엽니다.

![교육 실행 선택](../images/models-recipes/score/select-run.png)

교육 실행 **[!UICONTROL Evaluation]** 탭에서 화면 오른쪽 상단에 있는 **[!UICONTROL Score]**&#x200B;을 선택합니다. 새로운 점수 지정 워크플로우가 시작됩니다.

![](../images/models-recipes/score/training_run_overview.png)

입력 점수 데이터 세트를 선택하고 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/models-recipes/score/scoring_input.png)

출력 점수 데이터 세트를 선택합니다. 이것은 채점 결과가 저장되는 전용 출력 데이터 집합입니다. 선택을 확인하고 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/models-recipes/score/scoring_results.png)

워크플로우의 마지막 단계에서 점수 실행을 구성하라는 메시지가 표시됩니다. 이러한 구성은 점수부여 실행에 대해 모델이 사용합니다.
모델을 생성하는 동안 설정한 상속된 매개변수를 제거할 수 없습니다. 항목을 마우스로 가리키면서 값을 두 번 클릭하거나 되돌리기 아이콘을 선택하여 상속되지 않은 매개 변수를 편집하거나 되돌릴 수 있습니다.

![configuration](../images/models-recipes/score/configuration.png)

점수 지정 구성을 검토 및 확인하고 **[!UICONTROL Finish]**&#x200B;을 선택하여 점수부여 실행을 만들고 실행합니다. **[!UICONTROL Scoring Runs]** 탭으로 이동되고 **[!UICONTROL Pending]** 상태로 새 점수 실행이 표시됩니다.

![점수 실행 탭](../images/models-recipes/score/scoring_runs_tab.png)

점수 지정 실행은 다음 상태 중 하나로 표시될 수 있습니다.
- 보류 중
- 완료
- 실패
- 실행 중

상태는 자동으로 업데이트됩니다. 상태가 **[!UICONTROL Complete]** 또는 **[!UICONTROL Failed]**&#x200B;인 경우 다음 단계로 진행합니다.

## 채점 결과 보기

점수 지정 결과를 보려면 교육 실행을 선택하여 시작합니다.

![교육 실행 선택](../images/models-recipes/score/select-run.png)

**[!UICONTROL Evaluation]** 페이지가 실행되는 교육 실행 페이지로 리디렉션됩니다. 교육 실행 평가 페이지의 상단 근처에 있는 **[!UICONTROL Scoring Runs]** 탭을 선택하여 기존 점수 실행 목록을 봅니다.

![평가 페이지](../images/models-recipes/score/view_scoring_runs.png)

다음으로, 실행 세부 사항을 보려면 점수 실행을 선택합니다.

![세부 정보 실행](../images/models-recipes/score/view_details.png)

선택한 점수 실행 상태가 &quot;완료&quot; 또는 &quot;실패&quot;인 경우 **[!UICONTROL View Activity Logs]** 링크를 사용할 수 있습니다. 점수 실행이 실패하는 경우 실행 로그는 실패 이유를 확인하는 데 유용한 정보를 제공할 수 있습니다. 실행 로그를 다운로드하려면 **[!UICONTROL View Activity Logs]**&#x200B;을 선택합니다.

![보기 로그 선택](../images/models-recipes/score/view_logs.png)

**[!UICONTROL View activity logs]** 팝업 창이 나타납니다. 연관된 로그를 자동으로 다운로드할 URL을 선택합니다.

![](../images/models-recipes/score/activity_logs.png)

**[!UICONTROL Preview scoring results dataset]**&#x200B;을 선택하여 채점 결과를 볼 수도 있습니다.

![미리 보기 결과 선택](../images/models-recipes/score/view_results.png)

출력 데이터 세트의 미리 보기가 제공됩니다.

![결과 미리 보기](../images/models-recipes/score/preview_results.png)

전체 채점 결과 세트를 보려면 오른쪽 열에 있는 **[!UICONTROL Scoring Results Dataset]** 링크를 선택합니다.

## 다음 단계

이 자습서에서는 [!DNL Data Science Workspace]에서 훈련된 모델을 사용하여 데이터를 점수 매기는 단계를 안내합니다. 컴퓨터 학습 서비스에 손쉽게 액세스할 수 있도록 조직 내의 사용자가 데이터를 기록하도록 하려면 [UI](./publish-model-service-ui.md)에서 모델을 서비스로 게시하기 튜토리얼을 따르십시오.
