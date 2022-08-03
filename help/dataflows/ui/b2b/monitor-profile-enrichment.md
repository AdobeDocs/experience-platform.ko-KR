---
description: 를 사용하십시오 [!UICONTROL 프로필 보강] 대시보드 를 사용하여 프로필 데이터 보강 작업이 실행 및 완료되었는지 이해하고 데이터 보강 작업의 효과를 측정하는 기본 지표를 확인합니다.
solution: Experience Platform
title: 프로필 보강 작업 모니터링
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 842fe74b0b751c515a4faee437e1f94bd0662e11
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# UI에서 프로필 보강 작업 모니터링 {#monitor-profile-enrichment}

를 사용하십시오 [!UICONTROL 프로필 보강] 대시보드 를 사용하여 프로필 데이터 보강 작업이 실행 및 완료되었는지 이해하고 데이터 보강 작업의 효과를 측정하는 기본 지표를 확인합니다.

에서 [플랫폼 UI](https://platform.adobe.com), 선택 **[!UICONTROL 모니터링]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 모니터링] 대시보드 . 보기 선택기에서 을 선택합니다 **B2B 흐름** 에 해당하는 대시보드 요소를 보려면 [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  다음 [!UICONTROL 모니터링] 대시보드에는 최근 성공적인 실행의 기본 지표와 일별 작업 상태가 과거 최대 90일까지 포함됩니다.

## 관련 계정 프로필 보강 {#related-accounts}

다음 [!UICONTROL 관련 계정] 대시보드는 기본 지표와 [관련 계정](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) 프로필 보강.

![Experience Platform UI에서 프로필 보강 작업 모니터링 화면에 도달하는 방법에 대한 시각적 표시입니다.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

의 데이터 **[!UICONTROL 지표]** 카드에는 관련 계정 작업의 최근 성공적인 실행의 기본 지표가 포함되어 있습니다.

관련 계정 프로필 데이터 보강 작업에 다음 지표를 사용할 수 있습니다.

| 지표 | 설명 |
| --------- | ---------- |
| **[!UICONTROL 총 계정 프로필]** | 조직에서 액세스할 수 있는 총 계정 프로필을 나타냅니다. |
| **[!UICONTROL 계정 그룹]** | 관련 계정 기계 학습 작업에 의해 클러스터링된 계정 그룹 수를 나타냅니다. |
| **[!UICONTROL 단일 계정 그룹]** | 다른 계정과 함께 그룹화되지 않은 계정 수를 나타냅니다. |
| **[!UICONTROL 가장 큰 그룹 크기]** | 가장 큰 관련 계정 그룹의 크기를 나타냅니다. 허용되는 최대 그룹 크기는 30입니다. |
| **[!UICONTROL 중간 그룹 크기]** | 조직의 관련 계정 그룹의 중간값을 나타냅니다. |
| **[!UICONTROL 마지막 성공 실행]** | 마지막으로 성공한 관련 계정 작업 실행 날짜와 시간을 나타냅니다. |
| **[!UICONTROL 상태]** | 관련 계정 작업의 상태(성공, 실패 또는 처리)를 나타냅니다. |
| **[!UICONTROL 메시지]** | 특정 작업 실행에 대한 오류 또는 경고 메시지를 나타냅니다. |

## 계정 일치 프로필 데이터 보강 리드 {#lead-to-account-matching}

다음 [!UICONTROL 계정 일치 리드] 대시보드는 기본 지표와 [계정 일치 리드](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) 프로필 보강.

![계정 일치 프로필 데이터 보강 리드](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

프로필 데이터 보강 작업에서 계정 일치 항목에 이어지는 리드에 다음 지표를 사용할 수 있습니다.

| 지표 | 설명 |
| --------- | ---------- |
| **[!UICONTROL 계정이 있는 총 사용자 수]** | 계정과 연결된 총 사용자 수를 나타냅니다. |
| **[!UICONTROL 총 계정]** | 총 계정 수를 나타냅니다. |
| **[!UICONTROL 계정이 있는 기존 사용자]** | 데이터 소스의 계정과 이미 연결된 사람 수를 나타냅니다. |
| **[!UICONTROL 일치하는 사람]** | 계정에 일치된 사람 수를 나타냅니다. |
| **[!UICONTROL 미대응 사람]** | 계정과 일치하지 않는 사람 수를 나타냅니다. |
| **[!UICONTROL 마지막 성공 실행]** | 계정 일치 작업 실행에서 마지막으로 성공한 리드의 날짜 및 시간을 나타냅니다. |
| **[!UICONTROL 상태]** | 리드의 상태(성공, 실패 또는 처리)를 나타내는 계정 일치 작업을 나타냅니다. |

## UI 컨트롤 {#ui-controls}

이 섹션에서는 페이지에 표시되는 지표를 필터링할 수 있는 모니터링 인터페이스의 다양한 UI(사용자 인터페이스) 옵션에 대해 설명합니다.

화살표 아이콘 사용(![화살표 아이콘](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) 카드를 확장하거나 축소할 수 있습니다. 화면의 맨 위에는 프로필 보강 작업에 대한 요약 정보가 표시됩니다.

![화살표 아이콘 UI 컨트롤을 표시하는 화면 기록](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

를 사용하십시오 **[!UICONTROL 지표 및 그래프]** 최신 지표를 표시하는 보기를 해제하려면 전환합니다.

![지표 및 그래프를 표시하는 화면 기록](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

를 사용하십시오 **[!UICONTROL 실패만 표시]** 실패한 프로필 데이터 보강 작업만 표시하도록 전환합니다.

![실패 표시만 표시하는 화면 기록](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 다음 단계 {#next-steps}

이제 이 자습서를 따라 프로필 보강 작업에 대한 지표를 모니터링하고 이해할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 CDP B2B의 관련 계정](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [계정 프로필 UI 안내서의 관련 계정 탭](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [실시간 CDP B2B에서 계정 일치 시작](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
