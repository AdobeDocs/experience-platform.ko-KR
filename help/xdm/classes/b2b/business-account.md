---
title: XDM 비즈니스 계정 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 계정 클래스에 대한 개요를 제공합니다.
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 ] 계정 클래스(베타)

>[!IMPORTANT]
>
>이 클래스는 현재 베타에 있는 실시간 고객 데이터 플랫폼 B2B 에디션의 일부로 사용할 수 있습니다. 설명서 및 기능은 변경될 수 있습니다.

[!UICONTROL XDM 비즈니스 ] 계정은 비즈니스 계정의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다.

![](../../images/classes/b2b/business-account.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 계정 엔터티에 대한 복합 식별자입니다. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 외부 소스 시스템에서 계정이 가져온 경우 이 개체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 이 값은 `accountID`과 별도의 시스템에서 생성한 값입니다. |
| `accountID` | 문자열 | 계정 엔터티에 대한 고유 식별자입니다. |

{style=&quot;table-layout:auto&quot;}

이 클래스가 다른 B2B 클래스와 개념적으로 관련되는 방법과 Adobe Experience Platform UI에서 이러한 관계를 설정할 수 있는 방법에 대해 알아보려면 실시간 CDP B2B Edition](../../tutorials/relationship-b2b.md)의 스키마 관계에 대한 안내서를 참조하십시오.[
