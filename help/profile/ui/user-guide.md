---
keywords: Experience Platform;프로파일;실시간 고객 프로파일;문제 해결;API;통합 프로파일;통합 프로파일;프로파일;rtcp;프로파일 사용;프로파일 사용;프로파일;결합 스키마;UNION PROFILE;공용 프로파일
title: 실시간 고객 프로필 UI 안내서
topic-legacy: guide
description: 실시간 고객 프로파일은 온라인, 오프라인, CRM 및 제3자 데이터를 비롯한 여러 채널의 데이터를 취합하여 각 개별 고객을 전체적으로 파악할 수 있도록 지원합니다. 이 문서는 Adobe Experience Platform 사용자 인터페이스에서 실시간 고객 프로필과 상호 작용하기 위한 가이드 역할을 합니다.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 1%

---

# [!DNL Real-time Customer Profile] UI 가이드

[!DNL Real-time Customer Profile] 온라인, 오프라인, CRM 및 제3자 데이터를 비롯한 여러 채널의 데이터를 취합하여 각 개별 고객을 전체적으로 파악할 수 있습니다. 이 문서는 Adobe Experience Platform 사용자 인터페이스(UI)에서 [!DNL Real-time Customer Profile] 데이터와 상호 작용하기 위한 안내서의 역할을 합니다.

## 시작하기

이 UI 가이드를 사용하려면 [!DNL Real-time Customer Profiles] 관리와 관련된 다양한 [!DNL Experience Platform] 서비스를 이해해야 합니다. 이 안내서를 읽거나 UI에서 작업하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Real-time Customer Profile]](../home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Identity Service]](../../identity-service/home.md):인제스트할  [!DNL Real-time Customer Profile] 때 서로 다른 데이터 소스의 ID를 브리싱하여 사용할 수  [!DNL Platform]있습니다.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크

## 개요

Experience Platform UI의 왼쪽 탐색 영역에서 **[!UICONTROL Profiles]**&#x200B;을 선택하여 **[!UICONTROL Overview]** 탭을 엽니다. 이 탭에서는 프로파일을 이해하고 프로필 작업을 시작하는 데 도움이 되는 설명서 및 비디오에 대한 링크를 제공합니다.

![](../images/user-guide/profiles-overview.png)

### (알파) 프로필 대시보드

>[!IMPORTANT]
>
>대시보드 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

일부 사용자의 경우 왼쪽 탐색에서 **[!UICONTROL Profiles]**&#x200B;을 선택하고 **[!UICONTROL Overview]** 탭을 열면 프로필 데이터와 관련된 주요 지표에 대한 개요를 제공하는 대시보드가 제공됩니다.

자세한 내용은 [프로필 대시보드 안내서](profile-dashboard.md)를 참조하십시오.

## 찾아보기

ID별로 프로파일을 검색하려면 **[!UICONTROL Browse]** 탭을 선택합니다.

![](../images/user-guide/profiles-browse.png)

### 프로필 지표 {#profile-metrics}

