---
title: 의료 업계 데이터 모델 ERD
description: 의료 산업에 대한 표준화된 데이터 모델을 설명하는 ERD(엔티티 관계 다이어그램)를 봅니다. 이 데이터 모델은 Adobe Experience Platform에서 사용할 Experience Data Model(XDM)과 호환됩니다.
source-git-commit: 721059a87347e371228d00edeac141afa894af47
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 1%

---

# [!UICONTROL 의료] 업계 데이터 모델 ERD

다음 엔티티 관계 다이어그램(ERD)은 의료 산업에 대한 표준화된 데이터 모델을 나타냅니다. ERD는 Adobe Experience Platform에 데이터가 저장되는 방식을 고려하여 의도적으로 표준화된 방식으로 제공됩니다.

>[!NOTE]
>
>설명된 ERD는 이 업계 사용 사례에 대해 데이터를 모델링하는 방법에 대한 권장 사항입니다. Platform에서 이 데이터 모델을 사용하려면 권장 스키마와 관계를 직접 구성해야 합니다. 관리에 대한 안내서를 참조하십시오 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) ( UI에서)를 참조하십시오.

이 ERD를 해석하려면 다음 범례를 사용하십시오.

* 에 표시된 각 엔티티는 기본 [XDM(경험 데이터 모델) 클래스](../composition.md#class).
* 지정된 엔티티의 경우 각 행이 **굵게** 는 필드 그룹 또는 데이터 유형을 나타내며, 이 필드가 제공하는 관련 필드는 번역되지 않은 텍스트로 나열됩니다.
* 주어진 엔터티에 대해 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 다음 속성 중 하나가 &quot;기본 ID&quot;로 표시되어 있습니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 사람이나 개인을 결정할 수 없기 때문에 엔티티 관계는 비종속적으로 표시됩니다.

![의료 업계 데이터 모델의 엔티티 관계 다이어그램을 보여주는 이미지](../../images/industries/healthcare.png)

>[!NOTE]
>
>각 엔티티에는 고유한 문자열 식별자(`_id`) 속성을 사용하여 해당 레코드 또는 이벤트에 대한 값을 지정합니다. 이 필드는 개별 레코드나 이벤트의 고유성을 추적하고 데이터의 중복을 방지하며 다운스트림 서비스에서 해당 데이터를 찾는 데 사용됩니다. 어떤 경우에는 `_id` 다음을 수행할 수 있습니다. [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) 또는 [GUID(Globally Unique Identifier)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>그것을 구분하는 것은 중요하다 **이 필드는 개별 사용자와 관련된 ID를 나타내지 않습니다**&#x200B;하지만, 오히려 데이터 자체의 기록입니다. 개인, 이벤트 또는 사업자와 관련된 ID는 [id 필드](../composition.md#identity) 호환 필드 그룹에서 대신 제공합니다.

## [!UICONTROL 의료] 사용 사례

다음 표에서는 여러 가지 일반적인 의료 사용 사례에 대해 권장되는 클래스 및 스키마 필드 그룹에 대해 설명합니다.

| 사용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 보험을 구입하는 소비자의 디지털 획득 및 경험을 개선합니다. 해당 예는 다음과 같습니다. <ul><li>사람들이 일반 정보(예: 계획, 계획 이름/계층, 메디케이드, 웰빙 프로그램 등)가 포함된 페이지에 액세스할 때 홍보 이메일을 전송하거나 광고를 통해 타사 플랫폼에서 해당 페이지를 타겟팅하기 위해 해당 페이지의 행동과 콘텐츠를 파악합니다.</li><li>사람들이 심장 건강과 백신 정보를 검색할 때, 심장 건강에 대한 백신 관련 정보를 그들에게 보내 브랜드 인식을 창출하거나 백신을 예약하도록 요청하세요.</li></ul> | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li><li>사이에 관계 필드가 설정되어 있습니다. `planID` 를 사용하는 속성 및 스키마 [!UICONTROL 계획] 클래스 이름을 지정합니다.</li></ul></li><li>**[[!UICONTROL 지급인]](../../classes/payer.md)**</li><li>**[[!UICONTROL 계획]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 의료 계획 세부 정보]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 애플리케이션 세부 정보]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Sitetool 세부 정보]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  캠페인 마케팅 세부 사항]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| 과거의 온라인 행동 및 건강 데이터를 기반으로 타겟팅된 광고를 통해 환자의 디지털 고객 확보를 늘립니다. | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 공급자]](../../classes/provider.md)**:<ul><li>[[!UICONTROL 의료 기관]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 웹 세부 사항]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 광고 세부 사항]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 고객이 보험 회사에 대해 어떻게 알게 되었는지 이해하기 위해 다양한 채널을 통해 보험 마케팅을 추적하여 건강 보험 제도의 등록 및 계정 생성을 개선합니다. | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 지급인]](../../classes/payer.md)**</li><li>**[[!UICONTROL 계획]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 의료 계획 세부 정보]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 웹 세부 사항]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 광고 세부 사항]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 의료 보험 혜택의 낭비를 피하세요. | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 계획]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 의료 계획 세부 정보]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| DTC(Direct-to-Customer) 광고를 사용하여 공급자로 의약품 정보를 홍보합니다. | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 약물]](../../classes/medication.md)**:<ul><li>[[!UICONTROL 의료용 약물]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 웹 세부 사항]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 광고 세부 사항]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
