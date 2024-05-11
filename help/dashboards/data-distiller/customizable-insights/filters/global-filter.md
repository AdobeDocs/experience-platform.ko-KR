---
title: 글로벌 필터 만들기
description: 사용자 지정 전역 적용 필터를 사용하여 데이터 인사이트를 필터링하는 방법을 알아봅니다.
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 글로벌 필터 만들기 {#create-global-filter}

글로벌 필터를 만들려면 먼저 다음을 선택합니다. **[!UICONTROL 필터 추가]** 대시보드 보기에서 다음을 수행합니다. **[!UICONTROL 전역 필터]** 드롭다운 메뉴를 통해 액세스합니다.

>[!IMPORTANT]
>
>전역 필터를 모든 차트에 매핑하는지 확인합니다. 이것은 자동 프로세스가 아닙니다. 전역 필터를 사용하려면 다음을 포함해야 합니다. [쿼리 매개 변수](../../../../query-service/ui/parameterized-queries.md) 차트의 SQL [전역 필터 활성화](#enable-global-filter) 위젯 작성기에서 [런타임 값 선택](#select-global-filter) 전역 필터 대화 상자의 매개 변수 쿼리 매개 변수를 통합해야 하는 경우 SQL을 편집하는 방법은 query pro guide를 참조하십시오.

![필터 추가 및 드롭다운 메뉴가 강조 표시된 사용자 정의 대시보드.](../../../images/customizable-insights/add-filter.png)

사용자 지정된 전역 필터를 사용하여 SQL에서 제공하는 통찰력을 빠르게 변경할 수 있습니다.

다음 [!UICONTROL 글로벌 필터 만들기] 대화 상자가 열립니다. 전역 필터를 만드는 것은 SQL을 사용하여 통찰력을 만드는 것과 동일한 프로세스를 따릅니다. 먼저 쿼리할 데이터베이스(Insights 데이터 모델)를 선택한 다음 쿼리 편집기에서 사용자 지정 SQL을 입력하고 마지막으로 실행 아이콘(![실행 아이콘](../../../images/customizable-insights/run-icon.png)).

>[!IMPORTANT]
>
>글로벌 필터를 만들 때 ID와 값을 포함해야 합니다. 샘플 값을 사용하면 SQL 문을 실행하고 차트를 작성할 수 있습니다. 문을 작성할 때 제공하는 샘플 값은 런타임 시 날짜 또는 글로벌 필터에 대해 선택하는 실제 값으로 대체됩니다.

쿼리를 성공적으로 실행하면 결과 탭에 결과가 표시됩니다. **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![다음 [!UICONTROL 글로벌 필터 대화 상자 만들기] 데이터 세트 드롭다운 메뉴를 사용하여 실행 아이콘과 다음 이 강조 표시됩니다.](../../../images/customizable-insights/global-filter.png)

전역 필터 생성 워크플로우의 마지막 단계에서는 필터에 대한 레이블을 추가해야 합니다. 에 레이블 추가 **[!UICONTROL 필터 레이블]** 텍스트 필드를 선택하고 드롭다운 상자에서 필터 유형을 선택합니다.

>[!NOTE]
>
>만 [!UICONTROL 콤보 상자] 필터 유형 옵션은 현재 지원됩니다.

마지막으로 다음을 선택합니다. **[!UICONTROL 선택]** 을 클릭하여 대시보드 보기로 돌아갑니다.

![다음 [!UICONTROL 글로벌 필터 대화 상자 만들기] 선택 과 필터 레이블 텍스트 입력 이 강조 표시되어 있습니다.](../../../images/customizable-insights/global-filter-label.png)

## 각 인사이트에 대한 전역 필터 활성화 {#enable-global-filter}

>[!TIP]
>
>생성하는 모든 차트에서 전역 필터를 활성화합니다. 이렇게 하면 전역 필터로 선택한 값이 모든 차트에 반영되도록 합니다.

대시보드에 대한 전역 필터를 만들면 해당 전역 필터에 대한 토글을 위젯 작성기의 일부로 사용할 수 있습니다.

![전역 필터 토글이 강조 표시된 위젯 작성기입니다.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>전역 필터 매개 변수가 각 인사이트의 SQL에 포함되어 있는지 확인합니다.

## 글로벌 필터 선택 {#select-global-filter}

을(를) 열려면 [!UICONTROL 필터] 모든 사용자 정의 필터를 나열하는 대화 상자에서 필터 아이콘(![필터 아이콘](../../../images/customizable-insights/filter.png))을 클릭하여 제품에서 사용할 수 있습니다. 그런 다음 대시보드 인사이트에 효과를 적용하려면 전역 필터의 드롭다운 메뉴에서 옵션을 선택한 다음 을 선택합니다. **[!UICONTROL 적용]**.

![필터 대화 상자가 강조 표시된 사용자 지정 대시보드.](../../../images/customizable-insights/custom-filters.png)
