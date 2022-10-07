---
title: 계정 프로필 대시보드 안내서
description: Adobe Experience Platform은 조직의 B2B 계정 프로필에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 19d6d3c03e6b3b0f9f82ceeee30816fa054261a3
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 0%

---

# [!UICONTROL 계정 프로필] 대시보드

Adobe Experience Platform UI(사용자 인터페이스)는 일별 스냅샷 중에 캡처된 계정 프로필에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 [!UICONTROL 계정 프로필] 대시보드 를 참조하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

계정 프로필 사용자 인터페이스 내의 모든 기능에 대한 개요를 보려면 [계정 프로필 UI 안내서](../../rtcdp/accounts/account-profile-ui-guide.md).

## 시작하기

귀하는 [Real-time Customer Data Platform B2B 에디션](../../rtcdp/b2b-overview.md) B2B에 접근하기 위해 [!UICONTROL 계정 프로필] 대시보드 .

## 계정 프로필 데이터

다음 [!UICONTROL 계정 프로필] 대시보드는 마케팅 채널 전반에서 여러 소스의 통합 계정 정보와 조직에서 현재 고객 계정 정보를 저장하는 데 사용하는 다양한 시스템의 스냅샷을 표시합니다.

스냅샷의 프로필 데이터는 스냅샷을 가져온 특정 시점의 데이터와 동일하게 표시됩니다. 즉, 스냅샷은 데이터의 근사값이나 샘플이 아니며, [!UICONTROL 계정 프로필] 대시보드는 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 생성하기 때문에 데이터가 변경된 사항이나 업데이트는 다음 스냅샷을 가져올 때까지 대시보드에 반영되지 않습니다.

## 탐색 [!UICONTROL 계정 프로필] 대시보드

로 이동하려면 다음을 수행하십시오. [!UICONTROL 계정 프로필] 플랫폼 UI 내의 대시보드에서 **[!UICONTROL 프로필]** 아래에 [!UICONTROL 계정] 왼쪽 탐색 패널

![왼쪽 탐색 영역에 계정 프로필 이 있는 플랫폼 UI가 강조 표시되고 개요 탭이 표시됩니다.](../images/account-profiles/account-profiles-dashboard.png)

