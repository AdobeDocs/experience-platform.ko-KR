---
solution: Experience Platform
title: 금융 서비스 산업 데이터 모델 ERD
description: 은행, 금융 서비스 및 보험(BFSI) 산업에 대한 표준화된 데이터 모델을 설명하는 엔티티 관계 다이어그램(ERD)을 봅니다. 이 데이터 모델은 Adobe Experience Platform에서 사용하기 위해 XDM(Experience Data Model)과 호환됩니다.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# [!UICONTROL 금융 서비스] 업계 데이터 모델 ERD

다음의 개체관계도표(ERD)는 은행, 금융 서비스 및 보험(BFSI) 산업에 대한 표준화된 데이터 모델을 나타낸다. ERD는 Adobe Experience Platform에서 데이터가 저장되는 방식을 고려하여 비표준화된 방식으로 의도적으로 제공됩니다.

>[!NOTE]
>
>설명된 대로 ERD는 이 업계 사용 사례에 맞게 데이터를 모델링하는 방법에 대한 권장 사항입니다. Experience Platform에서 이 데이터 모델을 사용하려면 권장 스키마와 해당 관계를 직접 구성해야 합니다. 자세한 내용은 UI에서 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) 관리에 대한 안내서를 참조하십시오.

다음 범례를 사용하여 이 ERD를 해석하십시오.

* 에 표시된 각 엔터티는 기본 [XDM(경험 데이터 모델) 클래스](../composition.md#class)를 기반으로 합니다.
* 상위 필드 아래에 들여쓴 필드는 상위 필드 그룹에 속하는 하위 필드 또는 하위 필드를 나타냅니다.
* 지정된 엔티티에 대한 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 &quot;ID&quot;로 표시되며, 이러한 속성 중 하나는 &quot;기본 ID&quot;로 표시됩니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 개인이나 개인을 결정할 수 없는 경우가 많기 때문에 엔티티 관계는 종속되지 않는 것으로 표시됩니다.

![금융 산업 데이터 모델에 대한 ERD 예](../../images/industries/financial.png)

>[!NOTE]
>
>Experience Event 엔티티는 XDM ExperienceEvent 클래스에서 제공하는 고유 식별자(`_id`) 특성을 나타내는 &quot;_ID&quot; 필드를 포함합니다. 이 값에 필요한 사항에 대한 자세한 내용은 [XDM ExperienceEvent](../../classes/experienceevent.md)에 대한 참조 문서를 참조하십시오.

## [!UICONTROL 금융 서비스] 사용 사례

다음 표에서는 몇 가지 일반적인 금융 사용 사례에 대한 권장 클래스 및 스키마 필드 그룹을 간략하게 설명합니다.

| 활용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 옴니채널 보고 통찰력 및 여정 자동화를 통해 선호 세그먼트에 대한 규모에 맞게 개인화를 촉진하여 선호 보상 프로그램에 대한 등록을 늘리십시오. | <ul><li>**[[!UICONTROL 제품]](../../classes/product.md)**:<ul><li>[[!UICONTROL 제품 범주]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 카드 동작]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 견적 요청 세부 정보]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 예금 세부 정보]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 채널 세부 정보]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 잔고 전송]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 정보]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 충성도 세부 정보]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 온라인 및 오프라인 채널에서 크로스 채널 개인화를 최적화합니다. | <ul><li>**[[!UICONTROL 제품]](../../classes/product.md)**:<ul><li>[[!UICONTROL 제품 범주]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 채널 세부 정보]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 정보]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 충성도 세부 정보]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 크로스 채널 행동 분석에서 얻은 통찰력을 사용하여 새로운 제품 오퍼로 이어질 수 있는 제품 사용 패턴을 식별하여 새로운 수익 기회를 창출합니다. | <ul><li>**[[!UICONTROL 정책]](../../classes/policy.md)**</li><li>**[[!UICONTROL 제품]](../../classes/product.md)**:<ul><li>[[!UICONTROL 제품 범주]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 카드 동작]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 사이트 검색 지원]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 예금 세부 정보]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 채널 세부 정보]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 정보]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 충성도 세부 정보]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
