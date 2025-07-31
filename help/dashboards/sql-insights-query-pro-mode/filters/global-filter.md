---
title: 글로벌 필터 만들기
description: 사용자 지정 전역 적용 필터를 사용하여 데이터 인사이트를 필터링하는 방법을 알아봅니다.
exl-id: a0084039-8809-4883-9f68-c666dcac5881
source-git-commit: 60b0c73766c89b98685810b4f58cfe1a40316dc9
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# 글로벌 필터 만들기 {#create-global-filter}

전역 필터를 만들려면 먼저 대시보드 보기에서 **[!UICONTROL 필터 추가]**&#x200B;를 선택한 다음 드롭다운 메뉴에서 **[!UICONTROL 전역 필터]**&#x200B;를 선택하십시오.

>[!IMPORTANT]
>
>전역 필터를 모든 차트에 매핑하는지 확인합니다. 이것은 자동 프로세스가 아닙니다. 전역 필터를 사용하려면 차트의 SQL에 [쿼리 매개 변수](../../../query-service/ui/parameterized-queries.md)를 포함하고, 위젯 작성기에서 [전역 필터를 사용하도록 설정](#enable-global-filter)하고, 전역 필터 대화 상자에서 매개 변수에 대한 [런타임 값을 선택](#select-global-filter)해야 합니다. 쿼리 매개 변수를 통합해야 하는 경우 SQL을 편집하는 방법은 query pro guide를 참조하십시오.

![필터 추가 및 드롭다운 메뉴가 강조 표시된 사용자 지정 대시보드입니다.](../../images/sql-insights-query-pro-mode/add-filter.png)

사용자 지정된 전역 필터를 사용하여 SQL에서 제공하는 통찰력을 빠르게 변경할 수 있습니다.

[!UICONTROL 전역 필터 만들기] 대화 상자가 열립니다. 전역 필터를 만드는 것은 SQL을 사용하여 insight을 만드는 것과 동일한 프로세스를 따릅니다. 먼저 쿼리할 데이터베이스(Insights 데이터 모델)를 선택한 다음 쿼리 편집기에서 사용자 지정 SQL을 입력하고 마지막으로 실행 아이콘(![실행 아이콘.](/help/images/icons/play.png))을 선택합니다.

>[!IMPORTANT]
>
>글로벌 필터를 만들 때 ID와 값을 포함해야 합니다. 샘플 값을 사용하면 SQL 문을 실행하고 차트를 작성할 수 있습니다. 문을 작성할 때 제공하는 샘플 값은 런타임 시 날짜 또는 글로벌 필터에 대해 선택하는 실제 값으로 대체됩니다.

쿼리를 성공적으로 실행하면 결과 탭에 결과가 표시됩니다. **[!UICONTROL 다음]**&#x200B;을 선택합니다.

>[!NOTE]
>
>쿼리 결과는 기본적으로 100개의 행으로 제한됩니다. 행을 더 많이 반환하려면 원하는 행 수로 SQL 쿼리에 LIMIT 절을 추가합니다. 모든 행을 검색하고 기본 제한을 제거하려면 쿼리에 LIMIT 0을 사용합니다.

![데이터 집합 드롭다운 메뉴, 실행 아이콘 및 다음을 강조 표시한 [!UICONTROL 전역 필터 대화 상자 만들기].](../../images/sql-insights-query-pro-mode/global-filter.png)

전역 필터 생성 워크플로우의 마지막 단계에서는 필터에 대한 레이블을 추가해야 합니다. **[!UICONTROL 필터 레이블]** 텍스트 필드에 레이블을 추가하고 드롭다운 상자에서 필터 유형을 선택합니다.

>[!NOTE]
>
>현재 [!UICONTROL 콤보 상자] 필터 유형 옵션만 지원됩니다.

마지막으로 **[!UICONTROL 선택]**&#x200B;을 선택하여 대시보드 보기로 돌아갑니다.

![선택 및 필터 레이블 텍스트 입력이 강조 표시된 [!UICONTROL 전역 필터 대화 상자 만들기]입니다.](../../images/sql-insights-query-pro-mode/global-filter-label.png)

## 각 insight에 대한 글로벌 필터 활성화 {#enable-global-filter}

>[!TIP]
>
>생성하는 모든 차트에서 전역 필터를 활성화합니다. 이렇게 하면 전역 필터로 선택한 값이 모든 차트에 반영되도록 합니다.

대시보드에 대한 전역 필터를 만들면 해당 전역 필터에 대한 토글을 위젯 작성기의 일부로 사용할 수 있습니다.

![전역 필터 토글이 강조 표시된 위젯 작성기입니다.](../../images/sql-insights-query-pro-mode/global-filter-consent.png)

>[!IMPORTANT]
>
>전역 필터 매개 변수가 각 insight의 SQL에 포함되어 있는지 확인합니다.

## 글로벌 필터 선택 {#select-global-filter}

모든 사용자 지정 필터를 나열하는 [!UICONTROL 필터] 대화 상자를 열려면 필터 아이콘(![필터 아이콘)을 선택합니다.](/help/images/icons/filter.png))을(를) 클릭합니다. 그런 다음 대시보드 인사이트에 효과를 적용하려면 전역 필터의 드롭다운 메뉴에서 옵션을 선택한 다음 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![필터 대화 상자가 강조 표시된 사용자 지정 대시보드입니다.](../../images/sql-insights-query-pro-mode/custom-filters.png)

## 전역 필터 지우기 {#clear-global-filter}

사용자 지정 전역 필터를 모두 지우려면 **[!UICONTROL 필터]** 대화 상자에서 [!UICONTROL 모두 지우기]를 선택하십시오.

![모두 지우기가 강조 표시된 필터 대화 상자입니다.](../../images/sql-insights-query-pro-mode/clear-all.png)
