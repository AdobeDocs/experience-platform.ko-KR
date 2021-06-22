---
keywords: Experience Platform;프로필;세그먼트;세그먼트;세그먼테이션;사용자 인터페이스;UI;사용자 지정;세그먼트 대시보드;대시보드
title: 세그먼트 대시보드
description: 'Adobe Experience Platform은 조직이 만든 세그먼트에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# 세그먼트 대시보드 {#segment-dashboard}

Adobe Experience Platform UI(사용자 인터페이스)는 일별 스냅샷 중에 캡처된 대로 세그먼트에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 세그먼트 대시보드에 액세스하고 작업하는 방법을 간략하게 설명하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

플랫폼 사용자 인터페이스 내의 모든 Adobe Experience Platform 세그멘테이션 서비스 기능에 대한 개요를 알려면 [세그멘테이션 서비스 UI 안내서](../../segmentation/ui/overview.md)를 방문하십시오.

## 세그먼트 대시보드 데이터

세그먼트 대시보드는 Experience Platform의 프로필 저장소 내에 조직에서 가지고 있는 속성(레코드) 데이터의 스냅숏을 표시합니다. 스냅샷에는 이벤트(시계열) 데이터가 포함되지 않습니다.

스냅샷의 속성 데이터는 스냅샷을 가져온 특정 시점의 데이터와 동일하게 표시됩니다. 즉, 스냅샷은 데이터의 근사 또는 샘플이 아니며, 세그먼트 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 생성하기 때문에 데이터가 변경된 사항이나 업데이트는 다음 스냅샷을 가져올 때까지 대시보드에 반영되지 않습니다.

## 세그먼트 대시보드 탐색

Platform UI 내의 [!UICONTROL 세그먼트] 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL 세그먼트]**&#x200B;를 선택한 다음 **[!UICONTROL 개요]** 탭을 선택하여 대시보드를 표시합니다.

>[!NOTE]
>
>조직이 Platform을 처음 사용하고 아직 활성 프로필 데이터 세트 또는 병합 정책이 만들어지지 않은 경우 [!UICONTROL 세그먼트] 대시보드가 표시되지 않습니다. 대신 [!UICONTROL 개요] 탭에는 세그먼테이션을 시작하는 데 도움이 되는 링크와 설명서가 표시됩니다.

![](../images/segments/dashboard-overview.png)

### [!UICONTROL 세그먼트] 대시보드 수정

**[!UICONTROL 대시보드 수정]**&#x200B;을 선택하여 [!UICONTROL 세그먼트] 대시보드의 모양을 수정할 수 있습니다. 이를 통해 대시보드에서 위젯을 이동, 추가 및 제거할 수 있을 뿐만 아니라 [!UICONTROL 위젯 라이브러리]에 액세스하여 사용 가능한 위젯을 탐색하고 조직에 대한 사용자 지정 위젯을 만들 수 있습니다.

자세한 내용은 [대시보드](../modify.md) 및 [위젯 라이브러리](../widget-library.md) 설명서 를 참조하십시오.

## 세그먼트 선택

대시보드는 표시할 세그먼트를 자동으로 선택하지만 드롭다운 메뉴 또는 세그먼트 선택기를 사용하여 세그먼트를 변경할 수 있습니다.

다른 세그먼트를 선택하려면 세그먼트 이름 옆에 있는 드롭다운을 선택하거나 세그먼트 선택기를 사용하여 세그먼트 선택 대화 상자를 엽니다.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## 위젯 및 지표

세그먼트 대시보드는 위젯으로 구성되며, 위젯은 선택한 세그먼트에 대한 중요한 정보를 제공하는 읽기 전용 지표입니다.

위젯의 &quot;최근 업데이트&quot; 날짜 및 시간은 데이터의 마지막 스냅숏을 만든 시기를 보여줍니다. 스냅샷의 날짜 및 시간은 UTC로 제공됩니다.개별 사용자 또는 IMS 조직의 시간대에 있지 않습니다.

![](../images/segments/widget-timestamp.png)

## 사용 가능한 위젯

