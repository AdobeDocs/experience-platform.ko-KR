---
title: Audience Manager에서 Real-Time CDP으로의 진화
description: Audience Manager에서 Real-Time CDP으로의 마이그레이션을 계획하기 전에 고려 사항을 이해합니다.
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Audience Manager에서 Real-Time CDP으로의 진화

조직이 Adobe Real-Time CDP을 사용하기 위해 발전함에 따라 이러한 고려 사항을 살펴보고 데이터를 준비하여 두 기술 간의 중요한 차이점을 파악하십시오. 이 문서는 실무자 대상자를 대상으로 합니다.

![Real-Time CDP 진화 다이어그램에 대한 Audience Manager](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Audience Manager 내 데이터 아키텍처 고려

Audience Manager에서 Real-Time CDP으로의 발전을 고려한다면 지금이 분석을 위한 중요한 시기입니다. [Audience Manager 세그먼트](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en) 및 다음을 결정합니다. [신호](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en), [트레이트](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en), 및 [규칙](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section) 는 이러한 세그먼트를 구성하는 요소입니다.

또한 현재 Audience Manager에서 사용하는 데이터 소스에 대해서도 생각해 보십시오.

Adobe은 세그먼트를 다음과 같이 분류할 것을 권장합니다.

* 를 통해 Experience Platform에 보낼 수 있는 세그먼트 [[!UICONTROL Audience Manager 소스 커넥터]](/help/sources/connectors/adobe-applications/audience-manager.md), 데이터 종속성이 없고, 대상 또는 활성화 문제가 없으며, 실시간 CDP를 통해 세그멘테이션 규칙을 만들 수 있습니다 [세그먼트 빌더](/help/segmentation/ui/segment-builder.md) 나중에.
* 지원할 수 있는 규칙이 있지만 Real-Time CDP에서 사용할 수 없는 데이터가 포함되어 있을 수 있는 세그먼트입니다.
* Real-Time CDP에서 만들 수 없고 기능이 없는 세그먼트입니다.

>[!TIP]
>
>Adobe Real-Time CDP 오퍼 [세그먼트 평가의 세 가지 유형](/help/segmentation/home.md#evaluate-segments): [!UICONTROL 일괄 처리], [!UICONTROL 스트리밍], 및 [!UICONTROL Edge]. Audience Manager에서 실시간 세그먼트를 사용하는 고객은 현재 Real-Time CDP에서 500개의 스트리밍 세그먼트라는 제한에 의해 제한될 수 있습니다. 자세한 내용 [세그먼테이션 보호](/help/profile/guardrails.md).

## 2. 를 통해 전송하는 것이 중요한 세그먼트 [!UICONTROL Audience Manager 소스 커넥터]?

평가 기준에 따라 데이터 종속성이 없는 세그먼트, 대상 또는 활성화 문제 및 세그먼트 규칙은 다음과 같은 Real-Time CDP 데이터 수집을 통해 만들 수 있습니다 [Adobe Experience Platform 웹 SDK](/help/edge/web-sdk-faq.md) 나중에 Audience Manager 소스 커넥터를 통해 전송해야 합니다.

## 3. 다음을 사용하시겠습니까? [!UICONTROL Experience Cloud 대상] 데이터를 다시 Audience Manager으로 가져올 대상

Real-Time CDP에서 지원할 수 있는 규칙이 있지만 Audience Manager에 대한 활성화 종속성이 있는 세그먼트는 를 통해 Audience Manager에게 보낼 수 있습니다. [Experience Cloud 대상](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 대상 카드.

## 4. Real-Time CDP으로 이동할 수 있는 Audience Manager 내 현재 위치한 여행지는 어디입니까?

Adobe은 Audience Manager 시 활성화된 세그먼트를 [사용자 기반 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en) 을(를) 통해 Real-Time CDP으로 푸시 [!UICONTROL Audience Manager 소스 커넥터]을 클릭하여 Real-Time CDP을 통해 활성화합니다.

Audience Manager에서 사용할 수 있는 모든 사람 기반 대상 - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - Real-Time CDP에서도 사용할 수 있습니다.

다음과 같은 추가 자사 데이터 및 미디어 전략 파트너 [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon 광고](/help/destinations/catalog/advertising/amazon-ads.md), 및 [[!UICONTROL 트레이드 데스크]](/help/destinations/catalog/advertising/tradedesk.md) 사용할 수 있습니다.

Real-Time CDP은 현재 기본적으로 60개 이상의 대상을 지원합니다. [카탈로그](/help/destinations/catalog/overview.md), 20개 이상의 대상이 자사 대상 일치를 지원하는 광고 또는 소셜 대상입니다.

## 다음 단계

이 페이지를 읽고 나면 이제 Audience Manager에서 Real-Time CDP으로 진화를 시작할 때 수행해야 할 첫 번째 고려 사항 세트가 있습니다.
