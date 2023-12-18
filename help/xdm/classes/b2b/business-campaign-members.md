---
title: XDM 비즈니스 캠페인 멤버 클래스
description: 경험 데이터 모델(XDM)의 XDM 비즈니스 캠페인 멤버 클래스에 대해 알아봅니다.
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# [!UICONTROL XDM 비즈니스 캠페인 멤버] 클래스

>[!IMPORTANT]
>
>이 클래스는 다음에 액세스할 수 있는 조직에서 사용하기 위한 것입니다. [Adobe Real-time Customer Data Platform 에디션](../../../rtcdp/b2b-overview.md). 이 클래스가 참여하려면 Real-Time CDP B2B 에디션에 대한 액세스 권한이 있어야 합니다. [실시간 고객 프로필](../../../profile/home.md).

[!UICONTROL XDM 비즈니스 캠페인 멤버] 는 비즈니스 캠페인과 관련된 연락처 또는 잠재 고객을 설명하는 표준 경험 데이터 모델(XDM) 클래스입니다.

![UI에 표시되는 XDM 비즈니스 캠페인 멤버 클래스의 구조](../../images/classes/b2b/business-campaign-members.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 연계된 캠페인에 대한 복합 식별자. |
| `campaignMemberKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 캠페인 멤버십 엔티티에 대한 복합 식별자. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 캠페인 멤버십이 외부 소스 시스템에서 온 경우 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 연결된 캠페인의 멤버인 사용자에 대한 복합 식별자. |
| `_id` | 문자열 | 레코드에 대한 고유 식별자. 이 값은 와 별도인 시스템 생성 값입니다. `campaignMemberID`. |

{style="table-layout:auto"}

이 클래스가 다른 B2B 클래스와 개념적으로 관련되는 방법 및 Adobe Experience Platform UI에서 이러한 관계를 설정하는 방법에 대해 알아보려면 의 안내서를 참조하십시오. [Real-Time CDP B2B 에디션의 스키마 관계](../../tutorials/relationship-b2b.md)

이 클래스와 호환되는 추가 필드는 의 필드 그룹 참조를 참조하십시오. [[!UICONTROL XDM 비즈니스 캠페인 멤버 세부 정보]](../../field-groups/b2b-campaign-members/details.md).
