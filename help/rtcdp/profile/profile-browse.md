---
keywords: 프로필 rtcdp 보기;rtcdp 프로필 보기;rtcdp 프로필 보기
title: Real-time Customer Data Platform에서 프로필 찾아보기
description: Real-time Customer Data Platform에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 실시간 고객 프로필 데이터를 검색할 수 있습니다.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 6579e371a8729e926b7061418c786150a27d4876
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Real-time Customer Data Platform에서 프로필 찾아보기

실시간 고객 프로필은 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합함으로써 각 개별 고객에 대한 전체적인 보기를 만듭니다. 개별 프로필은 다양한 소스에서 시스템으로 가져온 데이터를 기반으로 집계되므로 각 프로필은 고객이 브랜드에 보유하고 있는 모든 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정이 됩니다.

Adobe Experience Platform 사용자 인터페이스 내에서는 이러한 읽기 전용 프로필을 보고 해당 환경 설정, 과거 이벤트, 상호 작용 및 개인이 속한 세그먼트 등 각 개별 고객에 대한 중요한 정보를 볼 수 있습니다.

Real-time Customer Data Platform은 Adobe Experience Platform을 기반으로 구축되어 Experience Platform UI에서 프로필 보기 기능을 사용할 수 있습니다. 플랫폼 사용자 인터페이스에서 고객 프로필을 보는 방법에 대한 자세한 안내서는 [실시간 고객 프로필 사용 안내서](../../profile/ui/user-guide.md)를 참조하십시오.

## 실시간 CDP, B2B Edition을 위한 프로필 개선 사항

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform에서 지원하는 프로필 찾아보기 기능 외에도 실시간 CDP와 B2B Edition 사용자는 각각 [!UICONTROL 속성] 및 [!UICONTROL 이벤트] 탭의 고객 프로필 내에서 B2B 속성 및 이벤트에 액세스할 수 있습니다. B2B 데이터는 B2B가 아닌 세그먼트와 함께 고객의 [!UICONTROL 세그먼트 멤버십] 탭 아래에 표시되는 세그먼테이션을 수행하는 데 사용할 수도 있습니다.

실시간 CDP와 B2B Edition을 사용하면 개별 고객과 연관된 엔터프라이즈 소스에서 [!UICONTROL 계정], [!UICONTROL 기회] 및 [!UICONTROL 소스 레코드]를 검색할 수도 있습니다.

이러한 개선 사항을 탐색하려면 [실시간 고객 프로필 사용 안내서](../../profile/ui/user-guide.md)에 설명된 단계를 수행하여 병합 정책 또는 ID 네임스페이스로 프로필을 탐색합니다.

![](images/b2b-browse-profile.png)

프로필 세부 정보에는 B2B 이벤트 및 속성으로 향상된 고객 프로필에 제공된 표준 정보 외에 [!UICONTROL 계정], [!UICONTROL 기회] 및 [!UICONTROL 소스 레코드] 탭에 대한 액세스가 포함됩니다.

![](images/b2b-profile-detail.png)

### 계정 탭

프로필과 관련된 계정 목록을 보려면 **[!UICONTROL 계정]**&#x200B;을 선택합니다. 이 목록에는 계정의 이름, 웹 사이트, 업계 등의 계정 프로필의 기본 정보와 계정 프로필에 대한 링크가 포함되어 있습니다.

계정 프로필 보기 및 탐색에 대한 자세한 내용은 [계정 프로필 개요](../accounts/account-profile-overview.md)를 읽으십시오.

![](images/b2b-profile-accounts.png)

### 기회 탭

**[!UICONTROL Opportunity]** 탭은 계정과 관련된 개설 및 마감된 기회에 대한 세부 정보를 제공합니다. 이러한 기회를 여러 소스에서 Experience Platform에 수집할 수 있지만 실시간 CDP인 B2B Edition을 사용하면 마케터가 이러한 모든 기회를 한 곳에서 함께 볼 수 있습니다.

영업 기회 이름, 영업 기회 금액, 단계, 영업 기회 개설, 마감, 승원 또는 손실 여부 등의 정보가 각 영업 기회에 포함됩니다.

![](images/b2b-profile-opportunities.png)

### 소스 레코드 탭

**[!UICONTROL 소스 레코드]** 탭을 사용하면 단일 고객 프로필에 기여하는 엔터프라이즈 소스에서 온 여러 소스 레코드를 쉽게 볼 수 있습니다. 각 소스 레코드는 [!UICONTROL 개인 소스 키] 및 전자 메일 주소 외에도 레코드 유형(예: &quot;연락처&quot; 또는 &quot;리드&quot; 레코드)과 소스를 제공합니다.

![](images/b2b-profile-source-records.png)
