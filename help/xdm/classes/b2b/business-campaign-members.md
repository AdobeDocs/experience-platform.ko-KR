---
title: XDM 비즈니스 캠페인 구성원 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 캠페인 구성원 클래스에 대한 개요를 제공합니다.
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# [!UICONTROL XDM 비즈니스 캠페인 구성원] 클래스

>[!IMPORTANT]
>
>이 클래스는 [Adobe Real-time Customer Data Platform B2B 에디션](../../../rtcdp/b2b-overview.md). 이 클래스가 참여하려면 Real-Time CDP B2B Edition에 액세스할 수 있어야 합니다 [실시간 고객 프로필](../../../profile/home.md).

[!UICONTROL XDM 비즈니스 캠페인 구성원] 는 비즈니스 캠페인과 연관된 연락처 또는 리드를 설명하는 표준 XDM(Experience Data Model) 클래스입니다.

![UI에 표시되는 XDM 비즈니스 캠페인 구성원 클래스의 구조](../../images/classes/b2b/business-campaign-members.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 연결된 캠페인에 대한 복합 식별자입니다. |
| `campaignMemberKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 캠페인 멤버십 엔티티에 대한 복합 식별자입니다. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 캠페인 멤버십이 외부 소스 시스템에서 가져오는 경우 이 개체는 해당 시스템의 감사 특성을 캡처합니다. |
| `personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 연결된 캠페인의 멤버인 사람에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 시스템에서 생성한 값으로, `campaignMemberID`. |

{style=&quot;table-layout:auto&quot;}

이 클래스가 다른 B2B 클래스와 개념적으로 관련이 있는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법에 대해 알아보려면 다음 안내서를 참조하십시오. [Real-Time CDP B2B Edition의 스키마 관계](../../tutorials/relationship-b2b.md)

이 클래스와 호환되는 추가 필드에 대해서는 필드 그룹 참조를 참조하십시오 [[!UICONTROL XDM 비즈니스 캠페인 구성원 세부 정보]](../../field-groups/b2b-campaign-members/details.md).
