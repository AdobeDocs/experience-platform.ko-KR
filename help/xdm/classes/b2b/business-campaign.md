---
title: XDM 비즈니스 캠페인 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 캠페인 클래스에 대한 개요를 제공합니다.
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 3%

---

# [!UICONTROL XDM 비즈니스 ] 캠페인 클래스(베타)

>[!IMPORTANT]
>
>이 클래스는 현재 베타에 있는 실시간 고객 데이터 플랫폼 B2B 에디션의 일부로 사용할 수 있습니다. 설명서 및 기능은 변경될 수 있습니다.

[!UICONTROL XDM 비즈니스 ] 캠페인은 비즈니스 캠페인의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다.

![](../../images/classes/b2b/business-campaign.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 캠페인 엔터티에 대한 복합 식별자입니다. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 캠페인이 외부 소스 시스템에서 가져오는 경우 이 개체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 이 값은 `campaignID`과 별도의 시스템에서 생성한 값입니다. |
| `campaignDescription` | 문자열 | 캠페인에 대한 설명입니다. |
| `campaignID` | 문자열 | 캠페인 엔터티에 대한 고유 식별자입니다. |
| `campaignName` | 문자열 | 캠페인의 이름입니다. |
| `campaignType` | 문자열 | 캠페인 유형 또는 타겟 대상. |

이 클래스가 다른 B2B 클래스와 개념적으로 관련되는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법에 대해 알아보려면 실시간 CDP B2B Edition](../../tutorials/relationship-b2b.md)의 스키마 관계에 대한 안내서를 참조하십시오.[
