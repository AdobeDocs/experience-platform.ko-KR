---
title: 대상자 비교
description: 대상 비교 대시보드를 사용하여 서로 다른 대상 그룹 간에 주요 지표를 비교하는 방법을 알아봅니다. 데이터 기반 결정을 위한 대상 필터 설정, 트렌드 분석 및 인사이트 내보내기
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# 대상자 비교

[!UICONTROL 대상 비교] 대시보드는 나란히 표시된 보기에서 주요 대상 지표를 비교하고 대조합니다. 이 대시보드에서 다양한 작업을 수행하여 두 대상 그룹을 비교하고 두 그룹 간의 주요 지표를 분석할 수 있습니다. 그런 다음 대상 세분화 및 타기팅 전략과 관련하여 데이터 기반 결정을 내릴 수 있습니다.

## 대상 비교 설정 {#set-audience-comparisons}

보다 의미 있는 통찰력과 비교를 허용하려면 시스템 필터를 사용하여 대상 세그먼트와 분석에 필요한 시간대를 정확하게 타깃팅하십시오. 필터 아이콘(![필터 아이콘을 선택합니다.](../../../images/icons/filter-icon-white.png)) 서로 다른 두 대상([!UICONTROL 대상 A] 및 [!UICONTROL 대상 B])을 선택하고 비교할 특정 매개 변수를 설정합니다.

![대상 비교 대시보드의 필터 대화 상자.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters.png)

[!UICONTROL 필터] 대화 상자가 나타납니다. 분석할 첫 번째 대상을 선택하려면 **[!UICONTROL 대상 A 선택]** 드롭다운을 선택합니다. 이 예에서는 `California Patients`이(가) 대상 A로 선택되었습니다. 이 대상자는 필터가 적용되면 비교의 왼쪽에 표시됩니다.

그런 다음 **[!UICONTROL 대상 B]** 선택 드롭다운에서 [!UICONTROL 대상 A]과(와) 비교할 두 번째 대상을 선택하십시오. 이 이미지에서 [!UICONTROL 전자 메일에 동의한 사용자]가 [!UICONTROL 대상자 B] (으)로 선택되었습니다. 필터가 적용되면 이 대상은 [!UICONTROL 대상 비교] 대시보드의 오른쪽에 표시됩니다.

### 날짜 범위 조정 {#adjust-date-ranges}

특정 기간별로 데이터를 필터링하여 사용자 지정 날짜 범위에서 이러한 대상이 어떻게 수행되거나 변경되는지 확인할 수도 있습니다. 특정 기간별로 대상 데이터를 필터링할 시간 범위를 설정하려면 달력 필드에서 시작 날짜와 종료 날짜를 선택합니다.

또한 이 대화 상자는 적용되는 필터 수를 나타냅니다(아래 스크린샷에서는 대상 A와 대상 B, 그리고 오늘을 날짜 범위로 하여 두 개의 필터가 사용되고 있음). 적용된 필터를 모두 제거하려면 **[!UICONTROL 모두 지우기]**&#x200B;를 선택하십시오.

대상 및 날짜 범위를 설정한 후 **[!UICONTROL 적용]**&#x200B;을 선택하여 [!UICONTROL 대상 비교] 대시보드를 새로 고치십시오.

![대상 비교 대시보드의 필터 대화 상자(적용 강조 표시)](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters-apply.png)

이제 대시보드에 각 대상자에 대해 나란히 표시된 비교 차트가 표시됩니다.

![대상 비교 대시보드에 각 대상에 대한 지표를 비교하는 여러 차트가 있습니다.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-dashboard.png)

## 사용 가능한 대상 비교 차트 {#available-charts}

<!-- Potentially could expand this section to include images of each widget.  -->

대시보드에는 인사이트를 비교할 수 있는 몇 가지 차트가 제공됩니다.

- [[!UICONTROL 대상 크기]](../../guides/audiences.md#audience-size): 포함된 프로필의 수에 따라 각 대상의 크기를 쉽게 추적할 수 있습니다. 이 지표는 비교하는 두 대상의 크기를 이해하는 데 도움이 됩니다.
- [!UICONTROL 대상 ID 분류]: 원형 차트는 각 대상 내의 ID의 상대적 구성에 대한 분석을 제공합니다. 총 ID 수를 보고 다른 식별자(예: 이메일 또는 CRM ID)가 해당 합계에 기여하는 방식을 검사할 수 있습니다. 이 차트는 ID 유형을 기반으로 한 각 대상의 구성을 이해하는 데 도움이 됩니다. 정확한 ID 수를 보려면 파이 차트의 섹션 위로 마우스를 가져갑니다.
- [[!UICONTROL 대상 크기 트렌드]](../../guides/audiences.md#audience-size-trend): 이 차트는 선택한 대상에 대한 시간 경과에 따른 크기 트렌드를 나타냅니다. 이 차트를 사용하여 프로필 수의 증가 또는 감소 기간을 나타내는 최고점과 최저점을 사용하여 선택한 기간 동안 각 대상자의 크기가 어떻게 변경되었는지 시각화할 수 있습니다.
- [[!UICONTROL 대상 크기 변경 트렌드]](../../guides/audiences.md#audience-size-change-trend): 이 차트에는 선택한 대상의 크기 변경 트렌드가 표시됩니다. 시간이 지남에 따라 대상자 크기가 얼마나 증가하거나 감소하는지 시각화하고, 대상자 모집단의 중요한 이동 또는 트렌드를 식별할 수 있습니다.

>[!NOTE]
>
>[!UICONTROL 대상 크기 트렌드] 및 [!UICONTROL 대상 크기 변경 트렌드] 차트를 통해 절대 크기와 지정된 기간 동안 두 대상 간의 크기 변동을 모두 추적하고 비교할 수 있습니다. 이 정보를 통해 대상자 변화에 영향을 주는 패턴 및 요인을 보다 쉽게 이해할 수 있습니다.

## 인사이트 내보내기 {#export-insights}

필터를 적용하고 대상을 분석한 후 추가적인 오프라인 분석 또는 보고 목적으로 데이터를 내보낼 수 있습니다. 인사이트를 내보내려면 표의 오른쪽 상단에서 **[!UICONTROL 내보내기]**&#x200B;를 선택합니다. [PDF 인쇄] 대화 상자가 나타납니다. 이 대화 상자에서 PDF으로 저장하거나 표에 표시된 데이터를 인쇄할 수 있습니다.

[!UICONTROL 템플릿] 개요로 돌아가려면 **[!UICONTROL 템플릿]**&#x200B;을(를) 선택하십시오.

![서식 파일이 강조 표시된 고급 대상 겹침 보기입니다.](../../images/sql-insights-query-pro-mode/templates/navigation.png)

## 다음 단계

이 문서를 읽고 나면 **대상 비교** 대시보드를 사용하여 서로 다른 대상 그룹 간의 주요 지표를 비교하는 방법에 대해 알아보았습니다. 대상자 세분화 및 타기팅 전략을 지속적으로 개선하려면 추가적인 통찰력을 제공하는 다른 데이터 Distiller 템플릿을 살펴보십시오. [대상 트렌드](./trends.md), [대상 ID 중복](./identity-overlaps.md) 및 [고급 대상 중복](./overlaps.md) UI 안내서를 참조하여 의사 결정을 더욱 향상시키고 참여 노력을 최적화하십시오.

