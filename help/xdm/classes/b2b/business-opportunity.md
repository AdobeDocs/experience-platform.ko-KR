---
title: XDM 비즈니스 영업 기회 클래스
description: 경험 데이터 모델(XDM)의 XDM 비즈니스 영업 기회 클래스에 대해 알아봅니다.
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# [!UICONTROL XDM 비즈니스 영업 기회] 클래스

>[!IMPORTANT]
>
>이 클래스는 [Adobe Real-time Customer Data Platform B2B 에디션](../../../rtcdp/b2b-overview.md)에 액세스할 수 있는 조직에서 사용하기 위한 것입니다. 이 클래스가 [실시간 고객 프로필](../../../profile/home.md)에 참여하려면 Real-Time CDP B2B 에디션에 액세스할 수 있어야 합니다.

[!UICONTROL XDM 비즈니스 영업 기회]은(는) 비즈니스 영업 기회의 최소 필요 속성을 캡처하는 표준 경험 데이터 모델(XDM) 클래스입니다.

![UI에 표시되는 XDM 비즈니스 영업 기회 클래스의 구조](../../images/classes/b2b/business-opportunity.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 해당 영업 기회와 연계된 계정에 대한 복합 식별자. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 Source 시스템 감사 특성]](../../data-types/external-source-system-audit-attributes.md) | 영업 기회가 외부 소스 시스템에서 온 경우 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 영업 기회 엔터티의 복합 식별자. |
| `_id` | 문자열 | 레코드에 대한 고유 식별자. `opportunityID`과(와) 별개인 시스템 생성 값입니다. |
| `accountID` | 문자열 | 해당 영업 기회와 연계된 계정에 대한 고유 ID. |
| `isDeleted` | 부울 | Marketo Engage 시 이 마케팅 목록 엔티티가 삭제되었는지 여부를 나타냅니다.<br><br>[Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md)를 사용할 때 Marketo에서 삭제된 모든 레코드는 자동으로 실시간 고객 프로필에 반영됩니다. 그러나 이러한 프로필과 관련된 레코드가 데이터 레이크에 계속 남아 있을 수 있습니다. `isDeleted`을(를) `true`(으)로 설정하면 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필드를 사용하여 필터링할 수 있습니다. |
| `opportunityDescription` | 문자열 | 영업 기회에 대한 설명. |
| `opportunityID` | 문자열 | 영업 기회 엔터티에 대한 고유 ID입니다. |
| `opportunityName` | 문자열 | 영업 기회의 이름입니다. |
| `opportunityStage` | 문자열 | 영업 기회의 판매 단계입니다. |
| `opportunityType` | 문자열 | 영업 기회 유형. |

{style="table-layout:auto"}

이 클래스가 다른 B2B 클래스와 개념적으로 관련되는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정하는 방법에 대해 알아보려면 [Real-Time CDP B2B 에디션의 스키마 관계](../../tutorials/relationship-b2b.md)에 대한 안내서를 참조하십시오.
