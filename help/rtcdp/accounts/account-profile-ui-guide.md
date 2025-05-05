---
keywords: rtcdp 프로필;프로필 rtcdp;rtcdp id;rtcdp 병합 정책;실시간 고객 프로필
title: 계정 프로필 UI 안내서
description: Adobe Real-Time Customer Data Platform B2B edition을 사용하면 계정 프로필을 사용하여 여러 소스에서 계정 정보를 통합할 수 있습니다. 이 안내서에서는 Adobe Experience Platform 사용자 인터페이스에서 계정 프로필과 상호 작용하는 방법에 대한 세부 정보를 제공합니다.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Profiles, B2B
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---

# 계정 프로필 UI 안내서

>[!NOTE]
>
>계정 프로필은 Real-Time Customer Data Platform B2B edition 고객만 사용할 수 있습니다. 각 라이선스 유형에서 사용할 수 있는 기능 및 기능을 포함하여 Real-Time CDP에 대한 자세한 내용은 [Real-Time CDP 개요](../overview.md)를 참조하세요.

계정 프로필을 사용하면 여러 소스의 계정 정보를 통합할 수 있습니다. 이렇게 통합된 계정 보기는 많은 마케팅 채널 및 조직에서 현재 고객 계정 정보를 저장하는 데 사용하는 다양한 시스템에서 데이터를 수집합니다. 이 문서에서는 Adobe Experience Platform UI(사용자 인터페이스)에서 사용할 수 있는 Real-Time CDP, B2B edition 기능을 사용하여 계정 프로필과 상호 작용하는 방법에 대한 안내서를 제공합니다.

B2B 워크플로의 일부로 계정 프로필을 만드는 방법에 대한 자세한 내용은 [전체 튜토리얼](../b2b-tutorial.md)을 참조하세요.

## 계정 프로필 개요 {#account-profiles-overview}

계정 프로필 개요를 보려면 왼쪽 탐색에서 [!UICONTROL 계정] 아래의 **[!UICONTROL 프로필]**&#x200B;을 선택하십시오. [!UICONTROL 개요] 탭에서 대시보드에는 단일 진입점에 위젯을 표시하는 그래픽 또는 차트가 표시됩니다.

![왼쪽 탐색 메뉴의 프로필과 개요가 강조 표시된 계정 프로필 개요 탭](images/b2b-account-profile-overview.png)

자세한 내용은 [[!UICONTROL 계정 프로필]](../../dashboards/guides/account-profiles.md) 대시보드의 설명서를 참조하세요. 인사이트 데이터 모델을 사용하여 대시보드에 대한 사용자 지정 차트를 만드는 방법에 대한 자세한 내용은 [실시간 고객 데이터 플랫폼 인사이트 데이터 모델 B2B edition](../../dashboards/data-models/cdp-insights-data-model-b2b.md)에 대한 설명서를 참조하십시오.

## 리드-계정 일치 구성 {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> B2B AI 관리자만 계정 일치 서비스에 대한 리드를 활성화, 비활성화 및 구성할 수 있습니다. 서비스를 비활성화하면 24시간 내에 일치하는 결과가 삭제됩니다.

리드-계정 일치를 구성하려면 왼쪽 탐색 메뉴의 [!UICONTROL 계정]에서 **[!UICONTROL 프로필]**&#x200B;을 선택하십시오. **[!UICONTROL 개요]** 탭에서 오른쪽 상단의 **[!UICONTROL 설정]**&#x200B;을 선택합니다.

![설정이 강조 표시된 계정 프로필 개요 탭](images/b2b-configuring-accounts-profile.png)

**[!UICONTROL 계정 설정]** 대화 상자가 열립니다. 여기에서 **[!UICONTROL 리드-계정 일치 활성화]** 전환을 선택하여 기능을 활성화하십시오. 드롭다운 메뉴를 사용하여 **[!UICONTROL 일치하는 케이던스]** 설정에 대해 **[!UICONTROL 일별]**&#x200B;을(를) 선택하십시오. 마지막으로 관련 **[!UICONTROL 일치 기준]** 옵션 다음에 **[!UICONTROL 저장]**&#x200B;을 선택하여 설정을 확인하고 **[!UICONTROL 계정 프로필]** 화면으로 돌아갑니다.

