---
keywords: rtcdp 프로필;프로필 rtcdp;rtcdp ID;rtcdp 병합 정책;실시간 고객 프로필
title: 계정 프로필 UI 안내서
description: Real-time Customer Data Platform B2B Edition에서는 계정 프로필을 사용하여 여러 소스에서 계정 정보를 통합할 수 있습니다. 이 안내서에서는 Adobe Experience Platform 사용자 인터페이스의 계정 프로필과 상호 작용하기 위한 세부 사항을 제공합니다.
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 85d3e5f265fdbfd51f184d36205127f005e2b9df
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 0%

---

# 계정 프로필 UI 안내서

>[!NOTE]
>
>계정 프로필은 Real-time Customer Data Platform B2B Edition 고객만 사용할 수 있습니다. 각 라이센스 유형에 사용할 수 있는 기능 및 기능을 포함한 실시간 CDP에 대한 자세한 내용은 [실시간 CDP 개요](../overview.md).

계정 프로필을 사용하면 여러 소스의 계정 정보를 통합할 수 있습니다. 이러한 계정 통합 보기는 다양한 마케팅 채널 및 조직에서 고객 계정 정보를 저장하는 데 현재 사용하는 다양한 시스템의 데이터를 통합합니다. 이 문서에서는 Adobe Experience Platform UI(사용자 인터페이스)에서 사용할 수 있는 실시간 CDP와 B2B Edition 기능을 사용하여 계정 프로필과 상호 작용하는 방법에 대한 안내서를 제공합니다.

B2B 워크플로우의 일부로 계정 프로필을 만드는 방법에 대한 자세한 내용은 다음을 참조하십시오. [엔드 투 엔드 자습서](../b2b-tutorial.md).

## 계정 프로필 개요 {#account-profiles-overview}

선택 **[!UICONTROL 프로필]** 아래에 [!UICONTROL 계정] 왼쪽 탐색에서 계정 프로필 개요를 확인합니다. 아래에 [!UICONTROL 개요] 탭에서 대시보드는 단일 시작 지점에 위젯을 표시하는 그래픽 또는 차트를 표시합니다.

![위젯을 표시하는 개요 탭](images/b2b-account-profile-overview.png)

다음 항목에 대한 설명서를 참조하십시오. [[!UICONTROL 계정 프로필]](../../dashboards/guides/account-profiles.md) 대시보드 를 참조하십시오.

## 리드와 계정 일치 구성 {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> B2B AI 관리자만 계정 일치 서비스에 대한 리드를 활성화, 비활성화 및 구성할 수 있습니다. 서비스를 비활성화하면 24시간 이내에 일치하는 결과가 삭제됩니다.

리드를 계정 일치로 구성하려면 **[!UICONTROL 프로필]** 아래에 [!UICONTROL 계정] 을 클릭합니다. 설정 **[!UICONTROL 개요]** 탭, 선택 **[!UICONTROL 설정]** 오른쪽 위에 있습니다.

![설정 선택](images/b2b-configuring-accounts-profile.png)

다음 **[!UICONTROL 계정 설정]** 대화 상자가 열립니다. 여기에서 **[!UICONTROL Lead-to-Account 일치 활성화]** 기능을 활성화하려면 전환합니다. 드롭다운 메뉴를 사용하여 선택 **[!UICONTROL 일별]** 대상 **[!UICONTROL 일치하는 대상]** 설정 마지막으로 관련 항목을 선택합니다 **[!UICONTROL 일치 기준]** 옵션 뒤에 **[!UICONTROL 저장]** 설정을 확인하고 로 돌아갑니다. **[!UICONTROL 계정 프로필]** 화면.

>[!NOTE]
>
> 주소는 일치하는 유일한 기준으로 사용할 수 없습니다. 다른 일치 기준 중 하나 이상을 선택해야 합니다.

![계정 설정 구성](images/b2b-configuring-account-settings.png)

