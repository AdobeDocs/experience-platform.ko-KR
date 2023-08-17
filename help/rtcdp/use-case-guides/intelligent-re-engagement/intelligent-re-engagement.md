---
title: 지능형 재참여
description: 주요 전환 순간 동안 매력적이고 연결된 경험을 제공하여 빈번하지 않은 고객을 지능적으로 다시 참여시킵니다.
hide: true
hidefromtoc: true
source-git-commit: 43e365e20a2fd91a0e822eb6f66bb7db6fc218f5
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 6%

---

# 고객에게 지능적으로 재참여를 유도하여 재방문

지능적이고 책임 있는 방식으로 완료하기 전에 전환을 포기한 고객을 다시 참여시킵니다. 미리 알림이 아닌 경험을 통해 고객의 참여를 유도하여 전환을 강화하고 고객 생애 가치 성장을 촉진합니다.

실시간 고려 사항을 적용하고, 모든 소비자의 특성과 행동을 고려하며, 온라인 및 오프라인 이벤트를 기반으로 신속한 재자격을 제공합니다.

![단계별 지능형 재참여 높은 수준의 시각적 개요.](../intelligent-re-engagement/images/step-by-step.png)

## 사용 사례 개요

재참여 여정의 예를 통해 작업할 때 스키마, 데이터 세트 및 대상을 구성합니다. 또한 예제 여정을 설정하는 데 필요한 기능을 살펴보게 됩니다. [!DNL Adobe Journey Optimizer] 그리고 목적지에서 유료 미디어 광고를 만드는 데 필요한 것들이죠. 이 안내서에서는 아래에 설명된 사용 사례 여정에서 고객을 다시 참여시키는 예제를 사용합니다.

* **재참여 여정** - 웹사이트와 모바일 앱 모두에서 제품 탐색을 중단한 고객을 타깃팅합니다.
* **포기한 장바구니 여정** - 장바구니에 제품을 배치했지만 아직 웹 사이트 및 모바일 앱에서 구매하지 않은 고객을 타깃팅합니다.
* **주문 확인 여정** - 웹 사이트 및 모바일 앱을 통한 제품 구매에 중점을 둡니다.

## 전제 조건 및 계획 {#prerequisites-and-planning}

사용 사례를 구현하는 단계를 완료하면 다음 Real-Time CDP 기능 및 UI 요소(사용할 순서대로 나열됨)를 사용하게 됩니다. 이러한 모든 영역에 대해 필요한 속성 기반 액세스 제어 권한이 있는지 확인하거나 시스템 관리자에게 필요한 권한을 부여하도록 요청하십시오.

