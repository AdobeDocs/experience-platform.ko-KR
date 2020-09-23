---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile;Union schema;UNION PROFILE;union profile
title: 실시간 고객 프로필 사용 안내서
topic: guide
description: 실시간 고객 프로파일은 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 다양한 채널의 데이터를 취합하여 각 개별 고객에 대한 전체적인 관점을 생성합니다. 이 문서는 Adobe Experience Platform 사용자 인터페이스에서 실시간 고객 프로필과 상호 작용하기 위한 가이드 역할을 합니다.
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] 사용 안내서

[!DNL Real-time Customer Profile] 온라인, 오프라인, CRM, 서드파티 데이터 등 다양한 채널에서 얻은 데이터를 통합하여 각 개별 고객의 전체 상황을 파악할 수 있습니다.

이 문서는 Adobe Experience Platform 사용자 인터페이스에서 [!DNL Real-time Customer Profile] 데이터와 상호 작용하는 데 대한 안내서의 역할을 합니다.

## 시작하기

이 사용자 가이드는 관리와 관련된 다양한 [!DNL Experience Platform] 서비스를 이해해야 합니다 [!DNL Real-time Customer Profiles]. 이 사용자 안내서를 읽기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL 실시간 고객 프로필]](../home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Identity Service]](../../identity-service/home.md):데이터 소스 [!DNL Real-time Customer Profile] 를 인제스트할 때 서로 다른 데이터 소스의 ID를 결합함으로써 사용할 수 있습니다 [!DNL Platform].
* [[!DNL Experience Data Model] (XDM)](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

## 개요

UI [[!DNL Experience Platform] ](http://platform.adobe.com)에서 **** 왼쪽 탐색 **[!UICONTROL 에서 프로필을 선택하여]** [개요]탭을엽니다. 이 탭에는 프로필 작업을 이해하고 시작하는 데 도움이 되는 설명서 및 비디오에 대한 링크가 제공됩니다.

![](../images/user-guide/profiles-overview.png)

## 찾아보기

ID **[!UICONTROL 로]** 프로파일을 찾아보려면 [찾아보기] 탭을 선택합니다.

![](../images/user-guide/profiles-browse.png)

### 프로필 지표 {#profile-metrics}

[ [!UICONTROL 검색] ] 탭 오른쪽에는 전체 [프로필 수](#profile-count) 및 네임스페이스별 [프로필 목록 등 프로필 데이터와 관련된 몇 가지 중요한 지표가 있습니다](#profiles-by-namespace).

이러한 프로필 지표는 조직의 기본 병합 정책을 사용하여 평가됩니다. 기본 병합 정책을 정의하는 방법을 비롯하여 병합 정책을 사용하는 방법에 대한 자세한 내용은 정책 [병합 사용 설명서를 참조하십시오](merge-policies.md).

이러한 지표 외에도 프로필 지표 섹션에서는 지표가 마지막으로 평가된 시기를 보여주는 [!UICONTROL 마지막 업데이트] 날짜 및 시간도 제공합니다.

![](../images/user-guide/profiles-profile-metrics.png)

### 프로필 수 {#profile-count}

조직의 기본 병합 정책이 프로필 조각을 병합하여 각 개별 고객에 대한 단일 프로필을 구성한 [!DNL Experience Platform]후 프로필 수는 조직에서 가지고 있는 총 프로필 수를 표시합니다. 즉, 조직은 여러 채널에서 브랜드와 상호 작용하는 단일 고객과 관련된 여러 프로필 조각을 가질 수 있지만 이러한 조각은 기본 병합 정책에 따라 병합되며 &quot;1&quot; 프로필의 개수가 반환됩니다. 모두 동일한 개인과 관련되어 있기 때문입니다.

프로필 수에는 속성(레코드 데이터)이 있는 프로필 및 Adobe Analytics 프로필과 같은 시간 시리즈(이벤트) 데이터만 포함된 프로파일도 모두 포함됩니다. 플랫폼 내에서 최신 총 프로필 수를 제공하기 위해 프로필 수는 정기적으로 새로 고쳐집니다.

스토어 내 레코드 수집이 5% 이상 카운트를 늘리거나 줄이면 [!DNL Profile] 카운트를 업데이트하도록 작업이 트리거됩니다. 스트리밍 데이터 워크플로우의 경우 시간별로 검사하여 5% 증가 또는 감소 임계값이 충족되었는지 확인합니다. 있는 경우 프로필 카운트를 업데이트하도록 작업이 자동으로 트리거됩니다. 일괄 처리를 위해, 성공적으로 배치를 프로필 스토어에 인제스트한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 작업이 실행되어 프로필 카운트를 업데이트합니다.

### 네임스페이스별 프로필 {#profiles-by-namespace}

네임스페이스별 **[!UICONTROL 프로필]** 지표는 프로필 스토어의 병합된 모든 프로필에서 네임스페이스의 전체 개수와 분류를 표시합니다. 네임스페이스별 총 프로필 수(즉, 각 네임스페이스에 대해 표시된 값을 함께 추가)는 하나의 프로필에 여러 네임스페이스가 연결되어 있으므로 항상 프로필 수 지표보다 높습니다. 예를 들어 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 해당 개별 고객과 여러 개의 네임스페이스가 연결됩니다.

프로필 수 [지표와 유사하게,](#profile-count) [!DNL Profile] 저장소에 레코드를 수집하면 카운트가 5% 이상 증가하거나 감소하면 네임스페이스 지표를 업데이트하기 위해 작업이 트리거됩니다. 스트리밍 데이터 워크플로우의 경우 시간별로 검사하여 5% 증가 또는 감소 임계값이 충족되었는지 확인합니다. 있는 경우 프로필 카운트를 업데이트하도록 작업이 자동으로 트리거됩니다. 일괄 처리 수정의 경우, 배치를 성공적으로 [!DNL Profile] 스토어에 인제스트한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 작업이 실행되어 지표를 업데이트합니다.

### 정책 병합

병합 정책 **** 선택기는 조직의 기본 병합 정책을 자동으로 선택합니다. 해당 병합 정책을 사용하지 않으려는 경우 기본 병합 정책 `X` 옆의 을 선택하여 다른 병합 정책을 선택할 수 있는 병합 정책 **** 선택 대화 상자를 열 수 있습니다. 플랫폼 내의 병합 정책과 그 역할에 대한 자세한 내용은 [병합 정책 사용 안내서를 참조하십시오](merge-policies.md).

![](../images/user-guide/profiles-search-merge-policy.png)

### ID 네임스페이스

ID **[!UICONTROL 네임스페이스]** 선택기는 검색할 ID 네임스페이스를 선택할 수 있는 대화 상자를 열고 필터 아이콘을 선택하고 추가 또는 제거할 속성을 선택하여 검색에서 표시되는 속성을 사용자 지정할 수 있습니다.

![](../images/user-guide/profiles-search-filter.png)

ID 네임스페이스 **[!UICONTROL 선택]** 대화 상자에서 검색할 네임스페이스를 선택하거나 대화 상자의 검색 막대를 사용하여 네임스페이스의 이름을 입력합니다. 추가 세부 사항을 볼 네임스페이스를 선택할 수 있으며, 사용할 네임스페이스를 찾은 경우 라디오 단추를 선택하고 선택을 눌러 **[!UICONTROL 계속 진행할]** 수 있습니다.

![](../images/user-guide/profiles-select-identity-namespace.png)

### ID 값

ID [!UICONTROL 네임스페이스를]선택한 후 [!UICONTROL ID] 값을 입력할 수 있는 **[!UICONTROL 찾아보기]**&#x200B;탭으로돌아갑니다. 이 값은 개별 고객 프로필에 고유하며 제공된 네임스페이스에 유효한 항목이어야 합니다. 예를 들어 [!UICONTROL ID 네임스페이스] &quot;이메일&quot;을 선택하려면 [!UICONTROL 유효한 이메일 주소] 형식의 ID 값이 필요합니다.

![](../images/user-guide/profiles-show-profile.png)

값을 입력했으면 프로필 **[!UICONTROL 표시]** 를 선택하면 값과 일치하는 단일 프로필이 반환됩니다. 프로필 **[!UICONTROL ID를]** 선택하여 프로필 세부 사항을 봅니다.

![](../images/user-guide/profiles-display-profile.png)

### 프로필 세부 사항 {#profile-detail}

프로필 [!UICONTROL ID를]선택하면 **[!UICONTROL 세부 사항]** 탭이열립니다. 세부 사항  탭에 표시되는 프로필 정보는 여러 프로필 조각에서 통합하여 개별 고객의 단일 보기를 형성했습니다. 여기에는 기본 속성, 연결된 ID 및 채널 환경 설정과 같은 고객 세부 사항이 포함됩니다. 표시되는 기본 필드는 기본 프로필 속성을 표시하도록 조직 수준에서 변경할 수도 있습니다. 속성 추가 및 제거, 대시보드 패널 크기 조정을 위한 단계별 지침 등 이러한 필드 사용자 지정에 대한 자세한 내용은 [프로필 세부 사용자 정의 안내서를 참조하십시오](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

사용 가능한 다른 탭을 선택하여 개별 프로파일과 관련된 추가 정보를 볼 수 있습니다. 이러한 탭에는 [!UICONTROL 속성], [!UICONTROL 이벤트]및 [!UICONTROL 세그먼트 멤버십이]포함되어 [!UICONTROL 있으며, 이] 탭에서는 현재 프로필의 자격이 있는세그먼트를 보여줍니다.

![](../images/user-guide/profiles-attributes-events-segments.png)

## 정책 병합

기본 [!UICONTROL 프로필] 메뉴에서 [정책 **[!UICONTROL 병합]** ] 탭을 선택하여 조직에 속하는 병합 정책 목록을 봅니다. 나열된 각 정책에는 해당 이름, 기본 병합 정책인지 여부 및 해당 정책이 적용되는 스키마가 표시됩니다.

병합 정책에 대한 자세한 내용은 [병합 정책 사용 안내서를 참조하십시오](merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## 결합 스키마 {#union-schema}

기본 [!UICONTROL 프로필] 메뉴에서 **[!UICONTROL 결합 스키마]** 탭을 선택하여 프로필 데이터에 대한 결합 스키마를 봅니다. 결합 스키마는 동일한 클래스 아래의 모든 [!DNL Experience Data Model] (XDM) 필드가 병합되어 스키마에서 사용할 수 있게 되었습니다 [!DNL Real-time Customer Profile]. 왼쪽에 있는 [!UICONTROL 클래스] 목록에서 클래스를 선택하여 캔버스에서 해당 스키마의 구조를 볼 수 있습니다. 예를 들어 &quot;[!DNL XDM Profile]&quot;를 선택하면 [!DNL XDM Individual Profile] 클래스에 대한 결합 스키마가 표시됩니다.

Adobe Experience Platform 내의 조합 스키마 및 해당 역할에 대한 자세한 내용은 [스키마 구성 안내서의 조합 스키마 섹션을 참조하십시오](../../xdm/schema/composition.md).

![](../images/user-guide/profiles-union-schema.png)

## 다음 단계

이제 이 안내서를 읽고 UI를 사용하여 [!DNL Profile] 데이터를 보고 관리하는 방법을 알 수 [!DNL Experience Platform] 있습니다. 실시간 고객 프로필 API를 사용하여 프로필 데이터를 사용하는 방법에 대한 자세한 내용은 [프로필 개발자 안내서를 참조하십시오](../api/overview.md).