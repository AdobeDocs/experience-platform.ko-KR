---
title: 대상자 ID 오버랩
description: 대상 ID 중복 대시보드를 사용하여 대상 ID 중복을 분석하는 방법을 알아봅니다. 대상을 필터링하고, 병합 정책을 지정하고, ID 관계를 검사하여 데이터 기반 결정을 내립니다.
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# 대상자 ID 중복

선택한 대상에 대한 ID 중복을 [!UICONTROL 대상 ID 중복] 대시보드와 분석합니다. 대상 내의 다양한 ID가 어떻게 서로 관련되는지에 대한 통찰력을 사용하여 결합 전략을 최적화하고, 중복을 줄이고, 고객 세그멘테이션의 정확도를 향상시킬 수 있습니다. ID 유형 간의 중복에 대한 이해를 높여 효과적인 타기팅 전략을 개발하고 고객 상호 작용을 간소화합니다.

## 대상자 필터링 {#filter-audiences}

특정 대상 및 ID 유형의 타깃팅된 분석에 사용자 지정 필터를 사용하여 제공된 데이터가 분석 목표에 부합하는지 확인하십시오. 분석을 시작하려면 필터 아이콘(![필터 아이콘](../../../images/icons/filter-icon-white.png))을 선택합니다.

![대상 ID 중복 대시보드를 필터 아이콘이 강조 표시된 상태로 만듭니다.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filter-icon.png)

**[!UICONTROL 필터]** 대화 상자가 나타납니다. 이 보기에서 전역 필터를 선택하여 대상, 병합 정책 및 비교할 ID를 구성합니다. 각 섹션의 드롭다운 메뉴에서 분석에 대한 설정을 선택합니다.

1. **[!UICONTROL 대상 선택]**: 분석할 대상 세그먼트를 선택합니다(예: **캐나다 - 앨버타**).
2. **[!UICONTROL 병합 정책 지정]**: 선택한 대상 간에 ID가 결합되는 방식을 나타내는 병합 정책을 정의합니다(예제 스크린샷에서는 **기본 시간 기반** 정책이 선택됨).
3. 비교할 **[!UICONTROL ID A]** 및 **[!UICONTROL ID B]** 선택&#x200B;**: 비교할 두 ID 유형을 선택하십시오. 이 예제에서 &#x200B;** ID A&#x200B;**&#x200B;은(는) &quot;crmId&quot;로 선택되고 &#x200B;** ID B**&#x200B;은(는) &quot;email&quot;로 선택됩니다.
4. **날짜 범위 설정**: &quot;오늘&quot;과 같은 미리 정의된 범위를 선택하거나 일정 필드를 사용하여 시작 날짜와 종료 날짜를 수동으로 설정합니다.

![대상 ID 중복 대시보드의 필터 대화 상자.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filters-dialog.png)

>[!TIP]
>
>사용자 지정 전역 필터를 모두 지우려면 [!UICONTROL 필터] 대화 상자에서 **[!UICONTROL 모두 지우기]**&#x200B;를 선택하십시오. 단일 필터를 제거하려면 필터 이름의 오른쪽에 있는 &#39;[!UICONTROL X]&#39;을(를) 선택하십시오.

필터를 선택한 후에는 **[!UICONTROL 적용]**&#x200B;을 선택하여 대시보드를 새로 고치십시오.

![대상 ID의 필터 대화 상자가 [적용]이 강조 표시된 대시보드와 겹칩니다.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-apply-filters.png)

## 사용 가능한 대시보드 인사이트 {#available-insights}

**대상 ID 중복** 대시보드는 대상 내의 ID 중복 및 트렌드를 이해하는 데 도움이 되는 몇 가지 시각화 및 표 형식의 데이터를 제공합니다.

### 대상자 ID 오버랩 {#overlaps-table}

**[!UICONTROL 대상 ID 중복]** 표에는 선택한 필터에 따라 ID 중복이 표시됩니다. 이 정보를 사용하여 다양한 ID 유형 간의 겹침을 평가하고 ID가 얼마나 효과적으로 해결되는지 파악합니다. 아래 표에서는 각 열에 대해 자세히 설명합니다.

