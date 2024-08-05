---
keywords: Experience Platform; 모델 점수 매기기; 데이터 과학 작업 영역; 인기 있는 주제; UI; 득점 실행; 채점 결과
solution: Experience Platform
title: 데이터 과학 작업 영역 UI에서 모델 점수 매기기
type: Tutorial
description: Adobe Experience Platform Data Science 작업 영역의 점수 매기기는 입력 데이터를 기존의 학습된 모델에 공급하여 달성할 수 있습니다. 그런 다음 점수 매기기 결과가 저장되고 지정된 출력 데이터 세트 에서 새 일괄 처리로 볼 수 있습니다.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---

# 데이터 과학 작업 영역 UI에서 모델 점수 매기기

>[!NOTE]
>
>Data Science 작업 영역은(는) 더 이상 구매할 수 없습니다.
>
>이 설명서는 데이터 과학 작업 영역 이전에 사용 권한이 있는 기존 고객을 대상으로 합니다.

Adobe Experience Platform [!DNL Data Science Workspace] 의 점수 매기기는 입력 데이터를 기존의 학습된 모델에 공급하여 수행할 수 있습니다. 그런 다음 점수 매기기 결과가 저장되고 지정된 출력 데이터 세트 에서 새 일괄 처리로 볼 수 있습니다.

이 튜토리얼 에서는 사용자 인터페이스에서 [!DNL Data Science Workspace] 모델의 점수를 매기는 데 필요한 단계를 보여 줍니다.

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]의 조직에 대한 액세스 권한이 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

이 자습서에는 훈련된 모델이 필요합니다. 훈련된 모델이 없는 경우 계속하기 전에 [UI에서 모델 교육 및 평가](./train-evaluate-model-ui.md) 자습서를 따르십시오.

## 새 채점 실행 만들기

채점 실행은 이전에 완료되고 평가된 교육 실행의 최적화된 구성을 사용하여 만들어집니다. 모델에 대한 최적 구성 세트는 일반적으로 교육 실행 평가 지표를 검토하여 결정됩니다.

채점에 해당 구성을 사용하기 위해 가장 최적의 교육 실행을 찾습니다. 그런 다음 해당 이름에 첨부된 하이퍼링크를 선택하여 원하는 교육 실행을 엽니다.

![교육 실행 선택](../images/models-recipes/score/select-run.png)

교육 실행 **[!UICONTROL 평가]** 탭에서 화면 오른쪽 상단의 **[!UICONTROL 점수]**&#x200B;를 선택합니다. 새 채점 워크플로우가 시작됩니다.

![](../images/models-recipes/score/training_run_overview.png)

입력 채점 데이터 세트를 선택하고 **[!UICONTROL 다음]**&#x200B;을(를) 선택합니다.

![](../images/models-recipes/score/scoring_input.png)

출력 채점 데이터 세트를 선택합니다. 이는 채점 결과가 저장되는 전용 출력 데이터 세트입니다. 선택을 확인하고 다음&#x200B;]**선택을 선택합니다**[!UICONTROL .

![](../images/models-recipes/score/scoring_results.png)

작업 과정 마지막 단계에서는 점수 실행을 구성하라는 메시지가 표시됩니다. 이러한 구성은 점수 매기기 실행을 위해 모델에서 사용됩니다.
모델을 만드는 동안 설정된 상속된 매개 변수는 제거할 수 없습니다. 값을 두 번 클릭하거나 항목 위로 마우스를 가져간 상태에서 되돌리기 아이콘을 선택하여 상속되지 않은 매개변수를 편집하거나 되돌릴 수 있습니다.

![구성](../images/models-recipes/score/configuration.png)

채점 구성을 검토하고 확인하고 **[!UICONTROL 완료]**&#x200B;를 선택하여 채점 실행을 만들고 실행합니다. 득점 실행 탭 으로 **[!UICONTROL 이동되고 보류 중]** 상태의 **[!UICONTROL 새 득점 실행이]** 표시됩니다.

![득점 득점 탭](../images/models-recipes/score/scoring_runs_tab.png)

점수 실행은 다음 상태 중 하나로 표시될 수 있습니다.
- 보류 중
- 완료
- 실패
- 실행 중

상태는 자동으로 업데이트됩니다. 상태가 **[!UICONTROL 완료]** 또는 **[!UICONTROL 실패]**&#x200B;인 경우 다음 단계로 진행합니다.

## 채점 결과 보기

채점 결과를 보려면 교육 실행을 선택하여 시작합니다.

![교육 실행 선택](../images/models-recipes/score/select-run.png)

교육 실행 **[!UICONTROL 평가]** 페이지로 리디렉션됩니다. 교육 실행 평가 페이지 상단 근처에서 **[!UICONTROL 채점 실행]** 탭을 선택하여 기존 채점 실행 목록을 확인합니다.

![평가 페이지](../images/models-recipes/score/view_scoring_runs.png)

그런 다음 채점 실행을 선택하여 실행 세부 정보를 확인합니다.

![실행 세부 정보](../images/models-recipes/score/view_details.png)

선택한 채점 실행의 상태가 &quot;완료&quot; 또는 &quot;실패&quot;이면 **[!UICONTROL 활동 로그 보기]** 링크를 사용할 수 있습니다. 채점 실행이 실패할 경우 실행 로그는 실패 이유를 확인하는 데 유용한 정보를 제공할 수 있습니다. 실행 로그를 다운로드하려면 활동 로그&#x200B;]**보기 를 선택합니다**[!UICONTROL .

![로그 보기 선택](../images/models-recipes/score/view_logs.png)

활동 로그&#x200B;]**보기 팝오버가**[!UICONTROL &#x200B;나타납니다. 연결된 로그를 자동으로 다운로드할 URL을 선택합니다.

![](../images/models-recipes/score/activity_logs.png)

데이터 세트 미리 보기 채점 결과를 선택하여  **[!UICONTROL 채점 결과를 볼 수도 있습니다]**.

![미리 보기 결과 선택](../images/models-recipes/score/view_results.png)

출력 데이터 세트 미리 보기가 제공됩니다.

![결과 미리 보기](../images/models-recipes/score/preview_results.png)

채점 결과의 전체 집합을 보려면 오른쪽 열에 있는 **[!UICONTROL 채점 결과 데이터 집합]** 링크를 선택하십시오.

## 다음 단계

이 자습서에서는 [!DNL Data Science Workspace]에서 훈련된 모델을 사용하여 데이터를 평가하는 단계를 안내했습니다. [UI에서 서비스로 모델 게시](./publish-model-service-ui.md)에 대한 자습서를 따라 조직의 사용자가 기계 학습 서비스에 쉽게 액세스하여 데이터를 평가할 수 있습니다.
