---
keywords: Experience Platform;시작;고객 아이디;인기 항목;고객 아이디 입력;고객 아이디 출력;고객 아이에이 출력;고객 아이문제 해결;고객 아이 오류
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 고객 AI 오류 문제 해결
topic-legacy: Getting started
description: 고객 AI에서 발생하는 일반적인 오류에 대한 답변을 확인할 수 있습니다.
type: Documentation
source-git-commit: ceb203899cda83aa79b994d45798d6147c3ff3b8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# 고객 AI 오류 문제 해결

고객 AI는 모델 트레이닝, 점수 지정 및 구성에 실패하면 오류를 표시합니다. **[!UICONTROL 서비스 인스턴스]** 섹션에서 **[!UICONTROL LAST RUN STATUS]**&#x200B;에 대한 열에 다음 메시지 중 하나가 표시됩니다.**[!UICONTROL 성공]**, **[!UICONTROL 교육 문제]** 및 **[!UICONTROL 실패]**.

![마지막 실행 상태](./images/errors/last-run-status.png)

**[!UICONTROL 실패]** 또는 **[!UICONTROL 교육 문제]**&#x200B;가 표시되는 경우 실행 상태를 선택하여 사이드 패널을 열 수 있습니다. 사이드 패널에는 **[!UICONTROL 마지막 실행 상태]** 및 **[!UICONTROL 마지막 실행 세부 사항]**&#x200B;이 있습니다. **[!UICONTROL 마지막 실행]** 세부 정보실행이 실패한 이유에 대한 정보를 포함합니다. 고객 AI에서 오류에 대한 세부 정보를 제공할 수 없는 경우 제공된 오류 코드를 지원 팀에 문의하십시오.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 모델 품질이 좋지 않음

&quot;[!UICONTROL 모델 품질이 불량한 경우 수정된 구성]&quot;을 사용하여 새 앱을 만드는 것이 좋습니다. 아래 권장 단계를 수행하여 문제를 해결하십시오.

<img src="./images/errors/model-quality.png" width="300" /><br />

### 권장 수정

&quot;모델 품질이 낮음&quot;은 모델 정확도가 허용 가능한 범위 내에 있지 않음을 의미합니다. 고객 AI가 교육 후 신뢰할 수 있는 모델 및 AUC(ROC 곡선 아래 영역)를 만들 수 없습니다. 65 오류를 수정하려면 구성 매개 변수 중 하나를 변경하고 교육을 다시 실행하는 것이 좋습니다.

먼저 데이터의 정확도를 확인하십시오. 예측 결과에 필요한 필드가 데이터에 포함되어 있어야 합니다.

- 데이터 세트에 최신 날짜가 있는지 확인합니다. 고객 AI는 모델이 트리거될 때 데이터가 항상 최신 데이터라고 가정합니다.
- 정의된 예측 및 자격 조건 창에서 누락된 데이터가 있는지 확인합니다. 데이터는 아무런 차이도 없이 완성되어야 합니다. 또한 데이터 세트가 [고객 AI 내역 데이터 요구 사항](./input-output.md#data-requirements)을 충족하는지 확인하십시오.
- 스키마 필드 속성 내에서 상거래, 응용 프로그램, 웹 및 검색에 누락된 데이터가 있는지 확인합니다.

데이터가 문제가 되지 않는 것으로 보이는 경우 자격 조건 모집단 조건을 변경하여 모델을 특정 프로필로 제한하십시오(예: `_experience.analytics.customDimensions.eVars.eVar142`은 지난 56일 동안 존재함). 이렇게 하면 교육 창에 사용되는 데이터의 모집단과 크기가 제한됩니다.

자격 모집단 제한이 작동하지 않거나 가능하지 않은 경우 예측 창을 변경하십시오.

- 예측 창을 7일로 변경해 보고 오류가 계속 발생하는지 확인하십시오. 오류가 더 이상 발생하지 않으면 정의된 예측 창에 대한 데이터가 충분하지 않을 수 있습니다.