에서 [!UICONTROL 계정 프로필] 대시보드 [조직에 수집된 계정 프로필을 찾아봅니다](#browse-account-profiles), 또는 [위젯을 사용하여 계정 프로필 데이터 전체를 한 눈에 보기](#standard-widgets) 데이터의 이러한 시각화 측면.

## 계정 프로필 찾아보기 {#browse-account-profiles}

다음 [!UICONTROL 찾아보기] 탭에서는 연결된 엔터프라이즈 소스에서 계정 ID를 사용하거나 소스 세부 사항을 직접 입력하여 조직에 수집된 읽기 전용 계정 프로필을 검색하고 볼 수 있습니다. 여기에서 이름, 업계, 매출 및 세그먼트 등 계정 프로필에 속하는 중요한 정보를 볼 수 있습니다.

을(를) 선택합니다 [!UICONTROL 프로필 ID] 에 표시되는 결과에서 [!UICONTROL 찾아보기] 탭을 클릭하여 열기 [!UICONTROL 세부 사항] 계정 프로필에 대한 탭입니다.

![결과가 표시되고 프로필 ID가 강조 표시된 계정 프로필 찾아보기 탭이 있습니다.](../images/account-profiles/account-profiles-browse-tab.png)

에 표시되는 계정 프로필 정보 [!UICONTROL 세부 사항] 탭이 여러 프로필 조각에서 병합되어 개별 계정의 단일 보기를 형성했습니다. 다음 문서를 참조하십시오. [Real-time Customer Data Platform에서 계정 프로필 찾아보기](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 플랫폼 UI의 계정 프로필 보기 기능에 대해 자세히 알아보십시오.

## 다음 [!UICONTROL 계정 프로필] [!UICONTROL 개요] {#overview}

다음 [!UICONTROL 개요] 탭은 계정 프로필에 대한 중요한 정보를 전달하는 읽기 전용 지표를 제공하는 위젯으로 구성됩니다. 선택 **[!UICONTROL 대시보드 수정]** 의 모양을 변경하려면 [!UICONTROL 개요] 탭 - 위젯을 이동하고 크기를 조정하여

![수정 대시보드가 강조 표시된 계정 프로필 개요 탭.](../images/account-profiles/modify-dashboard.png)

다음 문서를 참조하십시오. [대시보드 수정](../customize/modify.md) 그리고 [위젯 라이브러리 개요](../customize/widget-library.md) 추가 정보

## 표준 위젯 {#standard-widgets}

Adobe은 계정 프로필과 관련된 다양한 지표를 시각화하는 데 사용할 수 있는 표준 위젯을 제공합니다.

사용 가능한 각 표준 위젯에 대해 자세히 알아보려면 다음 목록에서 위젯 이름을 선택하십시오.

* [산업별 총 계정](#total-accounts-by-industry)
* [추가된 계정 프로필](#account-profiles-added)
* [예측 점수 분배](#predictive-scoring-distribution)
* [예측 점수 책정 상위 영향력 있는 요소](#predictive-scoring-top-influential-factors)

### 산업별 총 계정 {#total-accounts-by-industry}

이 위젯은 단일 지표에 있는 총 계정 수를 표시하며 도넛 차트를 사용하여 전체 개수를 구성하는 산업에 대한 비례 크기의 개수를 나타냅니다. 키는 도넛 차트를 구성하는 다양한 산업을 위한 색상 코딩 정보를 제공합니다.

커서가 도넛 차트의 각 섹션을 마우스로 가리키면 대화 상자에 다양한 산업에 대한 개별 카운트가 표시됩니다.

![업계 위젯별 총 계정 수.](../images/account-profiles/total-accounts-by-industry-widget.png)

### 추가된 계정 프로필 {#account-profiles-added}

이 위젯에서는 지정된 기간 동안 계정에 추가된 프로필의 수와 이러한 추가된 프로필을 구성하는 다양한 산업의 비율을 나타내는 색상 코딩된 막대 차트를 사용합니다. 업종은 컬러로 구분되며, 키는 막대 차트를 구성하는 다양한 산업의 색상 코딩 정보를 제공합니다. 분석 기간은 위젯 드롭다운 메뉴에서 선택합니다. 막대 차트는 30일, 90일 및 12개월 기간에 대해 시각화할 수 있습니다.

>[!NOTE]
>
>프로필은 계정에만 추가되고 제거되지 않아 한 번에 추가된 프로필의 수가 가장 낮습니다.

![추가된 계정 프로필 위젯.](../images/account-profiles/accounts-profiles-added-widget.png)

### 예측 점수 분배 {#predictive-scoring-distribution}

다음 [!UICONTROL 예측 점수 분배] 위젯은 모든 계정 프로필의 점수 분포를 표시하여 판매 파이프라인의 상태를 한 눈에 파악할 수 있습니다. 점수 데이터는 도넛 차트와 열 차트를 통해 전달됩니다.

도넛 차트는 높은, 중간 및 낮은 버킷 구매 성향 각에서 총 계정 프로필의 비율을 보여줍니다. 키는 점수 버킷 범위 및 해당 범위의 계정 프로필 수를 포함하여 색상 코딩된 섹션에 대한 자세한 정보를 제공합니다.

열 차트는 보다 세부적인 점수 분류를 제공합니다. 각 열에는 20개의 5포인트 증분 버킷의 계정 프로필 수가 표시됩니다.

위젯 내의 드롭다운 메뉴를 사용하면 계정 점수 모델을 선택할 수 있습니다.

![예측 점수 분배 위젯.](../images/account-profiles/predictive-scoring-distribution.png)

### 예측 점수 책정 상위 영향력 있는 요소 {#predictive-scoring-top-influential-factors}

다음 [!UICONTROL 예측 점수 책정 상위 영향력 있는 요소] 위젯을 사용하면 각 성향 버킷의 점수를 유도하는 가장 중요한 요소를 이해할 수 있습니다.

이 위젯은 높은, 중간 및 낮은 성향 버킷에 대해 가장 영향력 있는 요소를 보여줍니다. 각 영향력 있는 인자에 대한 막대는 특정 영향을 주는 요소를 포함하는 성향 버킷의 계정 프로필의 비율을 나타냅니다.

위젯 내의 드롭다운 메뉴를 사용하면 계정 점수 모델을 선택할 수 있습니다.

![예측 점수 책정 상위 영향력 있는 요소 위젯.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 다음 단계

이 문서를 따라 다음을 찾는 방법을 알아야 합니다 [!UICONTROL 계정 프로필] 대시보드 . 사용 가능한 위젯에 표시되는 지표도 이해해야 합니다. Experience Platform UI에서 B2B 데이터의 일부로 계정 프로필 작업에 대한 자세한 내용은 [계정 프로필 개요](../../rtcdp/accounts/account-profile-overview.md) Adobe Real-Time CDP용 B2B Edition.