>[!NOTE]
>
> 주소는 유일한 일치 기준으로 사용할 수 없습니다. 일치하는 다른 기준 중 하나 이상을 선택해야 합니다.

![계정 설정 구성](images/b2b-configuring-account-settings.png)

리드-계정 일치에 대한 자세한 내용은 Real-Time CDP B2B 개요의 [리드-계정 일치 개요](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)를 참조하십시오.

## 계정 프로필 찾아보기 {#browse-account-profiles}

계정 프로필을 찾아보려면 왼쪽 탐색에서 [!UICONTROL 계정]의 **[!UICONTROL 프로필]**&#x200B;을(를) 선택하십시오.

**[!UICONTROL 찾아보기]** 탭에서 연결된 엔터프라이즈 원본의 계정 ID를 사용하거나 원본 세부 정보를 직접 입력하여 계정 프로필을 탐색할 수 있습니다.

![계정 ID를 사용하여 프로필 탐색](images/b2b-account-browse-by.png)

### [!UICONTROL 연결된 엔터프라이즈 원본]별 검색 {#browse-by-connected-enterprise-source}

연결된 엔터프라이즈 소스별로 계정 프로필을 찾아보려면 **[!UICONTROL 찾아보기 기준]** 드롭다운에서 **[!UICONTROL 연결된 엔터프라이즈 소스]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Source]** 필드 옆에 있는 선택기 단추를 사용하여 연결된 소스를 선택하십시오.

![연결된 엔터프라이즈 소스별로 계정 프로필 찾아보기](images/b2b-account-browse.png)

이렇게 하면 조직에서 설정한 연결을 기반으로 소스를 선택할 수 있는 **[!UICONTROL 소스 선택]** 대화 상자가 열립니다.

>[!NOTE]
>
>조직에 동일한 서비스 공급자(예: Marketo)에 대해 구성된 소스가 여러 개 있을 수 있으므로, 연결 이름, 소스 시스템 및 소스 시스템 인스턴스를 검토하여 올바른 소스 인스턴스로 검색하는지 확인해야 합니다.

Enterprise 소스 연결에 대한 자세한 내용은 [소스 개요](../sources/sources-overview.md)를 참조하십시오.

연결 이름 옆에 있는 라디오 단추를 선택하여 소스를 선택한 다음 **[!UICONTROL 선택]**&#x200B;을 사용하여 [!UICONTROL 찾아보기] 탭으로 돌아갈 수 있습니다.

![소스 워크플로우 선택](images/b2b-account-select-source.png)

소스를 선택한 상태에서 이제 소스와 관련된 **[!UICONTROL 계정 ID]**&#x200B;를 입력해야 합니다. 예를 들어 Salesforce 소스를 선택하면 해당 ID에 연결된 계정 프로필을 보기 위해 Salesforce 인스턴스에서 계정 ID를 입력해야 합니다.

>[!NOTE]
>
>Marketo 계정 ID의 경우 참조할 수 있는 두 가지 가능한 계정 테이블이 있으므로 올바른 계정을 볼 수 있도록 특정 구문을 사용해야 합니다.
>
>가장 일반적인 표준 구문은 `.mkto_org`(예: `1234567.mkto_org`)이 추가된 Marketo 계정 ID입니다. Marketo Account-Based Marketing 고객에게는 `.mkto_account`이(가) 추가된 Marketo 계정 ID를 사용하여 찾을 수 있는 추가 값이 있을 수 있습니다. 사용할 구문을 잘 모르는 경우 Marketo 관리자에게 문의하십시오.

![계정 ID 선택](images/b2b-account-browse-id.png)

### [!UICONTROL 기타] 검색 {#browse-by-others}

