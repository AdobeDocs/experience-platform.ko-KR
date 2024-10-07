---
title: 더 보기
description: SQL 분석 데이터를 보는 다양한 옵션에 대해 알아봅니다. 사용자 지정 대시보드에서 분석 표의 결과를 보거나 처리된 데이터를 CSV 형식으로 다운로드할 수 있습니다.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: 1ef8208ccde2f44b6c5188bd5b9a57ff876da30f
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# 더 보기 {#view-more}

[쿼리 프로 모드](./overview.md)로 [사용자 지정 인사이트](../sql-insights/overview.md)를 만들면 차트 데이터를 다른 형식으로 볼 수 있습니다. 표 형식의 결과를 보거나 데이터를 CSV 파일로 다운로드하여 스프레드시트에서 볼 수 있습니다.

## 표로 정리된 결과 {#tabulated-results}

SQL을 통해 쿼리 프로 모드를 사용하여 작성된 모든 차트에 대해 Experience Platform UI 내에서 분석 결과가 표로 정리되어 표시됩니다.

사용자 지정 대시보드에서 위젯의 줄임표(`...`)를 선택하여 [!UICONTROL 자세히 보기] 및 [!UICONTROL SQL 보기] 옵션에 액세스합니다.

![인사이트의 줄임표 드롭다운 메뉴와 자세히 보기 및 SQL 보기 옵션이 강조 표시된 사용자 지정 대시보드입니다.](../../images/sql-insights/ellipses-dropdown.png)

## CSV 다운로드 {#download-csv}

[!UICONTROL 자세히 보기] 기능은 차트의 특정 데이터 포인트를 표 형식으로 표시합니다. 데이터 공유 및 조작 프로세스를 단순화하기 위해 이 대화 상자에서 처리된 데이터를 CSV 형식으로 다운로드할 수 있습니다. 데이터를 다운로드하려면 **[!UICONTROL CSV 다운로드]**&#x200B;를 선택하십시오.

>[!NOTE]
>
>CSV 다운로드는 처음 500개 레코드로 제한됩니다.

![인사이트 미리 보기 및 인사이트를 생성한 SQL의 표로 정리된 결과를 표시하는 대화 상자입니다.](../../images/query-pro-mode/view-more-download-csv.png)

## 열별 정렬 {#sort-column}

테이블화된 결과를 볼 때 정렬 기능을 사용하여 오름차순 또는 내림차순으로 열을 정렬할 수 있습니다. 사용자 지정 대시보드에서 테이블의 줄임표(`...`)를 선택하여 [!UICONTROL 자세히 보기] 옵션에 액세스합니다.

![테이블의 줄임표 드롭다운 메뉴와 [자세히 보기] 옵션이 강조 표시된 사용자 지정 대시보드입니다.](../../images/query-pro-mode/advanced-ellipses-dropdown.png)

열 이름 옆에 있는 드롭다운 메뉴를 선택한 다음 **[!UICONTROL 오름차순 정렬]** 또는 **[!UICONTROL 내림차순 정렬]**&#x200B;을 선택하여 열을 정렬할 수 있습니다.

>[!NOTE]
>
>[!UICONTROL 오름차순 정렬] 및 [!UICONTROL 내림차순 정렬] 옵션은 [정렬 기능](./overview.md#advanced-attributes)(으)로 구성된 열에 대해서만 표시됩니다.

![오름차순 정렬 및 내림차순 정렬 옵션을 강조 표시하는 테이블 열 드롭다운입니다.](../../images/query-pro-mode/advanced-sort-dropdown.png)

## 열 크기 조정 {#resize-column}

표 형식의 결과에서 열 크기를 조정하여 데이터 가독성을 향상시킬 수 있습니다. 사용자 지정 대시보드에서 테이블의 줄임표(`...`)를 선택하여 [!UICONTROL 자세히 보기] 옵션에 액세스합니다. 열 이름 옆에 있는 드롭다운 메뉴를 사용하여 크기를 조정한 다음 **[!UICONTROL 열 크기 조정]**&#x200B;을 선택합니다.

![열 크기 조정 옵션이 강조 표시된 표 열 드롭다운입니다.](../../images/query-pro-mode/advanced-resize-dropdown.png)

슬라이더를 선택하고 왼쪽 또는 오른쪽으로 드래그하여 필요에 따라 열 크기를 조정합니다.

![열 크기 조정 막대를 강조 표시한 표입니다.](../../images/query-pro-mode/advanced-resize-column.png)

## 표 페이지 매김 {#table-pagination}

페이지 매김은 [!UICONTROL 자세히 보기] 기능의 테이블에 자동으로 적용되므로 SQL 쿼리를 수동으로 수정할 필요가 없습니다. 이 기능을 사용하면 데이터가 보다 관리하기 쉬운 형식으로 표시되므로 큰 데이터 세트를 탐색하는 프로세스를 쉽게 수행할 수 있습니다.

페이지당 최대 500개의 레코드를 볼 수 있습니다. 레코드를 탐색하려면 페이지 아래쪽에 있는 **[!UICONTROL >]**&#x200B;을(를) 사용합니다.

![결과 및 페이지 매김이 강조 표시된 표 형식의 결과입니다.](../../images/query-pro-mode/advanced-table-pagination.png)

## 다음 단계

이제 이 문서를 읽고 나면 사용자 지정 차트의 SQL 분석의 표로 정리된 결과를 보고 데이터를 CSV 파일로 다운로드하는 방법을 알 수 있습니다. SQL 보기 문서를 참조하여 [사용자 지정 인사이트 뒤에 있는 SQL을 보는 방법](./view-more.md)을 알아보십시오.

[안내 디자인 모드 가이드](../../user-defined-dashboards.md)를 사용하여 Adobe Experience Platform UI에서 기존 데이터 모델에서 차트를 생성하는 방법을 배울 수도 있습니다.
