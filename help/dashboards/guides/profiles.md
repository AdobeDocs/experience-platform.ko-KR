---
keywords: Experience Platform;프로필;실시간 고객 프로필;사용자 인터페이스;UI;사용자 지정;프로필 대시보드;대시보드
title: 프로필 대시보드 안내서
description: Adobe Experience Platform은 조직의 실시간 고객 프로필 데이터에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 9a4257ef6f9e32feeb2bb90bc7dd46b0d533cb35
workflow-type: tm+mt
source-wordcount: '3859'
ht-degree: 1%

---

# [!UICONTROL 프로필] 대시보드

Adobe Experience Platform UI(사용자 인터페이스)는 사용자 인터페이스에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다 [!DNL Real-time Customer Profile] 데이터를 캡처할 수 있습니다. 이 안내서에서는 [!UICONTROL 프로필] 대시보드 를 참조하고 대시보드에 표시되는 지표에 대한 정보를 제공합니다.

Experience Platform 사용자 인터페이스 내의 모든 프로필 기능에 대한 개요를 보려면 [실시간 고객 프로필 UI 안내서](../../profile/ui/user-guide.md).

## 프로필 대시보드 데이터

다음 [!UICONTROL 프로필] 대시보드는 Experience Platform의 프로필 저장소 내에 조직에 있는 속성(레코드) 데이터의 스냅숏을 표시합니다. 스냅샷에는 이벤트(시계열) 데이터가 포함되지 않습니다.

스냅샷의 속성 데이터는 스냅샷을 가져온 특정 시점의 데이터와 동일하게 표시됩니다. 즉, 스냅샷은 근사 또는 데이터 샘플이 아니며, 프로필 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 생성하기 때문에 데이터가 변경된 사항이나 업데이트는 다음 스냅샷을 가져올 때까지 대시보드에 반영되지 않습니다.

## 탐색 [!UICONTROL 프로필] 대시보드

로 이동하려면 다음을 수행하십시오. [!UICONTROL 프로필] 플랫폼 UI 내의 대시보드에서 **[!UICONTROL 프로필]** 왼쪽 레일에서 **[!UICONTROL 개요]** 탭을 클릭하여 대시보드를 표시합니다.

>[!NOTE]
>
>조직이 Platform을 처음 사용하고 아직 활성 프로필 데이터 세트 또는 병합 정책이 만들어지지 않은 경우, [!UICONTROL 프로필] 대시보드가 표시되지 않습니다. 대신, [!UICONTROL 개요] 실시간 고객 프로필을 시작하는 데 도움이 되는 링크와 설명서가 탭에 표시됩니다.

![](../images/profiles/dashboard-overview.png)

### 수정 [!UICONTROL 프로필] 대시보드

의 모양을 수정할 수 있습니다 [!UICONTROL 프로필] 선택하여 대시보드 **[!UICONTROL 대시보드 수정]**. 이를 통해 대시보드에서 위젯을 이동, 추가 및 제거할 수 있을 뿐만 아니라 **[!UICONTROL 위젯 라이브러리]** 사용 가능한 위젯을 살펴보고 조직에 대한 사용자 지정 위젯을 만들려면

자세한 내용은 [대시보드 수정](../customize/modify.md) 및 [위젯 라이브러리 개요](../customize/widget-library.md) 설명서 를 참조하십시오.

### 위젯 추가 {#add-widget}

선택 **[!UICONTROL 위젯 추가]** 위젯 라이브러리로 이동하고 대시보드에 추가할 수 있는 위젯 목록을 확인합니다.

![추가 위젯이 강조 표시된 프로필 대시보드 개요.](../images/profiles/profiles-overview-add-widget.png)