Experience Platform은 세그먼트와 관련된 다양한 지표를 시각화하는 데 사용할 수 있는 여러 위젯을 제공합니다. 자세한 내용을 보려면 아래 위젯의 이름을 선택하십시오.

* [[!UICONTROL 대상 크기]](#audience-size)
* [[!UICONTROL 대상 크기 트렌드]](#audience-size-trend)
* [[!UICONTROL ID 겹치기]](#identity-overlap)
* [[!UICONTROL ID별 프로필]](#profiles-by-identity)

### [!UICONTROL 대상 크기] {#audience-size}

**[!UICONTROL 대상 크기]** 위젯은 스냅숏을 만들 때 선택한 세그먼트 내에서 병합된 프로필의 총 수를 표시합니다. 이 숫자는 프로필 조각을 함께 병합하여 세그먼트의 각 개인을 위한 단일 프로필을 구성하기 위해 프로필 데이터에 세그먼트 병합 정책을 적용한 결과입니다.

조각 및 병합된 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 읽어 보십시오.

![](../images/segments/audience-size.png)

### [!UICONTROL 대상 크기 트렌드] {#audience-size-trend}

**[!UICONTROL 대상 크기 트렌드]** 위젯은 지난 30일, 90일 또는 12개월 동안 일별 스냅샷 동안 캡처된 세그먼트의 총 프로필 수에 대한 정보를 제공합니다. 이 위젯은 새 프로필이 세그먼트에 대한 자격이 되거나 세그먼트에서 종료됨에 따라 세그먼트 크기가 시간에 따라 어떻게 변화했는지 표시합니다.

세그먼트 평가 및 프로필이 세그먼트에 대해 자격을 부여하고 종료하는 방법에 대한 자세한 내용은 [세그먼테이션 서비스 설명서](../../segmentation/home.md)를 참조하십시오.

![](../images/segments/audience-size-trend.png)

### [!UICONTROL ID 겹치기] {#identity-overlap}

**[!UICONTROL ID 겹치기]** 위젯에는 여러 ID가 포함된 세그먼트에서 프로필의 겹침을 보여주는 벤 다이어그램 또는 세트 다이어그램이 표시됩니다.

위젯의 드롭다운 메뉴를 사용하여 비교하려는 ID를 선택하면 원이 각 ID의 상대적 크기를 표시하는 반면 두 네임스페이스가 포함된 프로필의 수는 원 간 겹침 크기로 표시됩니다.

고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 ID가 해당 개별 고객과 연결되므로 조직에서 두 개 이상의 ID의 조각을 포함하는 여러 프로필을 가질 수 있습니다.

ID에 대한 자세한 내용은 [Adobe Experience Platform Identity 서비스 설명서](../../identity-service/home.md)를 참조하십시오.

![](../images/segments/identity-overlap.png)

### [!UICONTROL ID별 프로필] {#profiles-by-identity}

**[!UICONTROL ID별 프로필]** 위젯은 선택한 세그먼트에 있는 병합된 모든 프로필의 ID 분류를 표시합니다. 한 프로필에는 여러 개의 ID가 연결되어 있을 수 있으므로 ID별 총 프로필 수는 세그먼트의 총 프로필 수보다 높을 수 있습니다. 즉, 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 ID가 해당 개별 고객과 연결될 수 있으므로 각 ID에 대해 표시된 값을 함께 추가하면 세그먼트에서 총 대상 크기보다 커질 수 있습니다.

ID에 대한 자세한 내용은 [Adobe Experience Platform Identity 서비스 설명서](../../identity-service/home.md)를 참조하십시오.

![](../images/segments/profiles-by-identity.png)

## 다음 단계

이 문서에 따라 세그먼트 대시보드를 찾고 보려는 세그먼트를 선택할 수 있습니다. 사용 가능한 위젯에 표시되는 지표도 이해해야 합니다. Experience Platform UI에서 세그먼트 작업에 대한 자세한 내용은 [세그멘테이션 서비스 UI 안내서](../../segmentation/ui/overview.md)를 참조하십시오.
