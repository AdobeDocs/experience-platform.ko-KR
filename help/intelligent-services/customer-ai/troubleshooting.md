---
keywords: Experience Platform;시작하기;고객 ai;인기 항목;고객 ai 입력;고객 ai 출력;고객 ai 문제 해결;고객 ai 오류
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 고객 AI 오류 문제 해결
description: 고객 AI에서 발생하는 일반적인 오류에 대한 답변을 확인하십시오.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 고객 AI 오류 문제 해결

고객 AI에는 모델 교육, 점수 책정 및 구성이 실패하면 오류가 표시됩니다. 에서 **[!UICONTROL 서비스 인스턴스]** 섹션, 열 **[!UICONTROL 마지막 실행 상태]** 다음 메시지 중 하나를 표시합니다. **[!UICONTROL 성공]**, **[!UICONTROL 교육 문제]**, 및 **[!UICONTROL 실패]**.

![마지막 실행 상태](./images/errors/last-run-status.png)

이 경우 **[!UICONTROL 실패]** 또는 **[!UICONTROL 교육 문제]** 가 표시되면 실행 상태를 선택하여 사이드 패널을 열 수 있습니다. 사이드 패널에는 **[!UICONTROL 마지막 실행 상태]** 및 **[!UICONTROL 마지막 실행 세부 사항]**. **[!UICONTROL 마지막 실행 세부 사항]** 가 실패한 이유에 대한 정보가 들어 있습니다. 고객 AI가 오류에 대한 세부 정보를 제공할 수 없는 경우 제공된 오류 코드로 지원에 문의하십시오.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Chrome에서 Customer AI에 액세스할 수 없음

Google Chrome의 시크릿 모드 보안 설정에서 업데이트로 인해 Google Chrome의 시크릿 모드에서 오류가 발생합니다. 이 문제는 experience.adobe.com을 신뢰할 수 있는 도메인으로 만들기 위해 Chrome에서 현재 진행 중입니다.

<img src="./images/errors/error.PNG" width="500" /><br />

### 권장 수정

이 문제를 해결하려면 항상 쿠키를 사용할 수 있는 사이트로 experience.adobe.com을 추가해야 합니다. 다음으로 이동 **chrome://settings/cookies**. 다음으로 아래로 스크롤하여 **사용자 지정된 동작** 섹션 다음에 을(를) 선택하고 **추가** &quot;항상 쿠키를 사용할 수 있는 사이트&quot; 옆에 있는 단추. 팝오버가 나타나면 복사하여 붙여넣습니다. `[*.]experience.adobe.com` 그런 다음 **타사 쿠키 포함** 이 사이트에서 확인란을 선택합니다. 완료되면 을 선택합니다 **추가** incognito에서 Customer AI를 재로드합니다.

![권장 수정](./images/errors/cookies2.gif)

## 모델 품질이 좋지 않습니다

&quot; 오류가 표시되면[!UICONTROL 모델 품질이 좋지 않습니다. 수정된 구성으로 새 앱을 만드는 것이 좋습니다]&quot;. 아래 권장 단계에 따라 문제를 해결하십시오.

<img src="./images/errors/model-quality.png" width="300" /><br />

### 권장 수정

&quot;모델 품질이 낮음&quot;은 모델 정확도가 허용 가능한 범위 내에 있지 않음을 의미합니다. Customer AI에서 교육 후 신뢰할 수 있는 모델 및 AUC(ROC 곡선 아래 영역)를 작성할 수 없습니다. 오류를 수정하려면 구성 매개변수 중 하나를 변경하고 교육을 다시 실행하는 것이 좋습니다.

먼저 데이터의 정확도를 확인합니다. 예측 결과에 필요한 필드가 데이터에 포함되어 있어야 합니다.

- 데이터 세트에 최신 날짜가 있는지 확인합니다. 고객 AI는 모델이 트리거될 때 데이터가 항상 최신 것이라고 가정합니다.
- 정의된 예측 및 자격 조건 창에서 누락된 데이터를 확인합니다. 간격 없이 데이터를 완료해야 합니다. 또한 데이터 세트가 [고객 AI 이전 데이터 요구 사항](./input-output.md#data-requirements).
- 스키마 필드 속성 내에서 상거래, 애플리케이션, 웹 및 검색에서 누락된 데이터를 확인합니다.

데이터가 문제가 아닌 것 같은 경우에는 자격 조건 을 변경하여 모델을 특정 프로필로 제한해 보십시오(예: `_experience.analytics.customDimensions.eVars.eVar142` 가 최근 56일 동안 존재함). 교육 창에서 사용되는 데이터의 모집단 및 크기를 제한합니다.

자격 모집단 제한이 작동하지 않거나 불가능한 경우 예측 창을 변경합니다.

- 예측 창을 7일로 변경하고 오류가 계속 발생하는지 확인하십시오. 오류가 더 이상 발생하지 않으면 정의된 예측 창에 충분한 데이터가 없을 수 있음을 나타냅니다.
