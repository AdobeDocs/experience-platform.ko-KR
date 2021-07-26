---
solution: Experience Platform
title: 여행 및 숙박 업계 데이터 모델 ERD
topic-legacy: overview
description: Adobe Experience Platform에서 사용할 XDM(Experience Data Model)과 호환되는 여행 및 숙박 산업에 대한 표준화된 데이터 모델을 설명하는 ERD(엔티티 관계 다이어그램)를 봅니다.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 38fa2345cb87e50bd4c8788996f03939fb199cf9
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# [!UICONTROL 여행 및 ] 입원 업계 데이터 모델 ERD

다음 엔티티 관계 다이어그램(ERD)은 여행 및 숙박 산업에 대한 표준화된 데이터 모델을 나타냅니다. ERD는 Adobe Experience Platform에 데이터가 저장되는 방식을 고려하여 의도적으로 표준화된 방식으로 제공됩니다.

>[!NOTE]
>
>설명된 ERD는 이 업계 사용 사례에 대해 데이터를 모델링하는 방법에 대한 권장 사항입니다. Platform에서 이 데이터 모델을 사용하려면 권장 스키마와 관계를 직접 구성해야 합니다. 자세한 내용은 UI에서 [스키마](../../ui/resources/schemas.md) 및 [관계](../../tutorials/relationship-ui.md) 관리에 대한 안내서를 참조하십시오.

이 ERD를 해석하려면 다음 범례를 사용하십시오.

* 에 표시된 각 엔티티는 기본 [XDM(Experience Data Model) 클래스](../composition.md#class)를 기반으로 합니다.
* 지정된 엔티티의 경우 **bold**&#x200B;에 표시된 각 행은 필드 그룹 또는 데이터 유형을 나타내며, 필드 그룹은 아래에 제공되는 관련 필드가 굵게 없는 텍스트로 나열됩니다.
* 주어진 엔터티에 대해 가장 중요한 필드는 빨간색으로 강조 표시됩니다.
* 개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 다음 속성 중 하나가 &quot;기본 ID&quot;로 표시되어 있습니다.
* 쿠키 기반 이벤트는 트랜잭션을 수행한 사람이나 개인을 결정할 수 없기 때문에 엔티티 관계는 비종속적으로 표시됩니다.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>경험 이벤트 엔티티는 XDM ExperienceEvent 클래스에서 제공하는 고유 식별자(`_id`) 속성을 나타내는 &quot;_ID&quot; 필드를 포함합니다. 이 값에 대한 예상 값에 대한 자세한 내용은 [XDM ExperienceEvent](../../classes/experienceevent.md)의 참조 문서를 참조하십시오.