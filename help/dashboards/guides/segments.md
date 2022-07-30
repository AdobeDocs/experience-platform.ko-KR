---
keywords: Experience Platform;프로필;세그먼트;세그먼트;세그먼테이션;사용자 인터페이스;UI;사용자 지정;세그먼트 대시보드;대시보드
title: 세그먼트 대시보드
description: 'Adobe Experience Platform은 조직이 만든 세그먼트에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: e1d44c453385b8beaa49e9793eb4858876d865b0
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 0%

---

# 세그먼트 대시보드 {#segment-dashboard}

Adobe Experience Platform UI(사용자 인터페이스)는 일별 스냅샷 중에 캡처된 대로 세그먼트에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 세그먼트 대시보드에 액세스하고 작업하는 방법을 간략하게 설명하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

플랫폼 사용자 인터페이스 내의 모든 Adobe Experience Platform 세그멘테이션 서비스 기능에 대한 개요를 알려면 [세그멘테이션 서비스 UI 안내서](../../segmentation/ui/overview.md).

## 세그먼트 대시보드 데이터

세그먼트 대시보드는 Experience Platform의 프로필 저장소 내에 조직에서 가지고 있는 속성(레코드) 데이터의 스냅숏을 표시합니다. 스냅샷에는 이벤트(시계열) 데이터가 포함되지 않습니다.

스냅샷의 속성 데이터는 스냅샷을 가져온 특정 시점의 데이터와 동일하게 표시됩니다. 즉, 스냅샷은 데이터의 근사 또는 샘플이 아니며, 세그먼트 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 생성하기 때문에 데이터가 변경된 사항이나 업데이트는 다음 스냅샷을 가져올 때까지 대시보드에 반영되지 않습니다.

## 세그먼트 대시보드 탐색

로 이동하려면 다음을 수행하십시오. [!UICONTROL 세그먼트] 플랫폼 UI 내의 대시보드에서 **[!UICONTROL 세그먼트]** 왼쪽 레일에서 **[!UICONTROL 개요]** 탭을 클릭하여 대시보드를 표시합니다.

>[!NOTE]
>
>조직이 Platform을 처음 사용하고 아직 활성 프로필 데이터 세트 또는 병합 정책이 만들어지지 않은 경우, [!UICONTROL 세그먼트] 대시보드가 표시되지 않습니다. 대신, [!UICONTROL 개요] 탭에는 세그먼테이션을 시작하는 데 도움이 되는 링크 및 설명서가 표시됩니다.

![](../images/segments/dashboard-overview.png)

### 수정 [!UICONTROL 세그먼트] 대시보드

의 모양을 수정할 수 있습니다 [!UICONTROL 세그먼트] 선택하여 대시보드 **[!UICONTROL 대시보드 수정]**. 이를 통해 대시보드에서 위젯을 이동, 추가 및 제거할 수 있을 뿐만 아니라 **[!UICONTROL 위젯 라이브러리]** 사용 가능한 위젯을 살펴보고 조직에 대한 사용자 지정 위젯을 만들려면

자세한 내용은 [대시보드 수정](../customize/modify.md) 및 [위젯 라이브러리 개요](../customize/widget-library.md) 설명서 를 참조하십시오.

## 세그먼트 선택

대시보드는 표시할 세그먼트를 자동으로 선택하지만 드롭다운 메뉴 또는 세그먼트 선택기를 사용하여 세그먼트를 변경할 수 있습니다.

다른 세그먼트를 선택하려면 세그먼트 이름 옆에 있는 드롭다운을 선택하거나 세그먼트 선택기를 사용하여 세그먼트 선택 대화 상자를 엽니다.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## 위젯 및 지표

세그먼트 대시보드는 위젯으로 구성되며, 위젯은 선택한 세그먼트에 대한 중요한 정보를 제공하는 읽기 전용 지표입니다.

가장 최근 스냅샷의 날짜 및 시간이 [!UICONTROL 개요] 세그먼트 드롭다운 옆에 있는 탭입니다. 모든 위젯 데이터는 해당 날짜 및 시간에 따라 정확합니다. 스냅샷의 타임스탬프는 UTC로 제공됩니다. 개별 사용자 또는 조직의 시간대에 있지 않습니다.

![위젯 타임스탬프가 강조 표시된 세그먼트 개요 탭.](../images/segments/widget-timestamp.png)

## 표준 위젯 {#standard-widgets}