계정 일치에 대한 리드에 대해 자세히 알아보려면 [실시간 CDP B2B 개요에서 계정 일치 시작](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

## 계정 프로필 찾아보기 {#browse-account-profiles}

계정 프로필을 찾아보려면 먼저 **[!UICONTROL 프로필]** 아래에 [!UICONTROL 계정] 를 클릭합니다.

설정 **[!UICONTROL 찾아보기]** 탭에서 연결된 엔터프라이즈 소스에서 계정 ID를 사용하거나 소스 세부 사항을 직접 입력하여 계정 프로필을 탐색할 수 있습니다.

![계정 ID를 사용하여 프로필 탐색](images/b2b-account-browse-by.png)

### 찾아보기 기준 [!UICONTROL 연결된 엔터프라이즈 소스] {#browse-by-connected-enterprise-source}

연결된 엔터프라이즈 소스별로 계정 프로파일을 찾아보려면 **[!UICONTROL 연결된 엔터프라이즈 소스]** 에서 **[!UICONTROL 찾아보기 기준]** 드롭다운을 선택한 다음 옆에 있는 선택기 단추를 사용하여 연결된 소스를 선택합니다 **[!UICONTROL 소스]** 필드.

![연결된 엔터프라이즈 소스별로 계정 프로필 찾아보기](images/b2b-account-browse.png)

이렇게 하면 **[!UICONTROL 소스 선택]** 대화 상자에서 조직이 설정한 연결을 기반으로 소스를 선택할 수 있습니다.

>[!NOTE]
>
>조직에 동일한 서비스 공급자(예: Marketo)에 대해 구성된 소스가 여러 개 있을 수 있으므로, 올바른 소스 인스턴스에서 검색하고 있는지 확인하려면 연결 이름, 소스 시스템 및 소스 시스템 인스턴스를 검토해야 합니다.

엔터프라이즈 소스 연결에 대한 자세한 내용은 [소스 개요](../sources/sources-overview.md).

연결 이름 옆에 있는 라디오 단추를 선택하여 소스를 선택한 다음 **[!UICONTROL 선택]** 로 돌아가기 [!UICONTROL 찾아보기] 탭.

![소스 워크플로우 선택](images/b2b-account-select-source.png)

소스를 선택한 상태에서 이제 **[!UICONTROL 계정 ID]** 소스와 관련되어 있습니다. 예를 들어, Salesforce 소스를 선택하면 Salesforce 인스턴스에서 계정 ID를 입력해야 해당 ID에 연결된 계정 프로필을 볼 수 있습니다.

>[!NOTE]
>
>Marketo 계정 ID의 경우 참조할 수 있는 계정 테이블이 두 개 있으므로 올바른 계정을 보려면 특정 구문을 사용해야 합니다.
>
>가장 일반적인 표준 구문은 `.mkto_org` (예: `1234567.mkto_org`). Marketo Account-Based Marketing 고객은 다음에 추가한 Marketo 계정 ID를 사용하여 찾을 수 있는 추가 값을 가질 수 있습니다 `.mkto_account`. 사용할 구문을 잘 모르는 경우 Marketo 관리자에게 문의하십시오.

![계정 ID 선택](images/b2b-account-browse-id.png)

### 찾아보기 기준 [!UICONTROL 기타] {#browse-by-others}

실시간 CDP인 B2B Edition은 다음을 입력할 수 있도록 하여 직접 조회를 수행하는 기능을 지원합니다 **[!UICONTROL 소스 이름]**, **[!UICONTROL 소스 인스턴스]**, 및 **[!UICONTROL 계정 ID]** 확인할 계정에 대해 소스 이름과 인스턴스를 직접 입력하여 Experience Platform이 올바른 계정 프로필 데이터를 검색하고 표시하는 데 필요한 컨텍스트를 제공합니다.

직접 조회를 수행하는 기능은 데이터에 직접 연결할 수 없는 상황에서 유용합니다. 예를 들어 조직에 CRM에 직접 연결하지 못하는 데이터 거버넌스 정책이 있는 경우 해당 데이터를 클라우드 스토리지 시스템으로 내보내고 Experience Platform으로 수집할 수 있습니다.

다른 예로 시스템을 종료하고 Platform에 들어가는 시간 사이에 데이터를 변환하는 작업이 있을 수 있습니다. 직접 조회 기능을 사용하여 데이터에 대한 컨텍스트(예: Amazon S3 버킷에서 오고 있다는 사실에도 불구하고 Marketo 데이터임을 지정하는 등)를 제공하여 시스템이 데이터를 찾을 위치와 제대로 렌더링하는 방법을 알 수 있도록 할 수 있습니다.

직접 조회를 시작하려면 **[!UICONTROL 기타]** 에서 **[!UICONTROL 찾아보기 기준]** 드롭다운을 입력한 다음 **[!UICONTROL 소스 이름]**, **[!UICONTROL 소스 인스턴스]**, 및 **[!UICONTROL 계정 ID]** 보려는 계정에 대해

![다른 사람의 찾아보기](images/b2b-account-browse-adhoc.png)

## 계정 프로필 세부 사항 보기 {#view-account-profile-details}

를 사용한 후 **[!UICONTROL 찾아보기]** 탭에서 계정 프로필을 찾아 **[!UICONTROL 프로필 ID]** 열기 **[!UICONTROL 세부 사항]** 계정 프로필에 대한 탭입니다. 에 표시되는 프로필 정보 **[!UICONTROL 세부 사항]** 탭이 여러 프로필 조각에서 병합되어 개별 계정의 단일 보기를 형성했습니다. 여기에는 기본 속성 및 소셜 미디어 데이터와 같은 계정 세부 사항이 포함됩니다.

표시되는 기본 필드는 기본 계정 프로필 속성을 표시하기 위해 조직 수준에서 변경할 수도 있습니다.

>[!NOTE]
>
>고객 프로필에 유사한 기능을 사용할 수 있으며, 속성 추가 및 제거, 크기 조정 패널 등에 대한 지침과 함께 단계별 안내서를 만들었습니다. 자세한 내용은 [프로필 세부 정보 사용자 지정 안내서](../../profile/ui/profile-customization.md) 추가 정보

![계정 프로필 세부 사항 보기](images/b2b-account-details.png)

사용 가능한 다른 탭을 선택하여 계정과 관련된 추가 세부 사항을 볼 수 있습니다. 이러한 탭에는 기업 시스템의 계정과 관련된 개설 및 마감된 기회를 보여주는 속성, 인력 및 기회 탭이 포함됩니다. 각 탭에 대한 자세한 내용은 다음 섹션을 참조하십시오.

## 속성 탭 {#attributes-tab}

다음 **[!UICONTROL 속성]** 탭에는 계정과 관련된 모든 레코드 정보가 나열됩니다. 여기에는 단일 계정 보기를 구성하기 위해 함께 병합된 여러 소스에서 온 특성 데이터가 포함됩니다.

목록에서 데이터를 볼 수 있을 뿐만 아니라 검색 막대를 사용하여 특정 속성을 검색하거나 레코드 데이터를 JSON으로 볼 수 있습니다.

![속성 탭](images/b2b-account-attributes.png)

## 사람 탭 {#people-tab}

다음 **[!UICONTROL 사람]** 탭에는 계정과 연결된 개별 사용자 목록이 있습니다. 이러한 사용자는 조직 내의 여러 팀이 관리하는 다양한 엔터프라이즈 시스템의 연락처 및 리드일 수 있지만 실시간 CDP에서는 B2B Edition을 하나의 목록으로 함께 제공하여 계정 연락처를 보다 포괄적으로 볼 수 있습니다.

>[!NOTE]
>
>다음 [!UICONTROL 사람] 탭에는 계정과 연결된 최대 25명의 사람 목록이 표시됩니다. 25명 이상의 관련 사용자가 있는 계정의 경우 시스템에서 25개의 레코드를 임의 샘플링합니다.

목록에 나열된 각 사용자에게는 연락처에 대한 정보 스냅숏도 표시됩니다 **[!UICONTROL 프로필 ID]**: 해당 개인의 실시간 고객 프로필을 탐색할 수 있는 클릭 가능한 링크입니다. 계정과 관련된 개별 고객 프로필을 보는 방법에 대한 자세한 내용은 [실시간 CDP, B2B Edition에서 프로필 검색](../profile/profile-browse.md).

![사람 탭](images/b2b-account-people.png)

## 기회 탭 {#opportunities-tab}

다음 **[!UICONTROL 기회]** 탭에서는 계정과 관련된 개설 및 마감된 기회에 대한 정보를 제공합니다. 이러한 기회를 여러 소스에서 Experience Platform에 수집할 수 있지만 실시간 CDP인 B2B Edition을 사용하면 마케터가 이러한 모든 기회를 한 곳에서 함께 볼 수 있습니다.

>[!NOTE]
>
>다음 [!UICONTROL 기회] 탭에는 계정과 연관된 최대 25개의 기회 목록이 표시됩니다. 연관된 영업 기회가 25개 이상인 고객의 경우, 시스템에서 25개의 레코드를 임의 샘플링합니다.

영업 기회 이름, 영업 기회 금액, 단계, 영업 기회 개설, 마감, 승원 또는 손실 여부 등의 정보가 각 영업 기회에 포함됩니다.

![계정 기회 탭](images/b2b-account-opportunities.png)

## 관련 계정 탭 {#related-accounts-tab}

다음 **[!UICONTROL 관련 계정]** 탭에서는 탐색 중인 계정과 관련된 다른 계정에 대한 정보를 제공합니다. 기능에 대한 자세한 내용은 [관련 계정 개요](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* 관련 계정 그룹은 최대 30개의 계정 프로필을 가질 수 있습니다. 30개 이상의 계정 프로필이 관련된 경우 임의로 여러 그룹으로 분할되고 각각 30명 이하의 구성원을 갖습니다. 계정 프로필의 관련 계정 그룹은 항상 자신을 포함합니다.
>* 다음 [!UICONTROL 관련 계정] 현재 탭에는 탐색 중인 계정과 연결된 최대 25개의 관련 계정 목록이 표시됩니다. 이는 향후 업데이트로 해결될 수 있는 제한 사항입니다. 이 UI 제한 사항에도 불구하고 세그먼트 정의에 관련 계정을 사용하는 경우 30개의 관련 계정 프로필 그룹의 경우 모든 프로필이 타겟팅에 사용됩니다.


각 관련 계정에는 계정 프로필 ID 및 이름, 해당 계정 소스 키와 같은 정보가 포함되며, 홈 페이지, 주소, 상위 계정, 전화, 업계 및 연간 매출과 관련된 추가 정보가 포함됩니다.

![관련 계정 탭](images/b2b-account-related-accounts.png)

이 목록에서 관련 계정을 세그멘테이션을 위해 사용할 수 있습니다. 다음을 참조하십시오 [세분화 예](/help/rtcdp/segmentation/b2b.md#related-account) 관련 계정을 사용하여 세그먼트 정의에서 도달 범위를 확장하는 방법을 이해합니다.