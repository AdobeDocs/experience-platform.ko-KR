---
title: Audience Manager에서 Real-Time CDP로의 발전
description: Audience Manager에서 Adobe Real-Time CDP으로의 마이그레이션을 계획하기 전에 고려 사항을 이해합니다.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 86%

---

# Audience Manager에서 Real-Time CDP로의 발전

귀사에서 Adobe Real-Time CDP를 사용하고자 할 때 이러한 고려 사항을 통해 데이터를 준비하고 두 기술 간의 중요한 차이점을 파악하십시오. 이 문서는 실무자를 대상으로 합니다.

![Audience Manager에서 Real-Time CDP로의 발전 다이어그램](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Audience Manager 내에서 데이터 아키텍처 고려

Audience Manager에서 Real-Time CDP로의 발전을 고려할 때 지금이 바로 [Audience Manager 세그먼트](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html)를 분석하고 이러한 세그먼트를 구성하는 [신호](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html), [특성](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html) 및 [규칙](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html#segment-builder-section)이 무엇인지 확인해야 할 중요한 시기입니다.

또한 현재 Audience Manager에서 사용하는 데이터 소스에 대해 생각해 보십시오.

Adobe는 세그먼트를 다음과 같이 분류하는 것을 권장합니다.

* 를 통해 Experience Platform에 보낼 수 있는 세그먼트 [[!UICONTROL Audience Manager 소스 커넥터]](/help/sources/connectors/adobe-applications/audience-manager.md), 데이터 종속성이 없고, 대상 또는 활성화와 관련된 문제가 없으며, Real-Time CDP을 통해 세그멘테이션 규칙을 만들 수 있습니다 [세그먼트 빌더](/help/segmentation/ui/segment-builder.md) 나중에.
* 지원할 수 있는 규칙이 있지만 Real-Time CDP에서 사용할 수 없는 데이터를 포함할 수 있는 세그먼트.
* Real-Time CDP에서 만들 수 없고 기능이 없는 세그먼트입니다.

>[!TIP]
>
>Adobe Real-Time CDP는 [세 가지 세그먼트 평가 유형](/help/segmentation/home.md#evaluate-segments)([!UICONTROL 일괄 처리], [!UICONTROL 스트리밍] 및 [!UICONTROL Edge])을 지원합니다. Audience Manager에서 실시간 세그먼트를 사용하는 고객은 현재 Real-Time CDP에서 500개의 스트리밍 세그먼트 한도로 제한될 수 있습니다. [세분화 가드레일](/help/profile/guardrails.md)에 대해 자세히 살펴보십시오.

## 2. [!UICONTROL Audience Manager 소스 커넥터]를 통해 전송하기 위한 중요 세그먼트는 무엇입니까?

평가 기준에 따라 데이터 종속성, 대상 또는 활성화 문제가 없으며 나중에 [Adobe Experience Platform Web SDK](/help/web-sdk/faq.md)와 같은 Real-Time CDP 데이터 수집을 통해 세분화 규칙을 만들 수 있는 세그먼트는 Audience Manager 소스 커넥터를 통해 데이터를 전송해야 합니다.

## 3. Audience Manager로 데이터를 다시 가져오기 위해 [!UICONTROL Experience Cloud 대상자] 대상을 사용하시겠습니까?

Real-Time CDP에서 지원되지만 Audience Manager에 대한 활성화 종속성이 있는 규칙을 가진 세그먼트는 [Experience Cloud Audiences](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 대상 카드를 통해 Audience Manager에 전송됩니다.

## 4. 현재 Audience Manager에서 Real-Time CDP로의 전환을 시작할 수 있는 대상은 무엇입니까?

Adobe는 Audience Manager에서 [사람 기반 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html)으로 활성화된 세그먼트를 [!UICONTROL Audience Manager 소스 커넥터]를 통해 Real-Time CDP로 푸시한 다음, Real-Time CDP를 통해 활성화할 것을 권장합니다.

Audience Manager에서 사용할 수 있는 모든 사람 기반 대상은 Real-Time CDP에서도 사용할 수 있습니다([Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google 고객 일치 타겟팅]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md)).

[Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) 및 [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md)와 같은 추가 서드파티 데이터 및 미디어 전략 파트너를 사용할 수 있습니다.

Real-Time CDP는 기본적으로 현재 [카탈로그](/help/destinations/catalog/overview.md)에서 60여 개의 대상을 지원하고 있으며, 그 중 20여 개는 서드파티 대상자 일치를 지원하는 광고 또는 소셜 대상입니다.

## 다음 단계

이 페이지를 읽은 후 이제 Audience Manager에서 Real-Time CDP로의 발전을 시작할 때 숙지해야 할 첫 번째 고려 사항이 생겼습니다.
