---
keywords: 대상;adobe experience platform;플랫폼;대상 개요;데이터 활성화;활성화
title: 대상 개요
description: 대상은 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. Adobe Experience Platform에서 대상 을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# [!DNL Destinations] 개요 {#overview}

![대상 개요 배너](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

## 대상 및 소스 {#destinations-and-sources}

플랫폼의 핵심 기능 중 하나는 자사 데이터를 수집하여 비즈니스 요구에 맞게 활성화하는 것입니다. 사용 [소스](../sources/home.md) 데이터를 플랫폼 및 대상으로 수집하여 Platform에서 데이터를 내보냅니다.

## 대상 단계 {#steps}

* 선택 [셀프 서비스 카탈로그](./catalog/overview.md) 구현합니다.
* 대상을 사용하여 프로필 또는 세그먼트를 마케팅 자동화 플랫폼, 디지털 광고 플랫폼 등으로 보냅니다.
* 정기적으로 기본 대상으로 데이터 내보내기를 예약합니다.

## 컨트롤 {#controls}

의 컨트롤 [대상 작업 공간](./ui/destinations-workspace.md) 다음을 수행할 수 있습니다.

* 데이터를 활성화할 수 있는 대상 플랫폼의 카탈로그를 찾아봅니다.
* 카탈로그의 대상에 데이터 흐름 만들기, 편집, 활성화 및 비활성화
* 스토리지 위치에서 계정을 만들거나 대상 플랫폼의 계정에 플랫폼 연결
* 대상에 활성화해야 하는 세그먼트를 선택합니다.
* 어떤 항목을 선택하십시오 [XDM(경험 데이터 모델) 필드](../xdm/home.md) 세그먼트를 활성화할 때 이메일 마케팅 대상으로 내보내기

## 대상 유형 및 카테고리 {#types-and-categories}

자세한 내용은 [대상 유형 및 카테고리 개요](./destination-types.md).

## 대상 및 액세스 제어 {#access-controls}

Platform의 대상 기능은 Adobe Experience Platform 액세스 제어 권한과 함께 작동합니다. 사용자의 권한 수준에 따라 대상을 보고, 관리하고, 활성화할 수 있습니다. 개별 권한에 대한 자세한 내용은 [Adobe Experience Platform의 액세스 제어](../access-control/home.md) 페이지 아래쪽으로 스크롤합니다.

액세스 컨트롤에 대한 자세한 내용은 [액세스 제어 사용 안내서](../access-control/ui/overview.md).

## 대상에 데이터 활성화에 대한 데이터 거버넌스 제한 {#data-governance}

데이터 거버넌스는 다음을 통해 플랫폼 대상에 적용됩니다.

* *마케팅 작업* 대상 만들기 워크플로우에서 선택할 수 있습니다.
* *데이터 사용 정책* 특정 사용 레이블이 포함된 데이터를 특정 마케팅 작업이 있는 대상으로 활성화하지 않도록 제한합니다.

자세한 내용은 Platform의 데이터 거버넌스 설명서 를 참조하십시오 [마케팅 작업](../data-governance/policies/overview.md) 및 [데이터 정책 위반 해결](../data-governance/enforcement/auto-enforcement.md).

대상 만들기 워크플로우에서 마케팅 작업을 선택하는 방법에 대한 자세한 내용은 플랫폼의 다양한 대상 유형에 대한 다음 페이지를 참조하십시오.

* [광고 대상 - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [광고 대상 - Google 광고](./catalog/advertising/google-ads-destination.md)
* [광고 대상 - Google 디스플레이 및 비디오 360 ](./catalog/advertising/google-dv360.md)
* [클라우드 스토리지 대상](./catalog/cloud-storage/overview.md)
* [이메일 마케팅 대상](./catalog/email-marketing/overview.md)
* [소셜 대상](./catalog/social/overview.md)

세그먼트 활성화 워크플로우의 데이터 정책 위반에 대한 자세한 내용은 다음 안내서의 검토 단계를 참조하십시오.

* [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](./ui/activate-segment-streaming-destinations.md#review)
* [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](./ui/activate-streaming-profile-destinations.md#review)
* [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](./ui/activate-batch-profile-destinations.md#review)
