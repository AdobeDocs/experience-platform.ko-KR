---
keywords: Experience Platform;모델 점수 매기기;데이터 과학 작업 공간;인기 항목;ui;채점 실행;채점 결과
solution: Experience Platform
title: 데이터 과학 작업 공간 UI에서 모델에 점수 매기기
type: Tutorial
description: Adobe Experience Platform 데이터 과학 작업 영역의 점수는 입력 데이터를 기존의 훈련된 모델에 공급하여 달성할 수 있습니다. 그런 다음 채점 결과가 저장되고 지정된 출력 데이터 세트에 새 배치로 볼 수 있습니다.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---

# 데이터 과학 작업 공간 UI에서 모델에 점수 매기기

Adobe Experience Platform의 채점 [!DNL Data Science Workspace] 는 기존의 훈련된 모델에 입력 데이터를 공급하여 달성할 수 있습니다. 그런 다음 채점 결과가 저장되고 지정된 출력 데이터 세트에 새 배치로 볼 수 있습니다.

이 자습서에서는 다음에서 모델에 점수를 매기는 데 필요한 단계를 보여줍니다. [!DNL Data Science Workspace] 사용자 인터페이스.

## 시작하기

이 자습서를 완료하려면 다음에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]. 에서 IMS 조직에 대한 액세스 권한이 없는 경우 [!DNL Experience Platform]을(를) 계속하려면 시스템 관리자에게 문의하십시오.

이 자습서에는 훈련된 모델이 필요합니다. 교육된 모델이 없는 경우 다음을 따르십시오. [ui에서 모델 교육 및 평가](./train-evaluate-model-ui.md) 튜토리얼을 참조하십시오.

## 새 채점 실행 만들기

채점 실행은 이전에 완료되고 평가된 교육 실행의 최적화된 구성을 사용하여 만들어집니다. 모델에 대한 최적 구성 세트는 일반적으로 교육 실행 평가 지표를 검토하여 결정됩니다.

채점에 해당 구성을 사용하기 위해 가장 최적의 교육 실행을 찾습니다. 그런 다음 해당 이름에 첨부된 하이퍼링크를 선택하여 원하는 교육 실행을 엽니다.

![교육 실행 선택](../images/models-recipes/score/select-run.png)

교육 실행에서 **[!UICONTROL 평가]** 탭, 선택 **[!UICONTROL 점수]** 화면 오른쪽 상단에 있습니다. 새 채점 워크플로우가 시작됩니다.

![](../images/models-recipes/score/training_run_overview.png)

입력 채점 데이터 세트를 선택하고 **[!UICONTROL 다음]**.

![](../images/models-recipes/score/scoring_input.png)

출력 채점 데이터 세트를 선택합니다. 이는 채점 결과가 저장되는 전용 출력 데이터 세트입니다. 선택 내용을 확인하고 를 선택합니다. **[!UICONTROL 다음]**.

![](../images/models-recipes/score/scoring_results.png)

워크플로우의 마지막 단계에서 채점 실행을 구성하라는 메시지가 표시됩니다. 이 구성은 모델에서 채점 실행에 사용됩니다.
모델을 생성하는 동안 설정된 상속된 매개변수는 제거할 수 없습니다. 값을 두 번 클릭하거나 항목을 마우스로 가리키면서 되돌리기 아이콘을 선택하여 상속되지 않은 매개 변수를 편집하거나 되돌릴 수 있습니다.

![구성](../images/models-recipes/score/configuration.png)

채점 구성을 검토 및 확인하고 다음을 선택합니다. **[!UICONTROL 완료]**  채점 실행을 생성하고 실행합니다. 다음으로 이동되었습니다. **[!UICONTROL 채점 실행]** 탭과 새 채점은 **[!UICONTROL 보류 중]** 상태가 표시됩니다.

![채점 실행 탭](../images/models-recipes/score/scoring_runs_tab.png)

다음 상태 중 하나로 채점 실행을 표시할 수 있습니다.
- 보류 중
- 완료
- 실패
- 실행 중

상태는 자동으로 업데이트됩니다. 상태가 인 경우 다음 단계로 진행합니다. **[!UICONTROL 완료]** 또는 **[!UICONTROL 실패]**.

## 채점 결과 보기

채점 결과를 보려면 교육 실행을 선택하여 시작합니다.

![교육 실행 선택](../images/models-recipes/score/select-run.png)

교육 실행으로 리디렉션됩니다. **[!UICONTROL 평가]** 페이지를 가리키도록 업데이트하는 중입니다. 교육 실행 평가 페이지 상단에서 **[!UICONTROL 채점 실행]** 탭으로 이동하여 기존 채점 실행 목록을 확인합니다.

![평가 페이지](../images/models-recipes/score/view_scoring_runs.png)

그런 다음 채점 실행을 선택하여 실행 세부 정보를 확인합니다.

![실행 세부 정보](../images/models-recipes/score/view_details.png)

선택한 채점 실행이 &quot;완료&quot; 또는 &quot;실패&quot; 상태인 경우 **[!UICONTROL 활동 로그 보기]** 링크를 사용할 수 있습니다. 채점 실행이 실패할 경우 실행 로그는 실패 이유를 확인하는 데 유용한 정보를 제공할 수 있습니다. 실행 로그를 다운로드하려면 다음을 선택합니다. **[!UICONTROL 활동 로그 보기]**.

![로그 보기 선택](../images/models-recipes/score/view_logs.png)

다음 **[!UICONTROL 활동 로그 보기]** 팝오버가 표시됩니다. 관련 로그를 자동으로 다운로드할 URL을 선택하십시오.

![](../images/models-recipes/score/activity_logs.png)

을 선택하여 채점 결과를 조회할 수도 있습니다.  **[!UICONTROL 채점 결과 데이터 세트 미리 보기]**.

![미리 보기 결과 선택](../images/models-recipes/score/view_results.png)

출력 데이터 세트의 미리보기가 제공됩니다.

![결과 미리보기](../images/models-recipes/score/preview_results.png)

전체 채점 결과 세트에 대해 **[!UICONTROL 채점 결과 데이터 세트]** 오른쪽 열에 링크가 있습니다.

## 다음 단계

이 튜토리얼은에서 훈련된 모델을 사용하여 데이터에 점수를 매기는 단계를 안내합니다 [!DNL Data Science Workspace]. 다음에 대한 자습서를 따르십시오 [UI에서 서비스로 모델 게시](./publish-model-service-ui.md) 조직의 사용자가 기계 학습 서비스에 쉽게 액세스할 수 있도록 하여 데이터에 점수를 매길 수 있습니다.