**[!UICONTROL Browse]** 탭의 오른쪽에는 총 [프로필 수](#profile-count)와 이름 공간](#profiles-by-namespace)별 [프로필 목록을 포함하여 프로필 데이터와 관련된 몇 가지 중요한 지표가 있습니다.

이러한 프로필 지표는 조직의 기본 병합 정책을 사용하여 평가됩니다. 기본 병합 정책을 정의하는 방법을 비롯하여 병합 정책을 사용한 작업에 대한 자세한 내용은 [정책 병합 사용자 안내서](merge-policies.md)를 참조하십시오.

이러한 지표 외에도 프로필 지표 섹션에서는 지표가 마지막으로 평가된 시기를 보여주는 마지막 업데이트 날짜 및 시간도 제공합니다.

![](../images/user-guide/profiles-profile-metrics.png)

### 프로필 수 {#profile-count}

조직의 기본 병합 정책이 프로필 조각을 병합하여 각 개별 고객을 위한 단일 프로필을 구성한 후 프로필 수는 조직에서 가지고 있는 프로필의 총 수를 [!DNL Experience Platform] 내에 표시합니다. 즉, 조직에 여러 채널을 통해 브랜드와 상호 작용하는 단일 고객과 관련된 여러 프로필 조각이 있을 수 있지만 이러한 조각은 기본 병합 정책에 따라 병합되며 &quot;1&quot; 프로필의 개수가 모두 동일한 개인과 관련되어 있기 때문에 반환됩니다.

프로필 수에는 속성(레코드 데이터)이 있는 프로필 및 Adobe Analytics 프로필과 같은 시간 시리즈(이벤트) 데이터만 포함된 프로파일도 모두 포함됩니다. 플랫폼 내의 총 최신 프로파일 수를 제공하기 위해 프로파일 수가 정기적으로 갱신됩니다.

[!DNL Profile] 스토어에 레코드를 수집하면 카운트가 5% 이상 증가 또는 감소하면 작업이 트리거되어 카운트가 업데이트됩니다. 스트리밍 데이터 워크플로우의 경우 시간별로 검사하여 5% 증가 또는 감소 임계값이 충족되었는지 확인합니다. 있는 경우 프로필 수를 업데이트하도록 작업이 자동으로 트리거됩니다. 배치를 성공적으로 Profile Store에 인제스트한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 프로필 수를 업데이트하는 작업이 실행됩니다.

### 네임스페이스별 프로필 {#profiles-by-namespace}

**[!UICONTROL Profiles by namespace]** 지표는 프로필 스토어에 병합된 모든 프로필의 네임스페이스의 총 개수와 분류를 표시합니다. 네임스페이스별 전체 프로필 수(즉, 각 네임스페이스에 대해 표시된 값을 함께 추가)는 한 프로필에 여러 네임스페이스가 연결되어 있을 수 있으므로 항상 프로필 수 지표보다 높습니다. 예를 들어 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

[프로필 수](#profile-count) 지표와 유사하게, 레코드를 [!DNL Profile] 스토어에 수집하여 카운트가 5% 이상 증가하거나 감소하면 네임스페이스 지표를 업데이트하기 위해 작업이 트리거됩니다. 스트리밍 데이터 워크플로우의 경우 시간별로 검사하여 5% 증가 또는 감소 임계값이 충족되었는지 확인합니다. 있는 경우 프로필 수를 업데이트하도록 작업이 자동으로 트리거됩니다. 일괄 처리를 위해 배치를 [!DNL Profile] 스토어에 성공적으로 인제스트한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 작업을 실행하여 지표를 업데이트합니다.

### 정책 병합

**[!UICONTROL Merge policy]** 선택기는 조직의 기본 병합 정책을 자동으로 선택합니다. 해당 병합 정책을 사용하지 않으려면 기본 병합 정책 옆의 `X`을 선택하여 다른 병합 정책을 선택할 수 있는 **[!UICONTROL Select merge policy]** 대화 상자를 열 수 있습니다.

플랫폼 내에서 정책 병합 및 해당 역할에 대한 자세한 내용은 정책 병합 UI 안내서](merge-policies.md)를 참조하십시오.[

![](../images/user-guide/profiles-search-merge-policy.png)

### ID 네임스페이스

**[!UICONTROL Identity namespace]** 선택기는 검색할 ID 네임스페이스를 선택할 수 있는 대화 상자를 열고 필터 아이콘을 선택하고 추가 또는 제거할 속성을 선택하여 검색에 표시되는 속성을 사용자 지정할 수 있습니다.

![](../images/user-guide/profiles-search-filter.png)

**[!UICONTROL Select identity namespace]** 대화 상자에서 검색할 네임스페이스를 선택하거나 대화 상자의 검색 막대를 사용하여 네임스페이스 이름을 입력합니다. 추가 세부 사항을 볼 네임스페이스를 선택할 수 있으며, 사용하고자 하는 네임스페이스가 발견되면 라디오 단추를 선택하고 **[!UICONTROL Select]**&#x200B;을 눌러 계속할 수 있습니다.

![](../images/user-guide/profiles-select-identity-namespace.png)

### ID 값

ID 네임스페이스를 선택한 후 **[!UICONTROL Identity value]**&#x200B;을(를) 입력할 수 있는 **[!UICONTROL Browse]** 탭으로 돌아갑니다. 이 값은 개별 고객 프로필에 고유하며 제공된 네임스페이스에 대한 유효한 항목이어야 합니다. 예를 들어 ID 네임스페이스 &quot;이메일&quot;을 선택하려면 유효한 이메일 주소 형식의 ID 값이 필요합니다.

![](../images/user-guide/profiles-show-profile.png)

값을 입력했으면 **[!UICONTROL Show profile]**&#x200B;을 선택하고 값과 일치하는 단일 프로필이 반환됩니다. 프로필 세부 정보를 보려면 **[!UICONTROL Profile ID]**&#x200B;을 선택합니다.

![](../images/user-guide/profiles-display-profile.png)

### 프로필 세부 정보 {#profile-detail}

**[!UICONTROL Profile ID]**&#x200B;을 선택하면 **[!UICONTROL Detail]** 탭이 열립니다. **[!UICONTROL Detail]** 탭에 표시된 프로필 정보가 여러 프로필 조각에서 병합되어 개별 고객의 단일 보기를 형성했습니다. 여기에는 기본 속성, 연결된 ID 및 채널 환경 설정과 같은 고객 세부 사항이 포함됩니다. 표시되는 기본 필드는 기본 프로필 속성을 표시하도록 조직 수준에서 변경할 수도 있습니다. 속성을 추가 및 제거하고 대시보드 패널의 크기를 변경하는 단계별 지침을 포함하여 이러한 필드를 사용자 지정하는 방법에 대한 자세한 내용은 [프로필 세부 정보 사용자 지정 안내서](profile-customization.md)를 참조하십시오.

![](../images/user-guide/profiles-profile-detail.png)

사용 가능한 다른 탭을 선택하여 개별 프로파일과 관련된 추가 정보를 볼 수 있습니다. 이러한 탭에는 프로파일이 현재 자격을 갖춘 세그먼트를 보여주는 속성, 이벤트 및 세그먼트 멤버십이 있습니다.

![](../images/user-guide/profiles-attributes-events-segments.png)

## 정책 병합

기본 **[!UICONTROL Profiles]** 메뉴에서 **[!UICONTROL Merge Policies]** 탭을 선택하여 조직에 속하는 병합 정책 목록을 봅니다. 나열된 각 정책에는 해당 이름, 기본 병합 정책인지 여부 및 해당 정책이 적용되는 스키마 클래스가 표시됩니다.

병합 정책에 대한 자세한 내용은 [정책 병합 UI 안내서](merge-policies.md)를 참조하십시오.

실시간 고객 프로필 API를 사용하여 병합 정책을 사용하는 방법에 대한 자세한 내용은 [병합 정책 끝점 안내서](../api/merge-policies.md)를 참조하십시오.

![](../images/user-guide/profiles-merge-policies.png)

## 공용 스키마 {#union-schema}

기본 **[!UICONTROL Profiles]** 메뉴에서 **[!UICONTROL Union Schema]** 탭을 선택하여 인제스트한 데이터에 대해 사용 가능한 결합 스키마를 봅니다. 결합 스키마는 동일한 클래스 아래의 모든 [!DNL Experience Data Model](XDM) 필드의 병합으로서 [!DNL Real-time Customer Profile]에서 스키마를 사용할 수 있도록 설정되어 있습니다.

결합 스키마에 대한 자세한 내용은 [union schema UI 안내서](union-schema.md)를 참조하십시오.

![](../images/user-guide/profiles-union-schema.png)

## 다음 단계

이제 이 안내서를 읽고 [!DNL Experience Platform] UI를 사용하여 [!DNL Profile] 데이터를 보고 관리하는 방법을 알 수 있습니다. 실시간 고객 프로필 API를 사용하여 프로필 데이터를 사용하는 방법에 대한 자세한 내용은 [프로필 개발자 안내서](../api/overview.md)를 참조하십시오.
