---
title: 모니터링 대시보드 개요
description: Adobe Experience Platform UI에서 모니터링 대시보드를 사용하는 방법을 알아봅니다
exl-id: 06ea5380-d66e-45ae-aa02-c8060667da4e
source-git-commit: 710fa6930b27f95d34539a18881c0f9d23e1debd
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 1%

---

# 모니터링 대시보드 개요

Adobe Experience Platform UI의 모니터링 대시보드를 사용하여 수집에서 활성화까지의 데이터 여정을 볼 수 있습니다. 모니터링 대시보드를 사용하여 다음을 수행할 수 있습니다.

* 소스, ID 서비스, 실시간 고객 프로필, 대상 및 마지막으로 대상에서 데이터 여정을 모니터링합니다.
* 데이터가 있는 단계에 따라 다른 지표와 상태를 봅니다.
* 데이터 유형별로 데이터 모니터링 보기를 필터링합니다.

모니터링 대시보드는 다음과 같은 몇 가지 다양한 데이터 유형 보기를 지원합니다.

* **고객 및 계정**: 고객 데이터는에서 사용되는 데이터를 나타냅니다. [Real-time Customer Data Platform](../../rtcdp/home.md), 계정 데이터는 [계정 프로필 데이터](../../rtcdp/accounts/account-profile-overview.md) 구독 시 액세스할 수 있습니다. [Real-Time CDP, B2B 에디션](../../rtcdp/b2b-overview.md). Real-Time CDP 라이선스에 Real-Time CDP, B2B 에디션이 포함되지 않은 경우 모니터링 대시보드만 사용하여 고객 데이터를 모니터링할 수 있습니다.
* **잠재 고객**: [잠재 고객 프로필](../../profile/ui/prospect-profile.md) 은 회사와 아직 계약하지 않았지만 연결하고자 하는 사람을 나타내는 데 사용됩니다. 잠재 고객 프로필을 통해 신뢰할 수 있는 타사 파트너의 특성을 통해 고객 프로필을 보완할 수 있습니다. 잠재 고객 데이터 유형을 보려면 Real-Time CDP(앱 서비스), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate 라이선스가 있어야 합니다.
* **계정 프로필 보강**: 계정 프로필을 사용하면 여러 소스에서 계정 정보를 통합할 수 있습니다. 계정 프로필 보강 데이터를 모니터링하려면 Real-Time CDP, B2B 에디션 라이선스가 있어야 합니다.

모니터링 대시보드를 사용하여 다양한 Experience Platform 서비스에서 데이터 여정을 모니터링하는 방법에 대해 알아보려면 이 문서 를 참조하십시오.

## 시작하기

이 문서를 사용하려면 다음 Experience Platform 구성 요소에 대해 잘 알고 있어야 합니다.

