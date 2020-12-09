---
keywords: Experience Platform;profile;segment;segments;segmentation;user interface;UI;customization;segment dashboard;dashboard
title: 세그먼트 대시보드
description: '이 안내서에서는 Adobe Experience Platform UI에서 사용할 수 있는 세그먼트 대시보드에 대해 간략하게 설명합니다. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 63758450276d47e7e0eddeb047779222cb80a3e2
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 1%

---


# (알파) 세그먼트 대시보드 {#segment-dashboard}

>[!IMPORTANT]
>
>이 문서에 설명된 대시보드 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 사용자 인터페이스(UI)는 일일 스냅샷 중에 캡처되는 대로 세그먼트에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 세그먼트 대시보드에 액세스하여 작업하는 방법에 대해 설명하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

플랫폼 사용자 인터페이스에 있는 모든 Adobe Experience Platform 세그멘테이션 서비스 기능에 대한 개요는 [세그멘테이션 서비스 UI 가이드를 참조하십시오](overview.md).

## 세그먼트 대시보드 데이터

세그먼트 대시보드에는 Experience Platform의 프로필 저장소 내에 조직에 있는 속성(레코드) 데이터의 스냅숏이 표시됩니다. 스냅샷에는 이벤트(시계열) 데이터가 포함되지 않습니다.

스냅샷의 속성 데이터는 스냅샷이 생성된 특정 시점에 나타나는 데이터와 정확히 같습니다. 즉, 스냅숏은 데이터의 근사 또는 샘플이 아니며 세그먼트 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 촬영하여 변경한 데이터나 업데이트는 다음 스냅샷을 촬영하기 전까지 대시보드에 반영되지 않습니다.

## 세그먼트 대시보드 살펴보기

플랫폼 UI 내의 세그먼트 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL 세그먼트를]** 선택한 다음 **[!UICONTROL 개요]** 탭을 선택하여 대시보드를 표시합니다.

![](../images/ui/segment-dashboard/dashboard-overview.png)

### 세그먼트 선택

대시보드에서 볼 세그먼트를 선택하려면 세그먼트 **[!UICONTROL 선택]** 텍스트 상자에 대한 대화 상자 선택기를 선택합니다.

![](../images/ui/segment-dashboard/select-segment.png)

>[!NOTE]
>
>세그먼트가 이미 선택된 경우 세그먼트 `X` 를 먼저 제거한 다음 대화 상자 선택기가 나타납니다.
>
>![](../images/ui/segment-dashboard/remove-segment.png)

세그먼트 **[!UICONTROL 선택]** 대화 상자가 열려 볼 세그먼트를 선택할 수 있습니다. 원하는 세그먼트를 선택한 후 **[!UICONTROL 선택을]** 사용하여 대시보드로 돌아갑니다.

![](../images/ui/segment-dashboard/select-segment-dialog.png)

### 정책 병합

세그먼트를 선택하면 병합 정책 텍스트 상자가 해당 세그먼트와 관련된 병합 정책으로 자동으로 채워집니다.

Experience Platform에서 세그먼트 작성에 대한 자세한 내용은 [세그먼트 빌더 UI 안내서를 참조하십시오](segment-builder.md). 병합 정책에 대한 자세한 내용은 [실시간 고객 프로필 개요를 읽어 보십시오](../../profile/home.md).

![](../images/ui/segment-dashboard/merge-policy.png)

### 위젯 및 지표

세그먼트 대시보드는 위젯으로 구성되어 있습니다. 위젯은 선택한 세그먼트와 관련된 중요한 정보를 제공하는 읽기 전용 지표입니다. 위젯의 &quot;마지막 업데이트&quot; 날짜 및 시간은 데이터의 마지막 스냅숏을 만든 시점을 보여줍니다.

![](../images/ui/segment-dashboard/widget-timestamp.png)

## 사용 가능한 위젯

Experience Platform은 세그먼트와 관련된 다른 지표를 시각화하는 데 사용할 수 있는 여러 개의 위젯을 제공합니다. 자세한 내용을 보려면 아래 위젯의 이름을 선택하십시오.

* [[!UICONTROL 세그먼트 크기]](#segment-size)
* [[!UICONTROL 네임스페이스별 프로필]](#profiles-by-namespace)

### [!UICONTROL 세그먼트 크기] {#segment-size}

세그먼트 **[!UICONTROL 크기]** 위젯은 스냅샷을 촬영할 때 선택한 세그먼트 내에서 병합된 프로필의 총 수를 표시합니다. 이 숫자는 프로필 조각을 결합하여 세그먼트의 각 개인에 대한 단일 프로필을 구성하기 위해 세그먼트 병합 정책을 프로필 데이터에 적용한 결과입니다.

조각 및 병합된 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요를 읽어 보십시오](../home.md).

![](../images/ui/segment-dashboard/segment-size.png)

### [!UICONTROL 네임스페이스별 프로필] {#profiles-by-namespace}

네임스페이스별 **[!UICONTROL 프로필]** 위젯은 선택한 세그먼트에서 병합된 모든 프로필의 네임스페이스 분류를 표시합니다. 한 프로필에 [!UICONTROL ID 네임스페이스별] 총 프로필 수(즉, 각 네임스페이스에 대해 표시되는 값을 함께 추가)는 여러 네임스페이스가 연결되어 있으므로 일반적으로 세그먼트의 전체 프로필 수보다 높습니다. 예를 들어 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 해당 개별 고객과 여러 개의 네임스페이스가 연결될 수 있습니다.

ID 네임스페이스에 대한 자세한 내용은 [Adobe Experience Platform ID 서비스 문서를 참조하십시오](../../identity-service/home.md).

![](../images/ui/segment-dashboard/profiles-by-namespace.png)

## 추가 대시보드

플랫폼 UI는 Experience Platform 내에서 데이터의 스냅샷을 볼 수 있는 추가 대시보드를 제공합니다. 이러한 대시보드에는 실시간 고객 프로필 및 [!UICONTROL 라이센스 사용이 포함됩니다]. 이러한 추가 대시보드에 대한 자세한 내용을 보려면 다음 링크 중에서 선택하십시오.

* [[!DNL Profile] 대시보드](../../profile/ui/profile-dashboard.md)
* [[!UICONTROL 라이선스 사용] 대시보드](../../landing/license-usage-dashboard.md)

## 다음 단계

이제 이 문서를 팔로우하여 세그먼트 대시보드를 찾아 볼 세그먼트를 선택할 수 있습니다. 사용 가능한 위젯에 표시되는 지표도 이해해야 합니다. Experience Platform UI에서 세그먼트 작업에 대한 자세한 내용은 [세그멘테이션 서비스 UI 안내서를 참조하십시오](overview.md).