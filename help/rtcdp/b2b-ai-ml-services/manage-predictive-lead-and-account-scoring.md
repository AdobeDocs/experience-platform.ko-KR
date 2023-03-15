---
title: Real-Time CDP B2B에서 예측 리드 및 계정 점수 관리
type: Documentation
description: 이 문서에서는 Experience Platform CDP B2B의 예측 리드 및 계정 점수 기능을 관리하는 방법에 대한 정보를 제공합니다.
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 2%

---

# Adobe Real-time Customer Data Platform, B2B 에디션에서 예측 리드 및 계정 점수 관리

>[!NOTE]
>
>B2B AI 관리 권한이 있는 사용자만 점수 목표를 생성, 변경 및 삭제할 수 있습니다.

이 튜토리얼에서는 예측 리드 및 계정 점수 책정 서비스의 점수 목표를 관리하는 단계를 안내합니다. 점수 목표는 개인 프로필 또는 계정 프로필에 대한 것일 수 있습니다.

## 새 점수 만들기

새 점수를 만들려면 다음을 선택합니다. **[!UICONTROL 서비스]** 사이드바에서 를 클릭하고 를 선택합니다. **[!UICONTROL 점수 만들기]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

다음 **[!UICONTROL 기본 정보]** 프로필 유형을 선택하고 이름 및 설명(선택 사항)을 입력하라는 메시지가 표시되는 화면입니다. 완료되면 다음을 선택합니다. **[!UICONTROL 다음]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

다음 **[!UICONTROL 목표 정의]** 화면이 나타납니다. 드롭다운 화살표를 선택한 다음 표시되는 드롭다운 창에서 목표 유형을 선택합니다.

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

다음 **[!UICONTROL 목표 세부 사항]** 대화 상자가 열립니다. 드롭다운 화살표를 선택한 다음 표시되는 드롭다운 창에서 목표 필드 이름 을 선택합니다.

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

다음 **[!UICONTROL 목표 조건]** 선택 항목이 나타납니다. 드롭다운 화살표를 선택한 다음 표시되는 드롭다운 창에서 조건 을 선택합니다.

