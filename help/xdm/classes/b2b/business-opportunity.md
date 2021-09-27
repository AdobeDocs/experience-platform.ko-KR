---
title: XDM 비즈니스 기회 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 기회 클래스에 대한 개요를 제공합니다.
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 ] 기회 클래스

>[!NOTE]
>
>이 클래스는 실시간 고객 데이터 플랫폼 B2B 버전에 액세스할 수 있는 조직에서만 사용할 수 있습니다.

[!UICONTROL XDM Business ] Opportunity 는 비즈니스 기회의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다.

![](../../images/classes/b2b/business-opportunity.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 이 영업 기회와 연관된 계정의 복합 식별자입니다. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 외부 소스 시스템에서 기회가 발생하면 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `opportunityKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 영업 기회 엔터티에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 이 값은 `opportunityID`과 별도의 시스템에서 생성한 값입니다. |
| `accountID` | 문자열 | 이 영업 기회가 연관된 계정의 고유 ID입니다. |
| `opportunityDescription` | 문자열 | 기회에 대한 설명입니다. |
| `opportunityID` | 문자열 | 영업 기회 엔티티에 대한 고유 ID입니다. |
| `opportunityName` | 문자열 | 영업 기회의 이름입니다. |
| `opportunityStage` | 문자열 | 영업 기회의 영업 단계입니다. |
| `opportunityType` | 문자열 | 기회 유형입니다. |

이 클래스가 다른 B2B 클래스와 개념적으로 관련되는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법에 대해 알아보려면 실시간 CDP B2B Edition](../../tutorials/relationship-b2b.md)의 스키마 관계에 대한 안내서를 참조하십시오.[
