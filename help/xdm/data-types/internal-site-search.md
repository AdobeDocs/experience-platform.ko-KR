---
title: 내부 사이트 검색 데이터 유형
description: 이 문서에서는 내부 사이트 검색 XDM 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# [!UICONTROL 내부 사이트 검색] 데이터 유형

[!UICONTROL 내부 사이트 검색] 는 모든 관련 검색 동작 및 세부 사항을 포함하여 내부 사이트 검색을 설명하는 표준 XDM 데이터 유형입니다.

![](../images/data-types/internal-site-search.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL 부울] | 방문자가 검색을 실행하기 위해 제안된 검색 값 또는 자동 완성된 검색 값을 사용했는지 여부를 나타냅니다. |
| `autoCompleteTypedValue` | [!UICONTROL 문자열] | 자동 완성 시나리오의 경우 사용자가 때때로 검색을 포기하고 드롭다운에서 특정 용어를 선택합니다. 이 값은 특정 제안된 검색어 세트를 생성하기 위해 사용자가 입력하기 시작한 항목을 추적합니다. |
| `autoCompleteValue` | [!UICONTROL 문자열] | 자동 완성 시나리오의 경우 사용자가 때때로 검색을 포기하고 드롭다운 메뉴에서 특정 용어를 선택합니다. 이 값은 선택한 특정 용어를 추적하는 데 사용됩니다. |
| `instances` | [!UICONTROL 정수] | 내부 사이트 검색이 발생한 횟수입니다. |
| `locationInPage` | [!UICONTROL 문자열] | 페이지에 여러 개의 검색 상자가 있는 경우 이 값을 사용하여 사용자가 검색하는 데 사용한 특정 위치를 식별해야 합니다. |
| `nullInstances` | [!UICONTROL 정수] | 0개의 결과를 제공한 내부 사이트 검색이 발생한 횟수입니다. |
| `numberOfResults` | [!UICONTROL 정수] | 반환된 총 검색 결과 수입니다. |
| `postalCode` | [!UICONTROL 문자열] | 해당되는 경우 검색에 사용되는 우편 번호입니다. |
| `productFindingMethods` | [!UICONTROL 문자열] | 머천다이징 바인딩이 있는 내부 사이트 검색어 값입니다. 이 값은 제품을 보기 전에 즉시 검색한 단어를 나타냅니다. |
| `radiusDistance` | [!UICONTROL 정수] | 결합 `radiusType`은 검색 반경의 선택한 거리를 나타냅니다. |
| `radiusType` | [!UICONTROL 정수] | 선택한 거리 유형 `radiusDistance`5km 또는 km입니다. |
| `refinementInstances` | [!UICONTROL 정수] | 내부 사이트 검색이 세분된 횟수입니다. |
| `refinementType` | 문자열 배열 | 검색 결과에 적용된 구체화 유형을 나열합니다. 예를 들면 부서, 브랜드, 가격, 매장 내, 리뷰 등급, 색상, 재료 등이 있습니다. |
| `refinementValue` | [!UICONTROL 문자열] | 검색이 재지정된 값입니다. |
| `resultsPageNumber` | [!UICONTROL 정수] | 페이지 매김된 검색 결과의 경우 이 값은 방문자가 보고 있는 결과 페이지를 추적합니다. |
| `resultsPerPage` | [!UICONTROL 정수] | 페이지 매김된 검색 결과의 경우 이 값은 페이지당 표시되는 검색 결과 수를 추적합니다. |
| `searchType` | [!UICONTROL 문자열] | 해당되는 경우 실행될 검색 방법을 캡처합니다. 예를 들면 자동 완성 검색, 직접 입력 검색 또는 사이트에 있을 수 있는 기타 유형의 사용자 지정 검색 기능이 있습니다. |
| `sortOrder` | [!UICONTROL 문자열] | 결합 `sortType`, 검색 결과의 정렬 순서를 오름차순 또는 내림차순으로 나타냅니다. |
| `term` | [!UICONTROL 문자열] | 방문자가 입력한 내부 사이트 검색어입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
