---
solution: Experience Platform
title: 소매 업계 데이터 모델
description: Adobe Experience Platform에서 사용할 XDM(Experience Data Model)과 호환되는 소매 업계에 대한 표준화된 데이터 모델을 봅니다.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# [!UICONTROL 소매] 산업 데이터 모델

다음의 엔티티 관계 다이어그램(ERD)은 소매 산업에 대한 표준화된 데이터 모델을 나타냅니다. ERD는 Adobe Experience Platform에서 데이터가 저장되는 방식을 고려하여 비표준화된 방식으로 의도적으로 제공됩니다.

>[!NOTE]
>
>설명된 대로 ERD는 이 업계 사용 사례에 맞게 데이터를 모델링하는 방법에 대한 권장 사항입니다. 플랫폼에서 이 데이터 모델을 사용하려면 권장 스키마와 해당 관계를 직접 구성해야 합니다. 관리에 대한 가이드 보기 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) 을 참조하십시오.

다음 범례를 사용하여 이 ERD를 해석하십시오.

* 에 표시된 각 엔티티는 기본 엔티티를 기반으로 합니다 [XDM(경험 데이터 모델) 클래스](../composition.md#class).
* 주어진 엔티티에 대해 각 행이 표시됨 **굵게** 필드 그룹 또는 데이터 형식을 나타내며 아래에 굵게 표시되지 않은 텍스트로 제공된 관련 필드가 있습니다.
* 지정된 엔티티에 대한 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 &quot;ID&quot;로 표시되며, 이러한 속성 중 하나는 &quot;기본 ID&quot;로 표시됩니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 개인이나 개인을 결정할 수 없는 경우가 많기 때문에 엔티티 관계는 종속되지 않는 것으로 표시됩니다.

![](../../images/industries/retail.png)

>[!NOTE]
>
>Experience Event 엔티티는 고유 식별자 ( )를 나타내는 &quot;_ID&quot; 필드를 포함합니다.`_id`) XDM ExperienceEvent 클래스에서 제공하는 속성입니다. 다음에서 참조 문서 보기: [XDM ExperienceEvent](../../classes/experienceevent.md) 이 값에 대해 예상되는 사항에 대한 자세한 내용.

## [!UICONTROL 소매] 사용 사례

다음 표에서는 몇 가지 일반적인 소매 사용 사례에 대한 권장 클래스 및 스키마 필드 그룹을 간략하게 설명합니다.

| 사용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 온라인 및 오프라인 데이터 소스를 결합하고 크로스 디바이스 및 온라인/오프라인 ID를 확인하여 전체적인 크로스 채널 및 크로스 디바이스 속성 보고를 제공합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[상거래 세부 정보](../../field-groups/event/commerce-details.md)</li><li>[웹 세부 정보](../../field-groups/event/web-details.md)</li></ul></li><li>**[제품](../../classes/product.md)**:<ul><li>[제품 카탈로그](../../field-groups/product/product-catalog.md)</li><li>[제품 범주](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 다양한 세그먼트에 대한 타겟팅되고 개인화된 경험을 제공하여 매출을 증가시키고 옴니채널 오케스트레이션의 플랫폼을 강화하는 데 도움이 됩니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[캠페인 마케팅 세부 정보](../../field-groups/event/campaign-marketing-details.md)</li><li>[채널 세부 사항](../../field-groups/event/channel-details.md)</li><li>[상거래 세부 정보](../../field-groups/event/commerce-details.md)</li><li>[환경 세부 정보](../../field-groups/event/environment-details.md)</li><li>[웹 세부 정보](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[개인 연락처 세부 정보](../../field-groups/profile/personal-contact-details.md)</li><li>[회사 연락처 세부 정보](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 멀티 터치 속성을 분석하여 마케팅 효율성을 개선합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[캠페인 마케팅 세부 정보](../../field-groups/event/campaign-marketing-details.md)</li><li>[채널 세부 사항](../../field-groups/event/channel-details.md)</li><li>[상거래 세부 정보](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| 개선된 남녀 세분화를 통해 이메일 관련성을 개선합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[상거래 세부 정보](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[제품](../../classes/product.md)**:<ul><li>[제품 카탈로그](../../field-groups/product/product-catalog.md)</li><li>[제품 범주](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 충성도(파트너) 데이터를 수집하여 웹, 이메일 및 디지털 마케팅 채널 전반에서 관련 제품 정보를 증가시킵니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[웹 세부 정보](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM 개별 프로필](../../classes/individual-profile.md)**:<ul><li>[인구 통계 세부 정보](../../field-groups/profile/demographic-details.md)</li><li>[고객 충성도 세부 정보](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[제품](../../classes/product.md)**:<ul><li>[제품 카탈로그](../../field-groups/product/product-catalog.md)</li><li>[제품 범주](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 자동화된 개인화된 이메일을 통해 장바구니 포기를 재타겟팅합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[상거래 세부 정보](../../field-groups/event/commerce-details.md)</li><li>[웹 세부 정보](../../field-groups/event/web-details.md)</li></ul></li><li>**[제품](../../classes/product.md)**:<ul><li>[제품 카탈로그](../../field-groups/product/product-catalog.md)</li><li>[제품 범주](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}

*\*표준 제품 클래스는 향후 릴리스에 사용될 예정이지만 제품 스키마는 현재 사용자 지정 클래스를 사용하여 빌드되어야 합니다. 따라서 추가한 필드 그룹의 구조뿐만 아니라 스키마 클래스의 구조도 수동으로 빌드해야 합니다. 의 섹션을 참조하십시오. [사용자 정의 클래스 만들기](../../ui/resources/classes.md#create) 자세한 내용은 XDM UI 안내서 를 참조하십시오.*
