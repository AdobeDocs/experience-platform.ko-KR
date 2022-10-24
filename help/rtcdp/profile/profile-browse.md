---
keywords: 프로필 rtcdp 보기;rtcdp 프로필 보기;rtcdp 프로필 보기
title: Real-time Customer Data Platform에서 프로필 찾아보기
description: Adobe Real-time Customer Data Platform에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 실시간 고객 프로필 데이터를 검색할 수 있습니다.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Real-time Customer Data Platform에서 프로필 찾아보기

실시간 고객 프로필은 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합함으로써 각 개별 고객에 대한 전체적인 보기를 만듭니다. 개별 프로필은 다양한 소스에서 시스템으로 가져온 데이터를 기반으로 집계되므로 각 프로필은 고객이 브랜드에 보유하고 있는 모든 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정이 됩니다.

Adobe Experience Platform 사용자 인터페이스 내에서는 이러한 읽기 전용 프로필을 보고 해당 환경 설정, 과거 이벤트, 상호 작용 및 개인이 속한 세그먼트 등 각 개별 고객에 대한 중요한 정보를 볼 수 있습니다.

Adobe Real-time Customer Data Platform은 Adobe Experience Platform을 기반으로 구축되어 Experience Platform UI에서 프로필 보기 기능을 사용할 수 있습니다. 플랫폼 사용자 인터페이스 내에서 고객 프로필을 보는 방법에 대한 자세한 안내서는 [실시간 고객 프로필 사용 안내서](../../profile/ui/user-guide.md).

## Real-Time CDP, B2B Edition에 대한 프로필 개선 사항

B2B Edition 사용자는 Adobe Experience Platform에서 지원하는 프로필 찾아보기 기능 외에도 B2B 속성 및 이벤트에 액세스할 수 있습니다. [!UICONTROL 속성] 및 [!UICONTROL 이벤트] 탭들을 나타냅니다. B2B 데이터를 사용하여 세그먼테이션을 수행할 수도 있습니다. 이러한 세그먼트는 고객의 [!UICONTROL 세그먼트 멤버십] 비B2B 세그먼트와 함께 탭합니다.

Real-Time CDP, B2B Edition을 사용하여 검색할 수도 있습니다 [!UICONTROL 계정], [!UICONTROL 기회], 및 [!UICONTROL 소스 레코드] 개별 고객과 연관된 엔터프라이즈 소스에서.

이러한 개선 사항을 탐색하려면 [실시간 고객 프로필 사용 안내서](../../profile/ui/user-guide.md) 병합 정책 또는 id 네임스페이스로 프로필을 찾아보려면 다음을 수행하십시오.

![](images/b2b-browse-profile.png)

프로필 세부 정보에는 [!UICONTROL 계정], [!UICONTROL 기회], 및 [!UICONTROL 소스 레코드] B2B 이벤트 및 속성을 사용하여 개선된 고객 프로필에 제공된 표준 정보 외에도 탭이 있습니다.

![](images/b2b-profile-detail.png)

### 계정 탭

선택 **[!UICONTROL 계정]** 프로필과 관련된 계정 목록을 보려면 이 목록에는 계정의 이름, 웹 사이트, 업계 등의 계정 프로필의 기본 정보와 계정 프로필에 대한 링크가 포함되어 있습니다.

계정 프로필 보기 및 탐색을 위한 자세한 내용은 [계정 프로필 개요](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### 기회 탭

다음 **[!UICONTROL 기회]** 탭에서는 계정과 관련된 개설 및 마감된 기회에 대한 세부 정보를 제공합니다. 이러한 기회를 여러 소스에서 Experience Platform에 수집할 수 있지만 Real-Time CDP, B2B Edition을 사용하면 마케터가 이러한 모든 기회를 한 곳에서 함께 볼 수 있습니다.

영업 기회 이름, 영업 기회 금액, 단계, 영업 기회 개설, 마감, 승원 또는 손실 여부 등의 정보가 각 영업 기회에 포함됩니다.

![](images/b2b-profile-opportunities.png)

### 소스 레코드 탭

다음 **[!UICONTROL 소스 레코드]** 탭에서 단일 고객 프로필에 기여하는 엔터프라이즈 소스에서 온 여러 소스 레코드를 쉽게 볼 수 있습니다. 추가 [!UICONTROL 개인 소스 키] 그리고 전자 메일 주소, 각 소스 레코드에는 원본뿐만 아니라 레코드 유형(예: &quot;연락처&quot; 또는 &quot;리드&quot; 레코드)도 제공합니다.

![](images/b2b-profile-source-records.png)