![plas-goal-specifications-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

다음 **[!UICONTROL 목표 값]** 필드가 나타납니다. 그런 다음 을(를) 구성합니다 [!UICONTROL 목표 세부 사항]. 다음 항목 선택 [!UICONTROL 필드 값 입력] 패널 을 만들고 목표 값을 입력합니다.

>[!NOTE]
>
>여러 목표 값을 추가할 수 있습니다.

![plas-goal-details-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

필드를 추가하려면 다음을 선택합니다. **[!UICONTROL 필드 추가]**.

![plas-goal-specifications-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

예측 기간을 구성하려면 드롭다운 화살표를 선택한 다음 선택한 기간을 선택합니다.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

선택한 병합 정책은 개인 프로필의 필드 값을 선택하는 방법을 결정합니다. 드롭다운 화살표를 사용하여 원하는 병합 정책을 선택한 다음 을 선택합니다. **[!UICONTROL 완료]**.

다음 **[!UICONTROL 채점 설정이 완료되었습니다.]** 새 점수가 생성되었음을 확인하는 대화 상자가 나타납니다. 선택 **[!UICONTROL 확인]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>각 채점 프로세스가 완료되는 데 최대 24시간이 소요될 수 있습니다.

(으)로 돌아갑니다. **[!UICONTROL 서비스]** 점수 목록에서 만든 새 점수를 확인할 수 있는 탭입니다.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

마지막 실행 세부 정보에 대한 세부 정보 및 추가 정보를 보려면 점수를 선택합니다.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

마지막 실행 세부 정보에서 볼 수 있는 오류 코드에 대한 자세한 내용은 다음 섹션을 참조하십시오. [리드 AI 파이프라인 오류 코드](#leads-ai-pipeline-error-codes) 이 문서에서.

## 점수 편집

점수를 편집하려면 다음에서 점수를 선택합니다. **[!UICONTROL 서비스]** 탭하고 선택 **[!UICONTROL 편집]** (화면의 오른쪽에 있는 추가 세부 정보 패널)

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

다음 **[!UICONTROL 인스턴스 편집]** 점수에 대한 설명을 편집할 수 있는 대화 상자가 나타납니다. 변경 및 선택 **[!UICONTROL 저장]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>이 경우 모델 재교육 및 재점수가 트리거되므로 점수 구성을 변경할 수 없습니다. 점수를 삭제하고 새 점수를 만드는 것과 같습니다. 점수의 구성을 편집하려면 이 점수를 복제하거나 새 점수를 만들어야 합니다.

(으)로 돌아갑니다. **[!UICONTROL 서비스]** 탭. 화면 오른쪽의 추가 세부 정보 패널에서 업데이트된 설명 세부 정보를 보려면 점수를 선택합니다.

## 점수 복제

점수를 복제하려면 다음에서 점수를 선택합니다. **[!UICONTROL 서비스]** 탭하고 선택 **[!UICONTROL 복제]** (화면의 오른쪽에 있는 추가 세부 정보 패널)

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

다음 **[!UICONTROL 기본 정보]** 화면이 나타납니다. 프로필 유형, 이름 및 설명이 원래 점수에서 복제됩니다. 이러한 세부 사항을 수정하고 을(를) 선택합니다 **[!UICONTROL 다음]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

다음 **[!UICONTROL 목표 정의]** 화면이 나타납니다. 새 점수를 만들 때와 마찬가지로 목표 섹션을 완료하고 을 선택합니다. **[!UICONTROL 완료]**.

(으)로 돌아갑니다. **[!UICONTROL 서비스]** 목록에서 새로 복제된 점수를 확인할 수 있는 탭입니다.

>[!NOTE]
>
>다음 **[!UICONTROL 목표 정의]** 섹션은 원래 점수에서 복제되지 않습니다.

## 점수 삭제

점수를 삭제하려면 다음 목록에서 점수를 선택합니다 **[!UICONTROL 서비스]** 탭하고 선택 **[!UICONTROL 삭제]** (화면의 오른쪽에 있는 추가 세부 정보 패널)

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

다음 **[!UICONTROL 설명서 삭제]** 확인 대화 상자가 나타납니다. **[!UICONTROL 삭제]**&#x200B;를 선택합니다.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>점수 정의를 삭제하면 개인 프로필 또는 계정 프로필에 대한 모든 예상 점수가 삭제되지만, 점수 정의에 대해 생성된 필드 그룹은 삭제되지 않습니다. 필드 그룹은 데이터 모델에서 &quot;고립됨&quot; 상태로 유지됩니다.

(으)로 돌아갑니다. **[!UICONTROL 서비스]** 목록에서 더 이상 점수를 볼 수 없는 탭입니다.

## 리드 AI 파이프라인 오류 코드

| 오류 코드 | 오류 메시지 |
| --- | --- |
| 401 | 오류 401. 잠재 고객 AI 파이프라인 중단됨: 계정 점수에 유효한 계정이 충분하지 않음. 계정 수: {}. |
| 402 | 오류 402. 잠재 고객 AI 파이프라인 중지됨: 연락처 점수에 대해 유효한 연락처가 충분하지 않음. 연락처 수: {}. |
| 403 | 오류 403. 리드 AI 파이프라인 중단됨: 모델 교육에 대한 활동 볼륨이 충분하지 않습니다. 이벤트 수: {}. |
| 404 | 오류 404. 잠재 고객 AI 파이프라인 중단됨: 모델 교육에 대한 전환이 충분하지 않음. 전환 수: {}. |
| 405 | 오류 405. 리드 AI 파이프라인 중지됨: 유효한 모델 교육에 대해 활동이 너무 스파스 상태입니다. {}%의 계정에서만 활동이 있습니다. |
| 406 | 오류 406. 리드 AI 파이프라인 중지됨: 유효한 모델 교육에 대해 활동이 너무 스파스 상태입니다. {}%의 연락처에만 활동이 있습니다. |
| 407 | 오류 407. 잠재 고객 AI 파이프라인 중지됨: 점수 데이터 활동 유형이 교육 데이터와 일치하지 않습니다. |
| 408 | 오류 408. 잠재 고객 AI 파이프라인 중단됨: 활동 기능에 대한 누락 비율이 너무 높습니다. 누락 비율: {}. |
| 409 | 오류 409. 리드 AI 파이프라인 중지됨: 테스트 auc가 너무 낮습니다. 테스트 auc: {}. |
| 410 | 오류 410. 리드 AI 파이프라인 중지됨: 매개 변수 조정 후 테스트 auc가 너무 낮습니다. 테스트 auc: {}. |
| 411 | 오류 411. 리드 AI 파이프라인 중단됨: 교육 데이터에 신뢰할 수 있는 모델을 생성할 수 있는 충분한 전환이 없습니다. 전환: {}. |
| 412 | 오류 412. 잠재 고객 AI 파이프라인 중지됨: 테스트 데이터에 AUC-ROC를 계산하는 전환이 없습니다. |

| 경고/정보 코드 | 메시지 |
| --- | --- |
| 100 | 정보 100. 리드 AI 품질 검사: 계정 수: {}. |
| 101 | 정보 101. 잠재 고객 AI 품질 검사: 연락처 수: {}. |
| 102 | 정보 102. 잠재 고객 AI 품질 검사: 기회 수: {}. |
| 103 | 정보 103. AI 품질 검사 리드: 테스트 auc가 낮습니다. 매개변수 조정을 시작합니다. Auc 테스트: {}. |
| 200 | 경고 200. AI 품질 검사 리드: 펌웨어 기능 누락 비율: {}. |
| 201 | 경고 201. 리드 AI 품질 검사: 활동 기능의 누락 비율은 {}입니다. |

## 다음 단계

이제 이 자습서를 따라 점수를 만들고 관리할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [예측 리드 및 계정 점수](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [예측 리드 및 계정 채점 작업 모니터링](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
