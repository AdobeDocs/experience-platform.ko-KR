---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 모델 점수 지정(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# 모델 점수 지정(UI)

Adobe Experience Platform 데이터 과학 작업 공간의 채점이란 입력 데이터를 기존의 트레이닝된 모델에 제공함으로써 달성되는 것을 의미합니다. 그러면 점수 지정 결과가 저장되고 지정된 출력 데이터 세트에 새로운 일괄 처리로 표시됩니다.

이 자습서는 데이터 과학 작업 공간 사용자 인터페이스에서 모델을 점화하는 데 필요한 단계를 보여 줍니다.

## 시작하기

이 튜토리얼을 완료하려면 경험 플랫폼에 대한 액세스 권한이 있어야 합니다. Experience Platform에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자에게 문의하십시오.

이 자습서에서는 교육을 받은 모델이 필요합니다. 트레이닝된 모델이 없는 경우 [트레이닝을 따라 UI](./train-evaluate-model-ui.md) 튜토리얼에서 모델을 평가하는 후 계속합니다.

## 새로운 점수 실행 만들기

점수 실행은 이전에 완료되고 평가된 교육 실행의 최적화된 구성을 사용하여 만들어집니다. 모델에 대한 최적 구성 세트는 일반적으로 교육 실행 평가 지표를 검토하여 결정됩니다.

1. 점수를 매기는 데 해당 구성을 사용할 수 있는 최적의 트레이닝 실행을 찾습니다. 해당 이름을 클릭하여 원하는 교육 실행을 엽니다.

2. [교육 실행] **[!UICONTROL Evaluation]** 탭에서 화면 오른쪽 위에 있는 **[!UICONTROL Score]** 단추를 클릭합니다. 그러면 새로운 점수 *실행 워크플로우가* 시작됩니다.
   ![](../images/models-recipes/score/training_run_overview.png)

3. 입력 점수 데이터 세트를 선택하고 을 클릭합니다 **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. 출력 점수 데이터 세트를 선택합니다. 이것은 점수 결과가 저장되는 전용 출력 데이터 집합입니다. 선택을 확인하고 클릭합니다 **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. 워크플로우의 마지막 단계에서 점수 실행을 구성하라는 메시지가 표시됩니다. 이러한 구성은 검증 실행에 대해 모델에서 사용됩니다.
모델 생성 중에 설정된 상속된 매개변수를 제거할 수 없습니다. 항목을 마우스로 가리키면서 값을 두 번 클릭하거나 되돌리기 아이콘을 클릭하여 상속되지 않은 매개 변수를 편집하거나 되돌릴 수 있습니다.
   ![](../images/models-recipes/score/configuration.png)
점수 지정 구성을 검토 및 확인하고 클릭하여 점수 실행 **[!UICONTROL Finish]** 을 만들고 실행합니다. 점수 지정 실행 ** 탭으로 이동되고 새 점수 실행 상태가 표시됩니다.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
점수 실행 시 다음 네 가지 상태 중 하나가 표시됩니다. 보류 중, 완료, 실패 또는 실행 중 중, 자동으로 업데이트됩니다. 상태가 &quot;완료&quot; 또는 &quot;실패&quot;인 경우 다음 단계로 진행합니다.

## 점수 지정 결과 보기

1. 점수 책정기에 사용된 교육 실행을 찾은 다음 이름을 클릭하여 해당 **[!UICONTROL Evaluation]** 페이지를 확인합니다.

2. 교육 실행 평가 페이지의 맨 위에 있는 **[!UICONTROL Scoring Runs]** 탭을 클릭하여 기존 점수 실행 목록을 봅니다. 오른쪽 열에서 점수 목록을 클릭하여 세부 사항을 확인합니다.
   ![](../images/models-recipes/score/view_details.png)

3. 선택한 점수 실행 상태가 &quot;완료&quot; 또는 &quot;실패&quot;인 경우 오른쪽 열에 있는 **[!UICONTROL View Activity Logs]** 링크가 활성화됩니다. 실행 로그를 보거나 다운로드하려면 링크를 클릭합니다. 점수 실행이 실패한 경우 실행 로그는 실패 이유를 확인하는 데 유용한 정보를 제공할 수 있습니다.
   ![](../images/models-recipes/score/activity_logs.png)

4. 오른쪽 열에 있는 **[!UICONTROL Preview Scoring Results Dataset]** 링크를 클릭합니다. 점수 실행 시 출력 데이터 세트에 대한 미리 보기를 확인할 수 있습니다.
   ![](../images/models-recipes/score/preview_results.png)

5. 전체 점수 지정 결과를 보려면 오른쪽 열에 있는 **[!UICONTROL Scoring Results Dataset]** 링크를 클릭합니다.

## 다음 단계

이 자습서에서는 데이터 과학 작업 공간에서 교육된 모델을 사용하여 데이터를 점수 매기는 단계를 안내합니다. UI에서 [서비스로 모델을](./publish-model-service-ui.md) 게시하는 방법에 대한 자습서에 따라 조직 내의 사용자가 기계 학습 서비스에 손쉽게 액세스할 수 있도록 하여 데이터를 평가할 수 있습니다.