* [Adobe Real-time Customer Data Platform(Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - 데이터 소스 간의 데이터를 집계하여 캠페인을 실행합니다. 그런 다음 이 데이터를 사용하여 캠페인 대상자를 만들고 이메일 및 웹 프로모션 타일에 사용된 개인화된 데이터 요소(예: 이름 또는 계정 관련 정보)를 표시합니다. CDP는 이메일 및 웹(Adobe Target을 통해)에서 대상자를 활성화하는 데에도 사용됩니다.
   * [스키마](/help/xdm/home.md)
   * [프로필](/help/profile/home.md)
   * [데이터 세트](/help/catalog/datasets/overview.md)
   * [Audiences](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [대상](/help/destinations/home.md)
   * [이벤트 또는 대상 트리거](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [대상/이벤트](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [여정 작업](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### 사용 사례를 달성하는 방법: 높은 수준의 개요 {#achieve-the-use-case-high-level}

다음은 세 가지 재참여 여정 예제에 대한 높은 수준의 개요입니다.

>[!BEGINTABS]

>[!TAB 재참여 여정]

재참여 여정은 웹 사이트와 모바일 앱 모두에서 구매하지 않은 제품 탐색을 타깃팅합니다. 이 여정은 제품을 보았으나 장바구니에 구매하거나 추가하지 않은 경우 트리거됩니다. 지난 24시간 내에 목록 추가가 없는 경우 3일 후에 브랜드 참여가 트리거됩니다.<p>![고객 인텔리전트 재참여 여정 높은 수준의 시각적 개요](../intelligent-re-engagement/images/re-engagement-journey.png "고객 인텔리전트 재참여 여정 높은 수준의 시각적 개요"){width="1920" zoomable="yes"}</p>

1. 용으로 표시된 스키마 및 데이터 세트를 만듭니다. [!UICONTROL 프로필].
2. 데이터는 Web SDK, Mobile Edge SDK 또는 API를 통해 Experience Platform으로 집계됩니다. Analytics 데이터 커넥터 를 활용할 수도 있지만 여정 지연이 발생할 수 있습니다.
3. 프로필을 Real-Time CDP에 로드하고 거버넌스 정책을 구축하여 책임 있는 사용을 보장합니다.
4. 프로필 목록에서 포커스가 있는 대상을 빌드하여 **고객** 은(는) 지난 3일 동안 약정을 체결했습니다.
5. 에서 재참여 여정을 만듭니다. [!DNL Adobe Journey Optimizer].
6. 필요한 경우 **데이터 파트너** 원하는 유료 미디어 대상으로 대상자를 활성화하기 위해
7. [!DNL Adobe Journey Optimizer] 동의를 확인하고 구성된 다양한 작업을 전송합니다.

>[!TAB 포기한 장바구니 여정]

포기한 장바구니 여정은 장바구니에 넣었지만 아직 웹 사이트 및 모바일 앱 모두에서 구매하지 않은 제품을 대상으로 합니다. 또한, 유료 미디어 캠페인은 이 방법을 사용하여 시작 및 중지됩니다.<p>![고객이 장바구니 여정을 포기하는 경우 높은 수준의 시각적 개요.](../intelligent-re-engagement/images/abandoned-cart-journey.png "고객이 장바구니 여정을 포기하는 경우 높은 수준의 시각적 개요."){width="1920" zoomable="yes"}</p>

1. 용으로 표시된 스키마 및 데이터 세트를 만듭니다. [!UICONTROL 프로필].
2. 데이터는 Web SDK, Mobile Edge SDK 또는 API를 통해 Experience Platform으로 집계됩니다. Analytics 데이터 커넥터 를 활용할 수도 있지만 여정 지연이 발생할 수 있습니다.
3. 프로필을 Real-Time CDP에 로드하고 거버넌스 정책을 구축하여 책임 있는 사용을 보장합니다.
4. 프로필 목록에서 포커스가 있는 대상을 빌드하여 **고객** 이(가) 장바구니에 항목을 넣었지만 구매를 완료하지 않았습니다. 다음 **[!UICONTROL 장바구니에 추가]** 이벤트가 30분 동안 대기하는 타이머를 시작한 다음 구매를 확인합니다. 구매하지 않은 경우 **고객** 이(가)에 추가됩니다 **[!UICONTROL 장바구니 포기]** 대상.
5. Adobe Journey Optimizer에서 포기한 장바구니 여정을 만듭니다.
6. 필요한 경우 **데이터 파트너** 원하는 유료 미디어 대상으로 대상자를 활성화하기 위해
7. [!DNL Adobe Journey Optimizer] 동의를 확인하고 구성된 다양한 작업을 전송합니다.

>[!TAB 주문 확인 여정]

주문 확인 여정은 홈페이지와 모바일 앱을 통한 제품 구매에 중점을 두고 있다.<p>![고객 주문 확인 여정 개요](../intelligent-re-engagement/images/order-confirmation-journey.png "고객 주문 확인 여정 개요"){width="1920" zoomable="yes"}</p>

1. 용으로 표시된 스키마 및 데이터 세트를 만듭니다. [!UICONTROL 프로필].
2. 데이터는 Web SDK, Mobile Edge SDK 또는 API를 통해 Experience Platform으로 집계됩니다. Analytics 데이터 커넥터 를 활용할 수도 있지만 여정 지연이 발생할 수 있습니다.
3. 프로필을 Real-Time CDP에 로드하고 거버넌스 정책을 구축하여 책임 있는 사용을 보장합니다.
4. 프로필 목록에서 포커스가 있는 대상을 빌드하여 **고객** 을(를) 구매했습니다.
5. Adobe Journey Optimizer에서 확인 여정을 만듭니다.
6. [!DNL Adobe Journey Optimizer] 선호하는 채널을 사용하여 주문 확인 메시지를 보냅니다.

>[!ENDTABS]

## 사용 사례 달성 방법: 단계별 지침 {#step-by-step-instructions}

위의 높은 수준 개요에서 각 단계를 완료하려면 추가 정보 및 보다 자세한 지침에 대한 링크를 제공하는 아래 섹션을 참조하십시오.

### 사용할 UI 기능 및 요소 {#ui-functionality-and-elements}

사용 사례를 구현하는 단계를 완료하면 이 문서의 시작 부분에 나열된 Real-Time CDP 기능 및 UI 요소를 사용하게 됩니다. 이러한 모든 영역에 대해 필요한 속성 기반 액세스 제어 권한이 있는지 확인하거나 시스템 관리자에게 필요한 권한을 부여하도록 요청하십시오.

### 스키마 디자인 만들기 및 필드 그룹 지정

XDM(경험 데이터 모델) 리소스는 [!UICONTROL 스키마] Adobe Experience Platform의 작업 영역 Adobe에서 제공하는 핵심 리소스를 보고 탐색할 수 있으며, 조직에 대한 사용자 지정 리소스 및 스키마를 만들 수 있습니다.

스키마 만들기에 대한 자세한 내용은 [스키마 튜토리얼 만들기.](/help/xdm/tutorials/create-schema-ui.md)

재참여 여정에 사용되는 네 가지 스키마 디자인이 있습니다. 각 스키마에는 설정할 특정 필드와 강력하게 제안되는 일부 필드가 필요합니다.

#### 고객 속성 스키마

고객 속성 스키마는 로 표시됩니다. [!UICONTROL XDM 개별 프로필] 클래스로, 다음과 같은 필드 그룹이 포함됩니다.

+++개인 연락처 세부 정보(필드 그룹)

[개인 연락처 세부 정보](/help/xdm/field-groups/profile/personal-contact-details.md) 는 개인에 대한 연락처 정보를 설명하는 XDM 개인 프로필 클래스에 대한 표준 스키마 필드 그룹입니다.

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `mobilePhone.number` | 필수 여부 | SMS에 사용되는 개인 휴대폰 번호. |
| `personalEmail.address` | 필수 여부 | 개인 이메일 주소입니다. |

+++

+++인구 통계 세부 정보(필드 그룹)

[인구 통계 세부 정보](/help/xdm/field-groups/profile/demographic-details.md) 는 XDM 개인 프로필 클래스에 대한 표준 스키마 필드 그룹입니다. 필드 그룹은 루트 레벨 개인 객체를 제공하는데, 이 객체의 하위 필드에는 개별 개인에 대한 정보가 설명되어 있습니다.

| 필드 | 요구 사항 |
| --- | --- |
| `person.name.firstName` | 제안됨 |
| `person.name.lastName` | 제안됨 |

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

[외부 소스 시스템 감사 속성](/help/xdm/data-types/external-source-system-audit-attributes.md) 는 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

+++

+++동의 및 환경 설정 필드 그룹(필드 그룹)

[동의 및 환경 설정](/help/xdm/field-groups//profile/consents.md) 필드 그룹은 동의 및 환경 설정 정보를 캡처하기 위한 단일 개체 유형 필드인 동의를 제공합니다.

| 필드 | 요구 사항 |
| --- | --- |
| `consents.marketing.email.val` | 필수 여부 |
| `consents.marketing.preferred` | 필수 여부 |
| `consents.marketing.push.val` | 필수 여부 |
| `consents.marketing.sms.val` | 필수 여부 |
| `consents.personalize.content.val` | 필수 여부 |
| `consents.share.val` | 필수 여부 |

+++

+++프로필 테스트 세부 사항(필드 그룹)

이 필드 그룹은 우수 사례에 사용됩니다.

+++

#### 고객 디지털 트랜잭션 스키마

고객 디지털 거래 스키마는 로 표시됩니다. [!UICONTROL XDM ExperienceEvent] 클래스로, 다음과 같은 필드 그룹이 포함됩니다.

+++Adobe Experience Platform 웹 SDK ExperienceEvent (필드 그룹)

| 필드 | 요구 사항 |
| --- | --- |
| `device.model` | 제안됨 |
| `environment.browserDetails.userAgent` | 제안됨 |

+++

+++웹 세부 정보(필드 그룹)

웹 세부 정보 는 상호 작용, 페이지 세부 정보 및 레퍼러 등 웹 세부 정보 이벤트 관련 정보를 설명하는 데 사용되는 XDM ExperienceEvent 클래스의 표준 스키마 필드 그룹입니다.

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 제안됨 | 인터랙션에 해당하는 웹 링크 또는 URL의 ID입니다. |
| `web.webInteraction.linkClicks.value` | 제안됨 | 인터랙션에 해당하는 웹 링크 또는 URL의 클릭 수입니다. |
| `web.webInteraction.name` | 제안됨 | 웹 페이지의 이름입니다. |
| `web.webInteraction.URL` | 제안됨 | 웹 페이지의 URL입니다. |
| `web.webPageDetails.name` | 제안됨 | 웹 인터랙션이 발생한 웹 페이지의 이름입니다. |
| `web.webPageDetails.URL` | 제안됨 | 웹 인터랙션이 발생한 웹 페이지의 URL입니다. |
| `web.webReferrer.URL` | 제안됨 | 웹 인터랙션의 레퍼러(현재 웹 인터랙션이 기록되기 바로 전에 방문자가 들어온 URL)에 대해 설명합니다. |

+++

+++고객 경험 이벤트(필드 그룹)

| 필드 | 요구 사항 |
| --- | --- |
| `commerce.cart.cartID` | 제안됨 |
| `commerce.cart.cartSource` | 제안됨 |
| `commerce.cartAbandons.id` | 제안됨 |
| `commerce.cartAbandons.value` | 제안됨 |
| `commerce.order.orderType` | 제안됨 |
| `commerce.order.payments.paymentAmount` | 제안됨 |
| `commerce.order.payments.paymentType` | 제안됨 |
| `commerce.order.payments.transactionID` | 제안됨 |
| `commerce.order.priceTotal` | 제안됨 |
| `commerce.order.purchaseID` | 제안됨 |
| `commerce.productListAdds.id` | 제안됨 |
| `commerce.productListAdds.value` | 제안됨 |
| `commerce.productListOpens.id` | 제안됨 |
| `commerce.productListOpens.value` | 제안됨 |
| `commerce.productListRemoval.id` | 제안됨 |
| `commerce.productListRemoval.value` | 제안됨 |
| `commerce.productListViews.id` | 제안됨 |
| `commerce.productListViews.value` | 제안됨 |
| `commerce.productViews.id` | 제안됨 |
| `commerce.productViews.value` | 제안됨 |
| `commerce.purchases.id` | 제안됨 |
| `commerce.purchases.value` | 제안됨 |
| `marketing.campaignGroup` | 제안됨 |
| `marketing.campaignName` | 제안됨 |
| `marketing.trackingCode` | 제안됨 |
| `productListItems.name` | 제안됨 |
| `productListItems.priceTotal` | 제안됨 |
| `productListItems.product` | 제안됨 |
| `productListItems.quantity` | 제안됨 |

+++

+++최종 사용자 ID 세부 사항(필드 그룹)

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | 필수 여부 | 최종 사용자 이메일 주소 ID 인증 상태. |
| `endUserIDs._experience.emailid.id` | 필수 여부 | 최종 사용자 이메일 주소 ID. |
| `endUserIDs._experience.emailid.namespace.code` | 필수 여부 | 최종 사용자 이메일 주소 ID 네임스페이스 코드. |
| `endUserIDs._experience.mcid.authenticatedState` | 필수 여부 | MCID(Adobe Marketing Cloud ID) 인증 상태입니다. 이제 MCID를 ECID(Experience Cloud ID)라고 합니다. |
| `endUserIDs._experience.mcid.id` | 필수 여부 | Adobe Marketing Cloud ID(MCID). 이제 MCID를 ECID(Experience Cloud ID)라고 합니다. |
| `endUserIDs._experience.mcid.namespace.code` | 필수 여부 | Adobe Marketing Cloud ID(MCID) 네임스페이스 코드. |

+++

+++클래스 값(필드 그룹)

| 필드 | 요구 사항 |
| --- | --- |
| `eventType` | 필수 여부 |
| `timestamp` | 필수 여부 |

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

외부 소스 시스템 감사 속성 은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

+++

#### 고객 오프라인 트랜잭션 스키마

고객 오프라인 트랜잭션 스키마는 로 표시됩니다. [!UICONTROL XDM ExperienceEvent] 클래스로, 다음과 같은 필드 그룹이 포함됩니다.

+++상거래 세부 정보(필드 그룹)

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `commerce.cart.cartID` | 필수 여부 | 장바구니 ID. |
| `commerce.order.orderType` | 필수 여부 | 제품 주문 유형을 설명하는 객체입니다. |
| `commerce.order.payments.paymentAmount` | 필수 여부 | 제품 주문 결제 금액을 설명하는 객체입니다. |
| `commerce.order.payments.paymentType` | 필수 여부 | 제품 주문 결제 유형을 설명하는 객체입니다. |
| `commerce.order.payments.transactionID` | 필수 여부 | 객체 제품 주문 거래 ID입니다. |
| `commerce.order.purchaseID` | 필수 여부 | 오브젝트 제품 주문 구매 ID. |
| `productListItems.name` | 필수 여부 | 고객이 선택한 제품을 나타내는 항목 이름 목록입니다. |
| `productListItems.priceTotal` | 필수 여부 | 고객이 선택한 제품을 나타내는 품목 목록의 총 가격. |
| `productListItems.product` | 필수 여부 | 제품이 선택되었습니다. |
| `productListItems.quantity` | 필수 여부 | 고객이 선택한 제품을 나타내는 품목 목록의 수량. |

+++

+++개인 연락처 세부 정보(필드 그룹)

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `mobilePhone.number` | 필수 여부 | SMS에 사용되는 개인 휴대폰 번호. |
| `personalEmail.address` | 필수 여부 | 개인 이메일 주소입니다. |

+++

+++클래스 값(필드 그룹)

| 필드 | 요구 사항 |
| --- | --- |
| `eventType` | 필수 여부 |
| `timestamp` | 필수 여부 |

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

외부 소스 시스템 감사 속성 은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

+++

#### Adobe 웹 커넥터 스키마

Adobe 웹 커넥터 스키마는으로 표시됩니다. [!UICONTROL XDM ExperienceEvent] 클래스로, 다음과 같은 필드 그룹이 포함됩니다.

+++Adobe Analytics ExperienceEvent 템플릿(필드 그룹)

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 제안됨 | 인터랙션에 해당하는 웹 링크 또는 URL의 ID입니다. |
| `web.webInteraction.linkClicks.value` | 제안됨 | 인터랙션에 해당하는 웹 링크 또는 URL의 클릭 수입니다. |
| `web.webInteraction.name` | 제안됨 | 웹 페이지의 이름입니다. |
| `web.webInteraction.URL` | 제안됨 | 웹 페이지의 URL입니다. |
| `web.webPageDetails.name` | 제안됨 | 웹 인터랙션이 발생한 웹 페이지의 이름입니다. |
| `web.webPageDetails.URL` | 제안됨 | 웹 인터랙션이 발생한 웹 페이지의 URL입니다. |
| `web.webReferrer.URL` | 제안됨 | 웹 인터랙션의 레퍼러(현재 웹 인터랙션이 기록되기 바로 전에 방문자가 들어온 URL)에 대해 설명합니다. |
| `commerce.cart.cartID` | 제안됨 | |
| `commerce.cart.cartSource` | 제안됨 | |
| `commerce.cartAbandons.id` | 제안됨 | |
| `commerce.cartAbandons.value` | 제안됨 | |
| `commerce.order.orderType` | 제안됨 | |
| `commerce.order.payments.paymentAmount` | 제안됨 | |
| `commerce.order.payments.paymentType` | 제안됨 | |
| `commerce.order.payments.transactionID` | 제안됨 | |
| `commerce.order.priceTotal` | 제안됨 | |
| `commerce.order.purchaseID` | 제안됨 | |
| `commerce.productListAdds.id` | 제안됨 | |
| `commerce.productListAdds.value` | 제안됨 | |
| `commerce.productListOpens.id` | 제안됨 | |
| `commerce.productListOpens.value` | 제안됨 | |
| `commerce.productListRemoval.id` | 제안됨 | |
| `commerce.productListRemoval.value` | 제안됨 | |
| `commerce.productListViews.id` | 제안됨 | |
| `commerce.productListViews.value` | 제안됨 | |
| `commerce.productViews.id` | 제안됨 | |
| `commerce.productViews.value` | 제안됨 | |
| `commerce.purchases.id` | 제안됨 | |
| `commerce.purchases.value` | 제안됨 | |
| `marketing.campaignGroup` | 제안됨 | |
| `marketing.campaignName` | 제안됨 | |
| `marketing.trackingCode` | 제안됨 | |
| `productListItems.name` | 제안됨 | |
| `productListItems.priceTotal` | 제안됨 | |
| `productListItems.product` | 제안됨 | |
| `productListItems.quantity` | 제안됨 | |
| `endUserIDs._experience.emailid.authenticatedState` | 필수 여부 | 최종 사용자 이메일 주소 ID 인증 상태. |
| `endUserIDs._experience.emailid.id` | 필수 여부 | 최종 사용자 이메일 주소 ID. |
| `endUserIDs._experience.emailid.namespace.code` | 필수 여부 | 최종 사용자 이메일 주소 ID 네임스페이스 코드. |
| `endUserIDs._experience.mcid.authenticatedState` | 필수 여부 | MCID(Adobe Marketing Cloud ID) 인증 상태입니다. 이제 MCID를 ECID(Experience Cloud ID)라고 합니다. |
| `endUserIDs._experience.mcid.id` | 필수 여부 | Adobe Marketing Cloud ID(MCID). 이제 MCID를 ECID(Experience Cloud ID)라고 합니다. |
| `endUserIDs._experience.mcid.namespace.code` | 필수 여부 | Adobe Marketing Cloud ID(MCID) 네임스페이스 코드. |

+++

+++클래스 값(필드 그룹)

| 필드 | 요구 사항 |
| --- | --- |
| `eventType` | 필수 여부 |
| `timestamp` | 필수 여부 |

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

외부 소스 시스템 감사 속성 은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

+++

### 스키마에서 데이터 세트 만들기

데이터 세트는 데이터 그룹의 저장소 및 관리 구조이며, 필드(행)와 스키마(열)가 있는 테이블인 경우가 많습니다. 지능형 재참여 여정에 대한 모든 스키마에는 단일 데이터 세트가 있습니다.

스키마에서 데이터 세트를 만드는 방법에 대한 자세한 내용은 [데이터 세트 UI 안내서](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>스키마를 만드는 단계와 유사하게 데이터 세트를 실시간 고객 프로필에 포함할 수 있도록 해야 합니다. 실시간 고객 프로필에서 사용할 데이터 세트를 활성화하는 방법에 대한 자세한 내용은 [스키마 튜토리얼 만들기.](/help/xdm/tutorials/create-schema-ui.md#profile).

### 개인 정보, 동의 및 데이터 거버넌스

#### 동의 정책

>[!IMPORTANT]
>
>고객에게 브랜드로부터 커뮤니케이션 수신을 거부할 수 있는 기능을 제공하는 것은 법적 요건이며 이러한 선택이 존중되도록 하는 것입니다. [Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html)에서 해당 법률에 대해 자세히 알아보십시오.

재참여 경로를 생성할 때 다음 동의 정책을 고려하여 사용해야 합니다.

* If `consents.marketing.email.val = "Y"` 전자 메일로 전송 가능
* If `consents.marketing.sms.val = "Y"` SMS로 보낼 수 있음
* If `consents.marketing.push.val = "Y"` 푸시할 수 있음
* If `consents.share.val = "Y"` 광고 가능
* 고객 구현에 의해 정의된 요구 사항

#### DULE 레이블 및 적용

개인 이메일 주소는 디바이스가 아닌 특정 개인을 식별하거나 연락하는 데 사용되는 직접 식별 가능한 데이터로 사용됩니다.

* `personalEmail.address = I1`

#### 마케팅 정책

재참여 여정에 필요한 추가 마케팅 정책은 없지만, 다음과 같은 사항을 원하는 대로 고려해야 합니다.

* 중요 데이터 제한
* 온사이트 광고 제한
* 이메일 타겟팅 제한
* 교차 사이트 타겟팅 제한
* 직접 식별할 수 있는 데이터를 익명 데이터와 결합하는 것 제한

### 대상자 만들기

#### 브랜드 재참여 여정을 위한 대상 만들기

재참여 여정은 대상을 사용하여 프로필 스토어의 프로필 하위 집합이 공유하는 특정 속성이나 동작을 정의하여 마케팅 가능한 사용자 그룹과 고객 기반을 구분합니다. Adobe Experience Platform에서 대상자로 직접 구성하거나 플랫폼에서 파생된 세그먼트 정의를 통해 두 가지 다른 방식으로 대상을 만들 수 있습니다.

대상자를 직접 구성하는 방법에 대한 자세한 내용은 [대상 구성 UI 안내서](/help/segmentation/ui/audience-composition.md).

플랫폼에서 파생된 세그먼트 정의를 통해 대상자를 만드는 방법에 대한 자세한 내용은 [Audience Builder UI 안내서](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB 재참여 여정]

다음 여정은 사용자가 온라인으로 제품을 보고 다음 24시간 동안 장바구니에 추가하지 않았으며 다음 3일 동안은 브랜드 참여를 하지 않았던 재참여 이벤트에 사용됩니다.

이 대상자를 설정할 때 다음 필드와 조건이 필요합니다.

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.productListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

재참여 여정 설명자는 다음과 같이 표시됩니다.

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB 포기한 장바구니 여정]

다음 여정은 사용자가 장바구니에 제품을 추가했지만 지난 24시간 동안 구매를 완료하지 않았거나 장바구니를 지우지 않은 포기한 장바구니 이벤트에 사용됩니다.

이 대상자를 설정할 때 다음 필드와 조건이 필요합니다.

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 30 minutes before now and <= 1440 minutes before now`
* `EventType: commerce.purchases`
   * `Timestamp: <= 30 minutes before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 30 minutes before now`

포기한 장바구니 여정에 대한 설명자는 다음과 같이 표시됩니다.

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!ENDTABS]

### Adobe Journey Optimizer에서 여정 설정

>[!NOTE]
>
>Adobe Journey Optimizer은 이 페이지 상단에 있는 다이어그램에 표시된 모든 항목을 포함하지 않습니다. 모든 유료 미디어 광고는에서 만들어집니다. [!UICONTROL 대상].

Adobe Journey Optimizer은 고객에게 연관성 있고 상황에 맞는 개인화된 경험을 제공할 수 있도록 해줍니다. 고객 여정은 고객이 브랜드와 상호 작용하는 전체 프로세스입니다. 각 사용 사례 여정에 특정 정보가 필요합니다. 다음은 각 여정 분기에 필요한 정확한 데이터입니다.

>[!BEGINTABS]

>[!TAB 재참여 여정]

+++이벤트

* 제품 보기
   * 스키마: 고객 디지털 트랜잭션
   * 필드:
      * `EventType`
   * 조건:
      * `EventType = commerce.productViews`
      * 필드:
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* 장바구니에 추가
   * 스키마: 고객 디지털 트랜잭션
   * 필드:
      * `EventType`
   * 조건:
      * `EventType = commerce.productListAdds`
      * 필드:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* 브랜드 참여
   * 스키마: 고객 디지털 트랜잭션
   * 필드:
      * `EventType`
   * 조건:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * 필드:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++키 여정 논리

* 여정 시작 논리
   * 제품 보기 이벤트

* 조건
   * 제품을 마지막으로 본 이후 온라인 또는 오프라인 구매 이벤트가 하나 이상 있는지 확인합니다.
      * 스키마: 고객 디지털 트랜잭션
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 제품을 마지막으로 본 이후 하나 이상의 오프라인 구매 확인:
      * 스키마: 고객 오프라인 트랜잭션 v.1
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 조건 - Target 채널 선택
      * 이메일
         * `consents.marketing.email.val = y`
      * 푸시
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * 채널 개인화
      * 제품 보기에 따라 개인화된 채널 콘텐츠.

+++

>[!TAB 포기한 장바구니 여정]

+++이벤트

* 장바구니에 추가
   * 스키마: 고객 디지털 트랜잭션
   * 필드:
      * `EventType`
   * 조건:
      * `EventType = commerce.productListAdds`
      * 필드:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* 온라인 구매
   * 스키마: 고객 디지털 트랜잭션
   * 필드:
      * `EventType`
   * 조건:
      * `EventType = commerce.purchases`
      * 필드:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* 브랜드 참여
   * 스키마: 고객 디지털 트랜잭션
   * 필드:
      * `EventType`
   * 조건:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * 필드:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++키 여정 논리

* 여정 시작 논리
   * `AddToCart` 이벤트

* authenticated의 AuthenticatedState

* 조건: 장바구니가 마지막으로 중단된 이후 오프라인 구매:
   * 스키마: 고객 오프라인 트랜잭션 v.1
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* 조건: 장바구니를 마지막으로 포기한 이후 장바구니를 지웠습니다.
   * 스키마: 고객 디지털 트랜잭션 v.1
   * `eventType = commerce.cartCleared`
   * `cartID` (장바구니의 ID)
   * `timestamp > timestamp of cart was last abandoned`

* 타겟 채널 선택(더 넓은 범위를 위해 하나 이상의 채널 선택)
   * 이메일
      * `consents.marketing.email.val = y`
   * 푸시
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * 채널 개인화
      * 장바구니 세부 정보를 표시하고 테이블 형식으로 여러 제품을 표시할 수 있습니다.

+++

>[!TAB 주문 확인 여정]

+++이벤트

* 온라인 구매
   * 스키마: 고객 디지털 트랜잭션
   * 필드:
      * `EventType`
   * 조건:
      * `EventType = commerce.purchases`
      * 필드:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++키 여정 논리

* 여정 시작 논리
   * 주문 이벤트

* 조건
   * 타겟 채널 을 선택합니다(더 넓은 범위를 보려면 하나 또는 여러 채널을 선택).
      * 주문 확인은 사실상 서비스하는 것으로 간주되므로 일반적으로 동의 확인은 불필요하다.
      * 이메일
      * 푸시
      * SMS

   * 채널 콘텐츠 개인화
      * 주문 세부 정보를 표시하고 테이블 형식을 사용하여 제품 목록을 표시할 수 있습니다.

+++

>[!ENDTABS]

여정 만들기에 대한 자세한 내용은 [Adobe Journey Optimizer], 다음을 읽습니다 [여정 시작 안내서](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### 대상에서 유료 미디어 광고 설정

대상 프레임워크는 유료 미디어 광고에 사용됩니다. 동의를 확인하면 구성된 다양한 대상으로 전송됩니다. 예를 들어 DM, 이메일, 푸시 및 SMS가 있습니다.

#### 대상에 필요한 데이터

스트리밍 세그먼트 내보내기 대상(예: Facebook, Google Customer Match, Google DV360)은 고객 데이터에서 다양한 ID를 지원합니다.

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

장바구니 포기 세그먼트는 스트리밍 중이므로 이 사용 사례의 대상 프레임워크에서 사용할 수 있습니다.

* 스트림/트리거됨
   * [광고](/help/destinations/catalog/advertising/overview.md)/[유료 미디어 및 소셜](/help/destinations/catalog/social/overview.md)
   * [모바일](/help/destinations/catalog/mobile-engagement/overview.md)
   * [스트리밍 대상](/help/destinations/catalog/streaming/http-destination.md)
   * [사용자 지정 Destination SDK](/help/destinations/destination-sdk/overview.md)

* 3시간마다 파일/예약
   * [이메일 마케팅](/help/destinations/catalog/email-marketing/overview.md)
