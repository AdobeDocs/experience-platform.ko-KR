---
keywords: Experience Platform;user interface;UI;customization;license usage dashboard;dashboard;license usage;entitlement;consumption
title: 라이선스 사용 대시보드
description: '본 가이드는 Adobe Experience Platform UI에서 사용할 수 있는 라이센스 사용 대시보드에 대해 간략하게 설명합니다. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 63758450276d47e7e0eddeb047779222cb80a3e2
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---


# (Alpha) [!UICONTROL 라이센스 사용] 대시보드 {#license-usage-dashboard}

>[!IMPORTANT]
>
>이 문서에 설명된 대시보드 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 사용자 인터페이스(UI)는 일일 스냅샷 중에 캡처된 조직의 라이센스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 라이센스 사용 대시보드에 액세스하고 이를 사용하여 작업하는 방법에 대해 설명하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

플랫폼 UI에 대한 일반적인 개요는 [Experience Platform UI 안내서를 참조하십시오](ui-guide.md).

## 라이선스 사용 대시보드 데이터

라이선스 사용량 대시보드에는 Experience Platform에 대한 조직의 라이선스 관련 데이터 스냅샷이 표시됩니다. 대시보드의 데이터는 스냅샷이 생성된 특정 시점에 나타나는 것과 동일하게 표시됩니다. 즉, 스냅숏은 데이터의 근사값 또는 샘플이 아니며 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 촬영하여 변경한 데이터나 업데이트는 다음 스냅샷을 촬영하기 전까지 대시보드에 반영되지 않습니다.

## 라이선스 사용 대시보드 살펴보기

플랫폼 UI 내에서 라이센스 사용 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL 라이센스 사용을]** 선택합니다. 그러면 대시보드가 표시되는 **[!UICONTROL 개요]** 탭이 열립니다.

![](images/license-usage-dashboard/dashboard-overview.png)

### 샌드박스 선택

대시보드에서 볼 샌드박스를 선택하려면 [!UICONTROL 프로덕션] 또는 [!UICONTROL 개발을 선택합니다]. 선택한 샌드박스는 샌드박스 이름 옆에 있는 라디오 버튼으로 표시됩니다.

>[!NOTE]
>
>샌드박스에 대한 소비 보고는 동일한 유형의 모든 샌드박스에 대해 누적됩니다. 즉, [!UICONTROL 프로덕션] 또는 개발 [!UICONTROL 을] 선택하면 모든 프로덕션 또는 개발 샌드박스에 대해 각각 보고됩니다.

![](images/license-usage-dashboard/select-sandbox.png)

### 날짜 범위 선택

샌드박스를 선택한 후 날짜 범위 드롭다운을 사용하여 대시보드에 표시할 기간을 선택할 수 있습니다. 다음 세 가지 옵션을 사용할 수 있습니다. [!UICONTROL 지난 30일], [!UICONTROL 지난 90일], [!UICONTROL 지난 12개월]. 최근 30일은 기본적으로 선택됩니다.

![](images/license-usage-dashboard/select-date-range.png)

### 위젯 및 지표

라이선스 사용량 대시보드는 위젯으로 구성되어 있으며, 여기에는 조직의 라이선스 사용과 관련된 중요한 정보를 제공하는 읽기 전용 지표가 표시됩니다. 이러한 위젯에 대한 자세한 내용은 이 안내서의 사용 가능한 위젯 섹션을 참조하십시오.

## 사용 가능한 위젯 {#available-widgets}

Experience Platform은 현재 라이선스 사용을 시각화하는 데 사용할 수 있는 하나의 위젯을 제공하므로 더 많은 위젯이 곧 릴리스됩니다.

### [!UICONTROL 대응 가능 고객] {#addressable-audiences}

지정 가능한 **[!UICONTROL 대상]** 위젯은 시스템 생성 병합 정책을 적용하여 결정(비공개) 그래프 알고리즘을 사용하여 현재 모든 데이터 세트를 결합한 후 프로필 저장소에 있는 총 대상 수를 측정합니다. 이 지표를 계산하는 데 사용되는 병합 정책은 플랫폼에 의해 생성되므로 편집하거나 다른 병합 정책을 선택할 수 없습니다.

![](images/license-usage-dashboard/addressable-audiences.png)

## 추가 대시보드

플랫폼 UI는 Experience Platform 내에서 데이터의 스냅샷을 볼 수 있는 추가 대시보드를 제공합니다. 이러한 대시보드에는 실시간 고객 프로필 및 세그먼트가 포함됩니다. 이러한 대시보드에 대한 자세한 내용을 보려면 다음 링크 중에서 선택하십시오.

* [[!DNL Profile] 대시보드](../profile/ui/profile-dashboard.md)
* [세그먼트 대시보드](../segmentation/ui/segment-dashboard.md)

## 다음 단계

이 문서를 팔로우하면 라이센스 사용 대시보드를 찾아 볼 샌드박스를 선택할 수 있습니다. 사용 가능한 위젯에 표시되는 지표도 이해해야 합니다. Experience Platform UI에 대한 자세한 내용은 [플랫폼 UI 안내서를 참조하십시오](ui-guide.md).