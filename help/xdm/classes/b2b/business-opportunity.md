---
title: XDM 비즈니스 기회 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 기회 클래스에 대한 개요를 제공합니다.
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 기회] 클래스

>[!IMPORTANT]
>
>이 클래스는 [Adobe Real-time Customer Data Platform B2B 에디션](../../../rtcdp/b2b-overview.md). 이 클래스가 참여하려면 Real-Time CDP B2B Edition에 액세스할 수 있어야 합니다 [실시간 고객 프로필](../../../profile/home.md).

[!UICONTROL XDM 비즈니스 기회] 는 비즈니스 기회의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다.

![UI에 표시되는 XDM 비즈니스 기회 클래스의 구조](../../images/classes/b2b/business-opportunity.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 이 영업 기회와 연관된 계정의 복합 식별자입니다. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 외부 소스 시스템에서 기회가 발생하면 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `opportunityKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 영업 기회 엔터티에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 시스템에서 생성한 값으로, `opportunityID`. |
| `accountID` | 문자열 | 이 영업 기회가 연관된 계정의 고유 ID입니다. |
| `isDeleted` | 부울 | 이 마케팅 목록 엔터티가 Marketo Engage에서 삭제되었는지 여부를 나타냅니다.<br><br>를 사용할 때 [Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md)를 입력하면 Marketo에서 삭제된 모든 레코드가 실시간 고객 프로필에 자동으로 반영됩니다. 그러나 이러한 프로필과 관련된 레코드는 여전히 Data Lake에서 유지됩니다. 설정 `isDeleted` to `true`, 필드를 사용하여 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필터링할 수 있습니다. |
| `opportunityDescription` | 문자열 | 기회에 대한 설명입니다. |
| `opportunityID` | 문자열 | 영업 기회 엔티티에 대한 고유 ID입니다. |
| `opportunityName` | 문자열 | 영업 기회의 이름입니다. |
| `opportunityStage` | 문자열 | 영업 기회의 영업 단계입니다. |
| `opportunityType` | 문자열 | 기회 유형입니다. |

{style=&quot;table-layout:auto&quot;}

다음 안내서를 참조하십시오. [Real-Time CDP B2B Edition의 스키마 관계](../../tutorials/relationship-b2b.md) 이 클래스가 다른 B2B 클래스와 개념적으로 관련이 있는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법을 알아봅니다.
