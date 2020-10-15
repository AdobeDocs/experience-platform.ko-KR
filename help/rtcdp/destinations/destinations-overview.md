---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;destinations;destination;rtcdp
title: 대상 개요
seo-title: 대상 개요
description: 크로스 채널 마케팅 Campaign, 이메일, 타겟팅 광고 등을 위해 플랫폼 데이터를 대상으로 활성화합니다.
seo-description: 대상은 실시간 고객 데이터 플랫폼에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. Adobe 실시간 고객 데이터 플랫폼의 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 여러 가지 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
translation-type: tm+mt
source-git-commit: 4e358fda1c8f7aebe57a009a146b8b73cf88e169
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 3%

---


# [!DNL Destinations]개요{#overview}

![대상 개요 배너](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**[!DNL Destinations]** 실시간 고객 데이터 플랫폼에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

## 대상 및 소스 {#destinations-and-sources}

실시간 CDP의 핵심 기능 중 하나는 자사 데이터를 수집하여 비즈니스 요구 사항에 맞게 활성화하는 것입니다. 데이터를 실시간 CDP 및 대상으로 인제스트하여 실시간 CDP에서 데이터를 내보낼 수 있습니다.

## 대상 단계 {#steps}

* 실시간 CDP에서 사용할 수 있는 모든 대상의 [셀프 서비스 카탈로그](/help/rtcdp/destinations/destinations-catalog.md) 중에서 선택할 수 있습니다.
* 대상을 **[!UICONTROL 사용하여]** 프로필 또는 세그먼트를 [활성화하고](/help/rtcdp/destinations/activate-destinations.md) 마케팅 자동화 플랫폼, 디지털 광고 플랫폼 등으로 보낼 수 있습니다.
* 데이터 내보내기를 주기적으로 원하는 대상으로 예약합니다.

## 컨트롤 {#controls}

대상 작업 영역의 [컨트롤을](/help/rtcdp/destinations/destinations-workspace.md) 사용하여 다음을 수행할 수 있습니다.

* 데이터를 활성화할 수 있는 대상 플랫폼 카탈로그를 찾아보십시오.
* 카탈로그의 대상에 대한 데이터 흐름 만들기, 편집, 활성화 및 비활성화
* 스토리지 위치에 계정을 만들거나 대상 플랫폼의 계정에 실시간 CDP를 연결합니다.
* 대상에 활성화할 세그먼트 선택;
* 세그먼트를 이메일 마케팅 [대상으로 활성화할 때 내보낼 경험 데이터 모델(XDM) 필드를](../../xdm/home.md) 선택합니다.

## Destination types and categories {#types-and-categories}

자세한 내용은 [대상 유형 및 카테고리 개요를 참조하십시오](/help/rtcdp/destinations/destination-types.md).

## 대상 및 액세스 제어 {#access-controls}

실시간 CDP의 대상 기능은 Adobe Experience Platform 액세스 제어 권한과 함께 작동합니다. 사용자의 권한 수준에 따라 대상을 보고, 관리하고, 활성화할 수 있습니다. 개별 권한에 대한 자세한 내용은 Adobe Experience Platform [의 액세스](../../access-control/home.md) 제어 기능을 참조하고 페이지 아래쪽으로 스크롤을 내려가세요.

액세스 제어에 대한 자세한 내용은 [액세스 제어 사용 안내서를 참조하십시오](../../access-control/ui/overview.md).

## [!DNL Data Governance] 대상에 데이터 활성화 제한 {#data-governance}

데이터 거버넌스는 다음을 통해 실시간 CDP 대상에 적용됩니다.

* *대상 만들기 워크플로우에서 선택할 수 있는 마케팅 사용 사례* ;
* *특정 사용 레이블이 들어 있는 데이터를 특정 마케팅 사용 사례가 있는 대상으로 활성화하지 않는 데이터 사용 정책* .

[!DNL Data Governance] 마케팅 사용 사례 [및 데이터 정책 위반](/help/rtcdp/privacy/data-governance-overview.md#destinations) 해결에 대한 자세한 내용은 실시간 CDP 설명서를 참조하십시오 [](/help/rtcdp/privacy/data-governance-overview.md#enforcement).

대상 작성 워크플로우에서 마케팅 사용 사례를 선택하는 방법에 대한 자세한 내용은 실시간 CDP의 다양한 대상 유형에 대한 다음 페이지를 참조하십시오.

* [광고 대상 - Google 광고 관리자 ](/help/rtcdp/destinations/google-ad-manager-destination.md)
* [광고 대상 - Google 광고](/help/rtcdp/destinations/google-ads-destination.md)
* [광고 대상 - Google 디스플레이 및 비디오 360 ](/help/rtcdp/destinations/google-dv360-destination.md)
* [클라우드 스토리지 대상](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)
* [이메일 마케팅 대상](/help/rtcdp/destinations/email-marketing-destinations.md)
* [소셜 네트워크 대상](/help/rtcdp/destinations/social-network-destinations-workflow.md)

세그먼트 활성화 워크플로우의 데이터 정책 위반에 대한 자세한 내용은 프로필과 세그먼트를 대상으로 [활성화의 검토 단계를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md#review).