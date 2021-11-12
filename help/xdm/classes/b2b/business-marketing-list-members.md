---
title: XDM 비즈니스 마케팅 목록 구성원 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 마케팅 목록 멤버 클래스에 대한 개요를 제공합니다.
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 마케팅 목록 구성원] 클래스

[!UICONTROL XDM 비즈니스 마케팅 목록 구성원] 는 마케팅 목록과 연관된 구성원, 개인 또는 연락처를 설명하는 표준 XDM(Experience Data Model) 클래스입니다.

![](../../images/classes/b2b/business-marketing-list-members.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 마케팅 목록 구성원이 외부 소스 시스템에서 온 경우 이 개체는 해당 시스템의 감사 속성을 캡처합니다. |
| `marketingListKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 개인이 구성원으로 있는 마케팅 목록에 대한 복합 식별자입니다. |
| `marketingListMemberKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 마케팅 목록 구성원 엔터티에 대한 복합 식별자입니다. |
| `personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 마케팅 목록의 멤버인 개인에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 시스템에서 생성한 값으로, `marketingListMemberID`. |
| `marketingListID` | 문자열 | 마케팅 목록에 대한 고유 ID입니다. |
| `marketingListMemberID` | 문자열 | 마케팅 목록 멤버십 엔티티의 고유 ID입니다. |
| `personId` | 문자열 | 개인의 고유 ID입니다. |

{style=&quot;table-layout:auto&quot;}

다음 안내서를 참조하십시오. [실시간 CDP B2B Edition의 스키마 관계](../../tutorials/relationship-b2b.md) 이 클래스가 다른 B2B 클래스와 개념적으로 관련이 있는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법을 알아봅니다.
