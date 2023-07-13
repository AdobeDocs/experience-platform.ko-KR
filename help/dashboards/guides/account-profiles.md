---
title: 계정 프로필 대시보드 안내서
description: Adobe Experience Platform은 조직의 B2B 계정 프로필에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!UICONTROL 계정 프로필] 대시보드

Adobe Experience Platform UI(사용자 인터페이스)는 일별 스냅샷 중에 캡처된 계정 프로필에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 액세스 및 작업 방법을 간략하게 설명합니다. [!UICONTROL 계정 프로필] UI의 대시보드 및에서 대시보드에 표시된 시각화에 대한 자세한 정보를 제공합니다.

계정 프로필 사용자 인터페이스 내의 모든 기능에 대한 개요를 알려면 [계정 프로필 UI 안내서](../../rtcdp/accounts/account-profile-ui-guide.md).

## 시작하기

다음에 대한 권한이 있어야 합니다. [Adobe Real-time Customer Data Platform 에디션](../../rtcdp/b2b-overview.md) B2B에 액세스하려면 [!UICONTROL 계정 프로필] 대시보드입니다.

## 계정 프로필 데이터

다음 [!UICONTROL 계정 프로필] 대시보드에는 마케팅 채널 전반의 여러 소스에서 가져온 통합 계정 정보와 조직이 현재 고객 계정 정보를 저장하는 데 사용하는 다양한 시스템의 스냅샷이 표시됩니다.

스냅샷의 프로필 데이터는 스냅샷이 생성된 특정 시점에 나타나는 데이터를 정확하게 표시합니다. 즉, 스냅샷은 데이터의 근사값이나 샘플이 아니고 [!UICONTROL 계정 프로필] 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅숏을 만든 이후 데이터에 대한 변경 또는 업데이트는 다음 스냅숏을 만들 때까지 대시보드에 반영되지 않습니다.

## 탐색 [!UICONTROL 계정 프로필] 대시보드

로 이동하려면 [!UICONTROL 계정 프로필] Platform UI에서 대시보드를 선택한 다음 **[!UICONTROL 프로필]** 아래에 [!UICONTROL 계정] 을 클릭합니다.

![왼쪽 탐색 창에 계정 프로필이 있는 Platform UI가 강조 표시되고 개요 탭이 표시됩니다.](../images/account-profiles/account-profiles-dashboard.png)

