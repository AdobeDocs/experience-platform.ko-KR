---
title: Audience Manager에서 Real-Time CDP로의 발전
description: Audience Manager에서 Adobe Real-Time CDP으로의 마이그레이션을 계획하기 전에 고려 사항을 이해합니다.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 67%

---

# Audience Manager에서 Real-Time CDP로의 발전

귀사에서 Adobe Real-Time CDP를 사용하고자 할 때 이러한 고려 사항을 통해 데이터를 준비하고 두 기술 간의 중요한 차이점을 파악하십시오. 이 문서는 실무자를 대상으로 합니다.

![Audience Manager에서 Real-Time CDP로의 발전 다이어그램](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## &#x200B;1. Audience Manager 내에서 데이터 아키텍처 고려

Audience Manager에서 Real-Time CDP로의 발전을 고려할 때 지금이 바로 [Audience Manager 세그먼트](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html)를 분석하고 이러한 세그먼트를 구성하는 [신호](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html), [특성](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html) 및 [규칙](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html#segment-builder-section)이 무엇인지 확인해야 할 중요한 시기입니다.

또한 현재 Audience Manager에서 사용하는 데이터 소스에 대해 생각해 보십시오.

Adobe는 세그먼트를 다음과 같이 분류하는 것을 권장합니다.

* 데이터 종속성이 없고, 대상 또는 활성화 문제가 없으며, 나중에 Real-Time CDP [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md)세그먼트 빌더[를 통해 세그멘테이션 규칙을 만들 수 있으므로 &#x200B;](/help/segmentation/ui/segment-builder.md)을(를) 통해 Experience Platform으로 보낼 수 있는 세그먼트입니다.
* 지원할 수 있는 규칙이 있지만 Real-Time CDP에서 사용할 수 없는 데이터를 포함할 수 있는 세그먼트.
* Real-Time CDP에서 만들 수 없고 기능이 없는 세그먼트입니다.

>[!TIP]
>
>Adobe Real-Time CDP은 [세 가지 유형의 세그먼트 평가를 제공합니다](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming] 및 [!UICONTROL Edge]. Audience Manager에서 실시간 세그먼트를 사용하는 고객은 현재 Real-Time CDP에서 500개의 스트리밍 세그먼트 한도로 제한될 수 있습니다. [세분화 가드레일](/help/profile/guardrails.md)에 대해 자세히 살펴보십시오.

## &#x200B;2. [!UICONTROL Audience Manager Source Connector]을(를) 통해 전송해야 하는 세그먼트를 선택하십시오.

평가 기준에 따라 데이터 종속성, 대상 또는 활성화 문제가 없으며 나중에 [Adobe Experience Platform Web SDK](/help/collection/js/faq.md)와 같은 Real-Time CDP 데이터 수집을 통해 세분화 규칙을 만들 수 있는 세그먼트는 Audience Manager 소스 커넥터를 통해 데이터를 전송해야 합니다.

## &#x200B;3. [!UICONTROL Experience Cloud Audiences] 대상을 사용하여 데이터를 Audience Manager으로 다시 가져오시겠습니까?

Real-Time CDP에서 지원되지만 Audience Manager에 대한 활성화 종속성이 있는 규칙을 가진 세그먼트는 [Experience Cloud Audiences](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 대상 카드를 통해 Audience Manager에 전송됩니다.

## &#x200B;4. 현재 Audience Manager에서 Real-Time CDP로의 전환을 시작할 수 있는 대상은 무엇입니까?

Adobe에서는 Audience Manager에서 활성화된 세그먼트를 [사용자 기반 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html)에 푸시한 다음 [!UICONTROL Audience Manager Source Connector]을(를) 통해 Real-Time CDPReal-Time CDP 으로 활성화하도록 강력히 권장합니다.

Audience Manager에서 사용할 수 있는 모든 사용자 기반 대상([Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md))도 Real-Time CDP에서 사용할 수 있습니다.

[Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon 광고](/help/destinations/catalog/advertising/amazon-ads.md) 및 [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md)와 같은 추가 자사 데이터 및 미디어 전략 파트너를 사용할 수 있습니다.

Real-Time CDP는 기본적으로 현재 [카탈로그](/help/destinations/catalog/overview.md)에서 60여 개의 대상을 지원하고 있으며, 그 중 20여 개는 서드파티 대상자 일치를 지원하는 광고 또는 소셜 대상입니다.

## 다음 단계

이 페이지를 읽은 후 이제 Audience Manager에서 Real-Time CDP로의 발전을 시작할 때 숙지해야 할 첫 번째 고려 사항이 생겼습니다.
