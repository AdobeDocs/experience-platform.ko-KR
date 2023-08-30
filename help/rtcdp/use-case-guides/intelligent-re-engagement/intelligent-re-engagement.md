---
title: 지능형 재참여
description: 주요 전환 순간에 강력한 연결 환경을 제공하여 방문 빈도가 낮은 고객을 지능적으로 재참여시킵니다.
source-git-commit: 79ba0e350d64f43558af9bc3c2ecd4ac13d11499
workflow-type: tm+mt
source-wordcount: '3424'
ht-degree: 96%

---

# 지능적으로 고객이 돌아오도록 재참여 유도

지능적이고 책임 있는 방식으로 전환을 완료하기 전에 전환을 포기한 고객을 다시 참여시킵니다. 알림이 아닌 경험을 통해 이탈한 고객의 참여를 유도하여 전환율을 높이고 고객 생애 가치 성장을 촉진합니다.

실시간 고려 사항을 적용하고, 모든 소비자 특성과 행동을 감안하고, 온라인 및 오프라인 이벤트를 기반으로 빠른 재인증을 제공합니다.

![단계별 지능형 재참여의 높은 수준의 시각적 개요](../intelligent-re-engagement/images/step-by-step.png)

## 사용 사례 개요

재참여 여정의 예를 통해 작업하면서 스키마, 데이터 세트 및 대상자를 구성하게 됩니다. 또한 [!DNL Adobe Journey Optimizer]에서 예시 여정을 설정하는 데 필요한 기능과 대상에 유료 미디어 광고를 만드는 데 필요한 기능을 살펴봅니다. 이 안내서에서는 아래에 설명된 사용 사례 여정에서 고객 재참여의 예를 사용합니다.

* **재참여 여정** - 웹 사이트와 모바일 앱 모두에서 제품 탐색을 포기한 고객을 대상으로 합니다.
* **포기한 장바구니 여정** - 제품을 장바구니에 담았지만 웹 사이트와 모바일 앱에서 아직 구매하지 않은 고객을 대상으로 합니다.
* **주문 확인 여정** - 웹 사이트 및 모바일 앱을 통한 제품 구매에 중점을 둡니다.

## 전제 조건 및 계획 {#prerequisites-and-planning}