Adobe은 세그먼트와 관련된 다양한 지표를 시각화하는 데 사용할 수 있는 여러 표준 위젯을 제공합니다. 또한 [!UICONTROL 위젯 라이브러리]. 사용자 지정 위젯을 만드는 방법에 대해 자세히 알아보려면 [위젯 라이브러리 개요](../customize/widget-library.md).

사용 가능한 각 표준 위젯에 대해 자세히 알아보려면 다음 목록에서 위젯 이름을 선택하십시오.

* [[!UICONTROL 대상 크기]](#audience-size)
* [[!UICONTROL Audience Activation 순서]](#audience-activation-order)
* [[!UICONTROL 대상 크기 트렌드]](#audience-size-trend)
* [[!UICONTROL 대상 크기 변경 트렌드]](#audience-size-change-trend)
* [[!UICONTROL ID별 대상 크기 트렌드]](#audience-size-trend-by-identity)
* [[!UICONTROL 대상 겹치기]](#audience-overlap)
* [[!UICONTROL ID 겹치기]](#identity-overlap)
* [[!UICONTROL ID별 프로필]](#profiles-by-identity)

### [!UICONTROL 대상 크기] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="대상 크기"
>abstract="이 위젯은 선택한 세그먼트 내에서 병합된 프로필의 총 수를 표시합니다. 이 번호는 데이터에 적용된 병합 정책에 따라 다르며 가장 최근 스냅숏이 있을 때 정확합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#audience-size" text="설명서에서 자세히 알아보기"

다음 **[!UICONTROL 대상 크기]** 위젯은 스냅숏을 만들 때 선택한 세그먼트 내의 병합된 총 프로필 수를 표시합니다. 이 숫자는 프로필 조각을 함께 병합하여 세그먼트의 각 개인을 위한 단일 프로필을 구성하기 위해 프로필 데이터에 세그먼트 병합 정책을 적용한 결과입니다.

조각 및 병합된 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL 대상 크기 트렌드] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="대상 크기 트렌드"
>abstract="이 위젯은 **임의** 일별 스냅샷 동안 캡처된 세그먼트 정의, 최근 30일, 90일 또는 12개월 동안의 세그먼트 정의."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#audience-size-trend" text="설명서에서 자세히 알아보기"

다음 **[!UICONTROL 대상 크기 트렌드]** 위젯은 의 기준을 충족하는 총 프로필 수에 대한 선 그래프 일러스트레이션을 제공합니다 **임의** 주어진 기간에 대한 세그먼트 정의. 대상 크기 트렌드는 30일, 90일 및 12개월 기간에 걸쳐 시각화할 수 있습니다. 기간은 위젯의 드롭다운 메뉴에서 선택됩니다. 대상 크기는 x축의 y축 및 시간에 반영됩니다.

이 위젯에는 자동 위젯도 포함되어 있습니다 [!UICONTROL 캡션] 기계 학습 모델이 차트 및 세그먼트 데이터를 분석하고 주요 트렌드와 중요 이벤트를 설명하는 캡션을 자동으로 생성하는 기능입니다. 선택 **[!UICONTROL 캡션]** 자동 캡션 대화 상자를 열려면 다음을 수행하십시오.

![세그먼트 개요는 대상 크기 트렌드 위젯을 표시합니다.](../images/segments/audience-size-trend-captions.png)

데이터에 대한 통찰력을 제공하는 자동 캡션 대화 상자가 열립니다.

![대상 크기 트렌드 위젯에 대한 자동 캡션 대화 상자입니다.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

세그먼트 평가 및 프로필이 세그먼트의 자격을 받고 종료하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [Segmentation Service 설명서](../../segmentation/home.md).

### [!UICONTROL 대상 크기 변경 트렌드] {#audience-size-change-trend}

이 위젯은 가장 최근 일별 스냅샷 간 주어진 세그먼트에 자격을 부여받은 프로필의 총 수 차이에 대한 선 그래프 그림을 제공합니다. 분석을 위해 선택한 세그먼트는 개요 드롭다운에서 선택됩니다. 트렌드 분석 기간은 30일, 90일 및 12개월 기간으로 시각화할 수 있습니다. 기간은 위젯의 드롭다운 메뉴에서 선택됩니다. 대상 크기는 x축의 y축 및 시간에 반영됩니다.

![대상 크기 변경 트렌드 위젯.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL ID별 대상 크기 트렌드] {#audience-size-trend-by-identity}

이 위젯은 위젯 드롭다운 메뉴에서 선택한 ID 유형을 기반으로 하여 특정 세그먼트에 대한 대상 크기 트렌드를 보여줍니다. 분석에 사용된 세그먼트는 개요 드롭다운에서 선택됩니다. 트렌드 분석 기간은 30일, 90일 및 12개월 기간으로 시각화할 수 있습니다. 기간은 위젯의 드롭다운 메뉴에서 선택됩니다.

![ID 위젯별 대상 크기 트렌드입니다.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Audience Activation 순서] {#audience-activation-order}

다음 [!UICONTROL Audience Activation 순서] 위젯은 [!UICONTROL 대상 이름], [!UICONTROL platform], 및 활성화 [!UICONTROL 날짜] 시청자. 목록은 최신성에 따라 높에서 낮이로 정렬되며 최대 10개의 행을 수용할 수 있습니다.

![대상 활성화 순서 위젯.](../images/segments/audience-activation-order.png)

### [!UICONTROL 대상 겹치기] {#audience-overlap}

이 위젯은 두 세그먼트 정의에 대한 기준을 충족하는 두 세그먼트의 프로필 수를 나타냅니다. 비교에 사용된 세그먼트는 위젯 드롭다운 메뉴에서 선택됩니다. 관련 세그먼트 정의에 포함된 총 프로필 수는 원 또는 벤 다이어그램의 교차 지점을 마우스로 가리키면 볼 수 있습니다.

이 위젯을 사용하면 세그먼트 정의 결과의 유사성을 시각화하여 세그멘테이션 전략을 최적화할 수 있습니다.

![대상 겹치기 위젯입니다.](../images/segments/audience-overlap.png)

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by Highest or Lowest overlap percentages. -->

<!-- ![The Audience overlap report widget.]() -->

<!-- https://jira.corp.adobe.com/browse/PLAT-125511 -->

### [!UICONTROL ID 겹치기] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="ID 겹치기"
>abstract="이 위젯은 선택한 ID가 모두 포함된 세그먼트에서 프로필의 겹침을 보여줍니다. 원은 각 ID의 상대 크기를 표시합니다. 두 네임스페이스가 모두 포함된 프로필 수는 원 간에 겹쳐서 표시됩니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#identity-overlap" text="설명서에서 자세히 알아보기"

다음 **[!UICONTROL ID 겹치기]** 위젯은 여러 ID가 포함된 세그먼트에서 프로필의 겹침을 보여주는 벤 다이어그램 또는 세트 다이어그램을 표시합니다.

위젯의 드롭다운 메뉴를 사용하여 비교할 ID를 선택합니다. 원은 선택한 각 ID의 상대 크기를 표시하며, 두 네임스페이스가 포함된 프로필의 수는 원 간에 겹치는 크기의 크기로 표시됩니다.

고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 ID가 해당 개별 고객과 연결되므로 조직에서 두 개 이상의 ID의 조각을 포함하는 여러 프로필을 가질 수 있습니다.

ID에 대해 자세히 알아보려면 [Adobe Experience Platform Identity Service 설명서](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL ID별 프로필] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="ID별 프로필"
>abstract="이 위젯은 선택한 세그먼트에 병합된 모든 프로필의 ID 분류를 표시합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#profiles-by-identity" text="설명서에서 자세히 알아보기"

다음 **[!UICONTROL ID별 프로필]** 위젯은 선택한 세그먼트에 병합된 모든 프로필의 ID 분류를 표시합니다. 한 프로필에는 여러 개의 ID가 연결되어 있을 수 있으므로 ID별 총 프로필 수는 세그먼트의 총 프로필 수보다 높을 수 있습니다. 즉, 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 ID가 해당 개별 고객과 연결될 수 있으므로 각 ID에 대해 표시된 값을 함께 추가하면 세그먼트에서 총 대상 크기보다 커질 수 있습니다.

선택 **[!UICONTROL 캡션]** 자동 캡션 대화 상자를 열려면 다음을 수행하십시오.

![ID 캡션별 프로필 대화 상자](../images/segments/profiles-by-identity.png)

기계 학습 모델은 데이터의 전체 분포 및 주요 차원을 분석하여 데이터 인사이트를 자동으로 생성합니다.

ID에 대해 자세히 알아보려면 [Adobe Experience Platform Identity Service 설명서](../../identity-service/home.md).

## 다음 단계

이 문서에 따라 세그먼트 대시보드를 찾고 보려는 세그먼트를 선택할 수 있습니다. 사용 가능한 위젯에 표시되는 지표도 이해해야 합니다. Experience Platform UI에서 세그먼트 작업에 대한 자세한 내용은 [세그멘테이션 서비스 UI 안내서](../../segmentation/ui/overview.md).
