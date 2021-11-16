---
title: XDM 비즈니스 계정 개인 관계 분류
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 계정 개인 관계 클래스에 대한 개요를 제공합니다.
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 계정 담당자 관계] 클래스

>[!IMPORTANT]
>
>이 클래스는 [Real-time Customer Data Platform B2B 에디션](../../../rtcdp/b2b-overview.md). 이 클래스가 참여하려면 실시간 CDP B2B Edition에 액세스할 수 있어야 합니다 [실시간 고객 프로필](../../../profile/home.md).

[!UICONTROL XDM 비즈니스 계정 담당자 관계] 는 비즈니스 계정과 연결된 사람의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다.

![](../../images/classes/b2b/business-account-person-relation.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 계정-개인 관계에서 계정에 대한 복합 식별자입니다. |
| `accountPersonKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 계정-개인 관계 엔터티에 대한 복합 식별자입니다. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 계정-개인 관계가 외부 소스 시스템에서 가져온 경우 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 계정-개인 관계에서 개인의 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 이 값은 클래스에 의해 캡처된 다른 ID 필드와 별도의 시스템 생성 값입니다. |
| `accountID` | 문자열 | 계정-개인 관계에서 계정에 대한 고유 식별자입니다. |
| `accountPersonID` | 문자열 | 계정-개인 관계 엔터티에 대한 고유 식별자입니다. |
| `currencyCode` | 문자열 | 계정과 개인 간의 관계에 사용되는 ISO 4217 통화 코드입니다. |
| `isActive` | 부울 | 계정과 개인 간의 관계가 활성화되어 있는지 여부를 나타냅니다. |
| `isDirect` | 부울 | 계정과 개인 간의 직접적인 관계인지 여부를 나타냅니다. |
| `isPrimary` | 부울 | 개인이 이 계정의 기본 담당자인지 여부를 나타냅니다. |
| `personID` | 문자열 | 계정-개인 관계에서 개인의 고유 식별자입니다. |
| `personRole` | 문자열 | 계정-개인 관계에서 개인의 역할입니다. |
| `relationEndDate` | DateTime | 계정과 개인 간의 관계가 종료된 날짜입니다. |
| `relationStartDate` | DateTime | 계정과 개인 간의 관계가 시작된 날짜입니다. |

{style=&quot;table-layout:auto&quot;}

다음 안내서를 참조하십시오. [실시간 CDP B2B Edition의 스키마 관계](../../tutorials/relationship-b2b.md) 이 클래스가 다른 B2B 클래스와 개념적으로 관련이 있는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법을 알아봅니다.
