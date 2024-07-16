---
title: Query Pro 모드
description: Adobe Experience Platform UI에서 SQL 쿼리를 사용하여 사용자 정의 대시보드용 차트를 생성하는 방법에 대해 알아봅니다.
exl-id: 15c664c4-8546-4e04-b81d-c78bf83500d3
source-git-commit: 5bb954da7c1e05922a4e0f8d0bc7d3ab5c8e0e58
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# 쿼리 프로 모드 {#query-pro-mode}

쿼리 프로 모드는 Adobe Experience Platform UI에서 사용자 지정 SQL 쿼리를 통해 인사이트를 생성하는 프로세스를 안내하는 SQL 편집기 기반 워크플로우입니다. 사용자 지정 SQL 쿼리를 사용하여 인사이트를 생성하려면 먼저 [대시보드를 만들기](./overview.md#create-custom-dashboard)해야 합니다.

## SQL 구성 {#compose-sql}

쿼리 프로 모드로 대시보드를 만들도록 선택하면 **[!UICONTROL SQL 입력]** 대화 상자가 나타납니다. 드롭다운 메뉴에서 쿼리할 데이터베이스(인사이트 데이터 모델)를 선택하고 쿼리 프로 편집기에서 데이터 세트에 적합한 쿼리를 입력합니다.

>[!NOTE]
>
>Query pro 모드는 Data Distiller SKU를 구매한 사용자만 사용할 수 있습니다. [[!UICONTROL 디자인 모드]](../../user-defined-dashboards.md)는 모든 사용자가 기존의 데이터 모델에서 인사이트를 만들 수 있습니다.

UI 요소에 대한 자세한 내용은 [쿼리 편집기 사용 안내서](../../../query-service/ui/user-guide.md#query-authoring)를 참조하십시오.

![데이터 집합 드롭다운 메뉴와 실행 아이콘이 강조 표시된 [!UICONTROL SQL 입력] 대화 상자, 대화 상자에 채워진 SQL 쿼리와 쿼리 매개 변수 탭이 표시됩니다.](../../images/customizable-insights/enter-sql-database-dropdown.png)

### 쿼리 매개변수 {#query-parameters}

[전역](./filters/global-filter.md) 또는 [날짜 필터](./filters/date-filter.md)을(를) 포함하려면 쿼리 **must**&#x200B;를 사용하십시오. Query pro 모드에서 명령문을 작성할 때 쿼리에서 쿼리 매개 변수를 사용하는 경우 샘플 값을 제공해야 합니다. 샘플 값을 사용하면 SQL 문을 실행하고 차트를 작성할 수 있습니다. 문을 작성할 때 제공하는 샘플 값은 런타임 시 날짜 또는 글로벌 필터에 대해 선택하는 실제 값으로 대체됩니다.



>[!IMPORTANT]
>
>전역 필터를 사용하려면 SQL에 쿼리 매개 변수를 배치한 다음 해당 쿼리 매개 변수를 위젯 작성기의 전역 필터에 연결해야 합니다. 아래 스크린샷에서는 `CONSENT_VALUE_FILTER`이(가) SQL에서 전역 필터에 대한 쿼리 매개 변수로 사용됩니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [전역 필터 설명서](./filters/global-filter.md#enable-global-filter)를 참조하세요.

쿼리를 실행하려면 실행 아이콘(![실행 아이콘)을 선택합니다.](../../images/customizable-insights/run-icon.png)). 쿼리 편집기에 결과 탭이 표시됩니다. 그런 다음 구성을 확인하고 위젯 작성기를 열려면 **[!UICONTROL 선택]**&#x200B;을 선택합니다.

>[!TIP]
>
>쿼리에서 쿼리 매개 변수를 사용하는 경우 쿼리를 한 번 실행하여 사용된 모든 쿼리 매개 변수 키를 미리 채웁니다. 쿼리는 실패하지만 UI에 쿼리 매개 변수 탭이 자동으로 표시되고 포함된 키가 모두 나열됩니다. 키에 적절한 값을 추가합니다.

![SQL 입력이 있는 [!UICONTROL SQL 입력] 대화 상자, 결과 탭, 선택 강조 표시.](../../images/customizable-insights/enter-sql-select.png)

## 위젯 채우기 {#populate-widget}

이제 위젯 작성기가 실행된 SQL의 열로 채워집니다. 대시보드 유형은 왼쪽 위에 표시되어 있습니다. 이 경우 [!UICONTROL 수동 SQL 항목]입니다. 연필 아이콘(![연필 아이콘)을 선택합니다.언제든지 SQL을 편집할 수 있습니다.](../../images/customizable-insights/edit-icon.png)

>[!TIP]
>
>사용 가능한 속성은 실행된 SQL에서 가져온 열입니다.

위젯을 만들려면 [!UICONTROL 특성] 열에 나열된 특성을 사용합니다. 검색 창을 사용하여 속성을 찾거나 목록을 스크롤할 수 있습니다.

![생성 방법 및 특성 열이 강조 표시된 위젯 작성기입니다.](../../images/customizable-insights/creation-method-and-attribute-column.png)

### 속성 추가 {#add-attributes}

위젯에 특성을 추가하려면 더하기 아이콘(![더하기 아이콘)을 선택합니다.](../../images/customizable-insights/add-icon.png))을 클릭합니다. 표시되는 드롭다운 메뉴를 사용하여 SQL에서 결정한 옵션에서 차트에 속성을 추가할 수 있습니다. 차트 유형마다 X축 및 Y축 드롭다운과 같은 옵션이 다릅니다.

이 도넛 차트 예제에서 옵션은 크기와 색상입니다. 색상은 도넛 차트 결과를 분류하며 크기는 사용된 실제 지표입니다. [!UICONTROL 색상] 필드에 특성을 추가하여 해당 특성의 구성에 따라 결과를 다른 색상으로 분할합니다.

>[!TIP]
>
>위쪽 및 아래쪽 화살표 아이콘(![위쪽 및 아래쪽 화살표 아이콘막대 또는 선 차트에서 X축과 Y축의 배열을 전환합니다.](../../images/customizable-insights/switch-axis-icon.png)

![추가 아이콘 드롭다운과 스위치 화살표가 강조 표시된 위젯 작성기입니다.](../../images/customizable-insights/add-icon-and-switch-arrows.png)

위젯의 그래프 또는 차트 유형을 변경하려면 [!UICONTROL 표시] 드롭다운에서 사용 가능한 옵션을 선택하십시오. 옵션에는 [!UICONTROL 줄], [!UICONTROL 도넛], [!UICONTROL 큰 숫자] 및 [!UICONTROL 막대]가 있습니다. 선택하면 위젯의 현재 설정에 대한 미리보기 시각화가 생성됩니다.

![위젯 미리 보기가 강조 표시된 위젯 작성기입니다.](../../images/customizable-insights/widget-preview.png)

## 위젯 속성 {#properties}

속성 아이콘(![속성 아이콘)을 선택합니다.](../../images/customizable-insights/properties-icon.png))을(를) 오른쪽 레일에서 클릭하여 속성 패널을 엽니다. [!UICONTROL 속성] 패널에서 **[!UICONTROL 위젯 제목]** 텍스트 필드에 위젯 이름을 입력합니다. 차트의 다양한 측면 이름을 변경할 수도 있습니다.

>[!NOTE]
>
>속성 사이드바에서 사용할 수 있는 특정 필드는 편집 중인 차트 유형에 따라 다릅니다.

![속성 아이콘과 위젯 제목 필드가 강조 표시된 위젯 작성기입니다.](../../images/customizable-insights/widget-properties-title-text.png)

## 위젯 저장 {#save-widget}

위젯 작성기에 저장하면 위젯이 대시보드에 로컬로 저장됩니다. 작업을 저장하고 나중에 다시 시작하려면 **[!UICONTROL 저장]**&#x200B;을 선택하세요. 위젯 이름 아래에 있는 확인 표시 아이콘은 위젯이 저장되었음을 나타냅니다. 또는 위젯에 만족하면 **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택하여 대시보드에 액세스할 수 있는 다른 모든 사용자가 위젯을 사용할 수 있도록 합니다. 작업을 포기하고 사용자 지정 대시보드로 돌아가려면 취소를 선택합니다.

![저장, 위젯 저장, 저장 및 닫기가 강조 표시된 위젯 작성기입니다.](../../images/customizable-insights/insight-saved.png)

## 대시보드 및 차트 편집 {#edit}

전체 대시보드나 인사이트를 편집하려면 **[!UICONTROL 편집]**&#x200B;을 선택하세요. 편집 모드에서 위젯의 크기를 조정하거나 SQL을 편집하거나 전역 및 임시 필터를 만들고 적용할 수 있습니다. 이 필터는 대시보드 위젯에 표시되는 데이터를 제한합니다. 다양한 사용 사례에 대한 통찰력을 신속하게 업데이트하고 세부 조정할 수 있는 편리한 방법입니다.

![편집이 강조 표시된 사용자 지정 대시보드입니다.](../../images/customizable-insights/edit-dashboard.png)

**[!UICONTROL 필터 추가]**&#x200B;를 선택하여 [[!UICONTROL 날짜 필터]](#create-date-filter) 또는 [[!UICONTROL 전역 필터]](#create-global-filter)를 만듭니다. 만든 후에는 [필터 아이콘](#select-global-filter)(![필터 아이콘에서 모든 전역 및 날짜 필터를 사용할 수 있습니다.](../../images/customizable-insights/filter.png))을(를) 사용합니다.

![필터 추가 드롭다운 메뉴가 강조 표시된 사용자 지정 대시보드입니다.](../../images/customizable-insights/add-filter.png)

## 인사이트 편집, 복제 또는 삭제

[기존 위젯을 편집, 복제 또는 삭제하는 방법](../../user-defined-dashboards.md#duplicate)에 대한 지침은 사용자 지정 대시보드 안내서를 참조하십시오.

## 다음 단계

이제 이 문서를 읽고 Adobe Experience Platform UI에서 SQL 쿼리를 작성하여 사용자 정의 대시보드에 대한 차트를 생성하는 방법을 알 수 있습니다. 다음으로, [날짜 필터를 만들기](./filters/date-filter.md) 또는 [전역 필터를 만들기](./filters/global-filter.md)하여 데이터를 더 보강하는 방법을 알아보세요.

[SQL 분석 데이터에 대한 다양한 보기 옵션](./view-more.md) 또는 [사용자 지정 인사이트 뒤에 있는 SQL을 보는 방법](./view-sql.md)을 포함하여 다른 사용자 지정 인사이트 기능에 대해서도 자세히 알아볼 수 있습니다.
