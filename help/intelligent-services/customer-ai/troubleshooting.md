---
keywords: Experience Platform;시작하기;고객 ai;인기 항목;고객 ai 입력;고객 ai 출력;고객 ai 문제 해결;고객 ai 오류
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 고객 AI 오류 문제 해결
description: 고객 AI에서 일반적인 오류에 대한 답변을 찾아보십시오.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 고객 AI 오류 문제 해결

모델 교육, 채점 및 구성이 실패하면 고객 AI에 오류가 표시됩니다. 다음에서 **[!UICONTROL 서비스 인스턴스]** 섹션, 열 **[!UICONTROL 마지막 실행 상태]** 다음 메시지 중 하나를 표시합니다. **[!UICONTROL 성공]**, **[!UICONTROL 교육 문제]**, 및 **[!UICONTROL 실패]**.

![마지막 실행 상태](./images/errors/last-run-status.png)

일 경우에는 **[!UICONTROL 실패]** 또는 **[!UICONTROL 교육 문제]** 이 표시되면 실행 상태를 선택하여 사이드 패널을 열 수 있습니다. 사이드 패널에는 **[!UICONTROL 마지막 실행 상태]** 및 **[!UICONTROL 마지막 실행 세부 정보]**. **[!UICONTROL 마지막 실행 세부 정보]** 이 실행은 실패한 이유에 대한 정보를 포함합니다. 고객 AI가 오류에 대한 세부 정보를 제공할 수 없는 경우 제공된 오류 코드로 지원 센터에 문의하십시오.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Chrome 시크릿에서 고객 AI에 액세스할 수 없음

Google Chrome의 시크릿 모드 보안 설정의 업데이트로 인해 Google Chrome의 시크릿 모드에서 로드 오류가 발생합니다. experience.adobe.com 을 신뢰할 수 있는 도메인으로 만들기 위해 Chrome에서 문제가 활발히 진행되고 있습니다.

<img src="./images/errors/error.PNG" width="500" /><br />

### 권장 수정 사항

이 문제를 해결하려면 experience.adobe.com 을 항상 쿠키를 사용할 수 있는 사이트로 추가해야 합니다. 다음으로 이동하여 시작 **chrome://settings/cookies**. 다음으로 아래로 스크롤하여 **사용자 지정된 비헤이비어** 섹션 뒤에 다음을 선택합니다. **추가** &quot;항상 쿠키를 사용할 수 있는 사이트&quot; 옆에 있는 버튼입니다. 표시되는 팝오버에서 을 복사하여 붙여넣습니다 `[*.]experience.adobe.com` 그런 다음 **서드파티 쿠키 포함** 이 사이트 확인란에서 참조할 수 있습니다. 완료되면 다음을 선택합니다. **추가** 및 시크릿으로 고객 AI를 다시 로드합니다.

![권장 수정 사항](./images/errors/cookies2.gif)

## 모델 품질이 좋지 않습니다.

오류 메시지가 표시되면[!UICONTROL 모델 품질이 좋지 않습니다. 수정된 구성으로 새 앱을 만드는 것이 좋습니다]&quot;. 아래의 권장 단계에 따라 문제를 해결하십시오.

<img src="./images/errors/model-quality.png" width="300" /><br />

### 권장 수정 사항

&quot;모델 품질이 좋지 않음&quot;은 모델 정확도가 허용 가능한 범위 내에 있지 않음을 의미합니다. 고객 AI는 교육 후 신뢰할 수 있는 모델과 AUC(ROC 곡선 이하 면적) &lt; 0.65를 구축할 수 없었다. 오류를 수정하려면 구성 매개 변수 중 하나를 변경하고 교육을 다시 실행하는 것이 좋습니다.

먼저 데이터의 정확성을 확인합니다. 데이터에 예측 결과에 필요한 필드가 포함되어 있는 것이 중요합니다.

- 데이터 세트에 최신 날짜가 있는지 확인합니다. 고객 AI는 모델이 트리거될 때 데이터가 항상 최신 상태인 것으로 간주합니다.
- 정의된 예측 및 자격 창에서 누락된 데이터가 있는지 확인합니다. 데이터는 간격 없이 완성되어야 합니다. 또한 데이터 세트가 [Customer AI 내역 데이터 요구 사항](./data-requirements.md#data-requirements).
- 스키마 필드 속성 내에서 상거래, 애플리케이션, 웹 및 검색에서 누락된 데이터가 있는지 확인합니다.

데이터가 문제가 아닌 것 같으면 자격 모집단 조건을 변경하여 모델을 특정 프로필로 제한해 보십시오(예: `_experience.analytics.customDimensions.eVars.eVar142` 이(가) 지난 56일 내에 존재합니다. 이렇게 하면 교육 기간에 사용되는 데이터의 모집단과 크기가 제한됩니다.

자격 모집단을 제한할 수 없거나 가능하지 않은 경우 예측 창을 변경합니다.

- 예측 기간을 7일로 변경하고 오류가 계속 발생하는지 확인하십시오. 오류가 더 이상 발생하지 않으면 정의된 예측 기간에 충분한 데이터가 없을 수 있음을 나타냅니다.
