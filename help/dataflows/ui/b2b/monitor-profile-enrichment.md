---
description: 사용 [!UICONTROL 프로필 보강] 대시보드를 사용하여 프로필 보강 작업이 성공적으로 실행되고 완료되었는지 확인하고, 보강의 효과를 측정하는 기본 지표를 확인할 수 있습니다.
solution: Experience Platform
title: 프로필 보강 작업 모니터링
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# UI에서 프로필 보강 작업 모니터링 {#monitor-profile-enrichment}

사용 [!UICONTROL 프로필 보강] 대시보드를 사용하여 프로필 보강 작업이 성공적으로 실행되고 완료되었는지 확인하고, 보강의 효과를 측정하는 기본 지표를 확인할 수 있습니다.

다음에서 [플랫폼 UI](https://platform.adobe.com), 선택 **[!UICONTROL 모니터링]** 을(를) 왼쪽 탐색에서 [!UICONTROL 모니터링] 대시보드입니다. 보기 선택기에서 **B2B 플로우** 다음의 대시보드 요소를 보려면 다음과 같이 하십시오. [Real-Time CDP](/help/rtcdp/b2b-overview.md).  다음 [!UICONTROL 모니터링] 대시보드에는 최근 성공한 실행의 기본 지표와 과거 최대 90일 동안의 일일 작업 상태가 포함됩니다.

## 관련 계정 프로필 보강 {#related-accounts}

다음 [!UICONTROL 관련 계정] 대시보드에는 기본 지표와 관련 일별 작업의 상태가 표시됩니다. [관련 계정](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) 프로필 보강.

![Experience Platform UI에서 프로필 보강 작업 모니터링 화면으로 이동하는 방법을 시각적으로 표시합니다.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

의 데이터 **[!UICONTROL 지표]** 카드에는 관련 계정 작업의 최근 성공 실행의 기본 지표가 포함되어 있습니다.

다음 지표는 관련 계정 프로필 보강 작업에 사용할 수 있습니다.

| 지표 | 설명 |
| --------- | ---------- |
| **[!UICONTROL 총 계정 프로필]** | 조직에서 액세스할 수 있는 총 계정 프로필을 나타냅니다. |
| **[!UICONTROL 계정 그룹]** | 관련 계정 머신 러닝 작업으로 클러스터된 계정 그룹의 수를 나타냅니다. |
| **[!UICONTROL 단일 계정 그룹]** | 다른 계정과 함께 그룹화되지 않은 계정 수를 나타냅니다. |
| **[!UICONTROL 최대 그룹 크기]** | 가장 큰 관련 계정 그룹의 크기를 나타냅니다. 최대 허용 그룹 크기는 30입니다. |
| **[!UICONTROL 중간값 그룹 크기]** | 조직 내 관련 계정 그룹의 중간 크기를 나타냅니다. |
| **[!UICONTROL 마지막으로 성공한 실행]** | 마지막으로 성공한 관련 계정 작업 실행의 날짜 및 시간을 나타냅니다. |
| **[!UICONTROL 상태]** | 관련 계정 작업의 상태(성공, 실패 또는 처리)를 나타냅니다. |
| **[!UICONTROL 메시지]** | 특정 작업 실행에 대한 오류 또는 경고 메시지를 나타냅니다. |

## 리드-계정 일치 프로필 보강 {#lead-to-account-matching}

다음 [!UICONTROL 리드-계정 일치] 대시보드에는 와 관련된 기본 지표와 일별 작업 실행 상태가 표시됩니다. [리드-계정 일치](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) 프로필 보강.

![리드-계정 일치 프로필 보강](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

리드-계정 대응 프로필 보강 작업에 다음 지표를 사용할 수 있습니다.

| 지표 | 설명 |
| --------- | ---------- |
| **[!UICONTROL 계정이 있는 총 사용자 수]** | 계정과 연결된 총 사용자 수를 나타냅니다. |
| **[!UICONTROL 총 계정 수]** | 총 계정 수를 나타냅니다. |
| **[!UICONTROL 계정이 있는 기존 사용자]** | 데이터 소스의 계정과 이미 연결된 사용자의 수를 나타냅니다. |
| **[!UICONTROL 일치하는 사용자]** | 계정에 일치하는 사용자 수를 나타냅니다. |
| **[!UICONTROL 일치하지 않는 사용자]** | 계정과 일치하지 않는 사용자 수를 나타냅니다. |
| **[!UICONTROL 마지막으로 성공한 실행]** | 계정 일치 작업 실행에 대해 마지막으로 성공한 잠재 고객의 날짜와 시간을 나타냅니다. |
| **[!UICONTROL 상태]** | 잠재 고객 대 계정 일치 작업의 상태(성공, 실패 또는 처리)를 나타냅니다. |

## 예측 리드 및 계정 점수 프로필 보강 {#predictive-lead-to-account-scoring}

다음 [!UICONTROL 예측 리드 및 계정 점수] 대시보드에는 와 관련된 기본 지표와 일별 작업 실행 상태가 표시됩니다. [예측 리드 및 계정 점수](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) 프로필 보강.

![예측 리드 및 계정 점수 프로필 보강](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

예측 리드 및 계정 채점 프로필 보강 작업에 다음 지표를 사용할 수 있습니다.

| 지표 | 설명 |
| --------- | ---------- |
| **[!UICONTROL 작업 시작]** | 예측 리드 및 계정 채점 작업 실행의 시작 날짜 및 시간을 나타냅니다. |
| **[!UICONTROL 처리 시간]** | 작업을 완료하는 데 걸린 총 시간입니다. |
| **[!UICONTROL 점수 이름]** | 작업의 점수 이름입니다. |
| **[!UICONTROL 프로필 유형]** | 점수 유형: <ul><li>사람</li><li>계정</li></ul>. |
| **[!UICONTROL 작업 유형]** | 작업 유형:<ul><li>채점</li><li>교육</li>. |
| **[!UICONTROL 상태]** | 예측 리드 및 계정 점수 지정 작업의 상태(성공, 실패 또는 처리)를 나타냅니다. |

## UI 컨트롤 {#ui-controls}

이 섹션에서는 페이지에 표시되는 지표를 필터링할 수 있는 모니터링 인터페이스의 다양한 UI(사용자 인터페이스) 옵션에 대해 설명합니다.

화살표 아이콘 사용(![화살표 아이콘](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png))을 클릭하여 화면 맨 위에 있는 카드를 확장하거나 닫을 수 있습니다. 이 카드에는 프로필 보강 작업에 대한 정보가 한 눈에 표시됩니다.

![화살표 아이콘 UI 컨트롤을 보여 주는 화면 레코딩입니다.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

사용 **[!UICONTROL 지표 및 그래프]** 전환하여 최신 지표를 표시하는 보기를 닫습니다.

![지표와 그래프 토글을 보여주는 화면 레코딩입니다.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

사용 **[!UICONTROL 실패만 표시]** 실패한 프로필 보강 작업만 표시하도록 전환합니다.

![실패만 표시 토글을 보여 주는 화면 레코딩입니다.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 다음 단계 {#next-steps}

이제 이 자습서를 따라 프로필 보강 작업에 대한 지표를 정상적으로 모니터링하고 이해할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [Real-Time CDP B2B의 관련 계정](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [계정 프로필 UI 안내서의 관련 계정 탭](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Real-Time CDP B2B에서 계정 일치로 리드](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Real-Time CDP B2B의 예측 리드 및 계정 점수](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
