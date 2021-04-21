---
keywords: Experience Platform;프로파일;세그먼트;세그먼트;세그먼테이션;사용자 인터페이스;사용자 정의;세그먼트 대시보드;대시보드
title: 세그먼트 대시보드
description: 'Adobe Experience Platform은 조직에서 만든 세그먼트에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. '
topic-legacy: guide
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# (베타) 세그먼트 대시보드 {#segment-dashboard}

>[!IMPORTANT]
>
>이 문서에 설명된 대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 유저 인터페이스(UI)는 일일 스냅샷 중에 캡처되는 세그먼트에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI의 세그먼트 대시보드에 액세스하고 작업하는 방법에 대해 설명하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

플랫폼 사용자 인터페이스에 있는 모든 Adobe Experience Platform 세그멘테이션 서비스 기능에 대한 개요는 [세그멘테이션 서비스 UI 안내서](../../segmentation/ui/overview.md)를 참조하십시오.

## 세그먼트 대시보드 데이터

세그먼트 대시보드에는 Experience Platform의 프로필 저장소 내에 조직에 있는 특성(레코드) 데이터의 스냅숏이 표시됩니다. 스냅샷에는 이벤트(시계열) 데이터가 없습니다.

스냅샷의 속성 데이터는 스냅샷이 생성된 특정 시점에 나타나는 데이터와 정확히 같은 데이터를 보여줍니다. 즉, 스냅샷은 근사 또는 샘플 데이터가 아니며 세그먼트 대시보드는 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅숏을 만든 이후 데이터에 대한 변경 사항이나 업데이트는 다음 스냅샷을 촬영하기 전까지 대시보드에 반영되지 않습니다.

## 세그먼트 대시보드 탐색

플랫폼 UI 내의 세그먼트 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL Segments]**&#x200B;을 선택한 다음 **[!UICONTROL Overview]** 탭을 선택하여 대시보드를 표시합니다.

![](../images/segments/dashboard-overview.png)

### 세그먼트 선택

대시보드는 표시할 세그먼트를 자동으로 선택하지만 드롭다운 메뉴를 사용하여 표시되는 세그먼트를 변경할 수 있습니다. 다른 세그먼트를 선택하려면 세그먼트 이름 옆에 있는 드롭다운을 선택한 다음 보려는 세그먼트를 선택합니다.

>[!NOTE]
>
>드롭다운 메뉴에는 지금까지 조직에서 만든 모든 세그먼트가 표시됩니다. 사용 가능한 세그먼트의 전체 목록을 보려면 스크롤해야 할 수도 있습니다.

![](../images/segments/change-segment.png)

### 위젯 및 지표

세그먼트 대시보드는 선택한 세그먼트에 대한 중요한 정보를 제공하는 읽기 전용 지표인 위젯으로 구성됩니다. 위젯의 &quot;마지막 업데이트&quot; 날짜 및 시간은 데이터의 마지막 스냅숏을 만든 시기를 보여줍니다.

![](../images/segments/widget-timestamp.png)

## 사용 가능한 위젯

Experience Platform은 세그먼트와 관련된 다른 지표를 시각화하는 데 사용할 수 있는 여러 위젯을 제공합니다. 자세한 내용을 보려면 아래 위젯 이름을 선택하십시오.

* [[!UICONTROL Segment size]](#segment-size)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Segment size] {#segment-size}

**[!UICONTROL Segment size]** 위젯은 스냅샷을 만들 때 선택한 세그먼트 내에서 병합된 프로필의 총 수를 표시합니다. 이 번호는 세그먼트 병합 정책을 프로필 데이터에 적용하여 프로필 조각을 함께 병합하여 세그먼트에 있는 각 개인에 대한 단일 프로필을 구성한 결과입니다.

조각과 병합된 프로파일에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 읽으십시오.

![](../images/segments/segment-size.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

**[!UICONTROL Profiles added over time]** 위젯은 지난 30일 동안 일일 스냅샷 동안 캡처된 세그먼트의 총 프로필 수에 대한 정보를 제공합니다. 이 위젯은 새 프로필이 세그먼트에 적용되거나 종료되면 세그먼트 크기가 30일 동안 이동되었을 수 있는 방법을 표시합니다.

세그먼트 평가에 대한 자세한 내용과 프로파일이 세그먼트를 평가하고 종료하는 방법에 대한 자세한 내용은 [세그멘테이션 서비스 설명서](../../segmentation/home.md)를 참조하십시오.

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

**[!UICONTROL Profiles by namespace]** 위젯은 선택한 세그먼트에 병합된 모든 프로필의 네임스페이스 분류를 표시합니다. ID 네임스페이스별 전체 프로필 수([!UICONTROL ID namespace](위젯의 경우)는 한 프로필에 여러 네임스페이스가 연결되어 있을 수 있으므로 세그먼트의 전체 프로필 수보다 클 수 있습니다. 즉, 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결될 수 있으므로 각 네임스페이스에 대해 표시되는 값을 함께 추가하면 세그먼트의 전체 프로필보다 합계가 더 클 수 있습니다.

ID 네임스페이스에 대한 자세한 내용은 [Adobe Experience Platform Identity Service 설명서](../../identity-service/home.md)를 참조하십시오.

![](../images/segments/profiles-by-namespace.png)

## 다음 단계

이제 이 문서를 팔로우하여 세그먼트 대시보드를 찾고 볼 세그먼트를 선택할 수 있습니다. 사용 가능한 위젯에 표시되는 지표도 이해해야 합니다. Experience Platform UI에서 세그먼트 작업에 대한 자세한 내용은 [세그멘테이션 서비스 UI 안내서](../../segmentation/ui/overview.md)를 참조하십시오.
