---
title: XDM 비즈니스 마케팅 목록 구성원 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 마케팅 목록 멤버 클래스에 대한 개요를 제공합니다.
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---

# [!UICONTROL XDM 비즈니스 마케팅 목록 ] 멤버클래스(베타)

>[!IMPORTANT]
>
>이 클래스는 현재 베타에 있는 실시간 고객 데이터 플랫폼 B2B 에디션의 일부로 사용할 수 있습니다. 설명서 및 기능은 변경될 수 있습니다.

[!UICONTROL XDM 비즈니스 마케팅 목록 ] 멤버십은 마케팅 목록과 연관된 구성원, 개인 또는 연락처를 설명하는 표준 XDM(Experience Data Model) 클래스입니다.

![](../../images/classes/b2b/business-marketing-list-members.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 마케팅 목록 구성원이 외부 소스 시스템에서 온 경우 이 개체는 해당 시스템의 감사 속성을 캡처합니다. |
| `marketingListKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 개인이 구성원으로 있는 마케팅 목록에 대한 복합 식별자입니다. |
| `marketingListMemberKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 마케팅 목록 구성원 엔터티에 대한 복합 식별자입니다. |
| `personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 마케팅 목록의 멤버인 개인에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 이 값은 `marketingListMemberID`과 별도의 시스템에서 생성한 값입니다. |
| `marketingListID` | 문자열 | 마케팅 목록에 대한 고유 ID입니다. |
| `marketingListMemberID` | 문자열 | 마케팅 목록 멤버십 엔티티의 고유 ID입니다. |
| `personId` | 문자열 | 개인의 고유 ID입니다. |

{style=&quot;table-layout:auto&quot;}

이 클래스가 다른 B2B 클래스와 개념적으로 관련되는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법에 대해 알아보려면 실시간 CDP B2B Edition](../../tutorials/relationship-b2b.md)의 스키마 관계에 대한 안내서를 참조하십시오.[
