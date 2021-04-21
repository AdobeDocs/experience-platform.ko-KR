---
keywords: Experience Platform;프로파일;실시간 고객 프로파일;사용자 인터페이스;사용자 정의;프로파일 대시보드;대시보드
title: 프로필 대시보드
description: Adobe Experience Platform은 조직의 실시간 고객 프로필 데이터에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 1%

---

# (베타) [!UICONTROL Profiles] 대시보드

>[!IMPORTANT]
>
>이 문서에 설명된 대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 사용자 인터페이스(UI)는 일일 스냅샷 중에 캡처된 [!DNL Real-time Customer Profile] 데이터에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 [!UICONTROL Profiles] 대시보드에 액세스하고 작업하는 방법에 대해 설명하고 대시보드에 표시되는 지표와 관련된 정보를 제공합니다.

Experience Platform 사용자 인터페이스에 있는 모든 프로필 기능에 대한 개요를 보려면 [실시간 고객 프로필 UI 안내서](../../profile/ui/user-guide.md)를 방문하십시오.

## 프로필 대시보드 데이터

[!UICONTROL Profiles] 대시보드에는 Experience Platform의 프로필 저장소 내에 조직에 있는 특성(레코드) 데이터의 스냅숏이 표시됩니다. 스냅샷에는 이벤트(시계열) 데이터가 없습니다.

스냅샷의 속성 데이터는 스냅샷이 생성된 특정 시점에 나타나는 데이터와 정확히 같은 데이터를 보여줍니다. 즉, 스냅숏은 대략적인 데이터나 샘플이 아니며 프로필 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅숏을 만든 이후 데이터에 대한 변경 사항이나 업데이트는 다음 스냅샷을 촬영하기 전까지 대시보드에 반영되지 않습니다.

## [!UICONTROL Profiles] 대시보드 탐색

플랫폼 UI 내의 [!UICONTROL Profiles] 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL Profiles]**&#x200B;을 선택하고 **[!UICONTROL Overview]** 탭을 선택하여 대시보드를 표시합니다.

![](../images/profiles/dashboard-overview.png)

### 병합 정책 선택

[!UICONTROL Profiles] 대시보드에 표시되는 지표는 실시간 고객 프로필 데이터에 적용되는 병합 정책을 기반으로 합니다. 여러 소스에서 데이터를 취합하는 경우 데이터가 충돌하는 값을 포함할 수 있습니다. 예를 들어, 데이터 세트에 고객을 &quot;단일&quot;로 나열할 수 있고 다른 데이터 세트에 고객을 &quot;기혼&quot;으로 나열할 수 있습니다. 이 데이터는 프로필의 일부로 우선 순위를 지정하고 표시할 데이터를 결정하는 병합 정책의 작업입니다.

대시보드는 표시할 병합 정책을 자동으로 선택하지만 드롭다운 메뉴를 사용하여 선택한 병합 정책을 변경할 수 있습니다. 다른 병합 정책을 선택하려면 병합 정책 이름 옆에 있는 드롭다운을 선택한 다음 보려는 병합 정책을 선택합니다.

>[!NOTE]
>
>드롭다운 메뉴에는 XDM 개별 프로필 클래스와 관련된 병합 정책만 표시되지만 조직에서 여러 개의 병합 정책을 만든 경우 사용 가능한 병합 정책의 전체 목록을 보려면 스크롤해야 한다는 의미일 수 있습니다.

조직에 대한 기본 병합 정책을 만들고 편집 및 선언할 수 있는 방법을 포함한 병합 정책에 대한 자세한 내용은 [병합 정책 UI 안내서](../../profile/ui/merge-policies.md)를 참조하십시오.

![](../images/profiles/select-merge-policy.png)

### 위젯 및 지표

대시보드는 프로필 데이터에 대한 중요한 정보를 제공하는 읽기 전용 지표인 위젯으로 구성됩니다. 위젯의 &quot;마지막 업데이트&quot; 날짜 및 시간은 데이터의 마지막 스냅숏을 만든 시기를 보여줍니다.

![](../images/profiles/dashboard-timestamp.png)

## 사용 가능한 위젯