| 열 이름 | 설명 |
|-----------------|-------------------------------|
| **[!UICONTROL 대상 이름]** | 분석 중인 대상자의 이름입니다. 이 열은 인사이트가 의도한 타겟 그룹에 포커스를 두는지 확인하기 위해 검토 중인 대상 세그먼트를 식별합니다. |
| **[!UICONTROL ID A]** 및 **[!UICONTROL ID B]** | 비교 중인 ID(예: `crmId` 및 `email`). 비교되는 ID 유형을 파악하면 대상자 중복에 기여하는 ID 해결 전략을 식별하고 이러한 관계를 최적화하는 데 도움이 됩니다. |
| **[!UICONTROL 중복 개수]** | 두 ID가 모두 있는 프로필 수입니다. 이 지표는 대상 내에서 ID가 겹치는 범위에 대한 통찰력을 제공합니다. 이 정보는 여러 ID가 통합 프로필로 어떻게 효과적으로 확인되는지 평가하는 데 중요합니다. 이렇게 하면 타겟팅 및 개인화 전략을 향상시킬 수 있습니다. |
| **[!UICONTROL ID A 수]** | 선택한 대상자에서 **ID A**&#x200B;을(를) 포함하는 총 프로필 수입니다. 이 정보를 사용하여 대상자 내의 기본 ID 유형의 보급률을 이해하고 중복 분석에서 해당 역할을 평가합니다. |

![대상 ID 중복 대시보드의 대상 ID 중복 테이블입니다.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-chart.png)

### ID 분류 {#identity-breakdown}

**[!UICONTROL ID 분류]** 차트는 선택한 대상 내에서 ID의 상대적인 구성을 보여 줍니다. X축은 선택한 대상 내의 총 ID 수를 나타내고 Y축은 분석 중인 대상 이름을 나타냅니다. 이 시각화를 사용하여 각 ID 유형의 보급률을 이해하고 ID 관리 전략의 영향을 평가합니다. 이 차트는 고유한 색상을 사용하여 ID 유형 간에 차이를 보여 주며 ID가 대상 간에 어떻게 배포되는지에 대한 빠른 개요를 제공합니다.

>[!TIP]
>
>열 위로 마우스를 가져가면 각 ID 유형에 대한 개별 프로필 수를 볼 수 있습니다.

![ID 분류 차트입니다.](../../images/sql-insights-query-pro-mode/templates/identity-breakdown-chart.png)

### 대상자 ID 트렌드 {#audience-identity-trends}

**[!UICONTROL 대상 ID 트렌드]** 차트는 시간이 지남에 따라 총 ID 수가 어떻게 변경되었는지에 대한 통찰력을 제공합니다. X축은 분석되는 날짜 범위를 나타내고 Y축은 대상자별 총 ID 수를 나타냅니다. 이 지표를 사용하여 ID 증가를 추적하고, 안정성을 평가하고, 지속적인 ID 관리 노력의 효과를 측정할 수 있습니다.

>[!TIP]
>
>특정 날짜의 대상자에 대한 총 ID 수를 보려면 차트의 날짜 위로 마우스를 가져갑니다.

![대상 ID 트렌드 차트입니다.](../../images/sql-insights-query-pro-mode/templates/audience-identity-trends-chart.png)

## 인사이트 내보내기 {#export-insights}

ID 중복을 분석한 후 오프라인 분석 또는 보고를 위해 데이터를 내보낼 수 있습니다. 데이터를 내보내려면 표의 오른쪽 상단에서 **[!UICONTROL 내보내기]**&#x200B;를 선택합니다. 시각화된 데이터를 PDF으로 저장하거나 인쇄할 수 있는 PDF 인쇄 대화 상자가 나타납니다.

![대상자 ID 중복 대시보드가 강조 표시된 내보내기와 겹칩니다.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-export.png)

**대상 ID 중복** 대시보드는 선택한 대상 간에 서로 다른 ID가 어떻게 교차하는지에 대한 중요한 통찰력을 제공합니다. 이러한 통찰력을 활용하여 ID 결합 전략을 세분화하고 중복을 줄이고 대상 세그먼테이션이 보다 정확하고 효과적인지 확인할 수 있습니다.

## 다음 단계

이 문서를 읽은 후 **대상 ID 중복** 대시보드를 사용하여 선택한 대상의 ID 중복에 대한 중요한 통찰력을 얻는 방법에 대해 배웠습니다. 대상자 세분화 및 ID 관리에 대한 이해를 더욱 높이려면 포괄적인 통찰력을 제공하는 다른 데이터 Distiller 템플릿을 살펴보십시오. 타깃팅 및 참여 전략을 지속적으로 개선하려면 [대상 트렌드](./trends.md), [대상 비교](./comparison.md) 및 [고급 대상 중복](./overlaps.md) UI 안내서를 참조하십시오.

