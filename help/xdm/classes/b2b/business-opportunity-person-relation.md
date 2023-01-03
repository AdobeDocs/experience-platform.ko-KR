---
title: XDM 비즈니스 기회 개인 관계 분류
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 기회 개인 관계 클래스에 대한 개요를 제공합니다.
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 3%

---

# [!UICONTROL XDM 비즈니스 기회 개인 관계] 클래스

>[!IMPORTANT]
>
>이 클래스는 [Adobe Real-time Customer Data Platform B2B 에디션](../../../rtcdp/b2b-overview.md). 이 클래스가 참여하려면 Real-Time CDP B2B Edition에 액세스할 수 있어야 합니다 [실시간 고객 프로필](../../../profile/home.md).

[!UICONTROL XDM 비즈니스 기회 개인 관계] 는 비즈니스 기회에 연관된 사람의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다.

![UI에 표시되는 XDM Business Opportunity Person 클래스의 구조](../../images/classes/b2b/business-opportunity-person-relation.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 업무 담당자 관계가 외부 소스 시스템에서 생성된 경우 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `opportunityKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 기회-개인 관계에서 기회에 대한 복합 식별자입니다. |
| `opportunityPersonKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 기회-개인 관계 엔터티에 대한 복합 식별자입니다. |
| `personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 기회-개인 관계에 있는 개인에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 이 값은 클래스에 의해 캡처된 다른 ID 필드와 별도의 시스템 생성 값입니다. |
| `isDeleted` | 부울 | 이 마케팅 목록 엔터티가 Marketo Engage에서 삭제되었는지 여부를 나타냅니다.<br><br>를 사용할 때 [Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md)를 입력하면 Marketo에서 삭제된 모든 레코드가 실시간 고객 프로필에 자동으로 반영됩니다. 그러나 이러한 프로필과 관련된 레코드는 여전히 Data Lake에서 유지됩니다. 설정 `isDeleted` to `true`, 필드를 사용하여 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필터링할 수 있습니다. |
| `isPrimary` | 부울 | 개인이 이 기회에 대한 주요 담당자인지 여부를 나타냅니다. |
| `opportunityID` | 문자열 | 기회-개인 관계에서 기회에 대한 고유 식별자입니다. |
| `opportunityPersonID` | 문자열 | 영업 기회-개인 관계 엔터티에 대한 고유 식별자입니다 |
| `personID` | 문자열 | 기회-개인 관계에 있는 사람에 대한 고유 식별자입니다. |
| `personRole` | 문자열 | 기회-개인 관계에서 개인의 역할입니다. |

{style=&quot;table-layout:auto&quot;}

다음 안내서를 참조하십시오. [Real-Time CDP B2B Edition의 스키마 관계](../../tutorials/relationship-b2b.md) 이 클래스가 다른 B2B 클래스와 개념적으로 관련이 있는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법을 알아봅니다.