다음에서 [!UICONTROL 계정 프로필] 대시보드 다음 중 하나를 수행할 수 있습니다. [조직에 수집된 계정 프로필 검색](#browse-account-profiles), 또는 [위젯을 사용하여 계정 프로필 데이터 전체를 한눈에 볼 수 있습니다](#standard-widgets) 데이터의 측면을 시각화합니다.

## 계정 프로필 찾아보기 {#browse-account-profiles}

다음 [!UICONTROL 찾아보기] 탭에서는 연결된 엔터프라이즈 소스의 계정 ID를 사용하거나 소스 세부 정보를 직접 입력하여 조직에 수집된 읽기 전용 계정 프로필을 검색하고 볼 수 있습니다. 여기에서 계정 프로필에 속하는 이름, 업계, 매출 및 기타 고객 등 중요한 정보를 볼 수 있습니다.

다음 항목 선택 [!UICONTROL 프로필 ID] 에 표시된 결과에서 [!UICONTROL 찾아보기] 탭을 클릭하여 열기 [!UICONTROL 세부 사항] 계정 프로필에 대한 탭입니다.

![결과가 표시되고 프로필 ID가 강조 표시된 계정 프로필 찾아보기 탭입니다.](../images/account-profiles/account-profiles-browse-tab.png)

다음에 표시되는 계정 프로필 정보 [!UICONTROL 세부 사항] 탭이 여러 프로필 조각에서 함께 병합되어 개별 계정에 대한 단일 보기를 형성했습니다. 다음에서 설명서를 참조하십시오. [Adobe Real-time Customer Data Platform에서 계정 프로필 찾아보기](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) platform UI의 계정 프로필 보기 기능에 대해 자세히 알아보십시오.

## 다음 [!UICONTROL 계정 프로필] [!UICONTROL 개요] {#overview}

다음 [!UICONTROL 개요] 탭은 계정 프로필에 대한 중요한 정보를 전달하기 위해 읽기 전용 지표를 제공하는 위젯으로 구성됩니다. 선택 **[!UICONTROL 대시보드 수정]** 의 모양을 변경하려면 [!UICONTROL 개요] 위젯을 이동하고 크기를 조정하여 탭합니다.

![[수정] 대시보드가 강조 표시된 계정 프로필 개요 탭](../images/account-profiles/modify-dashboard.png)

다음 문서를 참조하십시오. [대시보드 수정](../customize/modify.md) 및 [위젯 라이브러리 개요](../customize/widget-library.md) 자세히 알아보십시오.

## 표준 위젯 {#standard-widgets}

Adobe은 계정 프로필과 관련된 다양한 지표를 시각화하는 데 사용할 수 있는 표준 위젯을 제공합니다.

사용 가능한 각 표준 위젯에 대해 자세히 알아보려면 다음 목록에서 위젯의 이름을 선택합니다.

* [업종별 총 계정 수](#total-accounts-by-industry)
* [계정 프로필 추가됨](#account-profiles-added)
* [예측 채점 분포](#predictive-scoring-distribution)
* [예측 점수 가장 영향력 있는 요인](#predictive-scoring-top-influential-factors)

### 업종별 총 계정 수 {#total-accounts-by-industry}

이 위젯은 단일 지표에 총 계정 수를 표시하고 도넛 차트를 사용하여 전체 수를 구성하는 산업에 대한 카운트의 비례 크기를 보여 줍니다. 키는 도넛 차트를 구성하는 다양한 산업에 대한 색상 코딩 정보를 제공합니다.

커서가 도넛 차트의 각 섹션 위로 마우스를 가져가면 서로 다른 업계에 대한 개별 카운트가 대화 상자에 표시됩니다.

![업계 위젯별 총 계정 수.](../images/account-profiles/total-accounts-by-industry-widget.png)

### 계정 프로필 추가됨 {#account-profiles-added}

이 위젯은 색상으로 구분된 막대 차트를 사용하여 주어진 기간 동안 계정에 추가된 프로필 수와 이러한 추가된 프로필을 구성하는 다양한 업종의 비율을 보여 줍니다. 업종은 색상 코딩되어 있으며, 막대형 차트를 구성하는 다양한 업종에 대한 색상 코딩 정보를 제공하는 것이 핵심입니다. 분석 기간은 위젯 드롭다운 메뉴에서 선택됩니다. 막대 차트는 30일, 90일 및 12개월 기간에 걸쳐 시각화할 수 있습니다.

>[!NOTE]
>
>프로필은 계정에만 추가되고 제거되지 않으므로 일정 기간 동안 추가될 수 있는 최소 프로필 수는 0입니다.

![계정 프로필 추가 위젯입니다.](../images/account-profiles/accounts-profiles-added-widget.png)

### 예측 채점 분포 {#predictive-scoring-distribution}

다음 [!UICONTROL 예측 채점 분포] 위젯은 모든 계정 프로필의 점수 분포를 표시하여 판매 파이프라인의 상태를 한 눈에 파악할 수 있도록 합니다. 채점 데이터는 도넛 차트와 세로 막대형 차트를 통해 전달됩니다.

도넛 차트는 높은, 중간 및 낮은 버킷 구매 성향에서 총 계정 프로필의 비율을 보여 줍니다. 키는 채점 버킷 범위 및 해당 범위의 계정 프로필 수를 포함하여 색상으로 구분된 섹션에 대한 자세한 정보를 제공합니다.

열 차트는 보다 세분화된 점수 분류를 제공합니다. 각 열에는 20개의 5포인트 증분 버킷에 있는 계정 프로필의 수가 표시됩니다.

위젯 내의 드롭다운 메뉴에서 계정 채점 모델을 선택할 수 있습니다.

![예측 채점 배포 위젯.](../images/account-profiles/predictive-scoring-distribution.png)

### 예측 점수 가장 영향력 있는 요인 {#predictive-scoring-top-influential-factors}

다음 [!UICONTROL 예측 점수 가장 영향력 있는 요인] 위젯을 통해 각 성향 버킷의 점수를 유도하는 가장 중요한 요소를 이해할 수 있습니다.

이 위젯은 높은 성향 버킷, 중간 성향 버킷 및 낮은 성향 버킷 각각에 대해 가장 영향력 있는 요인을 표시합니다. 각 영향 요인에 대한 막대는 특정 영향 요인이 포함된 성향 버킷의 계정 프로필 백분율을 나타냅니다.

위젯 내의 드롭다운 메뉴에서 계정 채점 모델을 선택할 수 있습니다.

![예측 점수 최상위 영향력 있는 요소 위젯.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 다음 단계

이 문서를 따르면 이제 를 찾는 방법을 알 수 있습니다. [!UICONTROL 계정 프로필] 대시보드입니다. 사용 가능한 위젯에 표시되는 지표도 이해해야 합니다. Experience Platform UI에서 B2B 데이터의 일부로 계정 프로필을 사용하는 작업에 대한 자세한 내용은 다음을 참조하십시오. [계정 프로필 개요](../../rtcdp/accounts/account-profile-overview.md) Adobe Real-Time CDP, B2B 에디션용.