위젯 라이브러리에서 표준 및 사용자 지정 세그먼트 위젯의 선택 항목을 찾아볼 수 있습니다.위젯을 추가하는 방법에 대한 자세한 내용은 위젯 라이브러리 설명서를 참조하십시오 [위젯 추가](../customize/widget-library.md#add-widgets).

## (베타) 프로필 유효성 통찰력 {#profile-efficacy-insights}

>[!IMPORTANT]
>
>프로필 유효성 인사이트 기능은 현재 베타 버전으로 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

다음 [!UICONTROL 효능] 탭은 프로필 유효성 위젯을 사용하여 프로필 데이터의 품질과 완전성에 대한 지표를 제공합니다. 이러한 위젯은 프로필의 구성, 시간 경과에 따른 완벽성 추세 및 프로필 데이터 품질에 대한 평가를 한눈에 보여줍니다.

![프로파일 효과 대시보드.](../images/profiles/attributes-quality-assessment.png)

자세한 내용은 [프로필 효과 위젯 섹션](#profile-efficacy-widgets) 위젯에 대한 자세한 내용은 현재 사용 가능합니다.

또한, 이 대시보드의 레이아웃은 [**[!UICONTROL 대시보드 수정]**](../customize/modify.md) 에서 [!UICONTROL 개요] 탭.

## 프로필 찾아보기 {#browse-profiles}

다음 [!UICONTROL 찾아보기] 탭에서 조직에 수집된 읽기 전용 프로필을 검색하고 볼 수 있습니다. 여기에서 기본 설정, 이전 이벤트, 상호 작용 및 세그먼트와 관련하여 프로필에 속하는 중요한 정보를 볼 수 있습니다

Platform UI에 제공된 프로필 보기 기능에 대한 자세한 내용은 [Real-time Customer Data Platform에서 프로필 검색](../../rtcdp/profile/profile-browse.md).

## 병합 정책 {#merge-policies}

에 표시되는 지표 [!UICONTROL 프로필] 대시보드는 실시간 고객 프로필 데이터에 적용되는 병합 정책을 기반으로 합니다. 고객 프로필을 만들기 위해 여러 소스에서 데이터를 함께 가져오는 경우 데이터에 충돌하는 값이 포함될 수 있습니다. 예를 들어, 하나의 데이터 세트에 고객이 &quot;단일&quot;로 나열되고 다른 데이터 세트에 고객이 &quot;기혼&quot;으로 나열될 수 있습니다. 프로필의 일부로 우선 순위를 지정하고 표시할 데이터를 결정하는 것은 병합 정책의 작업입니다.

조직의 기본 병합 정책을 만들고 편집하고 선언하는 방법 등 병합 정책에 대한 자세한 내용은 [정책 병합 개요](../../profile/merge-policies/overview.md).

대시보드에서 사용할 병합 정책을 자동으로 선택합니다. 적용된 병합 정책은 병합 정책 이름 옆에 있는 드롭다운 메뉴를 사용하여 변경할 수 있습니다.

>[!NOTE]
>
>드롭다운 메뉴에는 `_xdm.context.profile` 스키마. 그러나 조직에서 여러 개의 병합 정책을 만든 경우 사용 가능한 병합 정책의 전체 목록을 보려면 스크롤해야 할 수도 있습니다.

![병합 정책 드롭다운이 강조 표시된 프로필 개요 탭.](../images/profiles/select-merge-policy.png)

## 결합 스키마

다음 [!UICONTROL 결합 스키마] 대시보드는 특정 XDM 클래스에 대한 결합 스키마를 표시합니다. 을(를) 선택하여 **[!UICONTROL 클래스]** 드롭다운에서 다른 XDM 클래스에 대한 결합 스키마를 볼 수 있습니다.

결합 스키마는 동일한 클래스를 공유하고 프로필에 대해 활성화된 여러 스키마로 구성됩니다. 동일한 클래스를 공유하는 각 스키마 내에 포함된 모든 필드의 병합을 단일 보기에서 볼 수 있습니다.

자세한 내용은 결합 스키마 UI 안내서 를 참조하십시오 [플랫폼 UI 내에서 결합 스키마 보기](../../profile/ui/union-schema.md#view-union-schemas).

## 위젯 및 지표

대시보드는 프로필 데이터와 관련된 중요한 정보를 제공하는 읽기 전용 지표인 위젯으로 구성됩니다.

가장 최근 스냅샷의 날짜 및 시간이 [!UICONTROL 개요] 병합 정책 드롭다운 옆에 있는 탭입니다. 모든 위젯 데이터는 해당 날짜 및 시간에 따라 정확합니다. 스냅샷의 타임스탬프는 UTC로 제공됩니다. 개별 사용자 또는 조직의 시간대에 있지 않습니다.

![가장 최근 스냅샷 타임스탬프가 강조 표시된 프로필 대시보드 개요 탭.](../images/profiles/snapshot-timestamp.png)

## 표준 위젯 {#standard-widgets}

Adobe은 프로필 데이터와 관련된 다양한 지표를 시각화하는 데 사용할 수 있는 여러 표준 위젯을 제공합니다. 또한 [!UICONTROL 위젯 라이브러리]. 사용자 지정 위젯을 만드는 방법에 대해 자세히 알아보려면 [위젯 라이브러리 개요](../customize/widget-library.md).

사용 가능한 각 표준 위젯에 대해 자세히 알아보려면 다음 목록에서 위젯 이름을 선택하십시오.

* [[!UICONTROL 프로필 수]](#profile-count)
* [[!UICONTROL 프로필 수 트렌드]](#profile-count-trend)
* [[!UICONTROL 프로필 수 변경]](#profile-count-change)
* [[!UICONTROL 프로필 수 변경 트렌드]](#profiles-count-change-trend)
* [[!UICONTROL ID별 프로필 수 변경 트렌드]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL ID별 프로필]](#profiles-by-identity)
* [[!UICONTROL ID 겹치기]](#identity-overlap)
* [[!UICONTROL 단일 ID 프로필]](#single-identity-profiles)
* [[!UICONTROL ID별 단일 ID 프로필]](#single-identity-profiles-by-identity)
* [[!UICONTROL 세그먼트화되지 않은 프로필]](#unsegmented-profiles)
* [[!UICONTROL 세그먼트화되지 않은 프로필 트렌드]](#unsegmented-profiles-trend)
* [[!UICONTROL ID로 세그먼트화되지 않은 프로필]](#unsegmented-profiles-by-identity)
* [[!UICONTROL 대상자]](#audiences)
* [[!UICONTROL 대상 상태에 매핑된 대상]](#audiences-mapped-to-destination-status)
* [[!UICONTROL 대상 크기]](#audiences-size)
* [[!UICONTROL 병합 정책별 대상 겹치기]](#audience-overlap-by-merge-policy)

### [!UICONTROL 프로필 수] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="프로필 수"
>abstract="이 위젯은 스냅숏을 만들 때 프로필 저장소 내에 병합된 총 프로필 수를 표시합니다. 숫자는 프로필 데이터에 적용되는 선택한 병합 정책에 따라 달라집니다."

다음 **[!UICONTROL 프로필 수]** 위젯은 스냅숏을 만들 때 프로필 저장소 내에 병합된 총 프로필 수를 표시합니다. 이 숫자는 프로필 조각을 함께 병합하여 각 개인을 위한 단일 프로필을 구성하기 위해 선택한 병합 정책이 프로필 데이터에 적용되는 결과입니다.

자세한 내용은 [이 문서의 앞부분에서 병합 정책에 대한 섹션을 참조하십시오](#merge-policies) 추가 정보

>[!NOTE]
>
>다음 [!UICONTROL 프로필 수] 위젯에 표시된 프로필 수와 다른 숫자가 표시될 수 있습니다 [!UICONTROL 찾아보기] 탭에서 다음을 수행합니다. [!UICONTROL 프로필] 여러 가지 이유로 UI의 섹션을 참조하십시오. 가장 일반적인 이유는 [!UICONTROL 찾아보기] 탭은 조직의 기본 병합 정책을 기반으로 병합된 프로필의 총 수를 참조하는 반면, [!UICONTROL 프로필 수] 위젯은 대시보드에서 보기 위해 선택한 병합 정책을 기반으로 병합된 총 프로필 수를 참조합니다.
>
>다른 일반적인 이유는 대시보드 스냅샷을 가져오는 시간과 에 대해 샘플 작업을 실행하는 시간 간의 차이 때문입니다 [!UICONTROL 찾아보기] 탭. 언제 [!UICONTROL 프로필 수] 위젯이 위젯에서 타임스탬프를 보고, 위젯에서 샘플 작업이 트리거되는 방식에 대한 자세한 내용을 확인함으로써 마지막으로 업데이트되었습니다 [!UICONTROL 찾아보기] 탭에서 다음을 참조하십시오 [실시간 고객 프로필 UI 안내서의 프로필 카운트 섹션](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL 프로필 수 트렌드] {#profile-count-trend}

다음 [!UICONTROL 프로필 수 트렌드] 위젯은 선 그래프를 사용하여 시간에 따라 시스템에 포함된 총 프로필 수의 트렌드를 표시합니다. 이 총 숫자에는 마지막 일별 스냅샷 이후 시스템에 가져온 모든 프로필이 포함됩니다. 데이터는 30일, 90일 및 12개월 동안 시각화할 수 있습니다. 기간은 위젯의 드롭다운 메뉴에서 선택됩니다.

![프로필 수 트렌드 위젯.](../images/profiles/profile-count-trend.png)

### [!UICONTROL 프로필 수 변경] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="프로필 수 변경"
>abstract="이 위젯은 병합된 프로필의 총 수를 표시합니다 **추가됨** 최신 스냅샷 시 프로필 저장소에 추가 숫자는 프로필 데이터에 적용되는 선택한 병합 정책에 따라 달라집니다."

다음 **[!UICONTROL 프로필 수 변경]** 위젯은 이전 스냅숏 이후 프로필 저장소에 추가된 병합된 프로필 수를 표시합니다. 이 숫자는 프로필 조각을 함께 병합하여 각 개인을 위한 단일 프로필을 구성하기 위해 선택한 병합 정책이 프로필 데이터에 적용되는 결과입니다. 드롭다운 선택기를 사용하여 지난 30일, 90일 또는 12개월 동안 추가된 프로필 수를 볼 수 있습니다.

>[!NOTE]
>
>다음 [!UICONTROL 프로필 수 변경] 위젯은 추가된 프로필 수를 반영합니다 **after** 초기 프로필 수집 및 프로필 저장소 설정. 즉, 조직에서 프로필 스토어를 설정하고 1일에 4,000,000을 섭취하는 경우 24시간 이내에 대시보드를 사용할 수 있지만 [!UICONTROL 프로필 수 변경] 위젯이 0으로 설정됩니다. 이 작업은 프로필을 시스템으로 초기 수집과 관련된 스파이크를 방지하기 위해 수행됩니다. 향후 30일 동안 조직은 프로필 스토어에 100만 개의 프로필을 추가로 수집합니다. 다음 스냅샷을 만든 후 [!UICONTROL 프로필 수 변경] 위젯에는 추가된 총 100만 개의 프로필이 표시되고 [!UICONTROL 프로필 수] 위젯은 총 5,000,000개의 프로필을 표시합니다.

![프로필 수 변경 위젯이 강조 표시된 플랫폼 UI 프로필 대시보드 .](../images/profiles/profile-count-change.png)

### [!UICONTROL 프로필 수 변경 트렌드] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="프로필 수 변경 트렌드"
>abstract="이 위젯은 지난 30일, 90일 또는 12개월 동안 매일 프로필 저장소에 추가된 병합된 프로필 수를 표시합니다. 프로필 데이터에 적용되는 선택한 병합 정책에 따라서도 번호가 달라집니다."

다음 **[!UICONTROL 프로필 수 변경 트렌드]** 위젯은 지난 30일, 90일 또는 12개월 동안 매일 프로필 저장소에 추가된 병합된 프로필의 총 수를 표시합니다. 이 숫자는 스냅샷을 가져올 때마다 매일 업데이트되므로 프로필을 플랫폼으로 수집하려는 경우 다음 스냅샷을 가져올 때까지 프로필 수가 반영되지 않습니다. 추가된 프로필 수는 프로필 조각을 함께 병합하여 각 개인을 위한 단일 프로필을 구성하기 위해 선택한 병합 정책이 프로필 데이터에 적용되어 있는 결과입니다.

자세한 내용은 [이 문서의 앞부분에서 병합 정책에 대한 섹션을 참조하십시오](#merge-policies) 추가 정보

다음 **[!UICONTROL 프로필 수 변경 트렌드]** 위젯은 위젯의 오른쪽 상단에 &#39;캡션&#39; 단추를 표시합니다. 선택 **[!UICONTROL 캡션]** 자동 캡션 대화 상자를 열려면 다음을 수행하십시오.

![캡션 단추가 강조 표시된 프로필 수 변경 트렌드 위젯을 표시하는 프로필 개요 탭.](../images/profiles/profiles-count-change-trend-captions.png)

기계 학습 모델은 차트와 데이터를 분석하여 주요 트렌드와 중요한 이벤트를 설명하는 캡션을 자동으로 생성합니다. 캡션을 기반으로 차트에 주석이 추가됩니다. 해당 주석에 초점을 맞출 캡션을 선택합니다.

![프로필 수 변경 트렌드 위젯에 대한 자동 캡션 대화 상자입니다.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL ID별 프로필 수 변경 트렌드] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

이 위젯은 선택한 소스 ID 및 병합 정책을 기반으로 프로필 수를 필터링한 다음 선 그래프를 사용하여 다양한 기간의 숫자 변화를 보여줍니다. 페이지 맨 위의 개요 드롭다운에서 병합 정책이 선택되면 위젯 드롭다운 메뉴에서 소스 ID 및 기간이 선택됩니다. 이 트렌드는 30일, 90일 및 12개월 기간에 걸쳐 시각화할 수 있습니다.

이 위젯은 필요한 ID로 필터링된 프로필의 증가 패턴을 보여줌으로써 대상 활성화 요구 사항을 관리하는 데 도움이 됩니다.

![ID 위젯별 프로필 수 변경 트렌드입니다.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL ID별 프로필] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="ID별 프로필"
>abstract="이 위젯은 ID로 프로필 저장소에 병합된 모든 프로필의 분류를 표시합니다."

다음 **[!UICONTROL ID별 프로필]** 위젯은 프로필 저장소에 있는 병합된 모든 프로필의 ID 분류를 표시합니다. 한 프로필에는 여러 네임스페이스가 연결되어 있을 수 있으므로 ID별 총 프로필 수(즉, 각 네임스페이스에 대해 표시된 값을 함께 추가)는 병합된 총 프로필 수보다 높을 수 있습니다. 예를 들어 고객이 둘 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

자세한 내용은 [이 문서의 앞부분에서 병합 정책에 대한 섹션을 참조하십시오](#merge-policies) 추가 정보

![ID별 프로필 위젯이 강조 표시된 프로필 개요 대시보드.](../images/profiles/profiles-by-identity.png)

선택 **[!UICONTROL 캡션]** 자동 캡션 대화 상자를 열려면 다음을 수행하십시오.

![ID 캡션별 프로필 대화 상자](../images/profiles/profiles-by-identity-captions.png)

기계 학습 모델은 데이터의 전체 분포 및 주요 차원을 분석하여 데이터 인사이트를 자동으로 생성합니다.

ID에 대해 자세히 알아보려면 [Adobe Experience Platform Identity Service 설명서](../../identity-service/home.md).

### [!UICONTROL ID 겹치기] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="ID 겹치기"
>abstract="이 위젯은 벤 다이어그램을 사용하여 선택한 두 ID가 포함된 프로필 저장소에 프로필의 겹침을 표시합니다."

다음 **[!UICONTROL ID 겹치기]** 위젯은 벤 다이어그램 또는 설정 다이어그램을 사용하여 선택한 두 개의 ID가 포함된 프로필 저장소에 프로필의 겹침을 표시합니다.

위젯 드롭다운 메뉴를 사용하여 비교할 ID를 선택합니다. 원은 각 ID가 포함된 프로필의 상대적 총 개수를 표시합니다. 두 ID가 모두 포함된 프로필 수는 원 간의 겹침 크기로 표시됩니다. 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 ID가 해당 개별 고객과 연결되므로 조직에서 두 개 이상의 ID의 조각을 포함하는 여러 프로필을 가질 수 있습니다.

프로필 조각에 대한 자세한 내용은 [프로필 조각과 병합된 프로필](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) ( 실시간 고객 프로필 개요 )를 참조하십시오.

ID에 대해 자세히 알아보려면 [Adobe Experience Platform Identity Service 설명서](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

### [!UICONTROL 단일 ID 프로필] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="단일 ID 프로필"
>abstract="이 위젯은 ID를 만드는 유형의 ID만 있는 조직의 프로필 수를 제공합니다. 이 ID 유형은 이메일 또는 ECID일 수 있습니다."

다음 [!UICONTROL 단일 ID 프로필] 위젯은 해당 id를 만드는 하나의 유형의 ID만 사용하는 조직의 프로필 수를 제공합니다. 이 ID 유형은 이메일 또는 ECID일 수 있습니다. 프로필 수는 최신 스냅샷에 포함된 데이터에서 생성됩니다.

![단일 ID 프로필 위젯.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL ID별 단일 ID 프로필] {#single-identity-profiles-by-identity}

이 위젯에서는 막대 차트를 사용하여 하나의 고유 식별자만 사용하여 식별되는 프로필의 총 수를 보여줍니다. 위젯은 가장 일반적으로 발생하는 ID 중 최대 5개를 지원합니다.

개별 막대 위로 마우스를 가져가면 ID에 대한 총 프로필 수를 설명하는 대화 상자가 표시됩니다.

![ID 위젯별 단일 ID 프로필.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL 세그먼트화되지 않은 프로필] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="세그먼트화되지 않은 프로필"
>abstract="이 위젯은 세그먼트에 첨부되지 않은 모든 프로필의 총 수를 제공하며 조직 전체에서 프로필 활성화 기회를 나타냅니다."

다음 [!UICONTROL 세그먼트화되지 않은 프로필] 위젯은 어떤 세그먼트에도 첨부되지 않은 모든 프로필의 총 수를 제공합니다. 생성된 숫자는 마지막 스냅샷에서 정확하며 조직 전체에서 프로파일 활성화 기회를 나타냅니다. 또한 적절한 ROI를 제공하지 않는 프로필을 확장할 수 있는 기회를 나타냅니다.

![세그먼트화되지 않은 프로필 위젯.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL 세그먼트화되지 않은 프로필 트렌드] {#unsegmented-profiles-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="세그먼트화되지 않은 프로필 트렌드"
>abstract="이 위젯은 주어진 기간 동안 어떤 세그먼트에도 첨부되지 않는 프로필 수에 대한 선 그래프 그림을 제공합니다. 세그먼트에 첨부되지 않은 프로필의 트렌드는 30일, 90일 및 12개월 기간에 걸쳐 시각화할 수 있습니다."

다음 [!UICONTROL 세그먼트화되지 않은 프로필 트렌드] 위젯은 지정된 기간 동안 어떤 세그먼트에도 첨부되지 않는 프로필 수에 대한 선 그래프 일러스트레이션을 제공합니다. 세그먼트에 첨부되지 않은 프로필의 트렌드는 30일, 90일 및 12개월 기간에 걸쳐 시각화할 수 있습니다. 기간은 위젯의 드롭다운 메뉴에서 선택됩니다. 프로파일 수는 x축의 y축 및 시간에 반영됩니다.

![세그먼트화되지 않은 프로필 트렌드 위젯.](../images/profiles/unsegmented-profiles-trend.png)

### [!UICONTROL ID로 세그먼트화되지 않은 프로필] {#unsegmented-profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="ID로 세그먼트화되지 않은 프로필"
>abstract="이 위젯은 세그먼트화되지 않은 프로필의 총 수를 고유 식별자로 분류합니다."

다음 [!UICONTROL ID로 세그먼트화되지 않은 프로필] 위젯은 세그먼트화되지 않은 프로필의 총 수를 고유 식별자로 분류합니다. 쉽게 비교할 수 있도록 데이터가 막대 차트에 시각화됩니다.

![ID 위젯별로 세그먼트화되지 않은 프로필.](../images/profiles/unsegmented-profiles-by-identity.png)

### [!UICONTROL 대상자] {#audiences}

이 위젯은 프로필 데이터에 적용된 선택한 병합 정책에 따라 활성화될 준비가 된 총 세그먼트 수를 제공합니다.

선택 **[!UICONTROL 대상]** 로 이동 [!UICONTROL 세그먼트] 대시보드 [!UICONTROL 찾아보기] 탭. 여기에서 조직의 모든 세그먼트 정의 목록을 볼 수 있습니다.

![대상 위젯.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.  

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by highest or lowest overlap percentages by selected merge policy. -->
<!-- ![The Audiences overlap report widget.]() -->
<!-- https://jira.corp.adobe.com/browse/PLAT-126851 -->

### [!UICONTROL 대상 상태에 매핑된 대상] {#audiences-mapped-to-destination-status}

다음 [!UICONTROL 대상 상태에 매핑된 대상] 위젯은 단일 지표에 매핑되고 매핑되지 않은 대상의 총 수를 표시하고 도넛 차트를 사용하여 해당 합계의 비례 차이를 보여줍니다. 계산된 숫자는 선택한 병합 정책에 따라 달라집니다.

커서가 도넛 차트의 각 섹션을 마우스로 가리키면 매핑된 대상이나 매핑되지 않은 대상에 대한 개별 카운트가 대화 상자에 표시됩니다.

![대상 상태 위젯에 매핑된 대상](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL 대상 크기] {#audiences-size}

다음 [!UICONTROL 대상 크기] 위젯은 최대 20개의 세그먼트와 각 세그먼트에 포함된 총 대상 수를 나열하는 2열 테이블을 제공합니다. 목록은 총 대상 수에 따라 높음에서 낮음순으로 정렬됩니다. 총 대상 크기 번호는 적용된 병합 정책에 따라 다릅니다.

![대상 크기 위젯.](../images/profiles/audiences-size.png)

세그먼트에 대한 포괄적인 정보를 보려면 제공된 목록에서 세그먼트 이름을 선택하여 로 이동합니다 [!UICONTROL 세그먼트] [!UICONTROL 세부 사항] 페이지. 또한, **[!UICONTROL 모든 세그먼트 보기]** 위젯의 끝에서 [!UICONTROL 세그먼트] [!UICONTROL 찾아보기] 탭을 클릭하여 기존 세그먼트를 찾습니다.

![세그먼트 이름이 있는 대상 크기 위젯과 강조 표시된 모든 세그먼트 텍스트를 봅니다.](../images/profiles/audiences-size-view-all-segments.png)

자세한 내용은 설명서 를 참조하십시오. [[!UICONTROL 세그먼트] [!UICONTROL  찾아보기] 탭](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#browse).

### [!UICONTROL 병합 정책별 대상 겹치기] {#audience-overlap-by-merge-policy}

이 위젯은 벤 다이어그램을 사용하여 선택한 두 세그먼트의 겹침을 표시합니다. 병합 정책은 페이지 맨 위의 개요 드롭다운에서 선택되고 분석을 위한 세그먼트는 위젯 내의 두 드롭다운 메뉴에서 선택됩니다. 관련 세그먼트 정의 내에 포함된 총 프로필 수는 원 또는 교차를 마우스로 가리키면 볼 수 있습니다.

위젯에 세그먼트 정의의 시각적 크로스오버가 표시되므로 세그먼트 정의 간의 유사성을 검토하여 세그멘테이션 전략을 최적화할 수 있습니다.

![병합 정책 드롭다운과 위젯 세그먼트 드롭다운이 강조 표시된 플랫폼 UI 프로필 대시보드 .](../images/profiles/audience-overlap-by-merge-policy.png)


## (베타) 프로필 효율성 위젯 {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>프로필 효과 위젯은 현재 베타 버전이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe은 데이터 분석에 사용할 수 있는 수집된 프로필의 완전성을 평가하는 여러 위젯을 제공합니다. 각각의 프로필 효과 위젯은 병합 정책에 의해 필터링할 수 있습니다. 병합 정책 필터를 변경하려면[!UICONTROL 병합 정책을 사용한 프로필] 드롭다운을 클릭하고 사용 가능한 목록에서 적절한 정책을 선택합니다.

각 프로필 효과 위젯에 대해 자세히 알려면 다음 목록에서 위젯의 이름을 선택합니다.

* [[!UICONTROL 속성 품질 평가]](#attributes-quality-assessment)
* [[!UICONTROL 완벽을 기한 프로필]](#profiles-by-completeness)
* [[!UICONTROL 프로필 완결성 트렌드]](#profiles-completeness-trend)

### (베타) [!UICONTROL 속성 품질 평가] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="속성 품질 평가"
>abstract="이 위젯은 속성에 따라 모든 프로필의 완전성과 카디널리티를 보여줍니다. 각 행은 하나의 속성에 대해 설명합니다. 다음 **프로필** 열은 이 속성이 있고 null이 아닌 값으로 채워진 프로필 수를 제공합니다. 다음 **완전성** 백분율은 이 속성을 가지고 있고 null이 아닌 값으로 채워진 프로필의 총 개수를 해당 속성에 대한 프로필의 비어 있지 않은 값의 총 수로 나눈 값에 의해 결정됩니다. **카디널리티** 모든 속성에 대해 이 속성의 null이 아닌 고유한 값의 총 수를 제공합니다."

다음 [!UICONTROL 속성 품질 평가] 위젯은 속성에 따라 모든 프로필의 완전성과 카디널리티를 보여줍니다. 데이터가 마지막 처리 날짜까지 정확합니다. 이 정보는 테이블의 각 행이 단일 속성을 나타내는 네 개의 열이 있는 테이블로 표시됩니다.

| 열 | 설명 |
|---|---|
| 속성 | 속성의 이름입니다. |
| 프로필 | 이 특성이 있고 null이 아닌 값으로 채워진 프로필 수입니다. |
| 완전성 | 이 백분율은 이 속성을 가지고 있고 null이 아닌 값으로 채워진 총 프로필 수에 의해 결정됩니다. 이 숫자는 총 프로필 수를 해당 속성의 프로필에서 비어 있지 않은 값의 총 수로 나누어 계산됩니다. |
| 카디널리티 | 총 개수 **고유** 이 특성의 null이 아닌 값. 모든 프로필에서 측정됩니다. |

![속성 품질 평가 위젯](../images/profiles/attributes-quality-assessment.png)

### (베타) [!UICONTROL 완벽을 기한 프로필] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="완벽을 기한 프로필"
>abstract="도넛 차트는 관찰된 모든 속성 중에서 null이 아닌 값으로 채워진 프로필 속성의 백분율을 표시합니다. 높은 프로필, 중간 또는 완전성이 낮은 프로필의 비율을 보여줍니다. 완전성이 높은 프로필의 속성 중 70% 이상이 채워졌습니다. 중간 완결성 프로필의 속성 중 30%에서 70% 사이가 채워진 것입니다. 완전성이 낮은 프로필의 속성은 채워진 속성의 30% 미만입니다."

다음 [!UICONTROL 완벽을 기한 프로필] 위젯은 마지막 처리 날짜 이후 최종 프로필 완결성 도넛 차트를 만듭니다. 프로필의 완전성은 관찰된 모든 속성 중에서 null이 아닌 값으로 채워진 속성의 백분율로 측정됩니다.

이 위젯은 높은 프로필, 중간 또는 낮은 완전성을 나타내는 프로필의 비율을 표시합니다. 기본적으로 구성된 완결성 수준은 다음과 같습니다.

* 높은 완전성: 프로필의 속성 중 70% 이상이 채워져 있습니다.
* 미디어 완결성: 프로필의 속성 중 30%~70% 가량이 채워져 있습니다.
* 낮은 완결성: 프로필의 속성 중 30% 미만이 입력되었습니다.

![완결성 위젯의 프로필](../images/profiles/profiles-by-completeness.png)

### (베타) [!UICONTROL 프로필 완결성 트렌드] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="프로필 완결성 트렌드"
>abstract="이 위젯은 시간 경과에 따른 프로필 완결성의 트렌드를 나타내는 스택 영역 차트를 만듭니다. 완전성은 관찰된 모든 속성 중에서 null이 아닌 값으로 채워진 속성의 백분율로 측정됩니다."

이 위젯은 시간 경과에 따른 프로필 완결성의 트렌드를 나타내는 스택 영역 차트를 만듭니다. 완전성은 관찰된 모든 속성 중에서 null이 아닌 값으로 채워진 속성의 백분율로 측정됩니다. 마지막 처리 날짜 이후 프로필 완전성을 높음, 중간 또는 낮은 완전성으로 분류합니다.

x축은 시간을 나타내고, y축은 프로필 수를 나타내고, 색상은 세 가지 프로필 완결성 수준을 나타냅니다.

세 가지 완결성 수준은 다음과 같습니다.

* 높은 완전성: 프로필의 속성 중 70% 이상이 채워졌습니다.
* 미디어 완결성: 프로필의 속성 중 70% 미만과 30% 이상이 채워진 경우
* 낮은 완결성: 프로필의 속성 중 30% 미만이 입력되었습니다.

![프로필 완결성 트렌드 위젯](../images/profiles/profiles-completeness-trend.png)

## 다음 단계

이제 이 문서를 따라 프로필 대시보드를 찾고 사용 가능한 위젯에 표시되는 지표를 이해할 수 있습니다. 작업 방법에 대해 자세히 알아보려면 [!DNL Profile] Experience Platform UI의 데이터는 [실시간 고객 프로필 UI 안내서](../../profile/ui/user-guide.md).
