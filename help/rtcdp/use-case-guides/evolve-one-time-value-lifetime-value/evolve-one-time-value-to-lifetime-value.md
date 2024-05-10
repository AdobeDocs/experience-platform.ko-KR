---
title: 일회성 고객 가치를 라이프타임 가치로 향상
description: 특정 고객의 특성, 동작 및 과거 구매를 기반으로 최상의 보완 제품 또는 서비스를 제공하기 위해 개인화된 캠페인을 만드는 방법을 알아봅니다.
feature: Use Cases
source-git-commit: 1134ca4d8a5901b8fe125578ad7f0bc81f6a320f
workflow-type: tm+mt
source-wordcount: '3179'
ht-degree: 26%

---

# 일회성 고객 가치를 라이프타임 가치로 향상

>[!IMPORTANT]
> 
>* 이 페이지에는 설명된 사용 사례를 달성하기 위한 Real-Time CDP 및 Adobe Journey Optimizer의 샘플 구현이 나와 있습니다. 페이지에 제공된 수치, 자격 기준 및 기타 필드를 규범적 수치가 아닌 안내서로 사용하십시오.
>* 이 사용 사례를 완료하려면 Real-Time CDP 및 Adobe Journey Optimizer에 대한 라이선스가 있어야 합니다. 자세한 내용 [전제 조건 및 계획 섹션](#prerequisites-and-planning) 아래에 있습니다.

일회성 고객 가치 대 라이프타임 가치 사용 사례를 구현하여 브랜드 참여 및 브랜드 충성도를 높입니다. 의 강력한 Experience Platform 기능을 사용하여 여러 채널 또는 여정에서 연결된 고객 경험을 구축합니다. [Real-Time CDP](/help/rtcdp/home.md) 및 [Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home).

타겟팅하는 대상은 지난 3개월 이내에 구매한 적이 없는 속성 방문자입니다.

속성을 방문하고 제공하는 제품이나 서비스를 산발적으로 구매하는 이러한 고객을 고려하십시오. 브랜드가 일회성 값이 아닌 장기적인 가치를 제공할 수 있도록 이러한 고객에게 어필할 수 있는 개인화된 캠페인을 만들 수 있습니다. 방법 알아보기:

* 데이터 수집 및 관리
* 대상자 만들기
* Adobe Journey Optimizer에서 이러한 대상을 타깃팅하고 Real-Time CDP에서 활성화할 여정을 만듭니다.

![단계별로 일회성 값을 라이프타임 값으로 진화시키는 높은 수준의 시각적 개요.](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){width="500" zoomable="yes"}

## 전제 조건 및 계획 {#prerequisites-and-planning}

내부적으로 브랜드 충성도를 높이기 위한 비즈니스 목표 및 목표를 정의했습니다. 이는 고객 참여 및 충성도를 높이기 위한 사용 사례 실행으로 번역할 수 있습니다.

이를 위해 필요한 기술은 두 개의 Experience Platform 앱으로 구성되어 있다 [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html) 및 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=ko). 아래 목록은 사용 사례를 구현할 때 사용할 두 앱의 다양한 기능과 UI 요소입니다.