* [데이터 흐름](../home.md): 데이터 흐름은 Experience Platform 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 소스 작업 영역을 사용하여 주어진 소스에서 Experience Platform으로 데이터를 수집하는 데이터 흐름을 만들 수 있습니다.
* [소스](../../sources/home.md): Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 타사 데이터 소스에서 데이터를 수집합니다.
* [ID 서비스](../../identity-service/home.md): 디바이스와 시스템 간에 ID를 연결하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
* [실시간 고객 프로필](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
* [세분화](../../segmentation/home.md): 세분화 서비스를 사용하여 실시간 고객 프로필 데이터에서 세그먼트와 대상자를 만듭니다.
* [대상](../../destinations/home.md): 대상은 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례를 위해 플랫폼에서 데이터를 원활하게 활성화할 수 있는 일반적으로 사용되는 애플리케이션과의 사전 빌드된 통합입니다.

## 모니터링 대시보드 안내서

Experience Platform UI에서 **[!UICONTROL 모니터링]** 아래에 [!UICONTROL 데이터 관리] 왼쪽 탐색.

![Experience Platform UI의 모니터링 대시보드.](../assets/ui/monitor-overview/monitoring.png)

선택 **[!UICONTROL 데이터 유형]** 드롭다운 메뉴를 사용하여 보려는 데이터 유형을 선택합니다. 데이터 유형은 XDM(Experience Data Model) 스키마 클래스에서 정의되므로 Experience Platform에 데이터를 수집할 때 데이터가 표준 형식을 따르는지 확인할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [B2B 계정 데이터 유형](../../rtcdp/b2b-tutorial.md)
* [잠재 고객 데이터 유형](../../rtcdp/partner-data/prospecting.md)

다음 데이터 유형을 기반으로 보기를 필터링할 수 있습니다.

>[!BEGINTABS]

>[!TAB 모두]

선택 **[!UICONTROL 모두]** 대시보드를 업데이트하고, 주어진 기간 동안 Experience Platform에 수집된 모든 데이터에 지표를 표시합니다.

![모니터링 데이터 유형이 &quot;모두&quot;로 설정되어 있습니다.](../assets/ui/monitor-overview/all.png)

>[!TAB 고객 및 계정]

선택 **[!UICONTROL 고객 및 계정]** 대시보드를 업데이트하고, 지정된 기간 동안 Experience Platform에 수집된 고객 및 계정 데이터에 대한 지표를 표시할 수 있습니다.

![모니터링 데이터 유형이 &quot;고객 및 계정&quot;으로 설정되어 있습니다.](../assets/ui/monitor-overview/customer-account.png)

>[!TAB 잠재 고객]

선택 **[!UICONTROL 잠재 고객]** Experience Platform을 업데이트하고 주어진 기간 동안 수집된 전망 데이터에 지표를 표시합니다. **참고**: 다음과 같은 경우에만 잠재 고객 데이터 유형 활동을 볼 수 있습니다. [잠재 고객 데이터 이용 가능](../../rtcdp/partner-data/prospecting.md).

![모니터링 데이터 유형이 &quot;Prospect&quot;로 설정되어 있습니다.](../assets/ui/monitor-overview/prospect.png)

>[!TAB 계정 프로필 보강]

선택 **[!UICONTROL 계정 프로필 보강]** 대시보드를 업데이트하고 프로필 강화 데이터에 지표를 표시할 수 있습니다. **참고**: 다음에 대한 권한이 있는 경우에만 계정 프로필 보강 지표를 볼 수 있습니다. [B2B 데이터](../../rtcdp/b2b-tutorial.md).

![모니터링 데이터 유형이 &quot;계정 프로필 보강&quot;으로 설정되었습니다.](../assets/ui/monitor-overview/account-profile-enrichment.png)

>[!ENDTABS]

교차 서비스 모니터링 환경을 위해 대시보드의 상단 헤더를 사용합니다. 데이터 범주 헤더에서 선택한 기능 카드를 선택하여 지표 및 그래프 보기를 필터링할 수 있습니다.

>[!BEGINTABS]

>[!TAB 소스]

선택 **[!UICONTROL 소스]** 소스 수집 속도에 대한 지표를 보는 방법. 의 안내서 읽기 [소스 데이터 모니터링](monitor-sources.md) 추가 정보.

![소스 카드가 선택된 UI의 모니터링 대시보드.](../assets/ui/monitor-overview/sources.png)

>[!TAB ID]

선택 **[!UICONTROL ID]** id 데이터의 처리 성공률을 확인합니다. 의 안내서 읽기 [id 데이터 모니터링](monitor-identities.md) 추가 정보.

![ID 카드가 선택된 UI의 모니터링 대시보드.](../assets/ui/monitor-overview/identities.png)

>[!TAB 프로필]

선택 **[!UICONTROL 프로필]** 프로필 데이터의 처리 성공률을 확인합니다. 의 안내서 읽기 [프로필 데이터 모니터링](monitor-profiles.md) 추가 정보.

![프로필 카드가 선택된 UI의 모니터링 대시보드.](../assets/ui/monitor-overview/profiles.png)

>[!TAB 대상자]

선택 **[!UICONTROL 대상]** 대상자 및 세분화 작업에 대한 지표를 봅니다. 의 안내서 읽기 [대상자 데이터 모니터링](monitor-audiences.md) 추가 정보.

![대상자 카드가 선택된 UI의 모니터링 대시보드.](../assets/ui/monitor-overview/audiences.png)

>[!TAB 대상]

선택 **[!UICONTROL 대상]** 에서 지표를 보려면 [!UICONTROL 스트리밍 활성화 비율] 및 [!UICONTROL 일괄 처리 실패 데이터 흐름 실행]. 의 안내서 읽기 [대상 데이터 모니터링](monitor-destinations.md) 추가 정보.

![대상 카드가 선택된 UI의 모니터링 대시보드.](../assets/ui/monitor-overview/destinations.png)

>[!ENDTABS]

### 모니터링 시간대 구성 {#configure-monitoring-time-frame}

기본적으로 모니터링 대시보드에는 지난 24시간 내에 수집된 데이터에 대한 지표가 표시됩니다. 시간대를 업데이트하려면 **[!UICONTROL 지난 24시간]**.

![시간 구성이 선택된 UI의 모니터링 대시보드.](../assets/ui/monitor-overview/select-time.png)

표시되는 대화 상자에서 데이터 모니터링 보기에 대한 새 시간대를 구성할 수 있습니다. 사용자 지정 시간대를 만들거나 사전 구성된 옵션 목록에서 선택할 수 있는 옵션이 있습니다.

* [!UICONTROL 지난 24시간]
* [!UICONTROL 지난 7일]
* [!UICONTROL 지난 30일]

완료되면 다음을 선택합니다. **[!UICONTROL 적용]**.

![모니터링 대시보드의 시간대 구성 팝업 창.](../assets/ui/monitor-overview/update-time.png)

## 다음 단계

이제 이 문서를 읽고 UI의 모니터링 대시보드를 탐색할 수 있습니다. 특정 Experience Platform 서비스의 데이터를 모니터링하는 방법에 대한 자세한 내용은 아래 설명서를 참조하십시오.

* [소스 데이터 모니터링](monitor-sources.md).
* [ID 데이터 모니터링](monitor-identities.md).
* [프로필 데이터 모니터링](monitor-profiles.md).
* [대상자 데이터 모니터링](monitor-audiences.md).
* [대상 데이터 모니터링](monitor-destinations.md).