Experience Platform은 프로필 데이터와 관련된 여러 지표를 시각화하는 데 사용할 수 있는 여러 widget을 제공합니다. 자세한 내용을 보려면 아래 위젯 이름을 선택하십시오.

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)
* [[!UICONTROL Namespace overlap]](#namespace-overlap)

### [!UICONTROL Audience size] {#audience-size}

**[!UICONTROL Audience size]** 위젯은 스냅숏을 만들 때 프로필 데이터 저장소 내의 병합된 프로필의 총 수를 표시합니다. 이 숫자는 프로필 조각을 함께 병합하여 각 개인에 대한 단일 프로필을 구성하기 위해 선택한 병합 정책이 프로필 데이터에 적용되는 결과입니다.

조각 및 병합된 프로파일에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)의 *프로필 조각과 병합된 프로필* 섹션을 읽으십시오.

>[!NOTE]
>
>이 지표를 계산하는 데 사용되는 병합 정책이 [!UICONTROL License usage] 대시보드에서 [!UICONTROL Addressable audiences]을(를) 계산하는 데 사용되는 시스템 생성 병합 정책과 같지 않으므로 [!UICONTROL Profiles] 및 [!UICONTROL License usage] 대시보드의 대상 수가 정확히 동일하지는 않을 것입니다.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profiles added] {#profiles-added}

**[!UICONTROL Profiles added]** 위젯에는 마지막 스냅숏을 만든 이후 프로필 데이터 저장소에 추가된 병합된 프로필의 총 수가 표시됩니다. 이 숫자는 프로필 조각을 함께 병합하여 각 개인에 대한 단일 프로필을 구성하기 위해 선택한 병합 정책이 프로필 데이터에 적용되는 결과입니다.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

**[!UICONTROL Profiles added over time]** 위젯은 지난 30일 동안 매일 프로필 데이터 저장소에 추가된 병합된 프로필의 총 수를 표시합니다. 이 숫자는 스냅샷을 가져올 때마다 매일 업데이트되므로 프로파일을 Platform으로 인제스트할 경우 다음 스냅샷을 촬영하기 전까지 프로파일 수가 반영되지 않습니다.

프로필 수가 추가된 것은 프로필 조각을 결합하여 각 개인에 대한 단일 프로필을 구성하기 위해 선택한 병합 정책이 프로필 데이터에 적용되는 결과입니다.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

**[!UICONTROL Profiles by namespace]** 위젯은 프로필 스토어에 병합된 모든 프로필의 ID 네임스페이스 분류를 표시합니다. 한 프로필에 여러 네임스페이스가 연결되어 있을 수 있으므로 각 네임스페이스에 대해 표시된 값을 함께 추가하는 등의 총 프로필 수는 전체 병합 프로필 수보다 클 수 있습니다. [!UICONTROL ID namespace] 예를 들어 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

ID 네임스페이스에 대한 자세한 내용은 [Adobe Experience Platform Identity Service 설명서](../../identity-service/home.md)를 참조하십시오.

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Namespace overlap] {#namespace-overlap}

**[!UICONTROL Namespace overlap]** 위젯은 여러 ID 네임스페이스가 포함된 프로필 오버랩을 표시하는 벤 다이어그램 또는 다이어그램을 표시합니다.

위젯의 드롭다운 메뉴를 사용하여 비교할 ID 네임스페이스를 선택하면 원이 각 네임스페이스의 상대적 크기를 표시하는 것처럼 나타나고 원 간 겹침 크기로 표현되는 두 네임스페이스의 프로필 수가 모두 포함된 프로필의 수와 함께 원이 표시됩니다.

고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연관되므로 조직에서 둘 이상의 ID 네임스페이스의 단편을 포함하는 여러 프로필을 보유할 가능성이 있습니다.

ID 네임스페이스에 대한 자세한 내용은 [Adobe Experience Platform Identity Service 설명서](../../identity-service/home.md)를 참조하십시오.

![](../images/profiles/namespace-overlap.png)

## 다음 단계

이제 이 문서를 따라 프로필 대시보드를 찾고 사용 가능한 위젯에 표시되는 지표를 이해할 수 있습니다. Experience Platform UI에서 [!DNL Profile] 데이터를 사용하여 작업하는 방법에 대한 자세한 내용은 [실시간 고객 프로필 UI 안내서](../../profile/ui/user-guide.md)를 참조하십시오.