>[!TIP]
>
>이러한 모든 영역에 대해 필요한 [속성 기반의 액세스 제어 권한](/help/access-control/abac/end-to-end-guide.md)이 있는지 확인하거나, 시스템 관리자에게 필요한 권한 부여를 요청하십시오.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html): 데이터 소스 간에 데이터를 통합하여 캠페인을 실행합니다. 그런 다음 이 데이터를 사용하여 이메일 및 웹 프로모션 타일에 사용되는 표면 맞춤형 데이터 요소(예: 이름 또는 계정 관련 정보) 및 캠페인 대상자를 만듭니다. 마지막으로 Real-Time CDP은 유료 미디어 대상에 대한 대상을 활성화하는 데에도 사용됩니다.
   * [스키마](/help/xdm/home.md)
   * [프로필](/help/profile/home.md)
   * [데이터 세트](/help/catalog/datasets/overview.md)
   * [대상자](/help/segmentation/home.md)
   * [대상](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html): 여정을 디자인하고, 트리거를 설정하고, 방문자에게 적합한 메시지를 보냅니다.
   * [이벤트 또는 대상자 트리거](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [대상 및 이벤트](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [여정](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Real-Time CDP 및 Journey Optimizer 아키텍처

다음은 Real-Time CDP 및 Journey Optimizer의 다양한 구성 요소에 대한 높은 수준의 아키텍처 보기입니다. 이 다이어그램은 이 페이지에 설명된 사용 사례를 달성하기 위해 데이터가 데이터 수집에서 여정 또는 캠페인을 통해 활성화된 지점까지 두 Experience Platform 앱을 통해 어떻게 이동하는지를 보여 줍니다.

![아키텍처 높은 수준의 시각적 개요.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){width="1000" zoomable="yes"}

## 사용 사례를 달성하는 방법: 높은 수준의 개요 {#achieve-the-use-case-high-level}

다음은 워크플로, 활성화 워크플로 및 여정 워크플로의 조합에 대한 높은 수준의 개요입니다.

아래 그림에 나와 있는 샘플 워크플로우에서는 특정 기준을 충족하고 해당 기준을 웹 사이트 또는 앱으로 돌아가도록 유도하려는 고객을 찾습니다. 자산에 대한 제한된 활동 대신 더 반복적인 방식으로 돌아오는 여정에서 설정하려고 합니다. 자산으로 다시 가져온 다음 다시 돌아오면 여정에 입력하여 사이트에서 반복적으로 구매하도록 합니다. 여기서 설정한 캠페인은 매월 고객과의 1회 참여로 제한됩니다.

먼저 고가치 및 빈도가 낮은 고객에게 메시지를 보냅니다. 그런 다음 지난 30일 이내에 이 메시지가 수신되었는지 확인합니다. 등록되지 않은 경우 예를 들어 새 구독 프로그램에 대한 여정에 등록하면 됩니다. 그런 다음 며칠 동안(이 예에서는 7일) 대기할 수 있습니다. 이 시간 후에 사용자가 메시지를 보낸 구독을 구매하지 않았다면 대상을 통해 유료 미디어 광고를 게재할 수 있습니다. 구독을 구입한 경우 주문 확인 여정을 입력하도록 하면 사용 사례를 완료할 수 있습니다.

>[!IMPORTANT]
>
>이 페이지의 아래에 설명된 대로 [스키마의 전용 동의 필드 그룹](#customer-attributes-schema) 및 기준 [동의 정책 구현](#privacy-consent), 모든 작업 및 워크플로는 개인 정보 및 동의 우선 방식으로 구현됩니다.

>[!BEGINSHADEBOX]

![단계별로 일회성 값을 라이프타임 값으로 진화시키는 높은 수준의 시각적 개요.](../evolve-one-time-value-lifetime-value/images/step-by-step.png){width="1000" zoomable="yes"}

1. 스키마 및 데이터 세트를 만든 다음 다음을 위해 표시합니다. [!UICONTROL 프로필].
2. 데이터는 Web SDK, Mobile Edge SDK 또는 API를 통해 수집되고 Experience Platform에 통합됩니다. Analytics Data Connector도 활용할 수 있지만 여정 지연이 발생할 수 있습니다.
3. 프로필을 Real-Time CDP에 로드하고 책임 있는 사용을 보장하기 위한 거버넌스 정책을 구축합니다.
4. 프로필 목록에서 집중 대상자를 만들어 고가치 고객과 저빈도 고객을 확인합니다.
5. 에서 두 개의 여정을 만듭니다. [!DNL Adobe Journey Optimizer]- 사용자에게 새 구독 프로그램에 대한 메시지를 보내고, 나중에 구매를 확인하는 메시지를 보냅니다.
6. 원하는 경우, 원하는 유료 미디어 대상에 대한 구독을 구매하지 않은 고객 대상을 활성화합니다.

>[!ENDSHADEBOX]

## 사용 사례를 달성하는 방법 {#achieve-use-case-instruction}

위의 고급 개요에서 각 단계를 완료하려면 추가 정보 및 보다 자세한 지침에 대한 링크를 제공하는 아래 섹션을 참조하십시오.

### 사용할 UI 기능 및 요소 {#ui-functionality-and-elements}

사용 사례를 구현하는 단계를 완료하면 이 문서의 시작 부분에 나열된 Real-Time CDP, Adobe Journey Optimizer 기능 및 UI 요소를 사용하게 됩니다. 이러한 모든 영역에 대해 필요한 속성 기반의 액세스 제어 권한이 있는지 확인하거나, 시스템 관리자에게 필요한 권한 부여를 요청하십시오.

### 스키마 디자인 만들기 및 필드 그룹 지정 {#schema-design}

Experience Data Model(XDM) 리소스는 [!DNL Adobe Experience Platform]의 [!UICONTROL 스키마] 작업 영역에서 관리됩니다. 에서 제공하는 핵심 리소스를 보고 탐색할 수 있습니다. [!DNL Adobe] (예: [!UICONTROL 필드 그룹])을 만들고 조직에 대한 사용자 지정 리소스 및 스키마를 만듭니다.

[스키마](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko-KR) 만들기에 대한 자세한 내용은 [스키마 튜토리얼 만들기](/help/xdm/tutorials/create-schema-ui.md)를 참조하십시오.

이 샘플 구현에는 사용 사례에서 일회성 값을 라이프타임 값으로 발전시키는 데 사용할 수 있는 몇 가지 스키마 디자인이 있습니다. 각 스키마에는 설정할 특정 필수 필드와 일부 제안된 필드가 포함되어 있습니다.

Adobe 샘플 구현을 기준으로, 이 사용 사례를 달성하려면 다음 세 가지 스키마를 만드는 것이 좋습니다.

* [고객 속성 스키마](#customer-attributes-schema) (프로필 스키마)
* [고객 디지털 트랜잭션 스키마](#customer-digital-transactions-schema) (경험 이벤트 스키마)
* [고객 오프라인 트랜잭션 스키마](#customer-offline-transactions-schema) (경험 이벤트 스키마)

#### 고객 속성 스키마 {#customer-attributes-schema}

이 스키마를 사용하여 고객 정보를 구성하는 프로필 데이터를 구조화하고 참조합니다. 이 데이터는 일반적으로 CRM 또는 유사한 시스템을 통해 [!DNL Adobe Experience Platform]으로 수집되며, 개인화, 마케팅 동의, 향상된 세분화 기능에 사용되는 고객 세부 정보를 참조하는 데 필요합니다.

![필드 그룹이 강조 표시된 고객 속성 스키마](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

고객 속성 스키마는 [!UICONTROL XDM 개별 프로필] 클래스에 표시되며, 다음 필드 그룹을 포함합니다.

+++인구 통계 세부 정보(필드 그룹)

[인구 통계 세부 정보](/help/xdm/field-groups/profile/demographic-details.md)는 XDM 개별 프로필 클래스의 표준 스키마 필드 그룹입니다. 필드 그룹은 개별 사용자에 대한 정보를 설명하는 하위 필드가 있는 루트 수준의 사용자 오브젝트를 제공합니다.

+++

+++개인 연락처 세부 정보(필드 그룹)

[개인 연락처 세부 정보](/help/xdm/field-groups/profile/personal-contact-details.md) 는 개별 사용자에 대한 연락처 정보를 설명하는 XDM 개별 프로필 클래스에 대한 표준 스키마 필드 그룹입니다.

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

[외부 소스 시스템 감사 속성](/help/xdm/data-types/external-source-system-audit-attributes.md)은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

+++

+++동의 및 환경 설정 필드 그룹(필드 그룹)

[동의 및 환경 설정](/help/xdm/field-groups/profile/consents.md) 필드 그룹은 동의 및 기본 설정 정보를 캡처하기 위해 동의라는 단일 오브젝트 유형 필드를 제공합니다.

+++

#### 고객 디지털 트랜잭션 스키마 {#customer-digital-transactions-schema}

이 스키마는 웹 사이트 또는 기타 관련 디지털 플랫폼에서 발생하는 고객 활동을 구성하는 이벤트 데이터를 구조화하고 참조하는 데 사용됩니다. 이 데이터는 일반적으로 다음 위치에 수집됩니다 [!DNL Adobe Experience Platform] 경유 [웹 SDK](/help/web-sdk/home.md) 또한 여정 트리거, 자세한 온라인 고객 분석 및 향상된 세그멘테이션 기능에 사용되는 다양한 찾아보기 및 전환 이벤트를 참조해야 합니다.

![필드 그룹이 강조 표시된 고객 디지털 거래 스키마](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

고객 디지털 트랜잭션 스키마는 [!UICONTROL XDM ExperienceEvent] 클래스로 표시되며, 다음 필드 그룹을 포함합니다.

+++Adobe Experience Platform Web SDK ExperienceEvent(필드 그룹)

| 필드 | 요구 사항 |
| --- | --- |
| `device.model` | 권장 |
| `environment.browserDetails.userAgent` | 권장 |

+++

+++웹 세부 정보(필드 그룹)

[웹 세부 정보](/help/xdm/field-groups/event/web-details.md) 는 상호 작용, 페이지 세부 사항 및 레퍼러 등 웹 세부 사항 이벤트 관련 정보를 설명하는 데 사용되는 XDM ExperienceEvent 클래스의 표준 스키마 필드 그룹입니다.

+++

+++소비자 경험 이벤트(필드 그룹)

이 필드 그룹에는 웹 속성에서 사용자가 수행한 구매 또는 이벤트 검색 등의 작업에 대한 다양한 정보가 포함됩니다.

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

다음 [최종 사용자 ID 세부 정보](/help/xdm/field-groups/event/enduserids.md) 필드 그룹에는 방문 시 사이트에서 인증되었는지 여부와 사용자에 대한 id 정보 등 사용자에 대한 다양한 정보가 포함됩니다.

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

외부 소스 시스템 감사 속성은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

+++

#### 고객 오프라인 트랜잭션 스키마 {#customer-offline-transactions-schema}

이 스키마는 웹 사이트 외부 플랫폼에서 발생하는 고객 활동을 구성하는 이벤트 데이터를 구성하고 참조하는 데 사용됩니다. 이 데이터는 일반적으로 POS(또는 유사한 시스템)에서 [!DNL Adobe Experience Platform]으로 수집되며, API 연결을 통해 Platform으로 스트리밍되는 경우가 가장 많습니다. 읽어보기 [일괄 처리 수집](/help/ingestion/batch-ingestion/getting-started.md). 목적은 여정 트리거, 심층적인 온라인 및 오프라인 고객 분석, 향상된 세분화 기능에 사용되는 다양한 오프라인 전환 이벤트를 참조하는 것입니다.

![필드 그룹이 강조 표시된 고객 오프라인 트랜잭션 스키마](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

고객 오프라인 트랜잭션 스키마는 [!UICONTROL XDM ExperienceEvent] 클래스로 표시되며, 다음 필드 그룹을 포함합니다.

+++상거래 세부 정보(필드 그룹)

[Commerce 세부 정보](/help/xdm/field-groups/event/commerce-details.md) 는 의 표준 스키마 필드 그룹입니다. [!DNL XDM ExperienceEvent] 제품 정보(SKU, 이름, 수량) 및 표준 장바구니 작업(주문, 체크아웃, 포기)과 같은 상거래 데이터를 설명하는 데 사용되는 클래스입니다.

+++

+++개인 연락처 세부 정보(필드 그룹)

[[!UICONTROL 개인 연락처 세부 정보]](/help/xdm/field-groups/profile/personal-contact-details.md) 는 의 표준 스키마 필드 그룹입니다. [!DNL XDM Individual Profile] 클래스: 개별 사용자에 대한 연락처 정보를 설명합니다.

+++

+++외부 소스 시스템 감사 세부 정보(필드 그룹)

외부 소스 시스템 감사 속성은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

+++

#### Adobe 웹 커넥터 스키마 {#adobe-web-connector-schema}

>[!NOTE]
>
>[!DNL Adobe Analytics Data Connector]를 사용하는 경우 선택적 구현입니다.

이 스키마는 웹 사이트 또는 기타 관련 디지털 플랫폼에서 발생하는 고객 활동을 구성하는 이벤트 데이터를 구조화하고 참조하는 데 사용됩니다. 이 스키마는 고객 디지털 트랜잭션 스키마와 유사하지만, Web SDK가 데이터 수집에 대한 옵션이 아닐 때 사용할 수 있다는 점에서 다릅니다. 따라서 를 활용할 때 이 스키마를 사용할 수 있습니다. [!DNL Adobe Analytics Data Connector] 온라인 데이터를에 보내려면 [!DNL Adobe Experience Platform] 를 기본 또는 보조 데이터 스트림으로 사용합니다.

![필드 그룹이 강조 표시된 Adobe 웹 커넥터 스키마](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

[!DNL Adobe] 웹 커넥터 스키마는 [!UICONTROL XDM ExperienceEvent] 클래스로 표시되며, 다음 필드 그룹을 포함합니다.

+++Adobe Analytics ExperienceEvent 템플릿(필드 그룹)

[[!UICONTROL Adobe Analytics ExperienceEvent 전체 확장]](/help/xdm/field-groups/event/analytics-full-extension.md) 는 Adobe Analytics에서 수집하는 일반 지표를 캡처하는 표준 스키마 필드 그룹입니다.

+++

### 스키마에서 데이터 세트 만들기 {#dataset-from-schema}

데이터 세트는 데이터 그룹의 저장 및 관리 구조입니다. 이 샘플 구현을 수행하는 데 사용되는 각 스키마에는 단일 데이터 세트가 있습니다.

스키마에서 [데이터 세트](/help/catalog/datasets/overview.md)를 만드는 방법에 대한 자세한 내용은 [데이터 세트 UI 안내서](/help/catalog/datasets/user-guide.md)를 참조하십시오.

>[!NOTE]
>
>스키마를 생성하는 단계와 유사하게 실시간 고객 프로필에 포함할 데이터 세트를 활성화해야 합니다. 실시간 고객 프로필에서 사용할 데이터 세트를 활성화하는 방법에 대한 자세한 내용은 [스키마 튜토리얼 만들기](/help/xdm/tutorials/create-schema-ui.md#profile)를 참조하십시오.

### 개인 정보, 동의 및 데이터 거버넌스 {#privacy-consent}

#### 동의 정책

>[!IMPORTANT]
>
>고객에게 브랜드로부터 커뮤니케이션 수신을 거부할 수 있는 기능을 제공하고 이러한 선택이 존중되도록 하는 것은 법적 요구 사항입니다. 에서 해당 법률에 대해 자세히 알아보십시오. [개인 정보 보호 규정 개요](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

다음 구현 고려 [동의 정책](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) 및 다음 연락처로 연락하기 전에 방문자에게 동의를 요청합니다.

* `consents.marketing.email.val = "Y"`인 경우, 이메일 전송 가능
* `consents.marketing.sms.val = "Y"`인 경우, SMS 전송 가능
* `consents.marketing.push.val = "Y"`인 경우, 푸시 가능
* `consents.share.val = "Y"`인 경우, 광고 가능

#### 데이터 거버넌스 레이블 및 적용

다음을 추가하고 적용합니다. [데이터 거버넌스 레이블](/help/data-governance/labels/overview.md):

* 개인 이메일 주소는 디바이스가 아닌 특정 개인을 식별하거나 연락하는 데 사용되는 직접 식별 가능한 데이터로 사용됩니다.
   * `personalEmail.address = I1`

#### 마케팅 정책

없음 [마케팅 정책](/help/data-governance/policies/overview.md) 이 사용 사례의 일부로 만드는 여정에 필요합니다. 그러나 다음 정책을 원하는 대로 고려할 수 있습니다.

* 민감한 데이터 제한
* 온사이트 광고 제한
* 이메일 타겟팅 제한
* 사이트 간 타깃팅 제한
* 직접 식별 가능한 데이터와 익명 데이터의 결합 제한

### 대상자 만들기 {#create-audiences}

이 사용 사례에서는 두 명의 대상을 만들어 프로필 저장소의 프로필 하위 집합에서 공유하는 특정 속성이나 동작을 정의하여 마케팅 가능한 사람 그룹을 구별해야 합니다. Adobe Experience Platform에서 여러 가지 방법으로 대상을 만들 수 있습니다.

* 대상자를 만드는 방법에 대한 자세한 내용은 [Audience Service UI 안내서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).
* 구성 방법에 대한 자세한 내용 [대상](/help/segmentation/home.md), 다음을 읽습니다 [대상 구성 UI 안내서](/help/segmentation/ui/audience-composition.md).
* 플랫폼에서 파생된 세그먼트 정의를 통해 대상자를 만드는 방법에 대한 자세한 내용은 [Audience Builder UI 안내서](/help/segmentation/ui/segment-builder.md).

특히 아래 이미지에 표시된 대로 사용 사례의 여러 단계에서 두 개의 대상을 만들고 사용해야 합니다.

![강조 표시된 대상자.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){width="1000" zoomable="yes"}

>[!BEGINTABS]

>[!TAB Adobe Journey Optimizer Qualifying Audience]

가치가 높고 빈도가 낮은 이 대상에는 새 구독 프로그램에 대해 알리기 위해 여정을 통해 연락하려는 프로필이 포함됩니다. 대상자 세부 사항은 다음과 같습니다.

* 설명: 지난 3개월 동안 총 비용이 250달러 이상인 프로필
* 대상자에 필요한 필드 및 조건:
   * 이벤트: `commerce.order.payments.paymentamount`
* 합계: >= $250
   * 이벤트 유형: `commerce.purchases`
* 타임스탬프: 지금부터 3개월 미만


>[!TAB 유료 미디어 대상자]

이 대상자는 지난 3개월 동안 총계로 250달러 이상을 소비했으며 지난 7일 동안 구매를 하지 않은 프로필을 포함하도록 만들어집니다. 대상자 세부 사항은 다음과 같습니다.

* 설명: 지난 3개월 동안 총액이 250달러 이상이었고 지난 7일 동안 구매가 없었던 프로필입니다.
* 필요한 필드 및 조건:
   * 이벤트 유형: `journey.feedback`
      * 피연산자: = true
   * 이벤트: `experience.journeyOrchestration.stepEvents.nodeName`
      * 피연산자: = JourneyStepEventTracker - 구독을 구매하지 않음
      * 타임스탬프: 지난 7일
   * EventType은 `commerce.purchases`
      * 타임스탬프: &lt;= 7일 전
   * 이벤트: SKU
      * 값: = `subscription`

>[!ENDTABS]

### Adobe Journey Optimizer의 여정 설정 {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer]는 다이어그램에 표시된 모든 항목을 포함하지 않습니다. 모두 [유료 미디어 광고](/help/destinations/catalog/social/overview.md) 다음에서 생성됩니다. [!UICONTROL 대상] [작업 영역](/help/destinations/ui/destinations-workspace.md).

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)는 고객에게 연관성 있고 상황에 맞는 개인화된 경험을 제공할 수 있도록 해 줍니다. 고객 여정은 고객이 브랜드와 상호 작용하는 전체 프로세스입니다. 각 사용 사례 여정에 특정 정보가 필요합니다.

이 사용 사례를 달성하려면 두 개의 별도 여정을 만들어야 합니다.

* 라이프타임 여정 - 고가치 저빈도 고객에게 보내는 메시지를 포함합니다.
* 호출에 응답하고 구독을 구매하는 사용자를 위한 주문 확인 여정.

![강조 표시된 여정.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){width="1000" zoomable="yes"}

아래 목록은 각 Journey 분기에 필요한 정확한 데이터입니다.

>[!BEGINTABS]

>[!TAB 라이프타임 여정]

라이프타임 여정은 지난 30일 이내에 타겟팅되지 않은 고가치 및 저빈도 고객의 대상을 해결합니다. 이러한 고객에게 메시지가 표시된 다음 7일 후에도 구매하지 않는 경우 유료 미디어 광고를 표시할 수 있는 대상에 비구매자를 포함할 수 있습니다. 구매하는 경우 개별 탭에 자세히 나와 있는 주문 확인 여정에서 구매자를 설정할 수 있습니다.

![라이프타임 여정 높은 수준의 시각적 개요](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "라이프타임 여정에 대한 일회성 값 높은 수준의 시각적 개요."){width="2560" zoomable="yes"}

+++세부 여정 논리

위에 표시된 여정은 다음 논리를 따릅니다.

1. 대상 읽기: 사용 [대상자 활동 읽기](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=en) (위의 대상 섹션에서 만든 첫 번째 대상)

2. 조건 - 기본 채널: [조건 활동](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html) 이메일, SMS 또는 푸시 알림을 통해 고객에게 연락하는 방법을 결정합니다. 세 가지 작업 활동을 사용하여 세 개의 분기를 만듭니다.

3. 대기: [대기 활동](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html) 구매를 들을때까지 기다리세요.

4. 조건 - 지난 7일 동안 구매한 구독: 조건 활동을 사용하여 지난 7일 동안의 제품 구매를 수신합니다.

5. JourneyStepEventTracker - 구독이 구매되지 않음: [사용자 지정 작업](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html) 메시지를 수신했지만 아직 구독을 구매하지 않은 방문자 여정 종료 시 사용자 지정 조건의 일부로 `journey.feedback` 이벤트를 만들고 다음을 기반으로 데이터 세트에 추가 [!UICONTROL 여정 단계 이벤트] 스키마. 이 이벤트를 사용하여 구독을 구매하지 않은 대상과 유료 미디어 광고를 통해 타깃팅할 수 있는 대상을 세그먼트화할 수 있습니다.

+++

>[!TAB 주문 확인 여정]

주문 확인 여정은 구매가 홈페이지나 모바일 앱을 통해 이뤄졌는지에 초점을 맞춘다. 고객이 예를 들어 귀사와의 구독 구매를 성공적으로 완료한 후 주문 확인 여정에서 이를 설정할 수 있습니다.

![고객 주문 확인 여정의 높은 수준의 시각적 개요](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "고객 주문 확인 여정의 높은 수준의 시각적 개요"){width="2560" zoomable="yes"}

+++여정 논리

확인 여정에서 아래 제안된 이벤트, 필드 및 작업을 사용하십시오.

* 이 여정은 온라인 구매 이벤트에 의해 트리거됩니다
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
   * 대상 채널 을 선택합니다(더 넓은 범위를 위해 하나 이상의 채널을 선택할 수 있음).
      * 주문 확인은 본질적으로 제공되는 것으로 간주되므로, 일반적으로 동의 확인은 필요하지 않습니다.
      * 이메일
      * 푸시
      * SMS

   * 채널 콘텐츠 개인화
      * 주문 세부 정보를 표시하고 제품 목록을 테이블 형식으로 표시할 수 있습니다.

+++

>[!ENDTABS]

여정 만들기에 대한 자세한 내용은 [!DNL Adobe Journey Optimizer], 다음을 읽습니다 [여정 시작](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) 가이드.

### 유료 미디어 광고를 표시할 대상 설정 {#paid-media-ads}

일부 사용자는 새 프로그램에 대해 메시지를 보낸 후에도 구독을 구매하지 않았을 수 있습니다. 며칠 동안 기다린 후(이 예제의 경우 7일), 해당 사용자에게 유료 미디어 광고를 표시하여 구독을 구매하도록 유도할 수 있습니다.

유료 미디어 광고를 보려면 Real-Time CDP의 대상 프레임워크를 사용하십시오. 사용 가능한 여러 광고 대상 중 하나를 선택하여 고객에게 유료 미디어 광고를 표시하고 사용자가 선택한 유료 미디어 대상을 활성화합니다 [이전에 생성됨](#create-audiences) 원하는 목적지로 이동합니다. 사용 가능한 의 개요 보기 [advertising](/help/destinations/catalog/advertising/overview.md) 및 [소셜](/help/destinations/catalog/social/overview.md) 대상.

대상에 데이터를 활성화하는 방법을 알아보려면 다음 단계를 따르십시오(예: [트레이드 데스크](/help/destinations/catalog/advertising/tradedesk.md) 또는 [Google Customer Match](/help/destinations/catalog/advertising/google-customer-match.md)) 아래 설명서를 참조하십시오.

* [새 대상 연결 만들기](/help/destinations/ui/connect-destination.md)
* [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)

## 다음 단계 {#next-steps}

빈도가 낮고 가치가 높은 사용자를 여정에서 설정하고 유료 미디어 광고를 그 하위 집합에 표시함으로써 일부는 일회성 가치에서 라이프타임 가치 고객으로 전환하여 브랜드 충성도 및 고객 참여 지표를 향상시킬 수 있기를 바랍니다.

다음으로, 다음과 같이 Real-Time CDP에서 지원하는 다른 사용 사례를 살펴볼 수 있습니다. [지능적으로 재참여하는 고객](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) 또는 [인증되지 않은 사용자에게 개인화된 콘텐츠 표시](/help/rtcdp/partner-data/onsite-personalization.md) 웹 속성에서.