Real-Time CDP, B2B edition에서는 보려는 계정에 대해 **[!UICONTROL Source 이름]**, **[!UICONTROL Source 인스턴스]** 및 **[!UICONTROL 계정 ID]**&#x200B;를 입력할 수 있도록 하여 직접 조회를 수행하는 기능을 지원합니다. 소스 이름과 인스턴스를 직접 입력하여 Experience Platform이 올바른 계정 프로필 데이터를 검색하고 표시하는 데 필요한 컨텍스트를 제공합니다.

직접 조회를 수행하는 기능은 데이터에 직접 소스 연결이 불가능한 상황에서 유용합니다. 예를 들어 조직에 CRM에 직접 연결할 수 없는 데이터 거버넌스 정책이 있는 경우 해당 데이터를 클라우드 스토리지 시스템으로 내보낸 다음 Experience Platform으로 수집할 수 있습니다.

또 다른 예는 시스템에서 나와 Experience Platform으로 들어가는 시간 사이에 데이터에 대한 변환을 수행하는 것입니다. 직접 조회 기능을 사용하여 데이터에 대한 컨텍스트를 제공하여(예를 들어 Amazon S3 버킷에서 가져온다는 사실에도 불구하고 Marketo 데이터임을 지정하는 등) 시스템에서 데이터를 찾을 위치와 적절하게 렌더링하는 방법을 알 수 있습니다.

직접 조회를 시작하려면 **[!UICONTROL 찾아보기]** 드롭다운에서 **[!UICONTROL 기타]**&#x200B;를 선택한 다음 보려는 계정에 대해 **[!UICONTROL Source 이름]**, **[!UICONTROL Source 인스턴스]** 및 **[!UICONTROL 계정 ID]**&#x200B;를 입력하십시오.

![다른 사용자가 찾아보기](images/b2b-account-browse-adhoc.png)

## 계정 프로필 세부 정보 보기 {#view-account-profile-details}

**[!UICONTROL 찾아보기]** 탭을 사용하여 계정 프로필을 찾은 후 **[!UICONTROL 프로필 ID]**&#x200B;를 선택하면 계정 프로필에 대한 **[!UICONTROL 세부 정보]** 탭이 열립니다. **[!UICONTROL 세부 정보]** 탭에 표시되는 프로필 정보가 여러 프로필 조각에서 병합되어 개별 계정의 단일 보기를 형성했습니다. 여기에는 기본 속성 및 소셜 미디어 데이터와 같은 계정 세부 사항이 포함됩니다.

표시되는 기본 필드를 조직 수준에서 변경하여 기본 계정 프로필 속성을 표시할 수도 있습니다.

>[!NOTE]
>
>고객 프로필에 유사한 기능을 사용할 수 있으며 속성 추가 및 제거, 패널 크기 조정 등에 대한 지침과 함께 단계별 안내서가 작성되었습니다. 자세한 내용은 [프로필 세부 정보 사용자 지정 안내서](../../profile/ui/profile-customization.md)를 참조하십시오.

![계정 프로필 세부 정보 보기](images/b2b-account-details.png)

사용 가능한 탭 중 하나를 선택하여 계정과 관련된 추가 세부 정보를 볼 수 있습니다. 이러한 탭에는 속성, 인력 및 엔터프라이즈 시스템 전반의 계정과 관련된 개설 및 마감 기회를 표시하는 기회 탭이 포함됩니다. 각 탭에 대한 자세한 내용은 다음 섹션을 참조하십시오.

## 속성 탭 {#attributes-tab}

**[!UICONTROL 특성]** 탭에는 계정과 관련된 모든 레코드 정보가 나열됩니다. 여기에는 계정의 단일 보기를 형성하기 위해 함께 병합된 여러 소스에서 가져온 속성 데이터가 포함됩니다.

목록에서 데이터를 볼 수 있을 뿐만 아니라 검색 창을 사용하여 특정 속성을 검색하거나 레코드 데이터를 JSON으로 볼 수 있습니다.

![특성 탭](images/b2b-account-attributes.png)

## 인물 탭 {#people-tab}

