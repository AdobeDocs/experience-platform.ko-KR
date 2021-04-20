---
keywords: 대상;adobe experience platform;platform;destinations overview;activate data;activate
title: 대상 개요
seo-title: 대상 개요
description: 크로스 채널 마케팅 캠페인, 이메일, 타깃팅된 광고 등을 위해 Adobe Experience Platform 데이터를 대상으로 활성화하는 방법을 알아봅니다.
seo-description: 대상은 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. Adobe Experience Platform의 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 많은 사용 사례에서 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# [!DNL Destinations] 개요 {#overview}

![대상 개요 배너](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** Adobe Experience Platform의 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 여러 가지 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

## 대상 및 소스 {#destinations-and-sources}

플랫폼의 핵심 기능 중 하나는 자사 데이터를 수집하여 비즈니스 요구에 맞게 데이터를 활성화하는 것입니다. 플랫폼 및 대상으로 데이터를 인제스트하여 플랫폼에서 데이터를 내보내려면 [sources](../sources/home.md)를 사용합니다.

## 대상 단계 {#steps}

* 플랫폼에서 사용 가능한 모든 대상 중 [셀프 서비스 카탈로그](./catalog/overview.md)에서 선택합니다.
* 대상을 [활성화](./ui/activate-destinations.md)하고 프로필 또는 세그먼트를 마케팅 자동화 플랫폼, 디지털 광고 플랫폼 등으로 보냅니다.
* 데이터 내보내기를 정기적으로 원하는 대상으로 예약합니다.

## 컨트롤 {#controls}

[대상 작업 영역](./ui/destinations-workspace.md)의 컨트롤을 사용하여 다음을 수행할 수 있습니다.

* 데이터를 활성화할 수 있는 대상 플랫폼 카탈로그를 찾아보십시오.
* 카탈로그의 대상에 대한 데이터 흐름 만들기, 편집, 활성화 및 비활성화
* 스토리지 위치에 계정을 만들거나 대상 플랫폼의 계정에 플랫폼을 연결합니다.
* 대상에 활성화할 세그먼트를 선택합니다.
* 세그먼트를 이메일 마케팅 대상으로 활성화할 때 내보낼 [XDM(경험 데이터 모델) 필드](../xdm/home.md)을 선택합니다.

## 대상 유형 및 카테고리 {#types-and-categories}

자세한 내용은 [대상 유형 및 카테고리 개요](./destination-types.md)를 참조하십시오.

## 대상 및 액세스 컨트롤 {#access-controls}

플랫폼의 대상 기능은 Adobe Experience Platform 액세스 제어 권한과 함께 작동합니다. 사용자의 권한 수준에 따라 대상을 보고, 관리하고, 활성화할 수 있습니다. 개별 권한에 대한 자세한 내용은 Adobe Experience Platform](../access-control/home.md)의 [액세스 제어 및 페이지 아래쪽으로 스크롤을 참조하십시오.

액세스 제어에 대한 자세한 내용은 [액세스 제어 사용 안내서](../access-control/ui/overview.md)를 참조하십시오.

## [!DNL Data Governance] 대상에 데이터 활성화 제한  {#data-governance}

데이터 거버넌스는 다음을 통해 플랫폼 대상에 적용됩니다.

* *대상* 만들기 워크플로우에서 선택할 수 있는 마케팅 동작;
* *특정* 사용 레이블이 들어 있는 데이터를 특정 마케팅 활동이 있는 대상으로 활성화하지 않는 데이터 사용 정책입니다.

[마케팅 작업](../data-governance/policies/overview.md) 및 [데이터 정책 위반 해결](../data-governance/enforcement/auto-enforcement.md)에 대한 자세한 내용은 플랫폼 설명서의 [!DNL Data Governance]을 참조하십시오.

대상 만들기 워크플로우에서 마케팅 작업을 선택하는 방법에 대한 자세한 내용은 플랫폼의 다양한 대상 유형에 대한 다음 페이지를 참조하십시오.

* [광고 대상 - Google 광고 관리자  ](./catalog/advertising/google-ad-manager.md)
* [광고 대상 - Google 광고](./catalog/advertising/google-ads-destination.md)
* [광고 대상 - Google 디스플레이 및 비디오 360  ](./catalog/advertising/google-dv360.md)
* [클라우드 스토리지 대상](./catalog/cloud-storage/workflow.md)
* [이메일 마케팅 대상](./catalog/email-marketing/overview.md)
* [소셜 대상](./catalog/social/workflow.md)

세그먼트 활성화 작업 과정의 데이터 정책 위반에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](./ui/activate-destinations.md#review)에 대한 검토 단계를 참조하십시오.
