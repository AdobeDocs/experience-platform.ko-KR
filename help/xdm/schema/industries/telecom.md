---
solution: Experience Platform
title: 통신 산업 데이터 모델 ERD
description: Adobe Experience Platform에서 사용할 XDM(경험 데이터 모델)과 호환되는 통신 업계에 대한 표준화된 데이터 모델을 설명하는 ERD(엔티티 관계 다이어그램)를 봅니다.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!UICONTROL 통신] 산업 데이터 모델 ERD

다음의 엔티티 관계도(ERD)는 통신산업에 대한 표준화된 데이터 모델을 나타낸다. ERD는 Adobe Experience Platform에서 데이터가 저장되는 방식을 고려하여 비표준화된 방식으로 의도적으로 제공됩니다.

>[!NOTE]
>
>설명된 대로 ERD는 이 업계 사용 사례에 맞게 데이터를 모델링하는 방법에 대한 권장 사항입니다. Experience Platform에서 이 데이터 모델을 사용하려면 권장 스키마와 해당 관계를 직접 구성해야 합니다. 자세한 내용은 UI에서 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) 관리에 대한 안내서를 참조하십시오.

다음 범례를 사용하여 이 ERD를 해석하십시오.

* 에 표시된 각 엔터티는 기본 [XDM(경험 데이터 모델) 클래스](../composition.md#class)를 기반으로 합니다.
* 상위 필드 아래에 들여쓴 필드는 상위 필드 그룹에 속하는 하위 필드 또는 하위 필드를 나타냅니다.
* 지정된 엔티티에 대한 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 &quot;ID&quot;로 표시되며, 이러한 속성 중 하나는 &quot;기본 ID&quot;로 표시됩니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 개인이나 개인을 결정할 수 없는 경우가 많기 때문에 엔티티 관계는 종속되지 않는 것으로 표시됩니다.


![통신 산업 데이터 모델에 대한 ERD 예](../../images/industries/telecom.png)

>[!NOTE]
>
>Experience Event 엔티티는 XDM ExperienceEvent 클래스에서 제공하는 고유 식별자(`_id`) 특성을 나타내는 &quot;_ID&quot; 필드를 포함합니다. 이 값에 필요한 사항에 대한 자세한 내용은 [XDM ExperienceEvent](../../classes/experienceevent.md)에 대한 참조 문서를 참조하십시오.

## [!UICONTROL 통신] 사용 사례

다음 표에서는 통신 산업을 위한 몇 가지 일반적인 사용 사례에 대한 권장 클래스 및 스키마 필드 그룹을 간략하게 설명합니다.

| 활용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 현재 보유 주식과 탐색 행동을 기반으로 업셀 또는 크로스셀 기회에 적합한 후보인 고객을 파악합니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 업셀 세부 정보]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL 업그레이드 세부 정보]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 통신 구독]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 정보]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 관련 광고 및 자동화된 개인화된 이메일을 통해 장바구니 포기를 재타겟팅합니다. 변환할 때 광고를 표시하지 않습니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Commerce 세부 정보]](../../field-groups/event/upsell-details.md)(장바구니 포기 캡처)</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 통신 구독]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 정보]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 고객이 이탈할 가능성이 있는 것으로 표시되면(직원 상호 작용 또는 자동화된 머신 러닝 알고리즘 기반) 고객 세부 정보를 디지털 및 비디지털 채널로 보냅니다. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 캠페인 마케팅 세부 정보]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL 채널 세부 정보]](../../field-groups/event/channel-details.md)</li><li>개인화된 콘텐츠가 포함된 사용자 정의 필드 그룹</li></ul></li><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 인구 통계 세부 정보]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 개인 연락처 정보]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
