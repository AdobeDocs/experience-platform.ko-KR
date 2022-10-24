---
title: XDM 비즈니스 계정 개인 관계 분류
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 계정 개인 관계 클래스에 대한 개요를 제공합니다.
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# [!UICONTROL XDM 비즈니스 계정 담당자 관계] 클래스

>[!IMPORTANT]
>
>이 클래스는 [Adobe Real-time Customer Data Platform B2B 에디션](../../../rtcdp/b2b-overview.md). 이 클래스가 참여하려면 Real-Time CDP B2B Edition에 액세스할 수 있어야 합니다 [실시간 고객 프로필](../../../profile/home.md).

[!UICONTROL XDM 비즈니스 계정 담당자 관계] 는 비즈니스 계정과 연결된 사람의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다.

![UI에 표시되는 XDM 비즈니스 계정 개인 관계 클래스의 구조](../../images/classes/b2b/business-account-person-relation.png)

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
| `isDeleted` | 부울 | 이 계정-개인 관계가 Marketo Engage에서 삭제되었는지 여부를 나타냅니다.<br><br>를 사용할 때 [Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md)를 입력하면 Marketo에서 삭제된 모든 레코드가 실시간 고객 프로필에 자동으로 반영됩니다. 그러나 이러한 프로필과 관련된 레코드는 여전히 Data Lake에서 유지됩니다. 설정 `isDeleted` to `true`, 필드를 사용하여 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필터링할 수 있습니다. |
| `isDirect` | 부울 | 계정과 개인 간의 직접적인 관계인지 여부를 나타냅니다. |
| `isPrimary` | 부울 | 개인이 이 계정의 기본 담당자인지 여부를 나타냅니다. |
| `personID` | 문자열 | 계정-개인 관계에서 개인의 고유 식별자입니다. |
| `personRoles` | 문자열 배열 | 계정-개인 관계에서 개인의 역할을 나열합니다. |
| `relationEndDate` | DateTime | 계정과 개인 간의 관계가 종료된 날짜입니다. |
| `relationStartDate` | DateTime | 계정과 개인 간의 관계가 시작된 날짜입니다. |
| `relationshipSource` | 문자열 | 계정 담당자 관계의 출처. |

{style=&quot;table-layout:auto&quot;}

다음 안내서를 참조하십시오. [Real-Time CDP B2B Edition의 스키마 관계](../../tutorials/relationship-b2b.md) 이 클래스가 다른 B2B 클래스와 개념적으로 관련이 있는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법을 알아봅니다.
