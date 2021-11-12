---
title: XDM 비즈니스 캠페인 구성원 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 캠페인 구성원 클래스에 대한 개요를 제공합니다.
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 캠페인 구성원] 클래스

[!UICONTROL XDM 비즈니스 캠페인 구성원] 는 비즈니스 캠페인과 연관된 연락처 또는 리드를 설명하는 표준 XDM(Experience Data Model) 클래스입니다.

![](../../images/classes/b2b/business-campaign-members.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 연결된 캠페인에 대한 복합 식별자입니다. |
| `campaignMemberKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 캠페인 멤버십 엔티티에 대한 복합 식별자입니다. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 캠페인 멤버십이 외부 소스 시스템에서 가져오는 경우 이 개체는 해당 시스템의 감사 특성을 캡처합니다. |
| `personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 연결된 캠페인의 멤버인 사람에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 시스템에서 생성한 값으로, `campaignMemberID`. |
| `campaignID` | 문자열 | 연결된 캠페인에 대한 고유 ID입니다. |
| `campaignMemberID` | 문자열 | 캠페인 멤버십 엔티티에 대한 고유 ID입니다. |
| `personId` | 문자열 | 연결된 캠페인의 멤버인 사람의 고유 ID입니다. |

{style=&quot;table-layout:auto&quot;}

다음 안내서를 참조하십시오. [실시간 CDP B2B Edition의 스키마 관계](../../tutorials/relationship-b2b.md) 이 클래스가 다른 B2B 클래스와 개념적으로 관련이 있는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법을 알아봅니다.
