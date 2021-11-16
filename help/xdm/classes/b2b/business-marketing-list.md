---
title: XDM 비즈니스 마케팅 목록 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 마케팅 목록 클래스에 대한 개요를 제공합니다.
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 마케팅 목록] 클래스

>[!IMPORTANT]
>
>이 클래스는 [Real-time Customer Data Platform B2B 에디션](../../../rtcdp/b2b-overview.md). 이 클래스가 참여하려면 실시간 CDP B2B Edition에 액세스할 수 있어야 합니다 [실시간 고객 프로필](../../../profile/home.md).

[!UICONTROL XDM 비즈니스 마케팅 목록] 는 마케팅 목록의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다. 마케팅 목록을 사용하면 제품을 구매할 가능성이 가장 큰 잠재 고객을 우선 순위로 지정할 수 있습니다.

![](../../images/classes/b2b/business-marketing-list.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 마케팅 목록이 외부 소스 시스템에서 나온 경우 이 개체는 해당 시스템의 감사 속성을 캡처합니다. |
| `marketingListKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 마케팅 목록 엔티티에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 시스템에서 생성한 값으로, `marketingListID`. |
| `marketingListDescription` | 문자열 | 마케팅 목록에 대한 설명입니다. |
| `marketingListID` | 문자열 | 마케팅 목록 엔티티에 대한 고유 ID입니다. |
| `marketingListName` | 문자열 | 마케팅 목록의 이름입니다. |

{style=&quot;table-layout:auto&quot;}

다음 안내서를 참조하십시오. [실시간 CDP B2B Edition의 스키마 관계](../../tutorials/relationship-b2b.md) 이 클래스가 다른 B2B 클래스와 개념적으로 관련이 있는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법을 알아봅니다.