사용 사례를 구현하는 단계를 완료하면 다음 Real-Time CDP 기능 및 UI 요소(사용할 순서대로 나열됨)를 사용하게 됩니다. 이러한 모든 영역에 대해 필요한 속성 기반의 액세스 제어 권한이 있는지 확인하거나, 시스템 관리자에게 필요한 권한 부여를 요청하십시오.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - 데이터 소스 전체에서 데이터를 통합하여 캠페인을 촉진합니다. 그런 다음 이 데이터를 사용하여 이메일 및 웹 프로모션 타일에 사용되는 표면 맞춤형 데이터 요소(예: 이름 또는 계정 관련 정보) 및 캠페인 대상자를 만듭니다. CDP를 사용하여 이메일 및 웹([!DNL Adobe Target]을 통해)에서 대상자를 활성화합니다.
   * [스키마](/help/xdm/home.md)
   * [프로필](/help/profile/home.md)
   * [데이터 세트](/help/catalog/datasets/overview.md)
   * [대상자](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [대상](/help/destinations/home.md)
   * [이벤트 또는 대상자 트리거](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [대상자/이벤트](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [여정 작업](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### 사용 사례를 달성하는 방법: 높은 수준의 개요 {#achieve-the-use-case-high-level}

다음은 세 가지 재참여 여정 예시에 대한 높은 수준의 개요입니다.

>[!BEGINTABS]

>[!TAB 재참여 여정]

재참여 여정은 웹 사이트와 모바일 앱 모두에서 포기한 제품 탐색을 대상으로 합니다. 이 여정은 제품을 보았지만 구매하거나 장바구니에 추가하지 않은 경우에 트리거됩니다. 지난 24시간 동안 목록 추가가 없으면 3일 후에 브랜드 참여가 트리거됩니다.<p>![고객 지능형 재참여 여정의 높은 수준의 시각적 개요](../intelligent-re-engagement/images/re-engagement-journey.png "고객 지능형 재참여 여정의 높은 수준의 시각적 개요"){width="2560" zoomable="yes"}</p>

1. 스키마와 데이터 세트를 만든 다음 [!UICONTROL 프로필]로 지정합니다.
2. 데이터는 Web SDK, Mobile Edge SDK 또는 API를 통해 Experience Platform에 통합됩니다. Analytics Data Connector도 활용할 수 있지만 여정 지연이 발생할 수 있습니다.
3. 프로필을 Real-Time CDP에 로드하고 책임 있는 사용을 보장하기 위한 거버넌스 정책을 구축합니다.
4. **고객**&#x200B;이 지난 3일 동안 참여를 실행했는지 확인하기 위해 프로필 목록에서 집중 대상자를 구축합니다.
5. [!DNL Adobe Journey Optimizer]에서 재참여 여정을 만듭니다.
6. 필요한 경우, **데이터 파트너**&#x200B;와 협력하여 원하는 유료 미디어 대상에 대한 대상자를 활성화할 수 있습니다.
7. [!DNL Adobe Journey Optimizer]는 동의를 확인하고 구성된 다양한 작업을 보냅니다.

>[!TAB 포기한 장바구니 여정]

포기한 장바구니 여정은 장바구니에 담았지만 웹 사이트와 모바일 앱에서 아직 구매하지 않은 제품을 대상으로 합니다. 또한 이 방법을 사용하여 유료 미디어 캠페인을 시작하고 중지합니다.<p>![고객이 포기한 장바구니 여정의 높은 수준의 시각적 개요](../intelligent-re-engagement/images/abandoned-cart-journey.png "고객이 포기한 장바구니 여정의 높은 수준의 시각적 개요"){width="2560" zoomable="yes"}</p>

1. 스키마와 데이터 세트를 만든 다음 [!UICONTROL 프로필]로 지정합니다.
2. 데이터는 Web SDK, Mobile Edge SDK 또는 API를 통해 Experience Platform에 통합됩니다. Analytics Data Connector도 활용할 수 있지만 여정 지연이 발생할 수 있습니다.
3. 프로필을 Real-Time CDP에 로드하고 책임 있는 사용을 보장하기 위한 거버넌스 정책을 구축합니다.
4. **고객**&#x200B;이 장바구니에 품목을 넣었지만 구매를 완료하지 않았는지 확인하기 위해 프로필 목록에서 집중 대상자를 구축합니다. **[!UICONTROL 장바구니에 추가]** 이벤트는 30분 동안 대기한 다음 구매를 확인하는 타이머를 시작합니다. 구매가 완료되면 **고객**&#x200B;이 **[!UICONTROL 장바구니 포기]** 대상자에 추가됩니다.
5. [!DNL Adobe Journey Optimizer]에서 포기한 장바구니 여정을 만듭니다.
6. 필요한 경우, **데이터 파트너**&#x200B;와 협력하여 원하는 유료 미디어 대상에 대한 대상자를 활성화할 수 있습니다.
7. [!DNL Adobe Journey Optimizer]는 동의를 확인하고 구성된 다양한 작업을 보냅니다.

>[!TAB 주문 확인 여정]

주문 확인 여정은 웹 사이트 및 모바일 앱을 통한 제품 구매에 중점을 둡니다.<p>![고객 주문 확인 여정의 높은 수준의 시각적 개요](../intelligent-re-engagement/images/order-confirmation-journey.png "고객 주문 확인 여정의 높은 수준의 시각적 개요"){width="2560" zoomable="yes"}</p>

1. 스키마와 데이터 세트를 만든 다음 [!UICONTROL 프로필]로 지정합니다.
2. 데이터는 Web SDK, Mobile Edge SDK 또는 API를 통해 Experience Platform에 통합됩니다. Analytics Data Connector도 활용할 수 있지만 여정 지연이 발생할 수 있습니다.
3. 프로필을 Real-Time CDP에 로드하고 책임 있는 사용을 보장하기 위한 거버넌스 정책을 구축합니다.
4. [!DNL Adobe Journey Optimizer]에서 확인 여정을 만듭니다.
5. [!DNL Adobe Journey Optimizer]는 선호 채널을 사용하여 주문 확인 메시지를 보냅니다.

>[!ENDTABS]

## 사용 사례를 달성하는 방법 {#achieve-use-case-instruction}

위의 높은 수준의 개요에 있는 각 단계를 완료하려면 자세한 정보 및 상세 지침에 대한 링크를 제공하는 아래 섹션을 읽어보십시오.

### 사용할 UI 기능 및 요소 {#ui-functionality-and-elements}

사용 사례를 구현하는 단계를 완료하면 이 문서의 맨 앞에 나열된 Real-Time CDP 기능 및 UI 요소를 사용하게 됩니다. 이러한 모든 영역에 대해 필요한 속성 기반의 액세스 제어 권한이 있는지 확인하거나, 시스템 관리자에게 필요한 권한 부여를 요청하십시오.

### 스키마 디자인 만들기 및 필드 그룹 지정 {#schema-design}

Experience Data Model(XDM) 리소스는 [!DNL Adobe Experience Platform]의 [!UICONTROL 스키마] 작업 영역에서 관리됩니다. [!DNL Adobe]에서 제공하는 핵심 리소스(예: [!UICONTROL 필드 그룹])를 보고 탐색하며, 조직의 사용자 정의 리소스와 스키마를 만들 수 있습니다.

[스키마](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko-KR) 만들기에 대한 자세한 내용은 [스키마 튜토리얼 만들기](/help/xdm/tutorials/create-schema-ui.md)를 참조하십시오.

재참여 여정 사용 사례에 사용되는 네 가지 스키마 디자인이 있습니다. 각 스키마에는 설정할 특정 필드와 매우 권장하는 일부 필드가 필요합니다.

#### 고객 속성 스키마

이 스키마는 고객 정보를 구성하는 프로필 데이터를 구성하고 참조하는 데 사용됩니다. 이 데이터는 일반적으로 CRM 또는 유사한 시스템을 통해 [!DNL Adobe Experience Platform]으로 수집되며, 개인화, 마케팅 동의, 향상된 세분화 기능에 사용되는 고객 세부 정보를 참조하는 데 필요합니다.

고객 속성 스키마는 [!UICONTROL XDM 개별 프로필] 클래스에 표시되며, 다음 필드 그룹을 포함합니다.

+++개인 연락처 세부 정보(필드 그룹)

[개인 연락처 세부 정보](/help/xdm/field-groups/profile/personal-contact-details.md)는 개별 사용자의 연락처 정보를 설명하는 XDM 개별 프로필 클래스의 표준 스키마 필드 그룹입니다.

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `mobilePhone.number` | 필수 여부 | SMS에 사용될 개인의 휴대폰 번호 |
| `personalEmail.address` | 필수 여부 | 개인의 이메일 주소. |

+++

+++인구 통계 세부 정보(필드 그룹)

[인구 통계 세부 정보](/help/xdm/field-groups/profile/demographic-details.md)는 XDM 개별 프로필 클래스의 표준 스키마 필드 그룹입니다. 필드 그룹은 개별 사용자에 대한 정보를 설명하는 하위 필드가 있는 루트 수준의 사용자 오브젝트를 제공합니다.

| 필드 | 요구 사항 |
| --- | --- |
| `person.name.firstName` | 권장 |
| `person.name.lastName` | 권장 |

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

[외부 소스 시스템 감사 속성](/help/xdm/data-types/external-source-system-audit-attributes.md)은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

+++

+++동의 및 환경 설정 필드 그룹(필드 그룹)

[동의 및 환경 설정](/help/xdm/field-groups//profile/consents.md) 필드 그룹은 동의 및 기본 설정 정보를 캡처하기 위해 동의라는 단일 오브젝트 유형 필드를 제공합니다.

| 필드 | 요구 사항 |
| --- | --- |
| `consents.marketing.email.val` | 필수 여부 |
| `consents.marketing.preferred` | 필수 여부 |
| `consents.marketing.push.val` | 필수 여부 |
| `consents.marketing.sms.val` | 필수 여부 |
| `consents.personalize.content.val` | 필수 여부 |
| `consents.share.val` | 필수 여부 |

+++

+++프로필 테스트 세부 정보(필드 그룹)

이 필드 그룹은 모범 사례에 사용됩니다.

+++

#### 고객 디지털 트랜잭션 스키마

이 스키마는 웹 사이트 및/또는 관련 디지털 플랫폼에서 발생하는 고객 활동을 구성하는 이벤트 데이터를 구성하고 참조하는 데 사용됩니다. 이 데이터는 일반적으로 Web SDK를 통해 [!DNL Adobe Experience Platform]으로 수집되며, 여정 트리거, 상세한 온라인 고객 분석, 향상된 세분화 기능에 사용되는 다양한 찾아보기 및 전환 이벤트를 참조하는 데 필요합니다.

고객 디지털 트랜잭션 스키마는 [!UICONTROL XDM ExperienceEvent] 클래스로 표시되며, 다음 필드 그룹을 포함합니다.

+++Adobe Experience Platform Web SDK ExperienceEvent(필드 그룹)

| 필드 | 요구 사항 |
| --- | --- |
| `device.model` | 권장 |
| `environment.browserDetails.userAgent` | 권장 |

+++

+++웹 세부 정보(필드 그룹)

웹 세부 정보는 XDM ExperienceEvent 클래스의 표준 스키마 필드 그룹이며 상호 작용, 페이지 세부 정보 및 참조한 사람과 같은 웹 세부 정보 이벤트에 관한 정보를 설명하는 데 사용됩니다.

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 권장 | 상호 작용에 해당하는 웹 링크 또는 URL의 ID. |
| `web.webInteraction.linkClicks.value` | 권장 | 상호 작용에 해당하는 웹 링크 또는 URL의 클릭 수. |
| `web.webInteraction.name` | 권장 | 웹 페이지의 이름 |
| `web.webInteraction.URL` | 권장 | 웹 페이지의 URL. |
| `web.webPageDetails.name` | 권장 | 웹 상호 작용이 발생한 웹 페이지의 이름. |
| `web.webPageDetails.URL` | 권장 | 웹 상호 작용이 발생한 웹 페이지의 URL. |
| `web.webReferrer.URL` | 권장 | 현재 웹 상호 작용이 기록되기 직전에 방문자가 방문한 URL인 웹 상호 작용의 참조한 사람을 설명합니다. |

+++

+++소비자 경험 이벤트(필드 그룹)

| 필드 | 요구 사항 |
| --- | --- |
| `commerce.cart.cartID` | 권장 |
| `commerce.cart.cartSource` | 권장 |
| `commerce.cartAbandons.id` | 권장 |
| `commerce.cartAbandons.value` | 권장 |
| `commerce.order.orderType` | 권장 |
| `commerce.order.payments.paymentAmount` | 권장 |
| `commerce.order.payments.paymentType` | 권장 |
| `commerce.order.payments.transactionID` | 권장 |
| `commerce.order.priceTotal` | 권장 |
| `commerce.order.purchaseID` | 권장 |
| `commerce.productListAdds.id` | 권장 |
| `commerce.productListAdds.value` | 권장 |
| `commerce.productListOpens.id` | 권장 |
| `commerce.productListOpens.value` | 권장 |
| `commerce.productListRemoval.id` | 권장 |
| `commerce.productListRemoval.value` | 권장 |
| `commerce.productListViews.id` | 권장 |
| `commerce.productListViews.value` | 권장 |
| `commerce.productViews.id` | 권장 |
| `commerce.productViews.value` | 권장 |
| `commerce.purchases.id` | 권장 |
| `commerce.purchases.value` | 권장 |
| `marketing.campaignGroup` | 권장 |
| `marketing.campaignName` | 권장 |
| `marketing.trackingCode` | 권장 |
| `productListItems.name` | 권장 |
| `productListItems.priceTotal` | 권장 |
| `productListItems.product` | 권장 |
| `productListItems.quantity` | 권장 |

+++

+++최종 사용자 ID 세부 정보(필드 그룹)

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | 필수 여부 | 최종 사용자 이메일 주소 ID 인증 상태 |
| `endUserIDs._experience.emailid.id` | 필수 여부 | 최종 사용자 이메일 주소 ID |
| `endUserIDs._experience.emailid.namespace.code` | 필수 여부 | 최종 사용자 이메일 주소 ID 네임스페이스 코드 |
| `endUserIDs._experience.mcid.authenticatedState` | 필수 여부 | [!DNL Adobe] Marketing Cloud ID(MCID) 인증 상태. MCID는 이제 ECID(Experience Cloud ID)로 알려져 있습니다. |
| `endUserIDs._experience.mcid.id` | 필수 여부 | [!DNL Adobe] Marketing Cloud ID(MCID). MCID는 이제 ECID(Experience Cloud ID)로 알려져 있습니다. |
| `endUserIDs._experience.mcid.namespace.code` | 필수 여부 | [!DNL Adobe] Marketing Cloud ID(MCID) 네임스페이스 코드. |

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

외부 소스 시스템 감사 속성은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

+++

#### 고객 오프라인 트랜잭션 스키마

이 스키마는 웹 사이트 외부 플랫폼에서 발생하는 고객 활동을 구성하는 이벤트 데이터를 구성하고 참조하는 데 사용됩니다. 이 데이터는 일반적으로 POS(또는 유사한 시스템)에서 [!DNL Adobe Experience Platform]으로 수집되며, API 연결을 통해 Platform으로 스트리밍되는 경우가 가장 많습니다. 목적은 여정 트리거, 심층적인 온라인 및 오프라인 고객 분석, 향상된 세분화 기능에 사용되는 다양한 오프라인 전환 이벤트를 참조하는 것입니다.

고객 오프라인 트랜잭션 스키마는 [!UICONTROL XDM ExperienceEvent] 클래스로 표시되며, 다음 필드 그룹을 포함합니다.

+++상거래 세부 정보(필드 그룹)

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `commerce.cart.cartID` | 필수 여부 | 장바구니 ID |
| `commerce.order.orderType` | 필수 여부 | 제품 주문 유형을 설명하는 오브젝트입니다. |
| `commerce.order.payments.paymentAmount` | 필수 여부 | 상품 주문 결제 금액을 설명하는 오브젝트 |
| `commerce.order.payments.paymentType` | 필수 여부 | 상품 주문 결제 유형을 설명하는 오브젝트 |
| `commerce.order.payments.transactionID` | 필수 여부 | 오브젝트 제품 주문 트랜잭션 ID |
| `commerce.order.purchaseID` | 필수 여부 | 오브젝트 제품 주문 구매 ID |
| `productListItems.name` | 필수 여부 | 고객이 선택한 제품을 나타내는 항목 이름 목록 |
| `productListItems.priceTotal` | 필수 여부 | 고객이 선택한 제품을 나타내는 항목 목록의 총 가격 |
| `productListItems.product` | 필수 여부 | 선택한 제품 |
| `productListItems.quantity` | 필수 여부 | 고객이 선택한 제품을 나타내는 항목 목록의 수량 |

+++

+++개인 연락처 세부 정보(필드 그룹)

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `mobilePhone.number` | 필수 여부 | SMS에 사용될 개인의 휴대폰 번호 |
| `personalEmail.address` | 필수 여부 | 개인의 이메일 주소. |

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

외부 소스 시스템 감사 속성은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

+++

#### Adobe 웹 커넥터 스키마

>[!NOTE]
>
>[!DNL Adobe Analytics Data Connector]를 사용하는 경우 선택적 구현입니다.

이 스키마는 웹 사이트 및/또는 관련 디지털 플랫폼에서 발생하는 고객 활동을 구성하는 이벤트 데이터를 구성하고 참조하는 데 사용됩니다. 이 스키마는 고객 디지털 트랜잭션 스키마와 유사하지만, Web SDK가 데이터 수집 옵션이 아닐 때 사용된다는 점에서 다릅니다. 따라서 이 스키마는 [!DNL Adobe Analytics Data Connector]를 활용해 온라인 데이터를 [!DNL Adobe Experience Platform]으로 보낼 때 주 또는 보조 데이터스트림으로 필요합니다.

[!DNL Adobe] 웹 커넥터 스키마는 [!UICONTROL XDM ExperienceEvent] 클래스로 표시되며, 다음 필드 그룹을 포함합니다.

+++Adobe Analytics ExperienceEvent 템플릿(필드 그룹)

| 필드 | 요구 사항 | 설명 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 권장 | 상호 작용에 해당하는 웹 링크 또는 URL의 ID. |
| `web.webInteraction.linkClicks.value` | 권장 | 상호 작용에 해당하는 웹 링크 또는 URL의 클릭 수. |
| `web.webInteraction.name` | 권장 | 웹 페이지의 이름 |
| `web.webInteraction.URL` | 권장 | 웹 페이지의 URL. |
| `web.webPageDetails.name` | 권장 | 웹 상호 작용이 발생한 웹 페이지의 이름. |
| `web.webPageDetails.URL` | 권장 | 웹 상호 작용이 발생한 웹 페이지의 URL. |
| `web.webReferrer.URL` | 권장 | 현재 웹 상호 작용이 기록되기 직전에 방문자가 방문한 URL인 웹 상호 작용의 참조한 사람을 설명합니다. |
| `commerce.cart.cartID` | 권장 | |
| `commerce.cart.cartSource` | 권장 | |
| `commerce.cartAbandons.id` | 권장 | |
| `commerce.cartAbandons.value` | 권장 | |
| `commerce.order.orderType` | 권장 | |
| `commerce.order.payments.paymentAmount` | 권장 | |
| `commerce.order.payments.paymentType` | 권장 | |
| `commerce.order.payments.transactionID` | 권장 | |
| `commerce.order.priceTotal` | 권장 | |
| `commerce.order.purchaseID` | 권장 | |
| `commerce.productListAdds.id` | 권장 | |
| `commerce.productListAdds.value` | 권장 | |
| `commerce.productListOpens.id` | 권장 | |
| `commerce.productListOpens.value` | 권장 | |
| `commerce.productListRemoval.id` | 권장 | |
| `commerce.productListRemoval.value` | 권장 | |
| `commerce.productListViews.id` | 권장 | |
| `commerce.productListViews.value` | 권장 | |
| `commerce.productViews.id` | 권장 | |
| `commerce.productViews.value` | 권장 | |
| `commerce.purchases.id` | 권장 | |
| `commerce.purchases.value` | 권장 | |
| `marketing.campaignGroup` | 권장 | |
| `marketing.campaignName` | 권장 | |
| `marketing.trackingCode` | 권장 | |
| `productListItems.name` | 권장 | |
| `productListItems.priceTotal` | 권장 | |
| `productListItems.product` | 권장 | |
| `productListItems.quantity` | 권장 | |
| `endUserIDs._experience.emailid.authenticatedState` | 필수 여부 | 최종 사용자 이메일 주소 ID 인증 상태 |
| `endUserIDs._experience.emailid.id` | 필수 여부 | 최종 사용자 이메일 주소 ID |
| `endUserIDs._experience.emailid.namespace.code` | 필수 여부 | 최종 사용자 이메일 주소 ID 네임스페이스 코드 |
| `endUserIDs._experience.mcid.authenticatedState` | 필수 여부 | [!DNL Adobe] Marketing Cloud ID(MCID) 인증 상태. MCID는 이제 ECID(Experience Cloud ID)로 알려져 있습니다. |
| `endUserIDs._experience.mcid.id` | 필수 여부 | [!DNL Adobe] Marketing Cloud ID(MCID). MCID는 이제 ECID(Experience Cloud ID)로 알려져 있습니다. |
| `endUserIDs._experience.mcid.namespace.code` | 필수 여부 | [!DNL Adobe] Marketing Cloud ID(MCID) 네임스페이스 코드. |

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

외부 소스 시스템 감사 속성은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

+++

### 스키마에서 데이터 세트 만들기 {#dataset-from-schema}

데이터 세트는 데이터 그룹의 저장 및 관리 구조입니다. 지능형 재참여 여정을 위한 각 스키마에는 단일 데이터 세트가 있습니다.

스키마에서 [데이터 세트](/help/catalog/datasets/overview.md)를 만드는 방법에 대한 자세한 내용은 [데이터 세트 UI 안내서](/help/catalog/datasets/user-guide.md)를 참조하십시오.

>[!NOTE]
>
>스키마를 생성하는 단계와 유사하게 실시간 고객 프로필에 포함할 데이터 세트를 활성화해야 합니다. 실시간 고객 프로필에서 사용할 데이터 세트를 활성화하는 방법에 대한 자세한 내용은 [스키마 튜토리얼 만들기](/help/xdm/tutorials/create-schema-ui.md#profile)를 참조하십시오.

### 개인정보 보호, 동의 및 데이터 거버넌스 {#privacy-consent}

#### 동의 정책

>[!IMPORTANT]
>
>고객에게 브랜드의 커뮤니케이션 수신을 거부할 수 있는 기능을 제공하고, 이러한 선택을 존중하는 것은 법률에 명시된 사항입니다. 에서 해당 법률에 대해 자세히 알아보십시오. [개인 정보 보호 규정 개요](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

재참여 경로를 만들 때 다음 작업을 수행하십시오 [동의 정책](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) 다음 사항을 고려해야 합니다.

* `consents.marketing.email.val = "Y"`인 경우, 이메일 전송 가능
* `consents.marketing.sms.val = "Y"`인 경우, SMS 전송 가능
* `consents.marketing.push.val = "Y"`인 경우, 푸시 가능
* `consents.share.val = "Y"`인 경우, 광고 가능

#### 데이터 거버넌스 레이블 및 적용

재참여 경로를 만들 때 다음 작업을 수행하십시오 [데이터 거버넌스 레이블](/help/data-governance/labels/overview.md) 다음 사항을 고려해야 합니다.

* 개인 이메일 주소는 디바이스가 아닌 특정 개인을 식별하거나 연락하기 위한 직접 식별 가능한 데이터로 활용됩니다.
   * `personalEmail.address = I1`

#### 마케팅 정책

없음 [마케팅 정책](/help/data-governance/policies/overview.md) 재참여 여정에 필요하지만, 다음 사항을 원하는 대로 고려해야 합니다.

* 민감한 데이터 제한
* 온사이트 광고 제한
* 이메일 타겟팅 제한
* 크로스 사이트 타겟팅 제한
* 직접 식별 가능한 데이터와 익명 데이터의 결합 제한

### 대상자 만들기 {#create-audience}

#### 브랜드 재참여 여정을 위한 대상자 생성

재참여 여정은 고객층과 마케팅 가능한 대상 그룹을 구별하도록 프로필 스토어의 프로필 하위 집합에서 공유하는 특정 속성 또는 동작을 정의하기 위해 대상자를 사용합니다. [!DNL Adobe Experience Platform]에서 대상자를 다양한 방법으로 만들 수 있습니다.

대상자를 만드는 방법에 대한 자세한 내용은 [Audience Service UI 안내서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

직접 [대상자](/help/segmentation/home.md)를 구성하는 방법에 대한 자세한 내용은 [대상자 구성 UI 안내서](/help/segmentation/ui/audience-composition.md)를 참조하십시오.

플랫폼에서 파생된 세그먼트 정의를 통해 대상자를 구축하는 방법에 대한 자세한 내용은 [대상자 빌더 UI 안내서](/help/segmentation/ui/segment-builder.md)를 참조하십시오.

>[!BEGINTABS]

>[!TAB 재참여 여정]

이 대상자는 기존의 “장바구니 포기” 시나리오를 개선하여 만들어졌습니다. 장바구니 포기는 일반적으로 특정 기간 동안 후속 구매 없이 장바구니 추가 항목에 초점을 맞추는 반면, 이 대상자는 특정 제품을 탐색했지만 장바구니에 추가하지 않았고 특정 시간대 내에 해당 사이트에서 후속 활동이 없는 이전 참여를 특정적으로 찾습니다. 이 대상자는 이 포함 기준을 충족하는 고객의 시각에서 브랜드를 “최상위”로 유지하는 데 도움이 되며, 디지털 속성이 기존 e커머스 모델과 다를 수 있는 고객에게도 활용할 수 있습니다.

다음 이벤트는 사용자가 온라인에서 제품을 보고 다음 24시간 동안 장바구니에 추가하지 않은 후 3일 동안 브랜드 참여가 없는 재참여 여정에 사용됩니다.

이 대상자를 설정할 때 다음 필드와 조건이 필요합니다.

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.procuctListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

재참여 여정에 대한 설명은 다음과 같이 나타납니다.

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB 포기한 장바구니 여정]

이 대상자는 일반적인 “장바구니 포기” 시나리오를 지원하기 위해 만들어졌습니다. 목적은 장바구니에 제품을 추가했지만 최종적으로 구매를 완료하지 않은 고객을 찾는 것입니다. 이 대상자는 고객의 시각에서 해당 브랜드를 “최상위”로 유지하는 데 도움이 될 뿐만 아니라, 고객이 후속 구매 없이 포기한 제품도 그렇게 유지하는 데 도움이 됩니다.

다음 이벤트는 사용자가 장바구니에 제품을 추가했지만 지난 24시간 동안 구매를 완료하거나 장바구니를 비우지 않은 포기한 장바구니 여정에 사용됩니다.

이 대상자를 설정할 때 다음 필드와 조건이 필요합니다.

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `EventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

포기한 장바구니 여정에 대한 설명은 다음과 같이 나타납니다.

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB 주문 확인 여정]

이 여정은 대상자를 만들 필요가 없습니다.

>[!ENDTABS]

### Adobe Journey Optimizer의 여정 설정 {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer]는 다이어그램에 표시된 모든 항목을 포함하지 않습니다. 모두 [유료 미디어 광고](/help/destinations/catalog/social/overview.md) 다음에서 생성됨 [!UICONTROL 대상].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)는 고객에게 연관성 있고 상황에 맞는 개인화된 경험을 제공할 수 있도록 해 줍니다. 고객 여정은 고객이 브랜드와 상호 작용하는 전체 프로세스입니다. 각 사용 사례 여정에는 특정 정보가 필요합니다. 아래 목록은 각 Journey 분기에 필요한 정확한 데이터입니다.

>[!BEGINTABS]

>[!TAB 재참여 여정]

재참여 여정은 웹 사이트와 모바일 앱 모두에서 포기한 제품 탐색을 대상으로 합니다.<p>![고객 지능형 재참여 여정의 높은 수준의 시각적 개요](../intelligent-re-engagement/images/re-engagement-journey.png "고객 지능형 재참여 여정의 높은 수준의 시각적 개요"){width="2560" zoomable="yes"}</p>

+++이벤트

* 이벤트 1: 제품 보기
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

* 이벤트 2: 장바구니에 추가
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

* 이벤트 3: 브랜드 참여
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

+++주요 여정 논리

* 여정 입력 로직
   * 제품 보기 이벤트

* 조건
   * 제품을 마지막으로 본 이후 온라인 또는 오프라인 구매 이벤트가 하나 이상 있는지 확인합니다.
      * 스키마: 고객 디지털 트랜잭션
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 제품을 마지막으로 본 이후 최소 하나의 오프라인 구매를 확인합니다.
      * 스키마: 고객 오프라인 트랜잭션
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 조건 - 대상 채널 선택
      * 이메일
         * `consents.marketing.email.val = y`
      * 푸시
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * 채널 개인화
      * 제품 보기를 기반으로 개인화된 채널 콘텐츠입니다.

+++

>[!TAB 포기한 장바구니 여정]

포기한 장바구니 여정은 장바구니에 담았지만 웹 사이트와 모바일 앱에서 아직 구매하지 않은 제품을 대상으로 합니다.<p>![고객이 포기한 장바구니 여정의 높은 수준의 시각적 개요](../intelligent-re-engagement/images/abandoned-cart-journey.png "고객이 포기한 장바구니 여정의 높은 수준의 시각적 개요"){width="2560" zoomable="yes"}</p>

+++이벤트

* 이벤트 2: 장바구니에 추가
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

* 이벤트 4: 온라인 구매
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

* 이벤트 3: 브랜드 참여
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

+++주요 여정 논리

* 여정 입력 로직
   * `AddToCart` 이벤트

* 인증된 상태의 AuthenticatedState

* 조건: 장바구니를 마지막으로 포기한 이후 오프라인 구매:
   * 스키마: 고객 오프라인 트랜잭션
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* 조건: 장바구니를 마지막으로 포기한 후 장바구니를 비움:
   * 스키마: 고객 디지털 트랜잭션
   * `eventType = commerce.cartCleared`
   * `cartID`(장바구니 ID)
   * `timestamp > timestamp of cart was last abandoned`

* 대상 채널 선택(더 넓은 도달 범위를 위해 하나 또는 여러 채널 선택)
   * 이메일
      * `consents.marketing.email.val = y`
   * 푸시
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * 채널 개인화
      * 장바구니 세부 정보를 표시하고 여러 제품을 테이블 형식으로 표시할 수 있습니다.

+++

>[!TAB 주문 확인 여정]

주문 확인 여정은 웹 사이트 및 모바일 앱을 통한 제품 구매에 중점을 둡니다.<p>![고객 주문 확인 여정의 높은 수준의 시각적 개요](../intelligent-re-engagement/images/order-confirmation-journey.png "고객 주문 확인 여정의 높은 수준의 시각적 개요"){width="2560" zoomable="yes"}</p>

+++이벤트

* 이벤트 4: 온라인 구매
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

+++주요 여정 논리

* 여정 입력 로직
   * 주문 이벤트

* 조건
   * 대상 채널 선택(더 넓은 도달 범위를 위해 하나 또는 여러 채널 선택).
      * 주문 확인은 본질적으로 제공되는 것으로 간주되므로, 일반적으로 동의 확인은 필요하지 않습니다.
      * 이메일
      * 푸시
      * SMS

   * 채널 콘텐츠 개인화
      * 주문 세부 정보를 표시하고 제품 목록을 테이블 형식으로 표시할 수 있습니다.

+++

>[!ENDTABS]

[!DNL Adobe Journey Optimizer]의 여정 생성에 대한 자세한 내용은 [여정 시작 안내서](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)를 참조하십시오.

### 대상에서 유료 미디어 광고 설정 {#paid-media-ads}

대상 프레임워크는 유료 미디어 광고에 사용됩니다. 동의가 확인되면 구성된 다양한 대상으로 전송됩니다. 대상에 대한 자세한 내용은 [대상 개요](/help/destinations/home.md) 문서를 참조하십시오.

#### 대상에 필요한 데이터

스트리밍 세그먼트 내보내기 대상(예: Facebook, Google 고객 일치 타겟팅, Google DV360)은 고객 데이터의 다양한 ID를 지원합니다.

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

포기한 장바구니 세그먼트는 스트리밍 중이므로, 이 사용 사례의 대상 프레임워크에서 사용할 수 있습니다.

* 스트림/트리거됨
   * [광고](/help/destinations/catalog/advertising/overview.md)/[유료 미디어 및 소셜](/help/destinations/catalog/social/overview.md)
   * [모바일](/help/destinations/catalog/mobile-engagement/overview.md)
   * [스트리밍 대상](/help/destinations/catalog/streaming/http-destination.md)
   * [고객 Destination SDK](/help/destinations/destination-sdk/overview.md)
