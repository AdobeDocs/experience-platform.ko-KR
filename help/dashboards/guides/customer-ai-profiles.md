---
title: 프로필 대시보드 Customer AI 위젯
description: Customer AI가 조직의 실시간 고객 프로필 데이터에 대한 이탈 또는 성향과 관련된 중요한 통찰력을 제공하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: e14067606e4c4868c926433129d835c7b0a7a18f
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 2%

---

# 프로필 대시보드 고객 AI 위젯 {#customer-ai-profiles-widgets}

고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 정의 성향 점수를 생성하는 데 사용됩니다. 고객 AI는 기존 소비자 경험 이벤트 데이터를 분석하여 이탈 또는 전환 성향 점수를 예측하여 이를 수행합니다. 이러한 정확도가 높은 고객 성향 모델을 통해 보다 정확한 세분화 및 타기팅을 수행할 수 있습니다. 다음 [점수 분포](#customer-ai-distribution-of-scores) 및 [채점 요약](#customer-ai-scoring-summary) 통찰력은 대상의 구분을 보여 줍니다. 이 섹션에서는 높음/낮음/중간 성향인 프로필과 이러한 프로필이 프로필 수에 걸쳐 배포되는 방법을 강조합니다.

<!-- 
The links when required:
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL 고객 AI 점수 분배] {#customer-ai-distribution-of-scores}

다음 [!UICONTROL 고객 AI 점수 분배] 위젯은 성향 점수에 따라 총 프로필 수를 분류합니다. 프로필 수의 분포는 AI 모델과 선택한 병합 정책에 의해 결정된 다음 성향을 나타내는 5퍼센트 증분으로 시각화됩니다. 프로필 성향은 녹색, 노란색, 빨간색으로 높음, 중간, 낮음으로 각각 색상 코딩됩니다. 프로필의 카운트는 Y축을 따라 제공되고, 성향 점수는 X축을 따라 제공된다.

>[!NOTE]
>
>시각화가 전환 성향 점수인 경우, 높은 점수는 녹색으로 표시되고 낮은 점수는 빨간색으로 표시됩니다. 이탈 성향을 예측하는 경우 이것이 뒤집히면, 높은 점수는 빨간색이고 낮은 점수는 녹색이다. 중간 버킷은 선택한 성향 유형에 관계없이 노란색으로 유지됩니다.

성향 점수를 결정하는 AI 모델은 위젯 제목 아래의 드롭다운 선택기에서 선택됩니다. 드롭다운에는 구성된 모든 Customer AI 모델 목록이 포함되어 있습니다. 사용 가능한 모델 목록에서 분석에 적합한 AI 모델을 선택합니다. 사용 가능한 고객 AI 모델이 없는 경우 위젯 내의 메시지를 통해 하나 이상의 고객 AI 모델을 구성하도록 안내하고 고객 AI 모델 구성 페이지에 하이퍼링크를 제공합니다. 에 대한 지침은 설명서 를 참조하십시오. [고객 AI 인스턴스 구성 방법](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>개요 탭 바로 아래에 있는 드롭다운을 선택하여 분석에 포함된 프로필을 결정하는 병합 정책을 변경합니다. 의 섹션을 참조하십시오. [병합 정책](#merge-policies) 을 참조하십시오. [병합 정책 개요](../../profile/merge-policies/overview.md) 을 참조하십시오.

선택한 고객 AI 모델에 대한 세부 인사이트 페이지로 이동하려면 다음을 선택합니다. **[!UICONTROL 모델 세부 정보 보기]**.

![을 사용하는 Experience Platform 대상 대시보드 [!UICONTROL 고객 AI 점수 분배] 위젯 및 [!UICONTROL 모델 세부 정보 보기] 강조 표시됨.](../images/segments/customer-ai-distribution-of-scores.png)

자세한 모델 인사이트 페이지가 표시됩니다.

![고객 AI에 대한 인사이트 페이지.](../images/profiles/customer-ai-insights-page.png)

고객 AI에 대한 자세한 내용은 [insights UI 안내서 살펴보기](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL Customer AI 점수 요약] {#customer-ai-scoring-summary}

이 위젯은 채점된 총 프로필 수를 표시하고 높은 성향, 중간 성향 및 낮은 성향을 각각 녹색, 노란색 및 빨간색으로 포함하는 버킷으로 분류합니다. 도넛 차트는 높은 성향, 중간 성향 및 낮은 성향 사이의 프로필 비율 구성을 보여줍니다. 프로필은 75세 이상의 높은 성향, 25세에서 74세 사이의 중간 성향 및 24세 미만의 낮은 성향이 적합합니다. 범례는 색상 코드 및 성향의 임계값을 나타냅니다. 커서가 도넛 차트의 각 섹션 위로 마우스를 가져가면 높은, 중간 및 낮은 성향에 대한 프로필 수가 대화 상자에 표시됩니다.

위젯 제목 아래의 드롭다운 메뉴는 구성된 모든 Customer AI 모델의 목록을 제공합니다. 사용 가능한 모델 목록에서 분석에 적합한 AI 모델을 선택합니다. 사용 가능한 고객 AI 모델이 없는 경우 위젯 내의 메시지를 통해 하나 이상의 고객 AI 모델을 구성하도록 안내하고 고객 AI 모델 구성 페이지에 하이퍼링크를 제공합니다. 다음에서 설명서를 참조하십시오. [고객 AI 인스턴스 구성 방법](../../intelligent-services/customer-ai/user-guide/configure.md) 자세한 지침은 을 참조하십시오.

>[!NOTE]
>
>계산된 총 프로필 수는 선택한 병합 정책에 따라 다릅니다. 사용된 병합 정책을 변경하려면 개요 탭 바로 아래에 있는 드롭다운을 선택합니다. 의 섹션을 참조하십시오. [병합 정책](#merge-policies) 을 참조하십시오. [병합 정책 개요](../../profile/merge-policies/overview.md) 을 참조하십시오.

![Customer AI 점수 요약 위젯이 강조 표시된 Experience Platform 대상 대시보드입니다.](../images/segments/customer-ai-scoring-summary.png)

선택한 고객 AI 모델에 대한 세부 인사이트 페이지로 이동하려면 다음을 선택합니다. **[!UICONTROL 모델 세부 정보 보기]**. 고객 AI에 대한 자세한 내용은 [insights UI 안내서 살펴보기](../../intelligent-services/customer-ai/user-guide/discover-insights.md).