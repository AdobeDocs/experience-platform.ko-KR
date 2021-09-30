---
title: XDM 비즈니스 마케팅 목록 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 마케팅 목록 클래스에 대한 개요를 제공합니다.
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 마케팅 ] Listclass(베타)

>[!IMPORTANT]
>
>이 클래스는 현재 베타에 있는 실시간 고객 데이터 플랫폼 B2B 에디션의 일부로 사용할 수 있습니다. 설명서 및 기능은 변경될 수 있습니다.

[!UICONTROL XDM 비즈니스 마케팅 ] 는 마케팅 목록의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다. 마케팅 목록을 사용하면 제품을 구매할 가능성이 가장 큰 잠재 고객을 우선 순위로 지정할 수 있습니다.

![](../../images/classes/b2b/business-marketing-list.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 마케팅 목록이 외부 소스 시스템에서 나온 경우 이 개체는 해당 시스템의 감사 속성을 캡처합니다. |
| `marketingListKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 마케팅 목록 엔티티에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 이 값은 `marketingListID`과 별도의 시스템에서 생성한 값입니다. |
| `marketingListDescription` | 문자열 | 마케팅 목록에 대한 설명입니다. |
| `marketingListID` | 문자열 | 마케팅 목록 엔티티에 대한 고유 ID입니다. |
| `marketingListName` | 문자열 | 마케팅 목록의 이름입니다. |

{style=&quot;table-layout:auto&quot;}

이 클래스가 다른 B2B 클래스와 개념적으로 관련되는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법에 대해 알아보려면 실시간 CDP B2B Edition](../../tutorials/relationship-b2b.md)의 스키마 관계에 대한 안내서를 참조하십시오.[
