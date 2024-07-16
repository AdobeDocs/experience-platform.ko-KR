---
title: 의료 산업 데이터 모델 ERD
description: 의료 산업에 대한 표준화된 데이터 모델을 설명하는 ERD(엔티티 관계 다이어그램)를 봅니다. 이 데이터 모델은 Adobe Experience Platform에서 사용하기 위해 XDM(Experience Data Model)과 호환됩니다.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# [!UICONTROL 의료 서비스] 업계 데이터 모델 ERD

다음의 엔티티 관계 다이어그램(ERD)은 헬스케어 산업에 대한 표준화된 데이터 모델을 나타낸다. ERD는 Adobe Experience Platform에서 데이터가 저장되는 방식을 고려하여 비표준화된 방식으로 의도적으로 제공됩니다.

>[!NOTE]
>
>설명된 대로 ERD는 이 업계 사용 사례에 맞게 데이터를 모델링하는 방법에 대한 권장 사항입니다. 플랫폼에서 이 데이터 모델을 사용하려면 권장 스키마와 해당 관계를 직접 구성해야 합니다. 자세한 내용은 UI에서 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) 관리에 대한 안내서를 참조하십시오.

다음 범례를 사용하여 이 ERD를 해석하십시오.

* 에 표시된 각 엔터티는 기본 [XDM(경험 데이터 모델) 클래스](../composition.md#class)를 기반으로 합니다.
* 지정된 엔터티의 경우 **bold**&#x200B;로 표시된 각 행은 필드 그룹 또는 데이터 형식을 나타내며 아래에 제공된 관련 필드가 굵게 표시되지 않은 텍스트로 표시됩니다.
* 지정된 엔티티에 대한 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 &quot;ID&quot;로 표시되며, 이러한 속성 중 하나는 &quot;기본 ID&quot;로 표시됩니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 개인이나 개인을 결정할 수 없는 경우가 많기 때문에 엔티티 관계는 종속되지 않는 것으로 표시됩니다.

![의료 산업 데이터 모델에 대한 엔터티 관계 다이어그램을 보여 주는 이미지](../../images/industries/healthcare.png)

>[!NOTE]
>
>각 엔터티에는 해당 레코드 또는 이벤트에 대한 고유한 문자열 식별자(`_id`) 특성을 나타내는 &quot;_ID&quot; 필드가 포함되어 있습니다. 이 필드는 개별 레코드 또는 이벤트의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 데이터를 조회하는 데 사용됩니다. 경우에 따라 `_id`은(는) [UUID(Universally Unique Identifier)](https://tools.ietf.org/html/rfc4122) 또는 [GUID(Globally Unique Identifier)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)일 수 있습니다.<br><br>이 필드가 개별 사용자와 관련된 ID를 나타내는 것이 아니라 데이터 기록 자체를 나타내는 것임을 구별하는 것이 중요합니다&#x200B;**.** 개인, 이벤트 또는 비즈니스 엔터티와 관련된 ID 데이터는 호환 가능한 필드 그룹이 대신 제공하는 [ID 필드](../composition.md#identity)(으)로 이동해야 합니다.

## [!UICONTROL 의료 서비스] 사용 사례

다음 표에서는 몇 가지 일반적인 의료 서비스 사용 사례에 대한 권장 클래스 및 스키마 필드 그룹을 간략하게 설명합니다.

| 활용 사례 | 권장 클래스 및 필드 그룹 |
| --- | --- |
| 보험을 구매하는 소비자 간의 디지털 획득 및 경험을 개선합니다. 해당 예는 다음과 같습니다. <ul><li>사람들이 일반 정보(플랜, 플랜 이름/계층, 메디케이드, 웰니스 프로그램 등)가 포함된 페이지에 액세스할 때 프로모션 이메일을 보내거나 광고가 있는 서드파티 플랫폼에서 타겟팅하기 위해 사용자의 행동과 찾고 있는 사항을 이해합니다.</li><li>심장 건강 및 백신 정보를 검색할 때 심장 건강에 대한 백신 관련 정보를 보내어 브랜드 인지도를 높이거나 백신 관련 일정 수립을 요청합니다.</li></ul> | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 서비스 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li><li>[!UICONTROL Plan] 클래스를 사용하는 스키마와 `planID` 특성 간에 관계 필드가 설정되었습니다.</li></ul></li><li>**[[!UICONTROL 지불인]](../../classes/payer.md)**</li><li>**[[!UICONTROL 계획]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 의료 서비스 플랜 세부 정보]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 응용 프로그램 세부 정보]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL 사이트 도구 세부 정보]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  캠페인 마케팅 세부 정보]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| 과거의 온라인 행동 및 건강 데이터를 기반으로 타겟팅 광고를 통해 환자의 디지털 습득을 늘립니다. | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 서비스 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 공급자]](../../classes/provider.md)**:<ul><li>[[!UICONTROL 의료 서비스 공급자]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 웹 세부 정보]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising 세부 정보]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 고객이 보험 회사에 대해 알게 된 방법을 이해하기 위해 다양한 채널을 통해 보험 마케팅을 추적하여 의료 플랜의 등록 및 계정 생성을 개선합니다. | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 서비스 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 지불인]](../../classes/payer.md)**</li><li>**[[!UICONTROL 계획]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 의료 서비스 플랜 세부 정보]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 웹 세부 정보]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising 세부 정보]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 의료 보험 가입의 실패를 피하십시오. | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 서비스 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 계획]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 의료 서비스 플랜 세부 정보]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| DTC(고객 직접 방문) 광고를 사용하여 공급자에게 약물 정보를 홍보합니다. | <ul><li>**[[!UICONTROL XDM 개별 프로필]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 의료 서비스 구성원 세부 정보]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 약물]](../../classes/medication.md)**:<ul><li>[[!UICONTROL 의료 의약품]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 웹 세부 정보]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising 세부 정보]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
