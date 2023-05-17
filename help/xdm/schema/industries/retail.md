---
solution: Experience Platform
title: 소매 업계 데이터 모델
description: Adobe Experience Platform에서 사용할 XDM(Experience Data Model) 과 호환되는 소매 업계를 위한 표준화된 데이터 모델을 봅니다.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 4%

---

# [!UICONTROL 소매] 업계 데이터 모델

다음 엔티티 관계 다이어그램(ERD)은 소매 산업에 대한 표준화된 데이터 모델을 나타냅니다. ERD는 Adobe Experience Platform에 데이터가 저장되는 방식을 고려하여 의도적으로 표준화된 방식으로 제공됩니다.

>[!NOTE]
>
>설명된 ERD는 이 업계 사용 사례에 대해 데이터를 모델링하는 방법에 대한 권장 사항입니다. Platform에서 이 데이터 모델을 사용하려면 권장 스키마와 관계를 직접 구성해야 합니다. 관리에 대한 안내서를 참조하십시오 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) ( UI에서)를 참조하십시오.

이 ERD를 해석하려면 다음 범례를 사용하십시오.

* 에 표시된 각 엔티티는 기본 [XDM(경험 데이터 모델) 클래스](../composition.md#class).
* 지정된 엔티티의 경우 각 행이 **굵게** 는 필드 그룹 또는 데이터 유형을 나타내며, 이 필드가 제공하는 관련 필드는 번역되지 않은 텍스트로 나열됩니다.
* 주어진 엔터티에 대해 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 다음 속성 중 하나가 &quot;기본 ID&quot;로 표시되어 있습니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 사람이나 개인을 결정할 수 없기 때문에 엔티티 관계는 비종속적으로 표시됩니다.

![](../../images/industries/retail.png)

>[!NOTE]
>
>경험 이벤트 엔티티에는 고유 식별자(`_id`) 속성 을 사용할 수 있습니다. 다음에서 참조 문서를 참조하십시오. [XDM ExperienceEvent](../../classes/experienceevent.md) 를 참조하십시오.

## [!UICONTROL 소매] 사용 사례

다음 표에서는 일반적인 몇 가지 소매 사용 사례에 대해 권장되는 클래스 및 스키마 필드 그룹에 대해 설명합니다.

| 사용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 온라인 및 오프라인 데이터 소스를 결합하고 교차 장치 및 온라인/오프라인 ID를 확인하여 전체적인 크로스 채널 및 교차 장치 속성 보고를 제공합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[상거래 세부 사항](../../field-groups/event/commerce-details.md)</li><li>[웹 세부 사항](../../field-groups/event/web-details.md)</li></ul></li><li>**[제품](../../classes/product.md)**:<ul><li>[제품 카탈로그](../../field-groups/product/product-catalog.md)</li><li>[제품 카테고리](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 다양한 세그먼트를 위한 타겟팅되고 개인화된 경험을 제공하여 매출을 늘리고 옴니채널 오케스트레이션의 플랫폼을 강화하는 데 도움이 됩니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[캠페인 마케팅 세부 사항](../../field-groups/event/campaign-marketing-details.md)</li><li>[채널 세부 사항](../../field-groups/event/channel-details.md)</li><li>[상거래 세부 사항](../../field-groups/event/commerce-details.md)</li><li>[환경 세부 정보](../../field-groups/event/environment-details.md)</li><li>[웹 세부 사항](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 세부 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[작업 연락처 세부 정보](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 다중 터치 속성을 분석하여 마케팅 효율성을 개선합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[캠페인 마케팅 세부 사항](../../field-groups/event/campaign-marketing-details.md)</li><li>[채널 세부 사항](../../field-groups/event/channel-details.md)</li><li>[상거래 세부 사항](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| 개선된 남성과 여성의 세분화를 통해 이메일 관련성을 개선합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[상거래 세부 사항](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[제품](../../classes/product.md)**:<ul><li>[제품 카탈로그](../../field-groups/product/product-catalog.md)</li><li>[제품 카테고리](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 충성도(파트너) 데이터를 수집하여 웹, 이메일 및 디지털 마케팅 채널에서 관련 제품 정보를 증가시킵니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[웹 세부 사항](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[충성도 세부 사항](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[제품](../../classes/product.md)**:<ul><li>[제품 카탈로그](../../field-groups/product/product-catalog.md)</li><li>[제품 카테고리](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 자동화된 개인화된 이메일을 통해 장바구니 포기 고객을 재타깃팅합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[상거래 세부 사항](../../field-groups/event/commerce-details.md)</li><li>[웹 세부 사항](../../field-groups/event/web-details.md)</li></ul></li><li>**[제품](../../classes/product.md)**:<ul><li>[제품 카탈로그](../../field-groups/product/product-catalog.md)</li><li>[제품 카테고리](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
