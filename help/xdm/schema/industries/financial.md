---
solution: Experience Platform
title: 금융 서비스 업계 데이터 모델 ERD
description: 은행, 금융 서비스 및 보험(BFSI) 산업에 대한 표준화된 데이터 모델을 설명하는 ERD(엔티티 관계 다이어그램)를 봅니다. 이 데이터 모델은 Adobe Experience Platform에서 사용할 Experience Data Model(XDM)과 호환됩니다.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# [!UICONTROL 금융 서비스] 업계 데이터 모델 ERD

다음 엔티티 관계 다이어그램(ERD)은 은행, 금융 서비스 및 보험(BFSI) 산업에 대한 표준화된 데이터 모델을 나타냅니다. ERD는 Adobe Experience Platform에 데이터가 저장되는 방식을 고려하여 의도적으로 표준화된 방식으로 제공됩니다.

>[!NOTE]
>
>설명된 ERD는 이 업계 사용 사례에 대해 데이터를 모델링하는 방법에 대한 권장 사항입니다. Platform에서 이 데이터 모델을 사용하려면 권장 스키마와 관계를 직접 구성해야 합니다. 관리에 대한 안내서를 참조하십시오 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) ( UI에서)를 참조하십시오.

이 ERD를 해석하려면 다음 범례를 사용하십시오.

* 에 표시된 각 엔티티는 기본 [XDM(경험 데이터 모델) 클래스](../composition.md#class).
* 지정된 엔티티의 경우 각 행이 **굵게** 는 필드 그룹 또는 데이터 유형을 나타내며, 이 필드가 제공하는 관련 필드는 번역되지 않은 텍스트로 나열됩니다.
* 주어진 엔터티에 대해 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 다음 속성 중 하나가 &quot;기본 ID&quot;로 표시되어 있습니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 사람이나 개인을 결정할 수 없기 때문에 엔티티 관계는 비종속적으로 표시됩니다.

![](../../images/industries/financial.png)

>[!NOTE]
>
>경험 이벤트 엔티티에는 고유 식별자(`_id`) 속성 을 사용할 수 있습니다. 다음에서 참조 문서를 참조하십시오. [XDM ExperienceEvent](../../classes/experienceevent.md) 를 참조하십시오.

## [!UICONTROL 금융 서비스] 사용 사례

다음 표에서는 여러 가지 일반적인 금융 사용 사례에 대해 권장되는 클래스 및 스키마 필드 그룹에 대해 설명합니다.

| 사용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 옴니 채널 보고 인사이트를 살펴보고 여정을 자동화하여 선호하는 보상 프로그램으로 등록률을 높일 수 있으므로 기본 세그먼트를 위한 규모에 맞게 개인화를 수행할 수 있습니다. | <ul><li>**[[!UICONTROL 제품]](../../classes/product.md)**:<ul><li>[[!UICONTROL 제품 카테고리]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 카드 작업]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 견적 요청 세부 정보]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 예금 상세내역]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 채널 세부 사항]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 잔액 이전]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 세부 정보]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 충성도 세부 사항]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 온라인 및 오프라인 채널에서 교차 채널 개인화를 최적화합니다. | <ul><li>**[[!UICONTROL 제품]](../../classes/product.md)**:<ul><li>[[!UICONTROL 제품 카테고리]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 채널 세부 사항]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 세부 정보]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 충성도 세부 사항]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 크로스 채널 행동 분석에서 얻은 통찰력을 사용하여 새로운 제품 오퍼를 생성할 수 있는 제품 사용 패턴을 식별하여 새로운 매출 기회를 창출합니다. | <ul><li>**[[!UICONTROL 정책]](../../classes/policy.md)**</li><li>**[[!UICONTROL 제품]](../../classes/product.md)**:<ul><li>[[!UICONTROL 제품 카테고리]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 카드 작업]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 사이트 검색 지원]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 예금 상세내역]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 채널 세부 사항]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 세부 정보]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 충성도 세부 사항]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