**[!UICONTROL 사람]** 탭에서는 계정과 연결된 개별 사용자 목록을 제공합니다. 이러한 직원은 조직 내의 다른 팀에서 관리하는 다른 엔터프라이즈 시스템의 연락처 및 잠재 고객일 수 있지만, Real-Time CDP의 B2B edition에서는 계정 연락처를 보다 전체적으로 볼 수 있도록 단일 목록으로 표시됩니다.

>[!NOTE]
>
>[!UICONTROL 사람] 탭에는 계정과 연결된 최대 25명의 목록이 표시됩니다. 연결된 사람이 25명 이상인 계정의 경우 시스템에서 25개의 레코드를 무작위로 샘플링합니다.

연락처에 대한 정보 스냅숏을 표시하는 것 외에도 나열된 각 사용자에는 해당 사용자에 대한 실시간 고객 프로필을 살펴볼 수 있는 클릭 가능한 링크인 **[!UICONTROL 프로필 ID]**&#x200B;도 포함됩니다. 계정과 관련된 개별 고객 프로필을 보는 방법에 대한 자세한 내용은 [Real-Time CDP, B2B edition에서 프로필 탐색](../profile/profile-browse.md)을 위한 안내서를 참조하십시오.

![사람 탭](images/b2b-account-people.png)

## 기회 탭 {#opportunities-tab}

**[!UICONTROL 기회]** 탭에서는 계정과 관련된 개설 및 마감된 기회에 대한 정보를 제공합니다. 이러한 기회는 여러 소스에서 Experience Platform에 수집될 수 있지만, Real-Time CDP, B2B edition을 통해 마케터는 이러한 모든 기회를 한 곳에서 함께 볼 수 있습니다.

>[!NOTE]
>
>[!UICONTROL 기회] 탭에는 계정과 연결된 최대 25개의 기회 목록이 표시됩니다. 관련 영업 기회가 25개 이상인 고객의 경우 시스템에서 25개 레코드의 임의 샘플링을 표시합니다.

각 영업 기회는 영업 기회의 이름, 금액, 단계, 영업 기회의 개설 여부, 마감 여부, 성공 여부, 손실 여부 등의 정보를 포함합니다.

![계정 기회 탭](images/b2b-account-opportunities.png)

## 관련 계정 탭 {#related-accounts-tab}

**[!UICONTROL 관련 계정]** 탭에는 검색 중인 계정과 관련된 다른 계정에 대한 정보가 있습니다. 기능에 대한 자세한 내용은 [관련 계정 개요](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)를 참조하십시오.

>[!NOTE]
>
>* 관련 계정 그룹은 최대 30개의 계정 프로필을 가질 수 있습니다. 30개 이상의 계정 프로필이 관련성이 발견되면 임의로 여러 그룹으로 나뉘며, 각각 30명 이하의 구성원을 가지고 있습니다. 계정 프로필의 관련 계정 그룹은 항상 자신을 포함합니다.
>* [!UICONTROL 관련 계정] 탭에는 현재 검색 중인 계정과 연결된 최대 25개의 관련 계정 목록이 표시됩니다. 이는 향후 업데이트에서 다루게 될 제한 사항입니다. 이러한 UI 제한에도 불구하고 세그먼트 정의에서 관련 계정을 사용할 때 30개의 관련 계정 프로필 그룹의 경우 모든 프로필이 타겟팅에 사용됩니다.

각 관련 계정에는 계정 프로필 ID 및 이름, 계정 소스 키, 홈페이지, 주소, 상위 계정, 전화, 업계 및 연간 매출과 관련된 추가 정보 등의 정보가 포함됩니다.

![관련 계정 탭](images/b2b-account-related-accounts.png)

세분화 목적으로 이 목록의 관련 계정을 사용할 수 있습니다. 관련 계정을 사용하여 세그먼트 정의에서 범위를 확장하는 방법을 이해하려면 [세그먼테이션 예제](/help/rtcdp/segmentation/b2b.md#related-account)를 참조하십시오.